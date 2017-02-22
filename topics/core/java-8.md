## Java 8

### Stream

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

```
books.stream()
       .filter(book -> book.year > 2005)  // filter out books published in or before 2005
       .map(Book::getAuthor)              // get the list of authors for the remaining books
       .filter(Objects::nonNull)          // remove null authors from the list
       .map(Author::getName)              // get the list of names for the remaining authors
       .forEach(System.out::println);     // print the value of each remaining element
```

**Read Large File** 

Does not load whole file in memory. Though exceptions are wrapped in UncheckedIOException.

```
try(Stream<String> stream : Files.lines(Paths.get(“absolute-path”))){
   stream.forEach(System.out::println);  
}
```

**Group By**


```
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


### CompletionStage

```
stage.thenApply(x -> square(x))
        .thenAccept(x -> System.out.println(x))
        .thenRun(() -> System.out.println(“done”));
```
Each above functions have async variant

### CompletableFuture (= Future + CompletionStage)

Basically provide a call back to the future itself, so that as soon the result is available it can react to it by triggering those callbacks. In future we do .get which waits indefinitely for the result. In completableFuture we don’t wait. 

Also, the program itself becomes more fluent and readable. 

```
     CompletableFuture.supplyAsync(() -> getStockInfo(“GOOGL”), executor)   // if executor is not passed it uses internal pool
 			.whenComplete((info, exec) -> System.out.println(info))
			.thenApply(Stock::getRate)
			.thenAccept(rate -> System.out.println(rate))
			.thenRun(() -> System.out.println(“done”)));
```

So when you trigger this, then it immediately returns the CompletableFuture, and then you can check its methods below to check status and such if needed. 

**Massive API**

- get()
- join()  
- getNow(T valIfAbsent)
- cancel()
- isDone()

**Producer of the CompletableFuture**

So you return a new CompletableFuture immediately, and keep its reference so that while processing and after processing you can trigger the right methods on it (complete)

```

CompletionStage<String> getWebpage(URL url){

    CompletableFuture<String> future = new CompletableFuture<>();
    
    Runnable task = new Runnable(){
        public void run(){
            try {
                String webpage = blockingReadWebpage(url); // produce result
                future.complete(webpage);  // set result
            } catch(Exception e){
                future.completeExceptionally(e); //set exception
            }                 
        }
    }
    
    pool.execute(task);
    return future;
}
```


### StampedLock 

- Better alternative for ReadWriteLock
- It does optimistic reads so works faster only on less contended operations
- Not re-entrant

### @Contended

For fields shared within same cache line and if only 1 field in it is volatile, then for multiple threads, the cache line will be flushed and will be updated. Thus use of cache is of no use. 
To fix this, set the field to hot field by using @Contented so that JVM can pad the field so that it takes entire cache line and is not shared with other fields.

[Talk explaining the @Contented](https://www.youtube.com/watch?v=Q_0_1mKTlnY)


