1. Single Responsibility Principle (SRP):
The SRP states that a class should have only one reason to change, meaning it should have a single responsibility or job. By separating concerns, we can achieve better maintainability and avoid tightly coupled code
class EmailComposer:
    def compose_email(self, recipient, content):
        # Code for composing email content

class EmailSender:
    def send_email(self, recipient, content):
        # Code for sending the email
----------

2. Open/Closed Principle (OCP):
The OCP states that software entities (classes, modules, functions) should be open for extension but closed for modification. This means that we should be able to extend the behavior of a module without modifying its source code.

class Shape:
    def calculate_area(self):
        pass

class Circle(Shape):
    def calculate_area(self):
        # Code for calculating the area of a circle

class Rectangle(Shape):
    def calculate_area(self):
        # Code for calculating the area of a rectangle

# Adding a new shape without modifying existing code
class Triangle(Shape):
    def calculate_area(self):
        # Code for calculating the area of a triangle
---------------------

3. Liskov Substitution Principle (LSP):
The LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, a subclass should be able to be used wherever its superclass is expected.

class Bird:
    def fly(self):
        pass

class Duck(Bird):
    def fly(self):
        # Code specific to duck's flying behavior

class Eagle(Bird):
    def fly(self):
        # Code specific to eagle's flying behavior

------------------------

4. Interface Segregation Principle (ISP):
The ISP states that clients should not be forced to depend on interfaces they do not use. It promotes smaller, cohesive interfaces instead of larger, monolithic ones.

class Employee:
    def calculate_pay(self):
        pass

    def submit_time_sheet(self):
        pass

    def update_profile(self):
        pass

# Instead of a monolithic Employee interface, segregate into smaller interfaces
class Payable:
    def calculate_pay(self):
        pass

class ProfileUpdatable:
    def update_profile(self):
        pass


---------------------------------------

5. Dependency Inversion Principle (DIP):
The DIP states that high-level modules should not depend on low-level modules. Both should depend on abstractions. It encourages loose coupling between classes and promotes the use of dependency injection.

class OrderProcessor:
    def __init__(self, payment_processor):
        self.payment_processor = payment_processor

    def process_order(self):
        # Code to process the order
        self.payment_processor.process_payment()

class PaymentGateway:
    def process_payment(self):
        # Code for processing the payment

# Introduce an abstraction (interface) for payment processing
class PaymentProcessor:
    def process_payment(self):
        pass

class PaymentGateway(PaymentProcessor):
    def process_payment(self):
        # Code for processing the payment

# Usage of Dependency Injection to decouple the OrderProcessor from the PaymentGateway
payment_processor = PaymentGateway()
order_processor = OrderProcessor(payment_processor)

------------------------
