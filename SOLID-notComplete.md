The SOLID principles are a set of guidelines for designing software that aims to make code more maintainable, flexible, and scalable. The principles are named after the five initials of the concepts they represent: Single Responsibility Principle (SRP), Open/Closed Principle (OCP), Liskov Substitution Principle (LSP), Interface Segregation Principle (ISP), and Dependency Inversion Principle (DIP). Let's go through each principle with examples:

Single Responsibility Principle (SRP):
The SRP states that a class should have only one reason to change, meaning it should have a single responsibility or job. By separating concerns, we can achieve better maintainability and avoid tightly coupled code.

Example: Consider a class called EmailSender that is responsible for both composing the email and sending it. This violates SRP because it has multiple responsibilities. Instead, we can split it into two classes: EmailComposer and EmailSender, where EmailComposer is responsible for composing the email content, and EmailSender is responsible for sending the email.

Open/Closed Principle (OCP):
The OCP states that software entities (classes, modules, functions) should be open for extension but closed for modification. This means that we should be able to extend the behavior of a module without modifying its source code.

Example: Suppose we have a Shape class with different subclasses like Circle, Rectangle, and Triangle. Instead of modifying the Shape class every time we introduce a new shape, we can make the Shape class abstract and define an abstract method calculateArea(). Each subclass will implement this method according to its specific shape, allowing us to add new shapes without modifying existing code.

Liskov Substitution Principle (LSP):
The LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, a subclass should be able to be used wherever its superclass is expected.

Example: Consider a scenario where we have a Bird superclass with a method fly(). According to LSP, any subclass of Bird, such as Duck or Eagle, should be able to replace the Bird object in code that expects a Bird. If, for instance, the Duck subclass cannot fly, it would violate LSP, as it would not be substitutable for the Bird class.

Interface Segregation Principle (ISP):
The ISP states that clients should not be forced to depend on interfaces they do not use. It promotes smaller, cohesive interfaces instead of larger, monolithic ones.

Example: Suppose we have an Employee interface that contains methods like calculatePay(), submitTimeSheet(), and updateProfile(). If a class only needs to use the calculatePay() method, it should not be forced to implement the other methods. Instead, we can create smaller interfaces like Payable and ProfileUpdatable to segregate the responsibilities and allow classes to implement only the interfaces they need.

Dependency Inversion Principle (DIP):
The DIP states that high-level modules should not depend on low-level modules. Both should depend on abstractions. It encourages loose coupling between classes and promotes the use of dependency injection.

Example: Consider a scenario where a OrderProcessor class directly depends on a PaymentGateway class. This creates a tight coupling, and it becomes difficult to replace the PaymentGateway with a different implementation. Instead, we can introduce an interface, such as PaymentProcessor, which both the OrderProcessor and the concrete PaymentGateway implement. The `Order
