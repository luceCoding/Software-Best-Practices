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
* Abstract Factory
* Decorator
* Singleton
* State

### Design Patterns Categories
* Creational: ways and means of object instantiation
* Structural: mutual composition of classes or objects
* Behavioral: how classes or objects interact and distribute responsibilities among them
* Each can be class-level or object-level

### Notes
When creating concrete objects, this is an area of frequent change and usually requires encapsulation with a design pattern.
Don't code to an implementation(concrete class), instead code to an interface(abstract class or an agreed contract between two classes).

### Follow the Dependency Inversion Principle
* No variable should hold a reference to a concrete class. (Don't use the new operator for a variable, exceptions include hardcoded strings, we expect these to never really change.)
* No class should derive from a concrete class.
* No method should override an implemented method of any of its base class. (If you do this, your base class wasn't even an abstraction to begin with)

# Factory Pattern
### Definition
Defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

### Why we need the factory pattern?
In our programming, we ideally want to program by wishful thinking. Our method takes in or uses something that is passed into it and assume we already have 'said thing' to perform some opertion which satisfies the intended behavior of your method. Your method follows dependency injection, which is good. However, sooner or later, this 'said thing' that is passed into your method must be created. This is where the line between abstraction and concrete will need to be defined. This is a good place for the factory pattern.

However, during this defined place between creating this conrete instance, you must be careful with coupling. Some method will have to create this object. But what happens when this object in the future needs changing? Then you must maintain this piece of code. This is where the factory pattern can help allevite that problem.

If you wanted to change this concrete instance in the future, how would you likely do it? Ideally, you'd like to just create a new class from scratch correct? That way, all changes and anything different about your new custom object is contain in this one class. You don't want to look at any old code and just look at new code. In this way, you elimate any testing on the old code because you know 100% that the old code isn't broken because you never touched it!

### When should you use the factory pattern?

### Factory Pattern Vs. Abstract Factory Pattern
Both are very similar, however, each serve a slightly different purpose. If you have a bunch of different objects you need to create, go with the factory pattern. If you have a set of different objects to create, go with the abstrat factory. One is very focused on creating individual objects while the other is focused on creating a family of invdividual objects.

### Other Factory Pattern references
* https://www.youtube.com/watch?v=EcFVTgRHJLM
