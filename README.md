``` Java for learning 



Full Stack Development Syllabus

Sr. No	Topic	Duration

1	Computer Fundamental	6 hours
2	Figma	2 hours
3	HTML	3 hours
4	CSS	3 hours
5	Javascript	4 hours
6	Git & GitHub	2 hours
7	React Js	6 hours
8	Node Js	3 hours
9	Express Js	2 hours
10	MongoDB	4 hours
11	C Programming	6 hours
12	C++ Programming	12 hours
13	Java SE	16 hours
14	Aptitude & Leetcode	14 hours
15	SQL	7 hours
16	Java EE	10 hours
17	Hibernate Framework	10 hours
18	Spring Framework	12 hours
19	Spring Boot Framework	10 hours
20	Docker & Deployment	5 hours
21	Microservices	16 hours
*	Project	2 weeks


# ✅ 1. OOPS Concepts (Encapsulation, Inheritance, Polymorphism, Abstraction, Association, Coupling)

## Object-Oriented Programming (OOP) organizes code into objects, which are instances of classes. Key OOP principles include:

Encapsulation: Hiding internal state using access modifiers.

Inheritance: Child class inherits properties of parent.

Polymorphism: One interface, many implementations.

Abstraction: Showing only relevant features.

Association: Relationship between classes (like "uses-a").

Coupling: Level of dependency between classes.

🔸 Example:
```
// Encapsulation
class Person {
    private String name;
    public void setName(String name) { this.name = name; }
    public String getName() { return name; }
}

// Inheritance & Polymorphism
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

// Abstraction
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}

public class TestOOP {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound(); // Polymorphism

        Shape s = new Circle();
        s.draw(); // Abstraction
    }
}
```

## ✅ 2. Access Modifiers

🔸 Description:
Access modifiers define visibility and accessibility of classes, methods, and variables.

Modifier	Class	Package	Subclass	World
private	✔	✖	✖	✖
default	✔	✔	✖	✖
protected	✔	✔	✔	✖
public	✔	✔	✔	✔

🔸 Example:
```
public class ModifierDemo {
    private int a = 10;        // only inside this class
    protected int b = 20;      // accessible in subclass
    public int c = 30;         // accessible anywhere
    int d = 40;                // default/package-private
}
```

## ✅ 3. Transient Variable
🔸 Description:
transient is used with variables in serialization.

When an object is serialized, transient variables are not saved.

Useful for sensitive data like passwords.

🔸 Example:
```
import java.io.*;

class User implements Serializable {
    String name = "Alice";
    transient String password = "secret123";
}

public class TestTransient {
    public static void main(String[] args) throws Exception {
        User user = new User();

        // Serialize
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("user.ser"));
        out.writeObject(user);
        out.close();

        // Deserialize
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("user.ser"));
        User newUser = (User) in.readObject();
        in.close();

        System.out.println("Name: " + newUser.name);         // Alice
        System.out.println("Password: " + newUser.password); // null (transient)
    }
}
```

## ✅ 4. Volatile Variable
🔸 Description:
The volatile keyword is used in multithreading.

It tells Java not to cache the variable locally and read it from main memory.

Ensures visibility of changes across threads.

🔸 Example:
```
class SharedData {
    volatile boolean flag = false;

    void run() {
        while (!flag) {
            // waiting for flag to become true
        }
        System.out.println("Flag is true. Thread ends.");
    }

    public static void main(String[] args) {
        SharedData data = new SharedData();

        new Thread(() -> data.run()).start();

        try {
            Thread.sleep(1000); // wait before setting flag
        } catch (InterruptedException e) { }

        data.flag = true; // change visible to other thread
    }
}
```

## ✅ 5. Atomic Variable
🔸 Description:
Used for lock-free, thread-safe operations on single variables.

Classes like AtomicInteger, AtomicBoolean, AtomicLong in java.util.concurrent.atomic.

🔸 Example:
```
import java.util.concurrent.atomic.AtomicInteger;

public class AtomicDemo {
    AtomicInteger count = new AtomicInteger(0);

    void increment() {
        count.incrementAndGet(); // atomic operation
    }

    public static void main(String[] args) {
        AtomicDemo demo = new AtomicDemo();
        demo.increment();
        demo.increment();
        System.out.println(demo.count); // Output: 2
    }
}
```

## ✅ 6. final, finally
🔸 Description:
final: Used to declare constants, prevent method overriding or inheritance.

finally: A block that always executes after try-catch (used for cleanup).

finalize(): Method called by garbage collector before destroying an object (Deprecated in Java 9+).

🔸 Example:
```
public class FinalDemo {
    final int x = 10; // cannot be changed

    final void show() {
        System.out.println("This method cannot be overridden");
    }

    public static void main(String[] args) {
        try {
            int a = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Caught exception");
        } finally {
            System.out.println("Finally block always executes");
        }
    }
}
```
### ✅ 7. Immutable Class
🔸 Description:
An immutable class is one whose objects cannot be modified after creation.

To create:

Use final class.

All fields must be private and final.

No setters.

If returning mutable fields, return a copy.

🔸 Example:
```
final class Student {
    private final String name;
    private final int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Only getters, no setters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

public class TestImmutable {
    public static void main(String[] args) {
        Student s = new Student("Aman", 21);
        System.out.println(s.getName()); // Aman
    }
}
```


## ✅ 8. static and synchronized
🔸 Description:
static: Belongs to the class, not instance. Shared across all objects.

synchronized: Ensures only one thread accesses a block/method at a time (thread-safety).

🔸 Example:
```
public class SyncStaticDemo {
    static int count = 0;

    public synchronized static void increment() {
        count++;
    }

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for(int i = 0; i < 1000; i++) increment();
        });

        Thread t2 = new Thread(() -> {
            for(int i = 0; i < 1000; i++) increment();
        });

        t1.start(); t2.start();
        t1.join(); t2.join();

        System.out.println("Count: " + count); // 2000
    }
}
```

## ✅ 9. Ways to Create Object in Java
🔸 Description:
Java supports 5 ways to create an object:

new keyword

Class.forName() + reflection

clone() method

ObjectInputStream (deserialization)

newInstance() (deprecated)

🔸 Example:
```
// 1. Using new
Student s1 = new Student();

// 2. Using Class.forName
Student s2 = (Student) Class.forName("Student").getDeclaredConstructor().newInstance();

// 3. Using clone()
Student s3 = (Student) s1.clone();

// 4. Using deserialization
ObjectInputStream in = new ObjectInputStream(new FileInputStream("file.ser"));
Student s4 = (Student) in.readObject();

// 5. newInstance (deprecated)
Student s5 = Student.class.newInstance(); // discouraged in Java 9+
Make sure class implements Cloneable and Serializable as needed for clone and deserialization.
```

## ✅ 10. Abstract Class vs Interface
🔸 Description:
Feature	Abstract Class	Interface (Java 8+)
Methods	Abstract + Concrete	Abstract + default/static
Variables	Can have state	Only public static final
Inheritance	One abstract class	Multiple interfaces
Constructor	Yes	No

🔸 Example:
```
abstract class Animal {
    abstract void makeSound();
    void sleep() {
        System.out.println("Sleeping...");
    }
}

interface Flyable {
    void fly();
}

class Bird extends Animal implements Flyable {
    public void makeSound() {
        System.out.println("Chirp chirp");
    }
    public void fly() {
        System.out.println("Bird is flying");
    }
}
```


## ✅ 11. Try with Resources
🔸 Description:
Introduced in Java 7 to automatically close resources (like files, sockets, streams).

The object used inside try() must implement the AutoCloseable interface.

No need for a separate finally block to close resources.

🔸 Example:
```
import java.io.*;
public class TryWithResourcesDemo {
    public static void main(String[] args) {
        // FileReader and BufferedReader implement AutoCloseable
        try (BufferedReader br = new BufferedReader(new FileReader("input.txt"))) {
            String line;
            while ((line = br.readLine()) != null)
                System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
✅ Resource is automatically closed after try block, even if an exception occurs.


## ✅ 12. Design Patterns (Singleton, Prototype, Factory)
🔸 Description:
Design Patterns are proven solutions to common software design problems.

Common Patterns in Java:

Singleton: Only one object created.

Prototype: Create a clone of an object.

Factory: Create object without exposing instantiation logic.

🔸 Example: Singleton Pattern
```
class Singleton {
    private static Singleton instance;

    private Singleton() {} // private constructor

    public static Singleton getInstance() {
        if (instance == null)
            instance = new Singleton();
        return instance;
    }
}

public class SingletonTest {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2); // true (same object)
    }
}
```

## ✅ 13. Exception Handling in Java
🔸 Description:
Java handles runtime errors using try, catch, finally, and throw.

Types of Exceptions:

Checked: Must be handled (e.g., IOException)

Unchecked: Occurs at runtime (e.g., NullPointerException)

🔸 Example:
```
public class ExceptionDemo {
    public static void main(String[] args) {
        try {
            int a = 10 / 0; // ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero");
        } finally {
            System.out.println("Finally block always executes");
        }
    }
}
```

## ✅ 14. Custom Exception
🔸 Description:
You can define your own exception by extending Exception or RuntimeException. Useful for business-specific errors.

🔸 Example:
```
class AgeInvalidException extends Exception {
    AgeInvalidException(String msg) {
        super(msg);
    }
}

public class CustomExceptionDemo {
    static void validateAge(int age) throws AgeInvalidException {
        if (age < 18)
            throw new AgeInvalidException("Age must be >= 18");
    }

    public static void main(String[] args) {
        try {
            validateAge(15);
        } catch (AgeInvalidException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```

## ✅ 15. throw vs throws
🔸 Description:
Keyword	Used For
throw	To explicitly throw an exception
throws	To declare exceptions in method signature

🔸 Example:
```
public class ThrowThrowsDemo {
    // throws declares the possibility of an exception
    static void checkAge(int age) throws Exception {
        if (age < 18)
            throw new Exception("Not eligible"); // throw an exception
    }

    public static void main(String[] args) {
        try {
            checkAge(16);
        } catch (Exception e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```


## ✅ 16. JVM (Java Virtual Machine)
🔸 Description:
JVM is the engine that runs Java bytecode. It translates .class files into machine code and executes them.
It handles:

Memory allocation

Garbage Collection

Class loading

Thread management

JVM is platform-dependent, but Java code is platform-independent due to the JVM.

🔸 JVM Components:
Class Loader: Loads .class files

Runtime Memory: Heap, Stack, Method Area

Execution Engine: Executes bytecode

Garbage Collector: Frees memory automatically

🔸 No direct code, but every Java program runs inside the JVM.


## ✅ 17. Memory Management in Java
🔸 Description:
Java memory is divided into regions, managed by the JVM.

Heap: All objects and instance variables

Stack: Stores method calls and local variables

Method Area: Class metadata, static variables

Garbage Collector: Reclaims memory of unreachable objects

🔸 Example:
```
class MemoryDemo {
    int x = 5;  // stored in heap with object

    public static void main(String[] args) {
        int y = 10;         // stored in stack
        MemoryDemo obj = new MemoryDemo(); // obj in heap
    }
}
```
JVM takes care of allocating and releasing memory — no need for malloc() or free() like in C/C++.

## ✅ 18. Memory Leak
🔸 Description:
A memory leak happens when objects are no longer used but still referenced, so GC can’t clean them up.
Over time, this causes the program to use too much memory and potentially crash.

🔸 Example:
```
import java.util.*;
public class MemoryLeak {
    public static void main(String[] args) {
        List<Object> list = new ArrayList<>();
        while (true) {
            list.add(new Object()); // never released => memory leak
        }
    }
}
```
Fix: Nullify references, remove unused elements, avoid static references holding large objects.

## ✅ 19. Garbage Collection
🔸 Description:
Garbage Collection (GC) is the automatic process of reclaiming memory by removing objects that are no longer reachable.

GC in Java is non-deterministic — we can request GC with System.gc(), but JVM may ignore it.

🔸 Example:
```
class GCExample {
    protected void finalize() {
        System.out.println("Object is garbage collected");
    }

    public static void main(String[] args) {
        GCExample obj = new GCExample();
        obj = null;
        System.gc(); // Request GC
    }
}
```
finalize() is deprecated in Java 9+. Use Cleaner or try-with-resources instead.


## ✅ 20. How to Create an Immutable Class
🔸 Description:
An immutable class cannot be modified after its object is created. Steps:

Declare class as final

Make all fields private final

Initialize fields via constructor

No setters

Return defensive copies for mutable fields

🔸 Example:
```
final class Employee {
    private final String name;
    private final int id;

    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }

    // Getters only
    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }
}

public class ImmutableTest {
    public static void main(String[] args) {
        Employee e = new Employee("John", 101);
        System.out.println(e.getName()); // John
    }
}
```


## ✅ 21. Why String is Immutable in Java
🔸 Description:
A String in Java is immutable, meaning once it’s created, it cannot be changed. Instead, any modification creates a new object.

🔸 Why String is immutable:
Security: Strings used in class loaders, file paths, etc.

Thread Safety: No synchronization needed

String Pooling: Shared objects in heap for memory efficiency

Caching HashCode: Improves performance in collections like HashMap

🔸 Example:
```
public class StringImmutable {
    public static void main(String[] args) {
        String a = "Hello";
        String b = a;
        a = "World";

        System.out.println(b); // Hello (b still points to old object)
    }
}
```

## ✅ 22. SOLID Principles
🔸 Description:
SOLID is a set of 5 design principles for object-oriented programming that promote maintainable and scalable code.

Principle	Meaning
S - Single Responsibility	One class = one responsibility
O - Open/Closed	Open for extension, closed for modification
L - Liskov Substitution	Subtypes should be substitutable for base types
I - Interface Segregation	Use many small interfaces instead of one big one
D - Dependency Inversion	Depend on abstraction, not on concrete classes

🔸 Example (Single Responsibility Principle - SRP):
```
class Invoice {
    void calculateTotal() {
        // logic here
    }
}

class InvoicePrinter {
    void print(Invoice invoice) {
        // logic here
    }
}
```
✅ Each class handles one job — this is SRP in action.


## ✅ 23. Can We Override Static Methods?
🔸 Description:
Static methods cannot be overridden, because they belong to the class, not the object.

If a subclass defines a static method with the same name, it hides the parent method (called method hiding).

🔸 Example:
```
class Parent {
    static void show() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    static void show() {
        System.out.println("Child static method");
    }
}

public class StaticOverrideTest {
    public static void main(String[] args) {
        Parent.show(); // Parent static method
        Child.show();  // Child static method
    }
}
```
✅ This is method hiding, not true overriding.


## ✅ 24. Overloading vs Overriding
🔸 Description:
Feature	Overloading	Overriding Class Same class	Subclass Method name Same Same Parameters Different	Same
Return type	Can be same or different Must be same or covariant Binding Time Compile-time Runtime.

🔸 Example:
```
class A {
    void show(String msg) {
        System.out.println("Message: " + msg);
    }

    void show(String msg, int times) { // Overloaded
        for (int i = 0; i < times; i++)
            System.out.println(msg);
    }
}

class B extends A {
    @Override
    void show(String msg) { // Overridden
        System.out.println("B says: " + msg);
    }
}
```

## ✅ 25. Ways to Create Object in Java
🔸 Description:
There are five ways to create objects in Java:

Using new keyword

Using Class.forName() + reflection

Using clone() method

Using ObjectInputStream (deserialization)

Using Constructor.newInstance()

🔸 Example:
```
class Person implements Cloneable, Serializable {
    String name = "John";
    
    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

public class ObjectCreationDemo {
    public static void main(String[] args) throws Exception {
        // 1. Using new
        Person p1 = new Person();

        // 2. Using Class.forName
        Person p2 = (Person) Class.forName("Person").getDeclaredConstructor().newInstance();

        // 3. Using clone
        Person p3 = (Person) p1.clone();

        // 4. Using deserialization
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("obj.ser"));
        out.writeObject(p1);
        out.close();

        ObjectInputStream in = new ObjectInputStream(new FileInputStream("obj.ser"));
        Person p4 = (Person) in.readObject();
        in.close();

        // 5. Using Constructor
        Constructor<Person> constructor = Person.class.getConstructor();
        Person p5 = constructor.newInstance();
    }
}
```


## ✅ 26. Java is Call by Value
🔸 Description:
Java uses call by value for all method calls. This means:

A copy of the variable is passed.

For primitives: actual value is passed.

For objects: copy of the reference is passed (not the object itself).

Changing the object’s internal state works, but reassigning the reference does not affect the original object.

🔸 Example:
```
class Demo {
    int value = 10;
}

public class CallByValueTest {
    public static void modify(Demo d) {
        d.value = 20;         // changes original object's field
        d = new Demo();       // this new object is local
        d.value = 30;
    }

    public static void main(String[] args) {
        Demo obj = new Demo();
        modify(obj);
        System.out.println(obj.value); // Output: 20
    }
}
```

## ✅ 27. ClassLoader in Java
🔸 Description:
A ClassLoader is part of JVM that loads .class files. Types:

Bootstrap ClassLoader – loads core Java classes (rt.jar)

Extension ClassLoader – loads from ext folder

System/Application ClassLoader – loads user classes

🔸 Example:
```
public class ClassLoaderDemo {
    public static void main(String[] args) {
        System.out.println("ClassLoader of this class: " + ClassLoaderDemo.class.getClassLoader());
        System.out.println("ClassLoader of String class: " + String.class.getClassLoader()); // null => Bootstrap
    }
}
```


## ✅ 28. Serialization
🔸 Description:
Serialization is the process of converting an object into a byte stream so it can be saved to a file or sent over a network.

Use implements Serializable

Mark unwanted fields with transient

Use ObjectOutputStream and ObjectInputStream

🔸 Example:
```
import java.io.*;

class User implements Serializable {
    String name;
    transient String password; // not serialized
    User(String n, String p) {
        name = n;
        password = p;
    }
}

public class SerializationTest {
    public static void main(String[] args) throws Exception {
        User user = new User("John", "1234");

        // Serialization
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("user.ser"));
        out.writeObject(user);
        out.close();

        // Deserialization
        ObjectInputStream in = new ObjectInputStream(new FileInputStream("user.ser"));
        User u2 = (User) in.readObject();
        in.close();

        System.out.println(u2.name);     // John
        System.out.println(u2.password); // null (because it was transient)
    }
}
```

## ✅ 29. Marker Interface
🔸 Description:
A Marker Interface is an interface that has no methods or fields. It provides metadata to JVM or compiler.

Examples: Serializable, Cloneable, Remote

Used as a flag for some special treatment.

🔸 Example:
```
interface MyMarker {} // Marker Interface

class DemoClass implements MyMarker {
    // JVM or framework might use reflection to treat marked classes differently
}
```
✅ Useful when a class must be eligible for certain operations (like serialization).



## ✅ 30. String Class Methods
🔸 Description:
Java’s String class is rich in built-in methods. Some popular ones:

Method	Description
length()	Returns length of string
charAt(index)	Returns char at index
equals()	Checks content equality
equalsIgnoreCase()	Ignores case in comparison
substring()	Extracts part of the string
indexOf()	Finds index of a character or string
toUpperCase()	Converts to upper case
split()	Splits string into array
replace()	Replaces text

🔸 Example:
```
public class StringMethods {
    public static void main(String[] args) {
        String s = "Hello World";
        System.out.println(s.length());              // 11
        System.out.println(s.charAt(4));             // o
        System.out.println(s.substring(0, 5));       // Hello
        System.out.println(s.toUpperCase());         // HELLO WORLD
        System.out.println(s.indexOf("World"));      // 6
        String[] parts = s.split(" ");
        System.out.println(parts[1]);                // World
    }
}
```

## ✅ 31. Object Class Methods
🔸 Description:
Every class in Java implicitly extends Object, the root of the class hierarchy. It provides several useful methods:

Method	Purpose
toString()	Returns string representation of object
equals()	Compares object references or values
hashCode()	Returns hash code for use in collections
getClass()	Gets the runtime class
clone()	Creates a shallow copy (implements Cloneable)
finalize()	Called by GC before object removal (deprecated)

🔸 Example:
```
class Car {
    String model = "Tesla";

    public String toString() {
        return "Model: " + model;
    }

    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Car)) return false;
        Car c = (Car) o;
        return this.model.equals(c.model);
    }
}

public class ObjectMethods {
    public static void main(String[] args) {
        Car c1 = new Car();
        Car c2 = new Car();
        System.out.println(c1.toString());      // Model: Tesla
        System.out.println(c1.equals(c2));      // true
        System.out.println(c1.getClass());      // class Car
    }
}
```

## ✅ 32. hashCode() vs equals()
🔸 Description:
Method	Purpose
equals()	Compares objects logically (content)
hashCode()	Used in hashing, e.g., in HashMap

If you override equals(), you must also override hashCode()

Two equal objects must return the same hashCode()

🔸 Example:
```
class Book {
    int id;
    String title;

    Book(int id, String title) {
        this.id = id;
        this.title = title;
    }

    public boolean equals(Object o) {
        Book b = (Book) o;
        return this.id == b.id && this.title.equals(b.title);
    }

    public int hashCode() {
        return id * 31 + title.hashCode();
    }
}

public class HashCodeEqualsDemo {
    public static void main(String[] args) {
        Book b1 = new Book(1, "Java");
        Book b2 = new Book(1, "Java");

        System.out.println(b1.equals(b2));       // true
        System.out.println(b1.hashCode() == b2.hashCode()); // true
    }
}
```


## ✅ 33. Generics
🔸 Description:
Generics allow type-safe, reusable code. Introduced in Java 5.

Prevents ClassCastException

Adds compile-time type checking

🔸 Example:
```
import java.util.*;

public class GenericDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        // list.add(10); // compile-time error

        for (String s : list) {
            System.out.println(s);
        }
    }
}
```
🔸 Generic Method:
```
public class GenericMethod {
    public static <T> void printArray(T[] arr) {
        for (T t : arr) System.out.println(t);
    }

    public static void main(String[] args) {
        Integer[] nums = {1, 2, 3};
        printArray(nums); // Generic method call
    }
}
```


## ✅ 34. Enum in Java
🔸 Description:
enum is a special data type that holds fixed set of constants.

Can have fields, constructors, and methods.

🔸 Example:
```
enum Day {
    MON, TUE, WED, THU, FRI, SAT, SUN;

    public boolean isWeekend() {
        return this == SAT || this == SUN;
    }
}

public class EnumTest {
    public static void main(String[] args) {
        Day today = Day.FRI;
        System.out.println(today); // FRI
        System.out.println(today.isWeekend()); // false
    }
}
```


## ✅ 35. Inner Class & Anonymous Class
🔸 Description:
Inner Class: A class declared inside another class.

Anonymous Class: A class without a name, declared and instantiated in one go — often used with interfaces or abstract classes.

🔸 Example:
```
class Outer {
    private int data = 100;

    class Inner {
        void show() {
            System.out.println("Data: " + data);
        }
    }

    void anonymousClassExample() {
        Runnable r = new Runnable() {
            public void run() {
                System.out.println("Anonymous class running...");
            }
        };
        r.run();
    }
}

public class InnerDemo {
    public static void main(String[] args) {
        Outer o = new Outer();
        Outer.Inner in = o.new Inner();
        in.show();

        o.anonymousClassExample();
    }
}
```


## ✅ 36. Functional Interface
🔸 Description:
A functional interface is an interface with only one abstract method. It can have default or static methods.
Used heavily in Lambda expressions and Streams.

Annotated with @FunctionalInterface (optional but recommended)

🔸 Common Examples:
Runnable

Callable

Comparator

Function<T,R>, Predicate<T>

🔸 Example:
```
@FunctionalInterface
interface MyFunction {
    void display(); // Only one abstract method allowed
}

public class FunctionalInterfaceDemo {
    public static void main(String[] args) {
        MyFunction mf = () -> System.out.println("Hello from Lambda!");
        mf.display();
    }
}
```


## ✅ 37. Stream API
🔸 Description:
The Stream API (Java 8+) provides a functional-style way to process sequences of data (collections, arrays, etc.).

Lazily executed

Pipeline structure: source → intermediate operations → terminal operation

🔸 Example:
```
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Aman", "Alok", "Ravi", "Ramesh");

        names.stream()
             .filter(name -> name.startsWith("A"))
             .map(String::toUpperCase)
             .forEach(System.out::println); // AMAN, ALOK
    }
}
```


## ✅ 38. Intermediate vs Terminal Operations
🔸 Description:
Intermediate Operations	Terminal Operations
Returns another stream	Ends the stream pipeline
Lazy	Eager (triggers execution)
Examples: filter(), map(), sorted()	Examples: collect(), forEach(), count()

🔸 Example:
```
import java.util.*;
import java.util.stream.*;

public class StreamOps {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);

        long count = nums.stream()           // source
                         .filter(n -> n % 2 == 0) // intermediate
                         .count();               // terminal

        System.out.println("Even numbers: " + count); // Output: 2
    }
}
```

## ✅ 39. map() vs flatMap()
🔸 Description:
map()	flatMap()
Transforms each element	Flattens nested structure
Returns Stream<Stream<T>>	Returns Stream<T>

🔸 Example:
```
import java.util.*;
import java.util.stream.*;

public class MapFlatMapDemo {
    public static void main(String[] args) {
        List<List<String>> names = Arrays.asList(
            Arrays.asList("Aman", "Ajay"),
            Arrays.asList("Ravi", "Ramesh")
        );

        System.out.println("Using map:");
        names.stream()
             .map(list -> list.stream())
             .forEach(s -> s.forEach(System.out::println)); // Nested loops

        System.out.println("Using flatMap:");
        names.stream()
             .flatMap(list -> list.stream())
             .forEach(System.out::println); // Flattens all into one stream
    }
}
```

## ✅ 40. Stream vs Collection
🔸 Description:
Stream	Collection
Does not store data	Stores elements
Functional-style operations	Object-oriented access
Lazy evaluation (unless terminal op)	Eager evaluation
Cannot be reused (one-time use)	Can be reused
Added in Java 8 (java.util.stream)	Core API since Java 1.2

🔸 Example:
```
List<String> list = Arrays.asList("apple", "banana", "cherry");

// Collection operation
System.out.println(list.get(1)); // banana

// Stream operation
list.stream()
    .filter(f -> f.startsWith("b"))
    .forEach(System.out::println); // banana

```


## ✅ 41. Optional Class in Java
🔸 Description:
Optional<T> is a container object used to represent nullable values and avoid NullPointerException.

Introduced in Java 8, it helps handle cases where a value may or may not be present.

🔸 Common Methods:
isPresent()

ifPresent()

orElse()

orElseGet()

orElseThrow()

🔸 Example:
```
import java.util.Optional;

public class OptionalDemo {
    public static void main(String[] args) {
        Optional<String> name = Optional.ofNullable(null);

        System.out.println(name.isPresent());           // false
        System.out.println(name.orElse("Default Name")); // Default Name

        Optional<String> email = Optional.of("hello@xyz.com");
        email.ifPresent(e -> System.out.println("Email: " + e)); // prints email
    }
}
```

## ✅ 42. Lambda Expression
🔸 Description:
A lambda expression is a short block of code which takes in parameters and returns a value.
Used to implement functional interfaces inline.

Syntax:
```
(parameters) -> { expression }
🔸 Example:
java
Copy
Edit
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

public class LambdaDemo {
    public static void main(String[] args) {
        MathOperation add = (a, b) -> a + b;
        MathOperation mul = (a, b) -> a * b;

        System.out.println(add.operate(5, 3)); // 8
        System.out.println(mul.operate(5, 3)); // 15
    }
}
```


## ✅ 43. Method Reference
🔸 Description:
A method reference is a shorthand syntax for calling a method via a lambda expression.

Types of Method References:

ClassName::staticMethod

object::instanceMethod

ClassName::instanceMethod

ClassName::new (constructor reference)

🔸 Example:
```
import java.util.*;

public class MethodRefDemo {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("java", "python", "c++");

        // Using lambda
        list.forEach(s -> System.out.println(s));

        // Using method reference
        list.forEach(System.out::println); // cleaner
    }
}
```


## ✅ 44. Comparable vs Comparator
🔸 Description:
Feature	Comparable	Comparator
Package	java.lang	java.util
Interface	compareTo(Object o)	compare(Object o1, Object o2)
Sorting Logic	In the object itself	Separate class
Use Case	Natural ordering	Multiple sorting logic (custom)

🔸 Example:
```
// Comparable Example
class Student implements Comparable<Student> {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id; this.name = name;
    }

    public int compareTo(Student s) {
        return this.id - s.id;
    }
}

// Comparator Example
class NameComparator implements Comparator<Student> {
    public int compare(Student a, Student b) {
        return a.name.compareTo(b.name);
    }
}

Collections.sort(list);                    // Uses Comparable
Collections.sort(list, new NameComparator()); // Uses Comparator
```


## ✅ 45. Functional Interfaces in Java 8
🔸 Description:
Java 8 introduced many built-in functional interfaces in the java.util.function package.

Interface	Description
Function<T,R>	Takes T, returns R
Predicate<T>	Takes T, returns boolean
Consumer<T>	Takes T, returns nothing
Supplier<T>	Takes nothing, returns T

🔸 Example:
```
import java.util.function.*;

public class FunctionalInterfaceDemo {
    public static void main(String[] args) {
        Predicate<String> isLong = s -> s.length() > 5;
        System.out.println(isLong.test("Hello")); // false

        Function<Integer, Integer> square = x -> x * x;
        System.out.println(square.apply(4)); // 16

        Consumer<String> printer = s -> System.out.println(s.toUpperCase());
        printer.accept("java");

        Supplier<Double> randomSupplier = () -> Math.random();
        System.out.println(randomSupplier.get());
    }
}
```


## ✅ 46. Multithreading in Java
🔸 Description:
Multithreading allows concurrent execution of two or more parts of a program for better performance and resource utilization.

Each part runs as an independent thread in a single process.

🔸 Benefits:
Faster execution on multi-core systems

Efficient CPU usage

Useful in games, servers, UIs, etc.

🔸 Example:
```
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class MultiThreadDemo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();

        new Thread(() -> System.out.println("Lambda Thread")).start();
    }
}
```


## ✅ 47. Thread Life Cycle
🔸 Description:
Java threads go through the following states:

New → created using new Thread()

Runnable → after start()

Running → selected by the scheduler

Blocked/Waiting → waiting for a lock/resource

Terminated → after run() completes or exception occurs

🔸 Example:
```
class MyTask implements Runnable {
    public void run() {
        System.out.println("Running thread...");
    }
}

public class ThreadLifecycle {
    public static void main(String[] args) {
        Thread t = new Thread(new MyTask());
        System.out.println(t.getState()); // NEW
        t.start();
        System.out.println(t.getState()); // RUNNABLE
    }
}
```

## ✅ 48. Thread Class vs Runnable Interface
🔸 Description:
Feature	Thread class	Runnable interface
Inheritance	Extends Thread (single inheritance)	Can implement Runnable + extend other class
Design	Tightly coupled	Loosely coupled (recommended)
Reusability	Less reusable	More reusable

🔸 Example:
```
// Using Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread using Thread class");
    }
}

// Using Runnable interface
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread using Runnable");
    }
}

public class ThreadVsRunnable {
    public static void main(String[] args) {
        new MyThread().start();

        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```


## ✅ 49. Daemon Thread
🔸 Description:
A Daemon thread is a background service thread that runs until all user threads finish.

Common in GC, background cleanup, monitoring, etc.

Set with setDaemon(true) before starting the thread.

🔸 Example:
```
public class DaemonExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            while (true)
                System.out.println("Daemon thread running...");
        });

        t.setDaemon(true);
        t.start();

        System.out.println("Main thread ending...");
    }
}
```
The daemon thread will stop automatically once the main thread ends.



## ✅ 50. sleep() vs wait()
Feature	sleep()	wait()
Defined in	Thread class	Object class
Lock released?	❌ No	✅ Yes
Use case	Pause thread for fixed time	Coordination between threads
Throws	InterruptedException	InterruptedException
Must be called in synchronized block?	❌ No	✅ Yes

🔸 Example:
```
public class SleepWaitDemo {
    public static void main(String[] args) throws InterruptedException {
        Object lock = new Object();

        // sleep() example
        Thread.sleep(1000); // pause for 1 sec

        // wait() example
        synchronized (lock) {
            lock.wait(1000); // releases lock and waits
        }
    }
}
```


## ✅ 51. join() and yield() Methods
🔸 join():
Waits for a thread to finish execution before the next continues.

🔸 yield():
Suggests the scheduler to let another thread of same priority execute.

Does not release the lock.

🔸 Example:
```
class JoinYieldDemo {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            System.out.println("Thread t1 running");
        });

        Thread t2 = new Thread(() -> {
            System.out.println("Thread t2 started");
            Thread.yield(); // Hints to scheduler
            System.out.println("Thread t2 finished");
        });

        t1.start();
        t1.join(); // wait for t1 to complete

        t2.start();
    }
}
```


## ✅ 52. Synchronization
🔸 Description:
Synchronization is used to control access to shared resources in a multi-threaded environment and prevent race conditions.

🔸 Types:
Synchronized method

Synchronized block

🔸 Example:
```
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class SyncDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });

        t1.start(); t2.start();
        t1.join(); t2.join();

        System.out.println("Count: " + counter.getCount()); // 2000
    }
}
```


## ✅ 54. Deadlock in Java
🔸 Description:
A deadlock occurs when two or more threads wait forever for each other to release locks, causing program to hang.

🔸 Example:
```
public class DeadlockDemo {
    static final Object Lock1 = "Lock1";
    static final Object Lock2 = "Lock2";

    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (Lock1) {
                System.out.println("Thread 1: Holding Lock1...");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (Lock2) {
                    System.out.println("Thread 1: Acquired Lock2");
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized (Lock2) {
                System.out.println("Thread 2: Holding Lock2...");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (Lock1) {
                    System.out.println("Thread 2: Acquired Lock1");
                }
            }
        });

        t1.start();
        t2.start();
    }
}
```
❗ This example will hang because t1 waits for Lock2, t2 waits for Lock1.



## ✅ 55. Thread Pool (ExecutorService)
🔸 Description:
Thread pools manage multiple threads efficiently, especially when you need to execute many short-lived tasks.

Java provides ExecutorService for this purpose.

🔸 Benefits:
Reuses threads

Reduces overhead

Scales better under load

🔸 Example:
```
import java.util.concurrent.*;

public class ThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        Runnable task = () -> {
            System.out.println("Executing: " + Thread.currentThread().getName());
        };

        for (int i = 0; i < 5; i++) {
            executor.submit(task);
        }

        executor.shutdown(); // Required to exit program
    }
}
```


## ✅ 56. Callable vs Runnable
Feature	Runnable	Callable<V>
Return value	❌ No return	✅ Returns result (V)
Throws Exception?	❌ Cannot throw checked exceptions	✅ Can throw checked exceptions
Used With	Thread, ExecutorService	ExecutorService, Future
Introduced in	Java 1.0	Java 5

🔸 Example:
```
import java.util.concurrent.*;

public class CallableDemo {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<Integer> task = () -> {
            return 10 + 20;
        };

        Future<Integer> future = executor.submit(task);
        System.out.println("Result: " + future.get()); // 30

        executor.shutdown();
    }
}
```


## ✅ 57. Future & CompletableFuture
🔸 Future:
Represents the result of an async computation.
You get result using .get() which blocks until task completes.

🔸 CompletableFuture (Java 8+):
Advanced alternative to Future:

Non-blocking

Callback support

Chaining using thenApply(), thenAccept(), etc.

🔸 Example:
```
import java.util.concurrent.*;

public class FutureVsCompletableFuture {
    public static void main(String[] args) throws Exception {
        // Future
        ExecutorService ex = Executors.newSingleThreadExecutor();
        Future<String> future = ex.submit(() -> "Hello from Future");
        System.out.println(future.get()); // blocking
        ex.shutdown();

        // CompletableFuture
        CompletableFuture.supplyAsync(() -> "Hello from CompletableFuture")
                         .thenApply(str -> str.toUpperCase())
                         .thenAccept(System.out::println); // non-blocking
    }
}
```


## ✅ 58. Collections vs Arrays
Feature	Arrays	Collections (List, Set, etc.)
Size	Fixed	Dynamic
Type	Primitive or Objects	Objects only
Utility	Simple, fast	Rich API, more flexible
Performance	Slightly faster	Slightly heavier but convenient

🔸 Example:
```
// Array
int[] nums = {1, 2, 3};

// Collection
List<Integer> list = new ArrayList<>();
list.add(1); list.add(2);
```


## ✅ 59. Collection vs Collections Class
Feature	Collection (interface)	Collections (utility class)
What is it?	Root interface of Java Collections API	Final class with static helper methods
Package	java.util	java.util
Usage	Implemented by List, Set, etc.	Utility methods like sort(), reverse()

🔸 Example:
```
import java.util.*;

public class CollectionVsCollections {
    public static void main(String[] args) {
        Collection<String> col = new ArrayList<>();
        col.add("Java");

        List<String> list = new ArrayList<>(List.of("B", "A", "C"));
        Collections.sort(list); // sort using Collections class
        System.out.println(list); // [A, B, C]
    }
}
```
#
