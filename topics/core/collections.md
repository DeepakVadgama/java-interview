## Collections

### Resources

- [OCA/OCP Java SE 7 Programmer](https://www.amazon.com/Programmer-Study-1Z0-803-1Z0-804-Certification/dp/0071772006/ref=asap_bc?ie=UTF8) (book) 
- [Cheat sheet](http://files.zeroturnaround.com/pdf/zt_java_collections_cheat_sheet.pdf) (PDF)
- [Effective Java study notes](topics/design/effective-java.md)

### Collection Classes

**Lists** 

- ArrayList
    + Backed by array (which are co-located in memory), thus fast iteration and get(i) operation.
    + Slow inserts when the backed array is full and has to double in size.
    + Fail-fast iterators, which can throw ConcurrentModificationException.
    + Add is O(n) - When element is added to middle of list, all elements on the right have to be moved.  
    + [Use Case](http://stackoverflow.com/a/322742/3494368) - When iterations outnumber number of read/writes. 
    
- LinkedList
    + Chain of nodes referencing each other (doubly linked list).
    + No co-location of nodes, pointers need to be chased for next element, thus slow iterations and get(i) operation.
    + Fail-fast iterators, which can throw ConcurrentModificationException. 
    + Implements Queue interface, thus allows offer/pop/peek operations.
    + Add is O(1) - Adding element in middle of list is just adjusting the node pointers. 
    + Internally uses references (~ to skiplist) to optimize iterations. 
    + [Use Case](http://stackoverflow.com/a/322742/3494368) - Lot of inserts in middle of the list.
   
| Operation       | ArrayList                         | LinkedList                |
|-----------------|-----------------------------------|---------------------------|
| get(i)          | O(1)                              | O(n)                      |
| add()           | O(1) amortized                    | O(1)                      |
| remove(i)       | O(n) Remove and move all elements | O(n)  Iterate then remove |
| iterator.remove | O(n)                              | O(1)                      |
   
- Stack
    + For stack operations push/pop/peek.
    + Not used anymore. Recommended to use Deque implementations.

- Vector
    + Synchronized version of list.
    + Not used anymore. Recommended below mentioned alternatives. 
    
- CopyOnWriteArrayList
    + Thread-safe. 
    + Backed array is copied during every element insert. 
    + Avoids ConcurrentModificationException since iteration can continue in original copy, and insert results in new copy. 
    + High memory usage (more pressure on GC) due to the resulting copies.
    + Use case - Large number of threads for read, low number of writes. 
    
- Collections.synchronizedList
    + Thread-safe.
    + Can be slow due to mutual exclusion.
    + Iterations have to be externally synchronized by developer 
    + Can throw ConcurrentModificationException if (above mentioned) synchronization not done during iteration.

**Sets**

Collection of unique elements. No duplicates. 

- HashSet
    + Backed by HashMap. 
    + Performance can vary based on hashCode implementation.
    + Constant time get/remove/add/contains (subject to above point).
    + Fail-fast iterators.
    + Insertion order not retained. 
    
- LinkedHashSet
    + Insertion order is retained. 
    + Uses doubly-linked list to maintain the order.
    + Iteration can be slower due to this.
    + Other features, same as HashSet above (except iteration)

- TreeSet
    + Elements sorted by their natural order (or Comparator passed in constructor).
    + Log(n) time for add/remove/contains operations.
    + Navigable (floor, ceiling, higher, lower, headSet, tailSet operations).
    + Fail fast iterators.

- Collections.synchronizedSortedSet
    + Wrapper over any of the above sets. 
    + Thread-safe.

- ConcurrentSkipListSet
    + Thread-safe.
    + Log(n) time for add/remove/contains operations.
    + Navigable (floor, ceiling, higher, lower, headSet, tailSet operations).
    + Size method is not constant time operation. 
    + Weakly consistent iterators (do not throw ConcurrentModificationException but also __may not__ reflect concurrently added items).
    + Thus, bulk operations (addAll, removeAll, retainAll, containsAll etc) are not guaranteed to be atomic.

- CopyOnWriteArraySet
    + Backed by CopyOnWriteArrayList
    + Thread-safe. 
    + Slow. Operations have to iterate through the array for most operations.  
    + Recommended where reads vastly outnumber writes and set size is small.
    
- EnumSet
    + To be used with Enum types
    + Very efficient and fast (backed by bit-vectors)
    + Weakly consistent iterators 
    + Nulls not allowed

**Maps**

- HashMap
- Hashtable
- ConcurrentHashMap
- TreeMap
- ConcurrentSkipListMap

**Queues**

- Queue
- Deque
- BlockingQueue
- PriorityQueue


### equals and hashCode

- equals required for all collections. 
- equals and hashCode required for Maps and Sets (which are backed by Maps)


### Collections class

- Sorting
- Binary Search

### Hierarchy and classes

<image src="../../images/collection-hierarchy-2.png">

<image src="../../images/map-hierarchy-2.png">


