## Collections

### Resources

- [OCA/OCP Java SE 7 Programmer](https://www.amazon.com/Programmer-Study-1Z0-803-1Z0-804-Certification/dp/0071772006/ref=asap_bc?ie=UTF8) (book) 
- [Cheat sheet](http://files.zeroturnaround.com/pdf/zt_java_collections_cheat_sheet.pdf) (PDF)
- [Effective Java study notes](topics/design/effective-java.md)

### Table of contents

- [Lists](#lists)
  * [ArrayList](#arraylist)
  * [LinkedList](#linkedlist)
  * [Stack](#stack)
  * [Vector](#vector)
  * [CopyOnWriteArrayList](#copyonwritearraylist)
  * [Collections.synchronizedList](#collectionssynchronizedlist)
- [Sets](#sets)
  * [HashSet](#hashset)
  * [LinkedHashSet](#linkedhashset)
  * [TreeSet](#treeset)
  * [ConcurrentSkipListSet](#concurrentskiplistset)
  * [CopyOnWriteArraySet](#copyonwritearrayset)
  * [EnumSet](#enumset)
- [Maps](#maps)
  * [HashMap](#hashmap)
  * [HashMap implementation details](#hashmap-implementation-details)
  * [LinkedHashMap](#linkedhashmap)
  * [Hashtable](#hashtable)
  * [ConcurrentHashMap](#concurrenthashmap)
  * [TreeMap](#treemap)
  * [ConcurrentSkipListMap](#concurrentskiplistmap)
- [Queues](#queues)
  * [LinkedList](#linkedlist-1)
  * [ArrayBlockingQueue](#arrayblockingqueue)
  * [LinkedBlockingQueue](#linkedblockingqueue)
  * [ConcurrentLinkedQueue](#concurrentlinkedqueue)
  * [Deque classes](#deque-classes)
  * [PriorityQueue](#priorityqueue)
  * [PriorityBlockingQueue](#priorityblockingqueue)
  * [DelayQueue](#delayqueue)
  * [SynchronousQueue](#synchronousqueue)
- [equals and hashCode](#equals-and-hashcode)
- [Collections class](#collections-class)
  * [Utility methods](#utility-methods)
  * [Methods returning wrapped instances](#methods-returning-wrapped-instances)
- [Hierarchy and classes](#hierarchy-and-classes)

---

### Lists

#### ArrayList

- Backed by array (which are co-located in memory), thus fast iteration and get(i) operation.
- Slow inserts when the backed array is full and has to double in size.
- Fail-fast iterators, which can throw ConcurrentModificationException.
- Add is O(n) - When element is added to middle of list, all elements on the right have to be moved.  
- [Use Case](http://stackoverflow.com/a/322742/3494368) - When iterations outnumber number of read/writes. 
    
#### LinkedList

- Chain of nodes referencing each other (doubly linked list).
- No co-location of nodes, pointers need to be chased for next element, thus slow iterations and get(i) operation.
- Fail-fast iterators, which can throw ConcurrentModificationException. 
- Implements Queue interface, thus allows offer/pop/peek operations.
- Add is O(1) - Adding element in middle of list is just adjusting the node pointers. 
- Internally uses references (~ to skiplist) to optimize iterations. 
- [Use Case](http://stackoverflow.com/a/322742/3494368) - Lot of inserts in middle of the list.
   
| Operation       | ArrayList                         | LinkedList                |
|-----------------|-----------------------------------|---------------------------|
| get(i)          | O(1)                              | O(n)                      |
| add()           | O(1) amortized                    | O(1)                      |
| remove(i)       | O(n) Remove and move all elements | O(n)  Iterate then remove |
| iterator.remove | O(n)                              | O(1)                      |
   
#### Stack

- For stack operations push/pop/peek.
- Not used anymore. Recommended to use Deque implementations.

#### Vector

- Synchronized version of list.
- Not used anymore. Recommended below mentioned alternatives. 
    
#### CopyOnWriteArrayList

- Thread-safe. 
- Backed array is copied during every element insert. 
- Avoids ConcurrentModificationException since iteration can continue in original copy, and insert results in new copy. 
- High memory usage (more pressure on GC) due to the resulting copies.
- Use case - Large number of threads for read, low number of writes. 
    
#### Collections.synchronizedList

- Thread-safe.
- Can be slow due to mutual exclusion.
- Iterations have to be externally synchronized by developer 
- Can throw ConcurrentModificationException if (above mentioned) synchronization not done during iteration.

---

### Sets

Collection of unique elements. No duplicates. 

#### HashSet

- Backed by HashMap. 
- Performance can vary based on hashCode implementation.
- Constant time get/remove/add/contains (subject to above point).
- Fail-fast iterators.
- Insertion order not retained. 
    
#### LinkedHashSet

- Insertion order is retained. 
- Uses doubly-linked list to maintain the order.
- Iteration can be slower due to this.
- Other features, same as HashSet above (except iteration)

#### TreeSet

- Elements sorted by their natural order (or Comparator passed in constructor).
- Log(n) time for add/remove/contains operations.
- Navigable (floor, ceiling, higher, lower, headSet, tailSet operations).
- Fail fast iterators.

#### ConcurrentSkipListSet

- Thread-safe.
- Log(n) time for add/remove/contains operations.
- Navigable (floor, ceiling, higher, lower, headSet, tailSet operations).
- Size method is not constant time operation. 
- Weakly consistent iterators (do not throw ConcurrentModificationException but also __may not__ reflect concurrently added items).
- Thus, bulk operations (addAll, removeAll, retainAll, containsAll etc) are not guaranteed to be atomic.

#### CopyOnWriteArraySet

- Backed by CopyOnWriteArrayList
- Thread-safe. 
- Slow. Operations have to iterate through the array for most operations.  
- Recommended where reads vastly outnumber writes and set size is small.
    
#### EnumSet

- To be used with Enum types.
- Very efficient and fast (backed by bit-vectors).
- Weakly consistent iterators. 
- Nulls not allowed.

---

### Maps

#### HashMap

- key, value pairs.
- Permits a null key, and null values.
- Iteration order not guaranteed.
- Throws ConcurrentModificationException.
- [Article detailing implementation](http://www.deepakvadgama.com/blog/java-hashmap-internals/).

#### HashMap implementation details

- Backed by array (buckets), array-size is known as table-size.
- Position in array = element-hash % table-size. 
- If elements end up in same bucket, they are added to linked-list (or a balanced red-black tree).
- O(1) access (if hashcode properly distributes the values, else O(n) for linked-list & O(log(n)) for tree.
- Load factor - 0.75 default, decides when table-size should increase (double). 
- Bigger load-factor - more space-efficient, reduced speed (due to more elements in same bucket).
- Lower load-factor - less space-efficient, more speed (less, ideally 1 element in 1 bucket).
- Initial table-size = 16.

#### LinkedHashMap

- Insertion order is retained.

#### Hashtable

- Thread-safe.
- Not used anymore, ConcurrentHashMap recommended.

#### ConcurrentHashMap

- Thread-safe.
- Fine grained locking called striped locking (map is divided into segments, each with associated lock. Threads holding different locks don't conflict).
- Improved performance over Hashtable.

#### TreeMap

- Sorted by keys. 
- Uses Red-Black tree implementation. 

#### ConcurrentSkipListMap

- Thread-safe version of TreeMap.
- Navigable (floor, ceiling, higher, lower, headSet, tailSet operations).

---

### Queues

#### LinkedList

- Implements Queue interface. 
- offer, peek, poll operations.
- Use case - task queues

#### ArrayBlockingQueue

- Thread-safe.
- Backed by array. Thus bounded in size.  
- Adding element to full queue results in blocking.
- Polling an empty queue results in blocking.
- Use case - Producer consumer problem.
    
#### LinkedBlockingQueue

- Thread-safe.
- Backed by linked-list.
- Optionally bounded in size. Takes maxSize as constructor argument. 

#### ConcurrentLinkedQueue

- Thread-safe. 
- Uses CAS (Compare-And-Swap) for more throughput. Also known as lock free. 

#### Deque classes

- ArrayDeque - Double ended queue. Backed by array. Can throw ConcurrentModificationException.
- LinkedList - Implements Deque interface.  
- LinkedBlockingDeque
- ConcurrentLinkedDeque

#### PriorityQueue

- Elements sorted based on their natural order (or Comparator provided in Constructor).
- Use case - task queues where tasks can have different priorities.
    
#### PriorityBlockingQueue

- Thread-safe.
    
#### DelayQueue

- Elements added, are available to be removed only after their delay-time is expired. 

#### SynchronousQueue

- Holds single elements.
- Blocks for both producer and consumer to arrive.
- Use case - For safe/atomic transfer of objects between threads.

---

### equals and hashCode

- equals required for all collections. 
- equals and hashCode required for Maps and Sets (which are backed by Maps).

---

### Collections class

#### Utility methods

- sort(list, key) - guarantees stable sort
- reverse 
- reverseOrder - returns Comparator for reversed order
- shuffle
- rotate(list, distance) - rotates elements by the distance specified 
- binarySearch(list, key) 
    + list should be sorted else can get unpredictable results 
    + log(n) if list implements RandomAccess, else O(n)
    + RandomAccess - Marker interface that says, collection supports fast random access, get(i). Typically backed by arrays. 

#### Methods returning wrapped instances

- empty - emptyList, emptySet, emptyMap etc.
- synchronized - synchronizedList, synchronizedSet, synchronizedMap etc. 
- unmodifiable - unmodifiableList, unmodifiableSet, unmodifiableMap etc. 
- singleton(t) - singleton (returns set), singletonList, singletonMap etc.

---

### Hierarchy and classes

<image src="../../images/collection-hierarchy-2.png">

<image src="../../images/map-hierarchy-2.png">
