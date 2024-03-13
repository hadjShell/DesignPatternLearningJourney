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
  * ![entropy-and-cohesion](/Users/hadjshell/Library/CloudStorage/OneDrive-Personal/Extracurricular-Content/SOLID//imgs/entropy-and-cohesion.svg)
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

***

## Structural Design Patterns

***

## Behavioural Design Patterns

