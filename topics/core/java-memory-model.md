## Java Memory Model

### Resources

- [The Java memory model made easy by Rafael Winterhalter](https://vimeo.com/181788144) - Highly Recommended

### What is it?

- Specification deciding how JVM can reorder instructions (for performance) aka ensures guaranteed ordering of of reads and writes under certain conditions (happens-before). Every JVM has to implement this spec. 
- Barriers that forbid reordering instructions (load-load, load-store, store-load, store-store)
- Variables   
    + volatile
    + final = all writes before volatile write will be reflected when/after volatile is read (potentially by other thread). Threads need to use the same volatile variable for this to work. For double/long (which occupy multiple word spaces, word-breakdown is forbidden to ensure integrity of data). 
- Methods - synchronized
- Locks - normal objects used as locks, and lock classes like ReadWriteLock. 
- Threads - When a new thread is started, it is guaranteed to see all values written before thread started. 

## More details

This topic overlaps quite a bit with Concurrency. Please read [corresponding wiki page](concurrency.md)