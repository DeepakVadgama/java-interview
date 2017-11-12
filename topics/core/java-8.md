## Java 8

* [Streams](#streams)
* [Examples:](#examples-)
* [Comparators](#comparators)
* [Concurrency](#concurrency)
* [CompletableFuture](#completablefuture)
* [StampedLock](#stampedlock)
* [@Contended](#-contended)

### Streams

**Create**

- Stream.of(T… a)
- IntStream.rangeClosed(start, end)  + LongStream & DoubleStream
- Arrays.stream(array)
- list.stream()
- list.parallelStream()
- Files.getLines()
- Stream.generate(() -> Math.random());

**Filter**

- findAny
- findFirst
- filter
- distinct
- limit(long)
- skip(long)

**Operations**

- sorted
- boxed
- min(comparator)
- max(comparator)
- count
- forEach
- flatMap  // when each element maps to n elements
- toArray
- reduce (0, (c, e) -> c + e);   // accumulator, reducer function
- reduce (0, Integer::sum);

**Collectors**

- Collectors.toList()
- Collectors.toSet()
- Collectors.toMap(keyMapper, valueMapper)
- Collectors.toCollection(TreeSet::new)
- Collectors.joining(", ")   // needs stream of strings, use map(Object::toString) before this
- Collectors.summingInt(Employee::getSalary)
- Collectors.averagingInt(Employee::getSalary)
- Collectors.summarizingInt(Employee::getSalary)  [gives stats max,min,count,average]
- Collectors.groupingBy(Employee::getDepartment)

### Examples:

**FlatMap**

```
 Stream<String> lines = Files.lines(path, StandardCharsets.UTF_8);
 Stream<String> words = lines.flatMap(line -> Stream.of(line.split(" +")));
```

**Typical**

```java
books.stream()
       .filter(book -> book.year > 2005)  // filter out books published in or before 2005
       .map(Book::getAuthor)              // get the list of authors for the remaining books
       .filter(Objects::nonNull)          // remove null authors from the list
       .map(Author::getName)              // get the list of names for the remaining authors
       .forEach(System.out::println);     // print the value of each remaining element
```

**Read Large File** 

Does not load whole file in memory. Though exceptions are wrapped in UncheckedIOException.

```java
try(Stream<String> stream : Files.lines(Paths.get(“absolute-path”))){
   stream.forEach(System.out::println);  
}
```

**Group By**


```java
Map<Person.Sex, List<Person>> byGender 
    = roster.stream().collect(Collectors.groupingBy(Person::getGender));

ConcurrentMap<Person.Sex, List<Person>> byGender 
    = roster.parallelStream().collect(Collectors.groupingByConcurrent(Person::getGender))

// Group employees by department
Map<Department, List<Employee>> byDept
    = employees.stream().collect(Collectors.groupingBy(Employee::getDepartment));

// Compute sum of salaries by department
Map<Department, Integer> totalByDept  
    = employees.stream().collect(Collectors.groupingBy(Employee::getDepartment,Collectors.summingInt(Employee::getSalary)));

// Partition students into passing and failing
Map<Boolean, List<Student>> passingFailing 
    = students.stream().collect(Collectors.partitioningBy(s -> s.getGrade() >= PASS_THRESHOLD));
```


### Comparators

vehicles.sort(Comparator.comparing(Vehicle::getWheels));
vehicles.sort(Comparator.comparing(Vehicle::getWheels));
vehicles.sort(Comparator.comparing(Vehicle::getWheels).thenComparing(Vehicle:getColor);  //chaining


### Concurrency

**HashMap**

- compute
- computeIfPresent (blocking, so write smaller computations)
- computeIfAbsent (blocking, so write smaller computations)
- putIfAbsent
- merge
- getOrDefault (k, def)

**Adders/Accumulators**

Much more performant than AtomicLong (have single copy across threads). Accumulators, each thread has own copy tracking its own counter, and when retrieval is triggered in any thread, all threads coordinate and perform total sum of all threads’ counts.

Basically no contention, during increment, decrement, add, thus much faster.

- LongAdder
- DoubleAdder
- LongAccumulator
- DoubleAccumulator

Operations

- increment
- decrement
- add (long)
- sum  // retrieves result by coordinating between threads
- reset

### CompletableFuture

Similar to JavaScript promises. Multiple async tasks can be chained (performed one after another on separate thread). Better alternative to ```future``` where the method ```get``` is blocking (waits indefinitely for the result). In completableFuture the current thread is not blocked. Each task is executed once previous task is completed. 

Also, the program itself becomes more readable. 

```java
 CompletableFuture.supplyAsync(() -> getStockInfo(“GOOGL”), executor)   // if executor is not passed it uses internal pool
        .whenComplete((info, exec) -> System.out.println(info))  // triggered once previous operation is finished
        .thenApply(Stock::getRate)   
        .thenAccept(rate -> System.out.println(rate))  
        .thenRun(() -> System.out.println(“done”)));  
```

So when you trigger this, it immediately returns the CompletableFuture instance, which can be used to check its status and such.

- supply method takes ```Supplier``` which returns a value
- thenApply method argument is ```Function``` which takes input and returns value
- thenAccept method argument is ```Consumer``` which takes input
- thenRun method argument is ```Runnable``` which only runs 
- CompletableFuture has no control of tasks while they are running in the executor. So cancel method just sets returned value as Exceptional.

### StampedLock 

- Better alternative for ReadWriteLock
- It does optimistic reads so works faster only on less contended operations
- Not re-entrant

### @Contended

For fields shared within same cache line and if only 1 field in it is volatile, then for multiple threads, the cache line will be flushed and will be updated. Thus use of cache is of no use. 
To fix this, set the field to hot field by using @Contented so that JVM can pad the field so that it takes entire cache line and is not shared with other fields.

[Talk explaining the @Contented](https://www.youtube.com/watch?v=Q_0_1mKTlnY)


