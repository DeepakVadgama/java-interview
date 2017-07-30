## Design Patterns

### Resources

- [Design patterns explained too simply](https://github.com/kamranahmedse/design-patterns-for-humans)
- [Examples of design patterns in Java libraries](http://stackoverflow.com/questions/1673841/examples-of-gof-design-patterns-in-javas-core-libraries/2707195#2707195)

### Creational

- Singleton -  Single instance of class. Either Eager (static) or Lazy (broken pre-JDK5). Eg: Logger, Configurer
- Factory - Create types of instances. Eg: Trade type (Bonds, Bill, Notes)
- Abstract Factory - Factory of factories of related products. Eg: Trade Type (GermanBond, EuroBond, GermanBill, EuroBill)
- Builder - Eg: StringBuilder, PizzaMaker
- Prototype - Copying costly-creation objects. Classes should implement clone or similar method.
- Object pool - Re-use instances. Eg: Threadpool

### Behavioral

- Observer - Reactive streams.
- Strategy - Encapsulate algorithms and execute either. Eg: Trading strategy, select one and execute.
- Command - Object encapsulates action with common interface which executor calls. Eg: Remote click.
- State - Behavior based on current state of object.
- Visitor - Object which visits all similar instances. Eg: File Traverse, or Calculate total bill from cart.
- Iterator - Iterating through a collection of objects.
- Chain of Responsibility - object passes through various instances, coordinated by Handler. Eg: Stream API
- Template - Eg: HTML templates
- Interpreter - Format converter. Eg: JVM converts byte to native for JVM.
- Memento - Save and restore state of object.

### Structural

- Adapter - Adapting to a non-direct-compatible class/module/system. 
- Decorator - Wrap class with another Eg: FileReader, BufferedReader
- Facade - Hiding complexity behind simple interfaces. Eg: Turbo Tax
- Proxy - Eg: Hibernate proxy for lazy fetch. @Spy instances for JUnit/Mockito.
- Flyweight - Store common characteristics of multiple objects in single place. Eg: Glyph for all characters in a document.
- Bridge - Decouple abstraction from implementation so that both can vary independently. Bridge pattern is often created using Adapter pattern. 
- Composite - Eg: Folder and files


