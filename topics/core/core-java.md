## Core Java

This page focuses on oddities of Core Java from an interview perspective. For basic 
topics like inheritance, interfaces, etc. please read the book mentioned below. 

### Resources

- [OCA/OCP Java SE 7 Programmer I & II Study Guide](http://www.amazon.in/Programmer-Study-1Z0-803-1Z0-804-Certification/dp/0071772006)

### Default init values

- For fields (class level variables), values are auto assigned default values. 
- Method local variables should be manually assigned. 
- Default values (references = null, primitives = 0, boolean = false)
- Arrays initialize its elements: int[] numbers = new int[10]; will assign all ints in the array to 0.

### String pool

- String constants are placed in a memory pool 
- When retrieved, returns reference to string in the pool. 
- Pool saves memory. New string constants with same value share same instance in the pool.
- String is immutable thus these values are never changed. For any updates, new string constant is created.  
- String s = "abc" will place "abc" in pool and return its reference.
- String s = new String("abc") will also place "abc" in pool, as well as allocate new memory
- [implementation details](jvm-internals.md#string-interning)

### Wrapper class pool

- Boolean
- Byte
- Character from \u0000 to \u007f (7f is 127 in decimal)
- Short and Integer from –128 to 127

### Singleton options

- Using: static final variable (init guarantee)
- Using: Lazy loading (double checked) 
- Using: Enums (by default lazy, and init guarantee)

### Override method rules

- Same method name and parameter types
- Same or a subset of super methods' checked exceptions
- Any number of runtime exceptions
- Same or covariant return type 

### Covariant variables

- Variable types which are compatible. 
- Eg: an int is covariant of long
- Eg: an Lion class is covariant of Animal class (only if Lion extends Animal)
- Can be used in parameters, return types or assignments

### Varargs, boxing, widening

- Primitive Widening > Boxing > Varargs. [Example](http://stackoverflow.com/a/2128068/3494368). 
- Widening then Boxing not allowed. 
- Boxing then Widening allowed.   
- Widening between wrapper classes not allowed (eg: Long n = new Integer(10); not allowed)
 
### Inner classes

Personally I find this part of Java to be super annoying, unnecessary and hardly ever used in real-life (especially after Java 8). 
Also, this topic does not come up a lot in interviews, so just skimp through. 

- Inner class: Can access enclosing class's variables (even private ones)
- Method local inner class: Same as above. Plus, it can access final variables in encapsulating method. 
- Anonymous inner class: Just no name, otherwise same as above. 
- Static inner class: No special relationship with outer class. 

### Reference types

- **Weak reference** - Eligible for GC if object not referenced by any other variables. Good for caches. Are enqueued in ReferenceQueue just before GC (object can be resurrected in finalize). Returns null once object is eligible for GC, even if object is resurrected, the weak-reference still is dead, and will return null. 
- **Soft reference** - Same as above, but its GC’ed only when memory is low. Excellent for caches.
- **Phantom reference** - Even after GC, it references the object, until the memory is reclaimed. Enqueued in ReferenceQueue after complete reclamation. Always returns null, so that you cannot resurrect it. Can be helpful to check when memory is reclaimed so that you can load next large object. 
- **WeakHashMap** - Weak keys. Removes entry once key is GC’ed.
 
### Cloning  

- clone method (protected) of Object class returns shallow copy. Need to be explicitly cast back.
- Requires class to implement Cloneable marker interface. Else returns CloneNotSupportedException
- Singletons should override clone method and throw CloneNotSupportedException
- [More details](../design/effective-java.md#clone)
