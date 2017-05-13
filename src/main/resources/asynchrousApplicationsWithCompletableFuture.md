# Asynchronous applications with completable future
## "Asynchronous applications with completable future" by Thilo Frotscher ([slides](https://www.doag.org/formes/pubfiles/8909843/docs/Events/2017/JavaLand%202017%20(28.03.2017)/vortraege/Core%20Java%20&%20JVM-Sprachen/2017-CORE-Thilo_Frotscher-Asynchrone_Anwendungen_mit_CompletableFuture-Praesentation.pdf))

## Content
- synchronous flows don't scale
- asynchronous necessary because of 
    1. microservice architecture
    1. interfaces to other systems
- since Java 5: Future<T>:
    ````java
    ExecutorService executor = ... ;
    QuoteService quoteService =  ...;
  
    Future<Integer> futureQuoteFromA = executor.submit(quoteService::getQuoteFromSupplierA);
    Future<Integer> futureQuoteFromB = executor.submit(quoteService::getQuoteFromSupplierB);
  
  // do other tasks for some time...
  
  Integer quoteFromA = futureQuoteFromA.get();  // BLOCKING!
  Integer quoteFromB = futureQuoteFromB.get();  // BLOCKING!

  quoteService.processQuotes(quoteFromA, quoteFromB);
    ````
- example above: after having calculated everything in parallel, the get-call is blocking which causes waiting for the process
- pseudo-solution: put getter in own thread. Not pretty.
- another ugly solution:
    ````java
    Map<String, Integer> allQuotes = new HashMap<>();
    while(quotes.size() < 2) {
      try {
          allQuotes.put("A", futureQuoteFromA.get(500, MILLISECONDS));
      } catch (TimeoutException e) {
          log.info("Quote not yet available from supplier A.");
      }
      try {
          allQuotes.put("B", futureQuoteFromB.get(500, MILLISECONDS));
      } catch (TimeoutException e) {
          log.info("Quote not yet available from supplier B.");
      }
      // do other tasks for some time...
    }
    quoteService.processQuotes(allQuotes.get("A"), allQuotes.get("B"));
    ````
- CompletionService (Java 5) = implementation of these solutions. However, also not pretty.
- Completable Future (Java 8) = pretty solution
- push instead of poll => less resource usage
    ````java
    CompletableFuture<Integer> futureQuoteFromA = CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierA); 
    futureQuoteFromA.thenAcceptAsync(quoteService::displayQuote);
    ````
- CompletableFuture extends both Future AND CompletionStage => huge number of methods!
- Concurrent task with result:
    ````java 
    CompletableFuture<U> supplyAsync(Supplier<U> task) 
    CompletableFuture<U> supplyAsync(Supplier<U> task, Executor e) 
    ````    
- Concurrent task without result:
    ````java
  CompletableFuture<Void> runAsync(Runnable task) 
  CompletableFuture<Void> runAsync(Runnable task, Executor executor) 
    ````
- other code snipptes see [slides](https://www.doag.org/formes/pubfiles/8909843/docs/Events/2017/JavaLand%202017%20(28.03.2017)/vortraege/Core%20Java%20&%20JVM-Sprachen/2017-CORE-Thilo_Frotscher-Asynchrone_Anwendungen_mit_CompletableFuture-Praesentation.pdf)
- example with multiple stages: 
    ````java
    CompletableFuture<Void> futureAllStagesDone = 
      CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierA) 
                      .thenApply(quoteService::computeSalePrice)
                      .thenAccept(quoteService::displaySalePrice)
                      .thenRun(() -> sendEmailNotification());
- error-handling: unchecked exception in a stage => cancel execution, exception gets lost. Methods for error-handling:
    ````java
    CompletableFuture<T> exceptionally(Function<Throwable,T> task) 
    <U> CompletableFuture<U> handle(BiFunction<T,Throwable,U> task)
    CompletableFuture<T> whenComplete(BiConsumer<T,Throwable> task) 
     ````
- example:
    ````java
    CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierA)
                      .exceptionally(this::handleQuoteRetrievalIssue)
                      .thenAccept(quoteService::displaySalePrice);
    // ...
  
    protected Integer handleQuoteRetrievalIssue(Throwable t) {
      // handle error and return default quote
      return -1;
    }
    ````
- alternatively with "handle":
    ````java
    CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierA)
                      .handle((quote, t) -> {
                          quoteService.displaySalePriceOrError(quote, t); 
                          return null; 
                      });
    ````
- new stage uses results from former stages:
    ````java
    acceptEither(CompletionStage<T> other, Consumer<T> task) // example "Take first answer from servers"
    applyToEither(CompletionStage<T> other, Function<T, U> task)
    runAfterEither(CompletionStage<T> other, Runnable task)
  
    thenAcceptBoth(CompletionStage<U> other, BiConsumer<T, U> task)
    thenCombine(CompletionStage<U> other, BiFunction<T, U, V> task)
    runAfterBoth(CompletionStage<T> other, Runnable task)
     ````
- example:
    ````java
    CompletableFuture<Integer> futureQuoteFromA = CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierA)
                                                                  .exceptionally(this::handleQuoteRetrievalIssue);
     CompletableFuture<Integer> futureQuoteFromB = CompletableFuture.supplyAsync(quoteService::getQuoteFromSupplierB)
                                                                  .exceptionally(this::handleQuoteRetrievalIssue);
     CompletableFuture<Void> bothProcessed = futureQuoteFromA.thenCombine(futureQuoteFromB, quoteService::calculateAveragePrice)
                                                                  .thenApply(quoteService::computeSalePrice)
                                                                  .thenAccept(quoteService::displaySalePrice)
                                                                  .thenRun(() -> sendEmailNotification());
     ````
- in Java 9
    ````java
    Executor exe = CompletableFuture.delayedExecutor(50L, TimeUnit.SECONDS);
    new CompletableFuture().orTimeout(1, TimeUnit.SECONDS)
    new CompletableFuture().completeOnTimeout(value, 1, TimeUnit.SECONDS)
    ````

## Tasks
- Steven: Have a look at class Void
- merge this into [chapter Concurrency in Java 8 Workshop](https://github.com/stevenschwenke/Java8Workshop/blob/master/src/test/java/de/stevenschwenke/java/java8workshop/C_07_Concurrency.java) 