# The Pragmatic Developer's Guide to Java 9
## Talks
- "The Pragmatic Developer's Guide to Java 9", Oleg Shelajev, Simon Maple

## Content
### Modules
- (has been discussed, see other talks)

### G1GC
- former garbage collectors: one huge memory block that doesn't scale well because it would have to be traversed in whole length
- structures space in fixed-sized cells
- each cell can be 
    - eden space
    - survivor space
    - old generation 
- however, more CPU usage necessary to find right cell.
- G1GC available in since Java 6 
- change with Java 9: J1GC will be default GC
- most of the audience thinks they don't need G1GC

### REPL
- most of audience don't see the point of having a REPL

### APIs
- see slides if available
- List.of(1, 2, 3) - also for Set
- java.util.ImmutableCollections -> TODO Are these included in Java 9?
- Streams: dropWhile(x -> x < 5) and "takeWhile"
- Optional.empty().ifPresentOrElse(null, () -> ...) => 2 branches for condition and anti-condition instead of just 1 branch
- CompletableFuture -> see other talk
- ProcessHandle.current().info()
- Runtime.version()
- Multirelease JARs (Java 8, 9, 10 in one jar) => however not conceived as a good idea

## Tasks
- Find slides
