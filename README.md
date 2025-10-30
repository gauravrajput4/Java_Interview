Java OOP Concepts: A Comprehensive Guide

Here are the answers to your questions, organized by topic.

1. Core OOP Concepts

What are the four main pillars of Object-Oriented Programming?

The four main pillars of OOP are:

Encapsulation: Bundling data (fields) and the methods that operate on that data within a single unit (a class), and restricting access to the internal state.

Abstraction: Hiding complex implementation details and exposing only the essential features (functionality) to the user.

Inheritance: A mechanism where a new class (subclass) derives properties and behaviors (fields and methods) from an existing class (superclass).

Polymorphism: The ability of an object to take on many forms. In practice, it allows a parent class reference to refer to a child class object.

Explain Encapsulation with a real-world example.

Encapsulation is like a car. As a driver, you interact with a simple interface (steering wheel, pedals, gear stick). You don't need to know the complex, internal details of the engine, transmission, or steering rack.

The "car" (the object) encapsulates its internal state (engine temperature, fuel-air mixture) and hides it from you. It only exposes public methods (accelerate(), steer()).

Code Example:

// Encapsulation: fields are private, accessed via public methods
class BankAccount {
    private double balance; // Data is hidden

    // Public method to deposit (controls access)
    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
            System.out.println("Deposited: " + amount);
        }
    }

    // Public method to get balance (provides read-only access)
    public double getBalance() {
        return this.balance;
    }
}

// In another class:
BankAccount myAccount = new BankAccount();
// myAccount.balance = -1000; // Compile Error! Cannot access private field.
myAccount.deposit(100);       // OK!
System.out.println(myAccount.getBalance()); // OK!


What is Abstraction, and how is it implemented in Java?

Abstraction is the concept of hiding implementation complexity and showing only the necessary features. It focuses on what an object does rather than how it does it.

In Java, abstraction is implemented using:

Abstract Classes: Classes that cannot be instantiated and can have both abstract (unimplemented) and concrete (implemented) methods.

Interfaces: A 100% abstract blueprint that only defines what a class must do, not how.

Code Example:

// Abstraction using an interface
interface Vehicle {
    void start(); // Abstract method (no implementation)
    void stop();
}

// Implementation is hidden inside the concrete class
class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car engine starting...");
    }

    @Override
    public void stop() {
        System.out.println("Car applying brakes...");
    }
}

// User only interacts with the abstract interface
Vehicle myCar = new Car();
myCar.start(); // User doesn't need to know *how* it starts.


What is Inheritance, and why is it important?

Inheritance is a mechanism that allows a class (subclass or child class) to inherit the fields and methods of another class (superclass or parent class). This is an "is-a" relationship (e.g., a "Dog" is an "Animal").

It's important because it promotes code reusability and creates a clear hierarchy.

Code Example:

// Parent class
class Animal {
    String name;
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// Child class inherits from Animal
class Dog extends Animal {
    public void bark() {
        System.out.println("Woof!");
    }
}

// Usage:
Dog myDog = new Dog();
myDog.name = "Buddy"; // Inherited field
myDog.eat();          // Inherited method
myDog.bark();         // Own method


What is Polymorphism? Explain compile-time and runtime polymorphism.

Polymorphism means "many forms." It's the ability of an object to be treated as its parent type, but still invoke its own unique methods.

Compile-Time Polymorphism (Static Binding):

Achieved via method overloading.

The compiler knows which method to call at compile time based on the method's signature (name and parameter types).

class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    double add(double a, double b) {
        return a + b;
    }
}
// Compiler knows which 'add' to call based on arguments:
Calculator calc = new Calculator();
calc.add(10, 20);     // Calls the int version
calc.add(10.5, 20.5); // Calls the double version


Runtime Polymorphism (Dynamic Binding):

Achieved via method overriding.

The JVM determines which method to call at runtime based on the actual object type, not the reference type.

This is also known as Dynamic Method Dispatch.

class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}
class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow!");
    }
}
// Runtime Polymorphism:
Animal myAnimal = new Cat(); // Reference is Animal, Object is Cat
myAnimal.makeSound(); // JVM checks the *object* at runtime and calls Cat's method: "Meow!"


What are the advantages of using OOP principles?

Reusability: Inheritance allows us to reuse code from parent classes.

Maintainability: Encapsulation makes code easier to manage and update, as changes to a class's internal state don't affect other parts of the program.

Security: Encapsulation (data hiding) protects data from unauthorized access.

Flexibility: Polymorphism allows us to write flexible code that can work with objects of different types.

Modularity: Objects are self-contained, making troubleshooting and collaborative development easier.

2. Class and Object

What is a class in Java?

A class is a blueprint or template for creating objects. It defines a set of properties (fields) and behaviors (methods) that objects of that class will have.

// This is a class (a blueprint)
class Dog {
    String breed;
    void bark() {
        System.out.println("Woof!");
    }
}


What is an object, and how is it created in Java?

An object is a real-world entity and an instance of a class. It has its own state (values for its fields) and behavior (its methods).

Objects are created using the new keyword, which allocates memory for the object and calls its constructor.

// 'myDog' is an object (an instance) of the Dog class
Dog myDog = new Dog();
myDog.breed = "Golden Retriever"; // Setting the object's state
myDog.bark(); // Calling the object's behavior


What is the difference between class variables, instance variables, and local variables?

Class Variables (Static Variables):

Declared with the static keyword.

Belong to the class, not to any individual object.

There is only one copy, shared among all objects of the class.

Instance Variables:

Declared inside a class but outside any method.

Belong to the object (instance).

Each object has its own separate copy.

Local Variables:

Declared inside a method, constructor, or block.

Exist only within that block of code.

class Car {
    static int carCount = 0; // 1. Class variable (shared)
    String model;            // 2. Instance variable (one per object)

    Car(String model) {
        this.model = model;
        carCount++;
    }

    void drive() {
        int speed = 60; // 3. Local variable (only exists in this method)
        System.out.println(this.model + " is driving at " + speed + " mph.");
    }
}


What is the purpose of the this keyword?

The this keyword is a reference to the current object instance within its own class.
Its main uses are:

To disambiguate between instance variables and local variables (or parameters) that have the same name.

To call another constructor from within a constructor (this(...)).

class Person {
    private String name;

    // 1. Disambiguation
    Person(String name) {
        this.name = name; // 'this.name' is the instance var, 'name' is the parameter
    }

    // 2. Calling another constructor
    Person() {
        this("Unknown"); // Calls the Person(String name) constructor
    }

    void printName() {
        System.out.println(this.name); // 'this' refers to the current Person object
    }
}


Can we have multiple objects of a single class?

Yes. A class is a blueprint; you can create as many objects (instances) from that blueprint as you need, each with its own state.

Person person1 = new Person("Alice");
Person person2 = new Person("Bob");
// 'person1' and 'person2' are two different objects of the same 'Person' class.


What is a nested (inner) class, and why is it used?

A nested class is a class defined within another class.

Inner Class (Non-static): Has access to all members (including private) of the outer class. It's used to group related functionality and is logically part of the outer class's instance.

Static Nested Class: A static class inside another. It does not have access to the outer class's instance members, only its static members.

Why use it?

Encapsulation: It groups classes that are only used in one place.

Readability: It keeps related logic close together.

Access: An inner class can access the private members of its outer class.

class Outer {
    private int outerField = 10;

    // Inner class
    class Inner {
        void printOuterField() {
            // Can access private member of Outer
            System.out.println("Outer field: " + outerField);
        }
    }
}

// Usage:
Outer outerObj = new Outer();
Outer.Inner innerObj = outerObj.new Inner();
innerObj.printOuterField(); // Prints 10


3. Constructor

What is a constructor in Java?

A constructor is a special method that is automatically called when an object is created (new). Its primary purpose is to initialize the object's state (set initial values for its fields).

It has the same name as the class and no return type (not even void).

class Employee {
    String name;

    // This is the constructor
    Employee(String empName) {
        this.name = empName;
        System.out.println("Employee object created with name: " + this.name);
    }
}

// Constructor is called here:
Employee emp = new Employee("John");


What are the types of constructors in Java?

Default Constructor (No-Arg Constructor):

A constructor that takes no arguments.

If you don't define any constructor in your class, the Java compiler automatically adds a public, no-arg default constructor for you.

Parameterized Constructor:

A constructor that takes one or more parameters to initialize the object's state.

class Book {
    String title;

    // 1. No-Arg Constructor (this one is user-defined)
    Book() {
        this.title = "Untitled";
    }

    // 2. Parameterized Constructor
    Book(String title) {
        this.title = title;
    }
}


What is constructor overloading?

This is the process of defining multiple constructors in the same class, each with a different parameter list (different number, type, or order of parameters).

class Pizza {
    int size;
    boolean cheese;
    boolean pepperoni;

    // Constructor 1
    Pizza(int size) {
        this.size = size;
        this.cheese = true; // default
        this.pepperoni = false; // default
    }

    // Constructor 2 (Overloaded)
    Pizza(int size, boolean cheese, boolean pepperoni) {
        this.size = size;
        this.cheese = cheese;
        this.pepperoni = pepperoni;
    }
}


What is the difference between a constructor and a method?

Feature

Constructor

Method

Purpose

To initialize an object.

To perform an action or behavior.

Name

Must be the same as the class name.

Can be any valid name.

Return Type

Has no return type (not even void).

Must have a return type (void, int, etc.).

Invocation

Called implicitly by the new keyword.

Called explicitly on an object (obj.myMethod()).

Compiler

A default constructor is added if none exists.

No default methods are added.

Can a constructor be private?

Yes. A private constructor prevents the class from being instantiated from outside the class. This is commonly used in:

Singleton Pattern: To ensure only one instance of a class is ever created.

Utility Classes: Classes that only contain static methods (like Math) and should not be instantiated.

Factory Methods: To force users to create objects using a specific static method.

// Singleton Pattern
class DatabaseConnection {
    private static DatabaseConnection instance;

    // 1. Private constructor
    private DatabaseConnection() {
        // connect to DB...
    }

    // 2. Public static method to get the single instance
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
}


What is the default constructor?

The default constructor is a no-argument constructor that the Java compiler inserts into your class if and only if you do not define any other constructor yourself. It's public and simply calls the parent's super() constructor.

class MyClass {
    // No constructor defined here.
    // So, compiler adds:
    // public MyClass() {
    //     super();
    // }
}


If you define any constructor (e.g., a parameterized one), the compiler will not add the default one.

Can a constructor be abstract, static, or final?

No.

abstract: A constructor's job is to create an object. An abstract class/method is meant to be incomplete. This is a direct contradiction.

static: A constructor is tied to an object instance. A static method is tied to the class. This is also a contradiction.

final: A final method cannot be overridden. Constructors are never inherited, so they cannot be overridden, making final meaningless.

How do you call another constructor from the same class (this())?

You use this() with parameters. It must be the very first line in the constructor. This is called constructor chaining.

class Car {
    String model;
    int year;

    // Master constructor
    Car(String model, int year) {
        this.model = model;
        this.year = year;
    }

    // Overloaded constructor
    Car(String model) {
        // Calls the (String, int) constructor with a default year
        this(model, 2024); // MUST be the first line
    }
}


How do you call the parent class constructor (super())?

You use super() with parameters. It is also must be the very first line in the constructor.

If you don't explicitly call super(), the compiler implicitly inserts a call to super() (the parent's no-arg constructor) as the first line.

class Vehicle {
    String type;
    Vehicle(String type) {
        this.type = type;
    }
}

class Truck extends Vehicle {
    int loadCapacity;

    Truck(int loadCapacity) {
        // Must call parent constructor explicitly
        super("Truck"); // MUST be the first line
        this.loadCapacity = loadCapacity;
    }
}


4. Destructor / Finalizer

What is a destructor in Java?

Java does not have the concept of destructors.

Does Java support destructors like C++?

No. C++ requires manual memory management, so destructors are needed to explicitly free memory. Java uses automatic Garbage Collection (GC), so the JVM handles memory deallocation automatically.

What is the purpose of the finalize() method?

finalize() was a method in the Object class. The garbage collector could call this method just before reclaiming an object's memory. Its intended purpose was to clean up non-Java resources (like file handles or native connections).

Why was finalize() deprecated in Java 9?

It was deprecated because it is fundamentally flawed:

Unreliable: There is no guarantee when or even if the garbage collector will run and call finalize().

Performance Issues: It can significantly slow down garbage collection.

Error Prone: Exceptions thrown inside finalize() are ignored.

The modern and reliable replacement is the try-with-resources statement and the AutoCloseable interface.

How does garbage collection work in Java?

The Garbage Collector (GC) is a background process in the JVM. It automatically identifies and reclaims memory occupied by objects that are no-longer reachable (i.e., there are no active references pointing to them). This prevents memory leaks.

Can we manually destroy an object in Java?

No. You cannot force an object to be destroyed. The best you can do is remove all references to it, making it eligible for garbage collection.

String s = new String("Hello");
s = null; // 's' no longer refers to the "Hello" object.
          // The "Hello" object is now eligible for GC.


You can suggest the JVM run the GC with System.gc(), but it is not a command and is not guaranteed to run.

5. Access Modifiers

What are the four access modifiers in Java?

public: Accessible from everywhere.

protected: Accessible within the same package and by subclasses (even in different packages).

default (package-private): No keyword. Accessible only within the same package.

private: Accessible only within the same class.

What is the difference between private, default, protected, and public access?

Modifier

Same Class

Same Package

Subclass (Other Pkg)

Other Pkg (World)

public

Yes

Yes

Yes

Yes

protected

Yes

Yes

Yes

No

default

Yes

Yes

No

No

private

Yes

No

No

No

What is the default access level if no modifier is specified?

It is default (also called package-private). The member is accessible only to classes within the same package.

Can a class be private or protected?

A top-level class (a class in its own .java file) can only be public or default.

An inner/nested class can be private or protected. This restricts where the nested class can be instantiated.

Can a constructor be private? If yes, where is it used?

Yes. It is used to prevent instantiation from outside the class. Common use cases are:

Singleton Pattern

Utility Classes (e.g., java.lang.Math)

(See example in section 3).

What is the difference between protected and default access?

The key difference is subclasses in other packages.

default: Accessible only within the same package.

protected: Accessible within the same package AND by subclasses in different packages.

Can we override private methods?

No. Private methods are not visible to the subclass, so they cannot be overridden. If you define a method with the same signature in the-subclass, it is a completely new method, not an override.

Can an interface method be private or protected?

Before Java 9: No. All methods were implicitly public and abstract.

Since Java 9: An interface can have private methods. These are used as helper methods for the interface's default or static methods.

Protected: No, interface methods cannot be protected.

Why do we make variables private and provide public getter/setter methods?

This is the core principle of Encapsulation.

Data Hiding: It protects the internal state of the object.

Control: Setters allow you to add validation logic.

Flexibility: Getters allow you to return a computed value, not just the raw field.

Security: You can create read-only fields (by providing only a getter) or write-only fields (by providing only a setter).

class User {
    private int age;

    // Setter with validation
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }
    // Getter
    public int getAge() {
        return this.age;
    }
}


Can nested classes have private or protected access?

Yes. (See question "Can a class be private or protected?").

What is the difference between final, finally, and finalize()?

This is a classic interview question.

final (Keyword): A modifier.

Variable: The value cannot be changed (constant).

Method: The method cannot be overridden.

Class: The class cannot be inherited (extended).

finally (Block): Used in try-catch exception handling. The finally block always executes, whether an exception is thrown or not. It's used for cleanup (e.g., closing a file).

finalize() (Method): A (deprecated) method called by the garbage collector before an object is reclaimed.

6. Method Overloading and Overriding

What is method overloading?

Defining multiple methods in the same class with the same name but different parameters (different type, number, or order of parameters). This is compile-time polymorphism.

class Printer {
    void print(String s) { /* ... */ }
    void print(String s, int copies) { /* ... */ }
}


What is method overriding?

Defining a method in a subclass that has the exact same signature (name and parameters) as a method in its superclass. This is runtime polymorphism.

class Animal {
    void speak() { System.out.println("...?"); }
}
class Dog extends Animal {
    @Override // Annotation is optional but good practice
    void speak() { System.out.println("Woof!"); }
}


What are the rules for method overriding?

The method name, parameter list, and order must be identical.

The return type must be the same or a covariant type (a subtype of the parent's return type).

The access modifier cannot be more restrictive (e.g., you can't override a public method as private).

final, static, and private methods cannot be overridden.

The new method cannot throw new or broader checked exceptions.

What is the difference between overloading and overriding?

Feature

Overloading

Overriding

Purpose

Use same name for similar methods.

Provide specific implementation in subclass.

Location

Same class.

Two classes (parent and child).

Signature

Must have different parameters.

Must have identical parameters.

Polymorphism

Compile-Time (Static)

Runtime (Dynamic)

Return Type

Can be different.

Must be same or covariant.

Access

Can be different.

Cannot be more restrictive.

Can we overload the main() method?

Yes. You can have multiple methods named main with different parameters. However, the JVM will only ever call the one with the signature public static void main(String[] args).

Can we override static methods?

No. static methods belong to the class, not the object. If you define a static method with the same signature in a subclass, it is called method hiding, not overriding. The method called is determined at compile time based on the reference type, not at runtime.

What is dynamic method dispatch?

This is another name for runtime polymorphism. It's the mechanism the JVM uses to select which overridden method to execute. It "dispatches" the call to the correct method at runtime based on the actual object's type, not the reference variable's type.

Animal a = new Dog();
a.speak(); // Dynamic dispatch: JVM sees 'a' is *really* a Dog, calls Dog.speak()


Why do we use method overriding?

To allow a subclass to provide its own specific implementation of a method that is already defined in its parent class.

7. Inheritance

What is inheritance?

A core OOP pillar where one class (subclass) acquires the properties and behaviors of another class (superclass) using the extends keyword. It represents an "is-a" relationship.

What are the types of inheritance in Java?

Java supports:

Single Inheritance: A -> B (e.g., Dog extends Animal)

Multilevel Inheritance: A -> B -> C (e.g., GermanShepherd extends Dog extends Animal)

Hierarchical Inheritance: A -> B, A -> C (e.g., Dog extends Animal, Cat extends Animal)

Java does not support:

Multiple Inheritance (with classes): A -> C, B -> C. (This is supported using interfaces).

Hybrid Inheritance: A mix of multiple and multilevel (also not supported via classes).

Why doesn’t Java support multiple inheritance using classes?

To avoid the Diamond Problem.

If Class C inherits from Class A and Class B, and both A and B have a method void doWork(), which version does C inherit? This ambiguity is the diamond problem. Java avoids this by only allowing a class to extend one other class. (Interfaces solve this because default methods can be explicitly chosen).

What is the super keyword, and how is it used?

The super keyword is a reference to the immediate parent class. It is used to:

Call the parent class's constructor: super(parameters);

Access a parent class's method (usually one that is overridden): super.myMethod();

Access a parent class's field: super.myField;

class Parent {
    String name = "Parent";
    void print() { System.out.println("I am the parent."); }
}

class Child extends Parent {
    String name = "Child";
    @Override
    void print() {
        super.print(); // 1. Calls parent's method
        System.out.println("I am the child.");
        System.out.println(this.name); // "Child"
        System.out.println(super.name); // 2. Accesses parent's field
    }
}


Can a child class override private methods of its parent?

No. Private members are not visible to any other class, including subclasses. They are not inherited, so they cannot be overridden.

What is hierarchical inheritance?

When one superclass is extended by two or more subclasses.
Example: Vehicle (parent) is extended by Car, Truck, and Motorcycle.

Can a subclass inherit constructors?

No. Constructors are not inherited. A subclass must call its parent's constructor (either implicitly by the compiler, or explicitly using super()).

8. Abstract Class and Interface

What is an abstract class in Java?

A class declared with the abstract keyword.

It cannot be instantiated (you can't do new MyAbstractClass()).

It can have both abstract methods (no body) and concrete methods (with a body).

It can have fields, constructors, and static methods.

It is designed to be extended (inherited from).

abstract class Shape {
    int x, y; // Can have fields
    abstract void draw(); // Abstract method - must be overridden
    void moveTo(int x, int y) { // Concrete method
        this.x = x;
        this.y = y;
    }
}


Can we create objects of abstract classes?

No, they cannot be instantiated directly. You must create an object of a concrete subclass that extends the abstract class.

What is an interface, and why is it used?

An interface is a 100% abstract blueprint for a class, declared with the interface keyword.

It defines a "contract" of methods that a class must implement.

It is used to achieve 100% abstraction and multiple inheritance (a class can implement multiple interfaces).

By default, all methods are public and abstract (pre-Java 8).

By default, all fields are public, static, and final (constants).

interface Drivable {
    void steer(int direction); // public abstract
    void accelerate(int speed);
    int MAX_SPEED = 120; // public static final
}


What are the differences between abstract class and interface?

Feature

Abstract Class

Interface

Multiple Inheritance

No (can only extend one class)

Yes (can implement many)

Fields

Can have any type (static, final, non-final)

Only public static final (constants)

Methods

Can have abstract and concrete methods

All abstract (pre-J8). Can have default and static methods (J8+).

Constructor

Has a constructor (called by subclass)

No constructor.

Keyword

extends

implements

Purpose**

Share common code/state ("is-a")

Define a contract/behavior ("can-do")

Can an interface have default or static methods?

Yes. Since Java 8:

default methods: Have an implementation. They are automatically inherited by implementing classes, which can use them directly or override them. Used to add new methods to interfaces without breaking existing code.

static methods: Utility methods that belong to the interface itself, not to any implementing class.

Can an abstract class implement an interface?

Yes. An abstract class can implement an interface and can choose to not implement all of the interface's methods (it can leave them abstract for its own concrete subclasses to implement).

Can an interface extend another interface?

Yes. An interface can extend one or more other interfaces, creating an interface hierarchy.

interface Flyable { void fly(); }
interface Swimmable { void swim(); }
// This interface inherits methods from both
interface Amphibious extends Flyable, Swimmable {
    void crawl();
}


Can an interface have constructors?

No. An interface cannot be instantiated, so it has no need for a constructor.

What happens if a class does not implement all interface methods?

If a (concrete) class implements an interface but does not provide an implementation for all of its abstract methods, the class will not compile. To fix this, the class itself must be declared abstract.

9. Encapsulation

What is encapsulation?

(See Section 1) The practice of bundling an object's data (fields) and methods together, and hiding the internal data from the outside world. This is achieved by making fields private and providing public methods (getters/setters) to access them.

How is encapsulation implemented in Java?

Declare the class fields as private.

Provide public "getter" (accessor) and "setter" (mutator) methods to access and modify the private fields.

Why should class fields be private?

To prevent direct, uncontrolled access. If a field is public, any other class can change its value to anything, potentially an invalid one (e.g., myAccount.balance = -10000;). Private fields force access through setter methods, which can (and should) contain validation logic.

What are getter and setter methods?

Getter (Accessor): A public method used to read the value of a private field. (e.g., public String getName() { return this.name; })

Setter (Mutator): A public method used to modify the value of a private field. (e.g., public void setName(String name) { this.name = name; })

How does encapsulation improve data security?

It provides data integrity. By forcing all modifications to go through a setter method, the class can validate the new value before accepting it, ensuring the object's state is always valid.

10. Polymorphism

What is compile-time polymorphism?

(See Section 1) Also called static binding. Achieved via method overloading. The compiler determines which method to call at compile time based on the method signature.

What is runtime polymorphism?

(See Section 1) Also called dynamic binding. Achieved via method overriding. The JVM determines which method to call at runtime based on the actual object's type.

Can constructors be overloaded?

(See Section 3) Yes. This is very common. A class can have multiple constructors with different parameter lists.

Can constructors be overridden?

No. Constructors are not inherited, so they cannot be overridden.

Explain method binding (static vs. dynamic binding).

Static Binding (Compile-Time): The method call is "bound" to the method body at compile time. This is used for private, final, and static methods, as well as overloaded methods. The compiler knows exactly which method to call.

Dynamic Binding (Runtime): The method call is "bound" at runtime. This is used for all other instance methods (overridden methods). The JVM looks at the actual object to decide which version of the method to execute.

11. Static and Final Keywords

What is the static keyword, and where is it used?

The static keyword means the member belongs to the class itself, not to any individual object instance.

It is used for:

Variables (Class Variables): One copy shared by all instances.

Methods (Class Methods): Can be called without creating an object (e.g., Math.random()).

Blocks (Static Initializer): A block of code that runs once when the class is first loaded.

Nested Classes: A static nested class.

What are static variables, static methods, and static blocks?

class MyClass {
    // 1. Static Variable
    public static int instanceCount = 0;

    // 2. Static Block
    static {
        System.out.println("Class is being loaded!");
        instanceCount = 100; // Can initialize static vars
    }

    MyClass() {
        instanceCount++;
    }

    // 3. Static Method
    public static int getInstanceCount() {
        // Cannot use 'this' keyword here
        return instanceCount;
    }
}

// Usage:
System.out.println(MyClass.instanceCount); // Access before any objects
MyClass.getInstanceCount(); // Call method on class


What is the use of the final keyword?

The final keyword is used to make an entity unchangeable.

final variable: A constant. Its value cannot be reassigned after initialization.

final method: Cannot be overridden by a subclass.

final class: Cannot be extended (inherited from). (e.g., String is a final class).

Can a final class be inherited?

No. That is the definition of a final class.

Can a final method be overridden?

No. That is the definition of a final method.

What’s the difference between final, finally, and finalize()?

(See Section 5)

final: A keyword to make a variable, method, or class unchangeable.

finally: A code block in try-catch that always executes.

finalize(): A deprecated method called by the GC before object collection.

12. Miscellaneous OOP Topics

What is upcasting and downcasting?

Upcasting (Implicit): Casting a subclass object to a superclass reference. This is always safe and happens automatically.

Dog myDog = new Dog();
Animal myAnimal = myDog; // Upcasting (implicit)


Downcasting (Explicit): Casting a superclass reference back to its original subclass type. This is risky and requires an explicit cast. It can fail with a ClassCastException if the object isn't actually of that type.

// 'myAnimal' from above
if (myAnimal instanceof Dog) { // Good practice: check first
    Dog anotherDog = (Dog) myAnimal; // Downcasting (explicit)
    anotherDog.bark();
}


Can we inherit constructors?

No. (See Section 7).

What is object cloning in Java?

Creating an exact copy of an object. A class must implement the Cloneable interface and override the Object.clone() method.

Shallow Copy: Copies fields. If a field is an object reference, it copies the reference, not the object. Both old and new objects point to the same inner object.

Deep Copy: Creates a new copy of all fields, including new copies of any referenced objects.

What is the difference between == and .equals()?

== (Operator): Compares references. It checks if two variables point to the exact same object in memory.

.equals() (Method): Compares content. It checks if two objects are "meaningfully" equal.

In the Object class, the default .equals() behaves just like ==.

Classes like String, Integer, etc., override .equals() to compare the actual values (e.g., the sequence of characters).

String s1 = new String("Hello");
String s2 = new String("Hello");

System.out.println(s1 == s2);      // false (different objects in memory)
System.out.println(s1.equals(s2)); // true (same character content)


What is a concrete class?

A "normal" class that is not an abstract class or an interface. It is a complete class that can be instantiated to create objects.

What is a nested or inner class?

(See Section 2) A class defined within another class.

What is the difference between an object and an object reference?

Object: The actual data (the instance) that exists in the computer's memory (the heap).

Object Reference: The variable that points to the memory address of the object.

// 'myCar' is the REFERENCE (a variable on the stack)
// 'new Car()' creates the OBJECT (data in memory on the heap)
Car myCar = new Car();


You interact with the object through its reference.

Can we access private members of another class?

No. The only exception is an inner class, which can access the private members of its outer class.

What is the difference between aggregation, association, and composition?

These all describe relationships between classes.

Association (Uses-a): A relationship where one class uses another. It's the most general "has-a" relationship. (e.g., a Patient uses a Doctor).

Aggregation (Weak Has-a): A specialized "has-a" relationship where one class (the whole) has another class (the part), but the part can exist independently. (e.g., a Department has Professors. If the Department is deleted, the Professors still exist).

Composition (Strong Has-a / Is-part-of): A strong "has-a" relationship where the "part" cannot exist without the "whole". Its lifecycle is tied to the whole. (e.g., a House has Rooms. If the House is destroyed, the Rooms are also destroyed).

What is data hiding in OOPs?

This is the central concept of Encapsulation. It is the practice of hiding the internal state of an object (by making fields private) and requiring all access to go through public methods (getters/setters).

Can we use abstract + final together in Java?

No. This is a compiler error.

abstract means "this method/class must be overridden/extended."

final means "this method/class cannot be overridden/extended."
They are direct contradictions.

What is the purpose of super() and this() in constructors?

(See Section 3)

this(...): Calls another overloaded constructor in the same class.

super(...): Calls a constructor in the immediate parent class.

Both must be the very first line in their constructor, so you can never use both in the same constructor.
