# Modularization with Java 9
## Talks
* "Restrcturing your code base with Java 9", Rabea Gransberger, 1. talk Tuesday, [slides](https://speakerdeck.com/rgra/restrukturierung-der-code-basis-mit-java-9), [code](https://rgra.github.io)

## TL;DR
TODO insert short description about what is going on here
* new important topic in Java 9: Modularization (of JDK, JRE and for your applications)

## Advantages modules vs monolith
* modules make architecture explicit
* clear boundaries so that classes can be hidden (for real ;)
* swap of modules
* module path more robust than classpath: errors occur at startup time, not runtime. Better error messages. 
* better tooling to find missing dependencies
* small modules easier to deploy than large monoliths

## Project Jigsaw
* JSE 376
* until now: class not found on classpath, error at runtime
* with Java 9: no classpath but module-path. Error when starting application
* each module: module-info.java
    ```java
    module modulename {
      requires requiredmodule;
      exports exportedmodule;
      uses service;
      provides service with serviceimpl;
  }
    ```

## scenario from Rabea Gransbergers talk
* existing (non-modularized) application for vet clinic that should be able to be used with another business logic (automotive) - "Nice application you have there - could it work with my automotive business logic"
* goal: Manage cars instead of animals
* solution: Refactor application and extract business domain. Then, new business domain can use infrastructure of old application.
* existing entites: Customer, Pet, Visit, Invoice. Goal: Pet => Car

## Correct slicing in general
* slice application by business domain! Example: Customer, Pet, Visit, Invoice. 
* Each slice has technical layers in it like Model, DB, UI
* result: a lot of packages like customer.db, customer.model, customer.ui, invoice.db, invoice.model, ...
* With Java 9, packages get more important because developer has to decide explicitly what to expose and what not. However: Create new class in exposed package will pollute the API with that class!

## State of Java 9
* release date: 27.07.
* Eclipse needs some work to run with Java 9, even when it runs it's "kind of a hack"
* IntelliJ IDEA is cool with it
* NetBeans too

## Split-packages
* "Split package" = packages with the same name but in different modules. This is not allowed in Java 9.

## ServiceLoader
* chart 36: Introduced class TabService can load new tabs from other modules.
* ServiceLoader = "Get me all implementations of that service!" => possible to display tabs of the former vet domain AND the new automotive domain by picking the right service implementations from the list
* ApplicationConfigurationProvider: sadly no time left to have a look at that

## Tasks
* Have a look at Rabeas codebase and understand it. ;)
* Steven: Rabea said "definition of module = area without cyclic dependencies". Does that mean that there can be circular dependencies between modules? I don't understand that definition. Ask her.
* Steven: Release of Java 9 should be around July. Is it possible that our customer can install Java 9 and run the application with it? Shouldn't be possible because of WebStarter. Or could it? ... 
* to make this a complete Java 9 modularization chapter, add: unnamend modules, named modules (explicit, open, automatic module), module-info.java (versioning, "requires transitive", "exports package to module", opens package), jlink, jdeps

- Steven organize migrating all knowledge from here to other places (workshops, articles, talks, ...). Goal is to delete this repository and all its contents.