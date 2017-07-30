## JVM Internals

Some of the topics listed below are tricks JVM uses to improve performance. Subset of these can be exploited to further improve 
application performance. 

Note: These topics are highly unlikely to come up in an interview. Feel free to just glance through without digging deep. 

### Compressed pointers

- 32 bit references can address 4GB, while 64 bit can reference 2^64 bytes (though limited by OS/RAM on the machine). 
- Having 64 bit reference for every object increases memory usage. JVMs use [compressed pointers](https://wiki.openjdk.java.net/display/HotSpot/CompressedOops) to address this issue. 
- Basic idea is to store 32-bits per reference and then add to a base address to find final 64-bit address. 
- Flag: `-XX:+UseCompressedOops`. Latest versions of 64-bit Java have this argument by default.  
- Addresses upto 4gb untranslated. 
- Addresses 4gb to 28gb, remove 3bits, because Java has 8 byte word aligned, thus 3 bits need not be stored. 
- Important because Java has more references. In C++ memory layout follows struct layout. 
- Java 8 has JVM args, `+XX:ObjectAlignmentInBytes=16` for heap between 32gb and 64gb.

### String interning
 
- Interning = storing strings in a pool and re-using them
- If you intern a set of all strings, you can compare them by == improving performance.
- It is stored internally as a hashmap (it is native C code, not Java code).
- More details [here](http://java-performance.info/string-intern-in-java-6-7-8/) and [here](http://java-performance.info/changes-to-string-java-1-7-0_06/)
- How would you implement your own string interning?

```Java
private static final WeakHashMap<String, WeakReference<String>> s_manualCache
      = new WeakHashMap<String, WeakReference<String>>(100000);
 
private static String manualIntern(final String str){
    final WeakReference<String> cached = s_manualCache.get(str);
    if (cached != null){
        final String value = cached.get();
        if (value != null)
            return value;
    }
    s_manualCache.put(str, new WeakReference<String>(str));
    return str;
}
```

### Thread Affinity

Makes the thread stick to a CPU core, even if it has no tasks left to perform. Unlike normal threads, this won't go into sleep/wait.
Thread performs busy-spin. Note: This is wasting of CPU resources, and it can lead to thread starvation since other threads
do not get access to that core. Thus, it needs to be used for the right applications. Helpful in latency critical applications like FX Trading. 

Thread affinity only works for Linux and there are [Java libraries available](https://github.com/OpenHFT/Java-Thread-Affinity) to use the same

### Other topics

- [How does default hashCode method work?](https://srvaroa.github.io/jvm/java/openjdk/biased-locking/2017/01/30/hashCode.html)
- [What is Biased locking](https://blogs.oracle.com/dave/entry/biased_locking_in_hotspot)
- [JVM Threads link with OS threads](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html#Thread%20Management%7Coutline)
- [Class Loaders](https://zeroturnaround.com/rebellabs/rebel-labs-tutorial-do-you-really-get-classloaders/)
- [Memory consumptions of primitives and boxed variables](http://java-performance.info/overview-of-memory-saving-techniques-java/)
- Hoisting variables: JVM can hoist variables out of for loops to improve performance. [example](http://stackoverflow.com/a/9338302/3494368)
- Escape analysis: JVM can choose to place a method local object (if it never escapes the method) in Thread-stack instead of heap. 
 Improves performance since that object doesn't go through GC (can be just deleted once method completes). 