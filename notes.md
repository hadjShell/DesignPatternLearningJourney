# Design Pattern

***

## SOLID

### Single Responsibility Principle

* Every software component should have one and **only one responsibility / reason to change**
* Group the responsibilities in a sensible way
* Cohesion
  * The degree to which the various parts of a software component are related
  * Example of garbage classification
  * Aim for high cohesion
  * ![entropy-and-cohesion](imgs/entropy-and-cohesion.svg)
* Coupling
  * The level of inter dependency between various software components
  * Aim for loose coupling
  * ![entropy-and-coupling](imgs/entropy-and-coupling.svg)

* Changes are inevitable, so we need **Higher Cohesion and Loose Coupling**


### Open-Closed Principle

* Software components should be **closed for modification**, but **open for extension**
* New features getting added to the software component should NOT have to modify existing code
* A software component should be extendable to add a new feature or to add a new behavior to it
* Example of PS5 remote control and accessories
* **Key philosophy: one interface, different implementations**
  * Avoid modifying base class, derive from base and override methods
* Open closed principle often requires decoupling

### Liskov Substitution Principle

* Objects should be replacable with their subtypes without effecting the correctness of the program
* Derived classes must be usable through the base class interface, without the need for the user to know the difference
* **It is violated when child class completely modifies the behaviour of the base class method by overriding it**
* Change the way of "IS-A" thinking in the real world
  * E.g. `Square` should NOT be a subclass of `Rectangle`
* Two way of applying LSP
  * Break the hierarchy if it fails the substitution test
  * Use an interface
* Most of time using `instanceof` indicates an issue

### Interface Segregation Principle

* No client should be forced to depend on methods it does not use
* **Minimize the interface**
* Work with SRP and LSP
* Design first, try not to extract interface afterwards

### Dependency Inversion Principle

* High-level modules (business logics) should not depend on the low-level modules (functionalities). Both should depend on abstractions

* Abstractions should not depend on details. Details should depend on abstractions

  * **Instead of instantiating dependencies ourselves, let somebody else gives us the dependencies**

  * ```java
    // From this
    public void writeReport(Report r) {
      JSONFormatter f = new JSONFormatter();
      String report = f.format(r);
      FileWriter w = new FileWriter("report.json");
      w.write(report);
    }
    
    // To this
    public void writeReport(Report r, Formatter f, Writer w) {
      String report = f.format(r);
      w.write(report);
    }
    ```

***

## Creation Design Patterns

* Creational patterns concern the process of object creation
* The problem: **Hard-coding the classes that get instantiated**

### Builder

* Encapsulate the construction of a product and allow it to be constructed **in steps**
* ![builder](imgs/builder.png)
* When to use?
  * Several flavors of an object may be asked for
  * There are a lot of steps involved in creation of an object
  * Avoid to have too many parameters in the constructor
  * **Often used for building Composite**
* How to use?
  * The client creates the Director object and configures it with the desired Builder object, or the client play the role of Director
  * Director notifies the builder whenever a part of the product should be built
  * Builder handles requests from the director and adds parts to the product
  * The client retrieves the product from the builder
* In real world
  * Optionally Builder can keep reference to a Product that it has built so the same Product can be returned in the future
  * It is common to put the Builder as an inner class inside the Product
    * Setters are `private` to achieve **immutability**
  * The Director is rarely implemented as a separate class
  * Abstract Builder is not required if Product is not part of any inheritance hierarchy
  * The methods in Builder often support *method chaining*
* Examples
  * `StringBuilder`, `StringBuffer`
  * `java.util.Calendar.Builder`
* Pitfalls
  * Possibility of partially initialized object. If required properties are missing, `build()` method should provide suitable default values or throw an exception

### Factory Method

* Define an interface for creating an object, but let subclasses **decide** which class to instantiate. Factory Method lets a class **defer** instantiation to subclasses
* ![factory](imgs/factory.png)
  * **Parallel class hierarchy**
* When to use?
  * A class can't anticipate the class of objects it must create
  * A class wants its subclasses to specify the objects it creates
  * Classes delegate responsibility to one of several helper subclasses, and you want to localize the knowledge of which helper subclass is the delegate
* How to use?
  * Creator relies on its subclasses to define the factory method so that it returns an instance of the appropriate ConcreteProduct
* In real world
  * The Creator can be a concrete class and provide a default implementation of factory method
  * The factory method not only instantiates the ConcreteProduct, but can also perform additional operations
* Examples
  * `iterator()` method in `java.util.AbstractCollection`
* Pitfalls
  * It forces you to subclass the Creator class just to create a particular ConcreteProduct object
* Simple Factory Method
  * It isn't a design pattern, it is a programming idiom
  * Move the instantiation logic to a separate class and most commonly to a static method of this class
    * Applying the Dependency Inversion Principle
  * Typically used if we have more than one option when instantiating the object and a simple logic is used to decide the correct class (`switch` block)
    * "*Parameterized factory method*"
    * **No inheritance compared to Factory Method** (Just a ConcreteCreator)

### Abstract Factory

* Provide an interface for creating families of related or dependent objects (a **kit**) without specifying their concrete classes
* ![abstract-factory](imgs/abstract-factory.png)
  * **Like a bundle of Factory Methods**
* When to use?
  * A family of related Product objects is designed to be used together
* How to use?
  * Normally a single instance of a ConcreteFactory class is created at run-time. This concrete factory creates product objects having a particular implementation. To create different product objects, clients should use a different concrete factory
* In real world
  * A concrete factory is often a singleton
  * AbstractFactory classes are often implemented with factory methods, but they can also be implemented using Prototype
* Examples
* Pitfalls
  * Extending abstract factories to produce new sets of Products requires changing the AbstractFactory class and all of its subclasses
  * Difficult to realise the need at the start of the development and usually starts out as a Factory Method

***

## Structural Design Patterns

* Structural patterns deal with the composition of classes or objects

***

## Behavioural Design Patterns

* Behavioral patterns characterize the ways in which classes or objects interact and distribute responsibility

***

## References

* https://java-design-patterns.com/patterns/