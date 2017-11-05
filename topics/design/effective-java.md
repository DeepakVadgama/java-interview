## Effective Java

#### Resources

- [Effective Java by Joshua Bloch](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683) -- Highly recommended

### Table of Contents

- [Creating and Destroying Objects](#creating-and-destroying-objects)
  * [Consider static builders](#consider-static-builders)
  * [Service Interface Pattern](#service-interface-pattern)
  * [Builder pattern](#builder-pattern)
  * [Singleton with private instance or enum](#singleton-with-private-instance-or-enum)
  * [Private Constructor](#private-constructor)
  * [Avoid creating unnecessary objects](#avoid-creating-unnecessary-objects)
  * [Clear memory references](#clear-memory-references)
  * [Avoid finalizers](#avoid-finalizers)
- [Methods common to all objects](#methods-common-to-all-objects)
  * [equals](#equals)
  * [hashcode](#hashcode)
  * [toString](#tostring)
  * [clone](#clone)
  * [comparable](#comparable)
- [Classes and Interfaces](#classes-and-interfaces)
  * [Accessibility](#accessibility)
  * [Private fields with accessor methods](#private-fields-with-accessor-methods)
  * [Make fields as much immutable as possible](#make-fields-as-much-immutable-as-possible)
  * [Composition over inheritance](#composition-over-inheritance)
  * [Override in inheritance](#override-in-inheritance)
  * [Prefer interfaces to abstract classes](#prefer-interfaces-to-abstract-classes)
  * [Class hierarchies over tagged classes](#class-hierarchies-over-tagged-classes)
  * [Function objects to represent strategies](#function-objects-to-represent-strategies)
  * [Favor static member class over non-static](#favor-static-member-class-over-non-static)
- [Generics](#generics)
  * [Don't use Raw types](#don-t-use-raw-types)
  * [Prefer Lists to arrays](#prefer-lists-to-arrays)
- [Enums and Annotations](#enums-and-annotations)
  * [Enums instead of int constants](#enums-instead-of-int-constants)
  * [Prefer annotations over naming patterns](#prefer-annotations-over-naming-patterns)
- [Methods](#methods)
  * [Definition](#definition)
  * [Var args](#var-args)
  * [Return empty collections instead of null](#return-empty-collections-instead-of-null)
- [General](#general)
  * [Use Serializable Judiciously](#use-serializable-judiciously)

### Creating and Destroying Objects

#### Consider static builders

- They can have any name, thus can have multiple methods with same parameters (unlike constructors)
- They can return cached objects (eg: Boolean.valueOf)
- They can return their subtype, even class objects which are not public. Eg: Collection has 32 factory methods, return type of many are non-public classes. Ofcourse, the interface they extend is public. Returning such interface backed classes, also help in returning specific type based on argument. Eg: EnumSet returns RegularEnumSet or JumboEnumSet based on the argument. In future, JDK can add more types, without client/caller knowing about them. See service interface pattern below
- They can reduce verbosity of parameterized types. Eg: Maps.newHashMap()

#### Service Interface Pattern
- Here same pattern as above, where the implementation classes are not even known upfront.
- Example: JDBC connection driver classes. DriverManager.registerDriver, and DriverManager.getConnection.
- It needs to provide, registration API and then get service API
- Cannot subclass and take advantage of constructors. Though this enforces Composition instead of inheritance, so its not so bad.
- Cannot easily distinguish between constructing methods, and other methods. Need to use some convention to make it easy. Eg: newInstance, valueOf, of etc.

#### Builder pattern

- When too many parameters use builders instead.
- In Builders, each parameter setting can be through a good name method. In constructor its difficult to remember.
- Can easily add optional parameter support.

#### Singleton with private instance or enum

- static final variable (also provides init guarantee)
- Lazy loading (double checked) 
- Enums (by default lazy, and provides init guarantee)

#### Private Constructor


#### Avoid creating unnecessary objects
- Eg: Sring abc = new String("some value"); instead use String abc = "some value";
- Choose primitives over boxed, check for unnecessary boxing and unboxing

#### Clear memory references
- Let objects go out of scope quickly
- If not, nullify reference (eg: Stack.pop, within method, elements[size] = null)
- Check caches and message listeners, they hold references

#### Avoid finalizers
- JVM does not guarantee they will be called
- If called, they can be called anytime, not immediately after object is eligible for GC
- Never release resource in finalizer, if it does not run, the resource will still be lock (or in inconsistent state)
- Hampers performance
- Instead use explicit close methods like OutputStream, java.sql.Connection etc
- These classes also use finalizers, but that is safety net

-----------

### Methods common to all objects

#### equals
- If super class has implemented equals, then its okay to not implement (eg: Set used AbstractSet)
- Reflexive (equal to self), transitive, symmetric, consistent (unless modified)
- Maintain Liskov Substitution Principle, within equals (don't check o.getClass() == this.getClass() instead check with instanceof
- Consistent - Don't use external resources (eg: IP address)

#### hashcode
- every class which overrides equals must have it
- Consistent across multiple calls
- Dont use any fields, which are not used for equals
- You can exclude redundant fields (ones which are always same for all objects)
- You can cache the hashcode and return that (like String class), but then need to track if value is modified.

#### toString

#### clone
- Cloneable interface. Its a mixin interface. Does not have clone method.
- Object class's clone method is protected
- Atypical - Presence of Colenable modifies behavior of Object.clone() behavior. If present it returns object which is field by field copy, and if not present, then .clone method throws CloneNotSupportedException
- Cloning is not done using constructor
- If you override clone do return super.clone(), if all classes do that up the chain, then Object.clone will be called and you will get the right copy
- This is important because spec doesnt enforce anything from Cloneable interface. So someone might override clone and not clone, nor call super.clone, causing problems
- Note: Objects.clone() creates a shallow copy
- If you override and write clone, ofcourse you cannot set final field, thus need to remove final modifiers
- Object's clone method is declared to throw CloneNotSupportedException, but overriding clone methods can omit this declaration.
- Like constructor, clone method should not call non-final methods, because super object might not be properly constructed yet, causing some data corruption
- Clone method must be synchronized in case of concurrency
- In short, you are better off, creating and using a copy-constructor

#### comparable
- Opposing sign for symmetry x.compareTo(y) == -y.compareTo(x)
- If compareTo returns 0, objects should ideally be equal (but thats not in contract)
- Weird: Inserting new BigDecimal("1.0") and new BigDecimal("1.00") in HashSet stores 2 elements (they use equals), while TreeSet stores only 1 element (they use compareTo)

-----------

### Classes and Interfaces

#### Accessibility
- Make fields, classes etc as much inaccessible as possible (private, protected, package, then public)
- Anything that is public is now part of API, thus difficult to make private later

#### Private fields with accessor methods
- Helps in validating inputs (setters)
- Helps in returning copies in outputs (getters)

#### Make fields as much immutable as possible
- Immutable objects are simple
- They are thread-safe
- They can be shared freely
- They can expose their internals
- Can take advantage of cached hashCode & lazyInit hashCode
- Only disadvantage is memory use

#### Composition over inheritance
- Inheritance violates encapsulation, if super class changes sub-class behavior changes even if its not touched
- Super class can later add method, sub-class havent thought of
- In fact, it can add method which mutates the state which sub-class never promised to do.
- If you add your own methods in sub-class, and later super-class adds same name method its a problem. Either it may not compile based on return type, or contract of that method in super might be different than subclass method.
- Instead use composition and forward/delegate the calls
- Such classes are called Wrapper classes (decoration pattern)
- Only problem is library/frameworks do not know of your class type, and can't trigger message callbacks and such.

#### Override in inheritance
- Constructor must not call method (which is overridden), because super() constructor will call override() of subclass, which is not yet constructed
- Same problems can occur with clone and readObject (so avoid inheritance with Cloneable and Serializable)

#### Prefer interfaces to abstract classes
- Classes can be retrofitted to have more interfaces
- Interfaces allow mix-in types (markup), without need to implement any methods
- Interfaces allow cross-types (eg: SingerWriter implements Singer, Writer)
- Interfaces are not allowed methods, but Skeleton types can be created. Eg: AbstractSet, AbstractList etc. These classes help create concrete implementations by providing part of functionality
- If class cannot extend Skeletal (Abstract) class, we can implement the Interface, and have Skeletal class instance as composition field, and delegate all interface methods, to skeletal class instance. This is called, simulated multiple inheritance.
- Disadvantage: Once release, interfaces are impossible to change (all implementations need to be updated)

#### Class hierarchies over tagged classes
- Lot of boilerplate in tagged classes: Enums, fields, switch statements
- Memory issue: Tagged classes can contains fields specific for one type, but object of all types will have those extra fields.

#### Function objects to represent strategies
- Use classes (stateless) to represent computation. This can be passed around. Ex: StringLengthComparator

#### Favor static member class over non-static
- Every non-static class object has instance of enclosing class. Takes more memory.
- Non-static class instances cannot be created without creating instances of enclosing class
- Though one valid use of non-static class is, implementing Iterator for the class
- Static classes are typically used to create Helper classes
- Defining them public or private depends on whether you want to expose it in API

-----------

### Generics

#### Don't use Raw types
- Using types in all reference variables, helps in safety and avoiding boilerplate of casting
- Use generic fields (public E element) in class
- Use generic methods (public static <E> Set<E> union(Set<E> s1, Set<E> s2)).. <E> helps in type inference

#### Prefer Lists to arrays
- Arrays are covariant (Object[] a = new Long[]), but it fails at runtime (a[0] = "string value");
- Arrays retain types at runtime (reified) thus they throw ArrayStoreExceptions. Lists (generics) do type erasure at compile time.

-----------

### Enums and Annotations

#### Enums instead of int constants
- Enums provide name space. If you use int constants for 2 different Type hierarchies (AppleTypes & OrangeTypes), you can pass value of one to method of another, accidently, and compiler wont complain
- Enums are iterable. Cannot iterate over int constants
- Enums have default toString. Cannot sysout int constants (they will print numbers which are not helpful)
- You can extend functionality of enums
- Enums can be based on multiple fields
- EnumSet instead of Bit set (way to define union of types eg: STYLE_BOLD | STYLE_ITALIC), instead just use EnumSet.of(STYLE_BOLD, STYLE_ITALIC).
- EnumMap

#### Prefer annotations over naming patterns
- Eg: @Test instead of all method names starting with test
- Annotations have retention policy. Eg: RetentionPolicy.RUNTIME
- Annotations have target. Eg: @Target(ElementType.METHOD)

-----------

### Methods

#### Definition
- Choose method names carefully - they are part of API
- Choose parameter types as interfaces instead of implementations
- Long list of methods with identically typed parameters is wrong
- Dont have too many parameters
- Prefer Enum over boolean

#### Var args
- If method needs to take 1 or more, then have 1st param, then 2nd as var..args
- Arrays.asList() was a mistake, because you can pass multiple values to it, but if you pass array to it, then it considers that as var..args with single element of type array.
- Instead it should have had Arrays.gather(T... args) and then return Arrays.asList(args)

#### Return empty collections instead of null
- These return values are iterable

-----------

### General

- Avoid float and double for exact answers use BigDecimal
- Avoid boxed, (== does not work), and constant boxing-unboxing consumes CPU
- Use StringBuilder instead of direct concatenation
- Refer to objects by their interfaces
- Use checked exceptions for recoverable conditions, and runtime exceptions for programming errors
- Favor standard exception like IllegalStateException, IllegalArgumentException etc
- Prefer Executors and Tasks to threads
- Prefer concurrency classes instead of wait notify

#### Use Serializable Judiciously
- Like APIs once serialized, then cant change class structure
- Increases testing burden (backwards compatible)
- Increases security loopholes, because it does not use default constructor
- Inheritance based classes should avoid serializable