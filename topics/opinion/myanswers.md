## Importance of Compile Time vs JIT

- In compile - code is converted directly to architecture (machine language). Example: Go
- In JIT - code is converted at runtime, just before 
- Advantage: it can check availability of resources (RAM, CPU etc) and decide on corresponding optimizations 
- Advantage: it can keep running for a while a find hot snippets of code, and optimize them even further. Eg: Android 7
- Disadvantage: introduces latency during startup (for conversion)
- Disadvantage: have to perform conversion every time during application start (cannot save and re-use the best optimization results)

## What do you like about Java

- Performance (Eg: Memory allocation). Thanks to years of iterative work on the JVM it is very performant. JIT Compilation. 
- Garbage Collection. Algorithms keep improving. 
- Ecosystem (Vast number of mature, stable libraries, frameworks, IDEs, Tools available)
- Applicable to multiple use cases - Low Latency Trading apps, Web server, Batch Backend, etc.


## What do you not like about Java

- Verbosity - It is very difficult to write succinct code in Java. Too much boilerplate. Slightly subsidised by lambdas.
- Threads could be less expensive akin to Go channels or Kotlin co-routines.
- Message passing and Immutability are not baked-in.
- Thread communication by sharing memory is brittle (that is why so many locks are introduced), difficult to developers at all skill levels to write correct code.
- I wish primitives could be directly added to collections and used as list
- Null-checks (no ?. operator). Lot of boilerplate code and time wasted in checking for nulls. Especially in finance industry where POJOs have deeply nested structure. Doing a.getB().getC().getD() cannot be written. Every object needs to be null checked.
- No tuples (especially helpful in multiple return types which currently have to be put in HashMap)
- In fact, just check the kotlin language list
- All pojos have to write getter, setter, equals, hash, clone/copy… kotlin fixes this
- No built-in lightweight UI framework - They failed with JavaFX, Applets, etc.

