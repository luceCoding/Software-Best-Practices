### What do design patterns try to solve?
- Reduce maintenance of code.
  - Most of the work for software engineers occur after the code is written. Design patterns attempt to reduce the amount of effort that engineers face during this phase.
- Create a language that other engineers can easily relate to.
  - By having a standard nomenclature, engineers can communicate effectively between each other on a higher level abstraction without discussing implementation details.
- Allow code reuse.
  - Instead of having multiple ways of doing the same thing which indirectly increases maintenance effort. Design patterns can allow engineers to create a collection of items that engineers can easily piece together.
- Deal with the issue of coupling
  - If code is too tightly coupled, it is hard for engineers to change the code without something else breaking.
  - This also indirectly deals with relationships between classes, many design patterns are meant to deal with one-to-one or one-to-many relationships

### Design Patterns use combinations of the following:
* Composition vs. Decomposition (Has-A vs. Is-A relationship)
* Encapsulatation of variances
* Concrete classes vs. dynamic classes (Compile time vs. run-time)
* Hold vs. Wrap

### Design Patterns every software engineer should know
* Strategy
* Observer
* Factory
* Decorator
* Singleton

### Design Patterns Categories
* Creational: ways and means of object instantiation
* Structural: mutual composition of classes or objects
* Behavioral: how classes or objects interact and distribute responsibilities among them
* Each can be class-level or object-level

### Notes
When creating concrete objects, this is an area of frequent change and usually requires encapsulation with a design pattern.
Don't code to an implementation(concrete class), instead code to an interface(abstract class).

### Follow the Dependency Inversion Principle
* No variable should hold a reference to a concrete class. (Don't use the new operator for a variable)
* No class should derive from a concrete class.
* No method should override an implemented method of any of its base class. (If you do this, your base class wasn't even an abstraction to begin with)

### Factory Pattern
Defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
