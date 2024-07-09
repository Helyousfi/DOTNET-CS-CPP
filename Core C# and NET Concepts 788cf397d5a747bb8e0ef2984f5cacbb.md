# Core C# and .NET Concepts

# 1.1 Advanced OOP (inheritance, polymorphism, interfaces, abstract classes)

### a. Inheritance

Inheritance allows one class (derived class) to inherit the properties and methods of another class (base class). 

### Example

```csharp
// Base class
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

// Derived class
public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}

// Usage
Dog dog = new Dog();
dog.Eat(); // Inherited method
dog.Bark(); // Method from Dog class
```

### b. Polymorphism

Polymorphism allows objects to be treated as instances of their base class rather than their derived class. There are two types: compile-time (method overloading) and runtime (method overriding) polymorphism.

### Method Overloading (Compile-time Polymorphism)

Multiple methods with the same name but different signatures.

```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}

// Usage
Calculator calc = new Calculator();
Console.WriteLine(calc.Add(1, 2)); // Calls int Add(int, int)
Console.WriteLine(calc.Add(1.5, 2.5)); // Calls double Add(double, double)
```

### Method Overriding (Runtime Polymorphism)

Derived classes provide a specific implementation of a method declared in a base class.

```csharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Some generic animal sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Bark");
    }
}

// Usage
Animal animal = new Dog();
animal.MakeSound(); // Outputs: Bark

```

### c. Interfaces

Interfaces define a contract that implementing classes must follow. An interface can contain declarations of methods, properties, events, or indexers but cannot contain implementations.

```csharp
public interface IAnimal
{
    void Eat();
    void Sleep();
}

public class Dog : IAnimal
{
    public void Eat()
    {
        Console.WriteLine("Dog is eating");
    }

    public void Sleep()
    {
        Console.WriteLine("Dog is sleeping");
    }
}

// Usage
IAnimal dog = new Dog();
dog.Eat();
dog.Sleep();
```

### 4. Abstract Classes

Abstract classes cannot be instantiated and may contain abstract members (methods without implementation) that must be implemented by derived classes.

```csharp
public abstract class Animal
{
    public abstract void MakeSound(); // Abstract method

    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Bark");
    }
}

// Usage
Animal animal = new Dog();
animal.MakeSound(); // Outputs: Bark
animal.Eat(); // Outputs: Eating...
```

# 1.2 Generics

### a - Generic classes

A generic class is a class that can operate with any data type. The data type is specified when an instance of the class is created.

```csharp
public class GenericList<T>
{
    private List<T> _list = new List<T>();

    public void Add(T item)
    {
        _list.Add(item);
    }

    public T Get(int index)
    {
        return _list[index];
    }
}

// Usage
GenericList<int> intList = new GenericList<int>();
intList.Add(1);
int value = intList.Get(0);

GenericList<string> stringList = new GenericList<string>();
stringList.Add("Hello");
string str = stringList.Get(0);
```

### b - Generic Methods

Generic methods are methods that can operate on different data types specified as parameters.

```csharp
public class Utilities
{
    public void Print<T>(T item)
    {
        Console.WriteLine(item);
    }
}

// Usage
Utilities utilities = new Utilities();
utilities.Print<int>(123);
utilities.Print<string>("Hello");
```

### c - **Constraints**

You can apply constraints to generics to specify the type of arguments that can be used. Constraints help to enforce certain requirements on the type parameters.

```csharp
public class Repository<T> where T : class, new()
{
    public T CreateInstance()
    {
        return new T();
    }
}

// Usage
public class MyClass { }

Repository<MyClass> repository = new Repository<MyClass>();
MyClass instance = repository.CreateInstance();
```

# 1.3 Delegates, Events & Lambda Expressions

**Delegates** in C# are type-safe function pointers or references to methods. They allow methods to be passed as parameters, enabling callback mechanisms and implementing event handling.

```csharp
// Define a delegate type
public delegate void MyDelegate(string message);

public class DelegateExample
{
    // A method that matches the delegate signature
    public void ShowMessage(string message)
    {
        Console.WriteLine(message);
    }

    public void Run()
    {
        // Instantiate the delegate
        MyDelegate del = ShowMessage;

        // Call the delegate
        del("Hello, World!");
    }
}

// Usage
DelegateExample example = new DelegateExample();
example.Run();
```

**Events** are a special kind of delegate in C#. They are used to provide notifications and are typically used in the publisher-subscriber model. An event in a class is like a delegate field except that it can only be invoked from within the class that declares it.

```csharp
public class Publisher
{
    // Declare an event using EventHandler delegate
    public event EventHandler<string> MyEvent;

    public void RaiseEvent(string message)
    {
        // Raise the event
        MyEvent?.Invoke(this, message);
    }
}

public class Subscriber
{
    public void OnEventRaised(object sender, string message)
    {
        Console.WriteLine($"Event received: {message}");
    }
}

// Usage
Publisher publisher = new Publisher();
Subscriber subscriber = new Subscriber();

// Subscribe to the event
publisher.MyEvent += subscriber.OnEventRaised;

// Raise the event
publisher.RaiseEvent("Hello, Events!");
```

**Lambda expressions** are a concise way to represent anonymous methods using a special syntax. They are often used to create delegates or expression tree types and can make code more readable.

```csharp
// Using a lambda expression with a delegate
Func<int, int, int> add = (a, b) => a + b;
int result = add(3, 4);
Console.WriteLine(result); // Output: 7

// Using a lambda expression with LINQ
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
List<int> evenNumbers = numbers.Where(n => n % 2 == 0).ToList();
evenNumbers.ForEach(n => Console.WriteLine(n)); // Output: 2, 4
```

# 1.3 LINQ (Language Integrated Query)

LINQ provides a way to query various data sources (such as arrays, collections, databases, XML documents, etc.) using query syntax similar to SQL. 

**Query syntax** is similar to SQL and is more readable for those familiar with SQL.

```csharp
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var evenNumbers = from num in numbers
                  where num % 2 == 0
                  select num;

foreach (var n in evenNumbers)
{
    Console.WriteLine(n); // Output: 2, 4, 6, 8, 10
}
```

**Method syntax** uses extension methods and lambda expressions, and is more flexible and powerful.

```csharp
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var evenNumbers = numbers.Where(num => num % 2 == 0);

foreach (var n in evenNumbers)
{
    Console.WriteLine(n); // Output: 2, 4, 6, 8, 10
}
```

# 1.3 Asynchronous Programming in C# (async and await)

Asynchronous programming is a method of programming that allows you to perform tasks without blocking the main thread. This is especially useful in scenarios where tasks take a long time to complete, such as I/O operations, network calls, or database queries. In C#, the `async` and `await` keywords are used to implement asynchronous programming.

### async and await Keywords

- **async**: Used to declare a method as asynchronous.
- **await**: Used to pause the execution of an async method until the awaited task completes.
    
    ```csharp
    public async Task<string> GetDataAsync()
    {
        // Simulate a long-running operation
        await Task.Delay(2000);
        return "Hello, async world!";
    }
    
    public async Task RunAsync()
    {
        string result = await GetDataAsync();
        Console.WriteLine(result);
    }
    
    // Usage
    await RunAsync();
    ```
    

# 1.4 Reflection and Attributes

**Reflection** in C# is a mechanism that allows you to inspect and interact with metadata about assemblies, modules, and types at runtime. This includes obtaining information about methods, properties, fields, and events, and invoking methods or accessing fields and properties dynamically.

```csharp
using System;
using System.Reflection;

public class MyClass
{
    public void MyMethod()
    {
        Console.WriteLine("MyMethod invoked");
    }
}

public class ReflectionExample
{
    public static void Main()
    {
        // Get type information
        Type myClassType = typeof(MyClass);

        // Create an instance of MyClass
        object myClassInstance = Activator.CreateInstance(myClassType);

        // Get method information
        MethodInfo myMethod = myClassType.GetMethod("MyMethod");

        // Invoke the method
        myMethod.Invoke(myClassInstance, null);
    }
}
```

**Attributes** in C# are used to add metadata to code elements (such as classes, methods, properties, etc.). Attributes can be queried at runtime using reflection, providing additional information or behavior to the code elements.

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = false)]
public class MyCustomAttribute : Attribute
{
    public string Description { get; }

    public MyCustomAttribute(string description)
    {
        Description = description;
    }
}

[MyCustomAttribute("This is a sample class")]
public class MyClass
{
    [MyCustomAttribute("This is a sample method")]
    public void MyMethod()
    {
        Console.WriteLine("MyMethod invoked");
    }
}

public class AttributeExample
{
    public static void Main()
    {
        Type myClassType = typeof(MyClass);

        // Get custom attribute from class
        MyCustomAttribute classAttribute = (MyCustomAttribute)Attribute.GetCustomAttribute(myClassType, typeof(MyCustomAttribute));
        Console.WriteLine($"Class attribute description: {classAttribute.Description}");

        // Get custom attribute from method
        MethodInfo myMethod = myClassType.GetMethod("MyMethod");
        MyCustomAttribute methodAttribute = (MyCustomAttribute)Attribute.GetCustomAttribute(myMethod, typeof(MyCustomAttribute));
        Console.WriteLine($"Method attribute description: {methodAttribute.Description}");
    }
}
```

### Common Built-in Attributes

1. **[Obsolete]**: Marks a program element as obsolete.
2. **[Serializable]**: Indicates that a class can be serialized.
3. **[DllImport]**: Used for calling unmanaged code.

# 1.5 Exception Handling

Exception handling in C# is a mechanism to handle runtime errors, ensuring that the program can continue execution or terminate gracefully. It uses `try`, `catch`, `finally`, and `throw` keywords.

```csharp
try
{
    // Code that may throw an exception
    int[] numbers = { 1, 2, 3 };
    Console.WriteLine(numbers[3]); // This will throw an IndexOutOfRangeException
}
catch (IndexOutOfRangeException ex)
{
    // Code to handle the exception
    Console.WriteLine("An error occurred: " + ex.Message);
}
finally
{
    // Code that will always execute
    Console.WriteLine("The try-catch block has finished executing.");
}
```

- **try**: Block contains code that may throw an exception.
- **catch**: Block catches and handles the specific `IndexOutOfRangeException`.
- **finally**: Block executes regardless of whether an exception was thrown.

You can have multiple catch blocks to handle different types of exceptions.

```csharp
try
{
    // Code that may throw different exceptions
    int num = int.Parse("abc"); // This will throw a FormatException
}
catch (FormatException ex)
{
    Console.WriteLine("Format error: " + ex.Message);
}
catch (Exception ex)
{
    // General exception handler
    Console.WriteLine("An error occurred: " + ex.Message);
}

```

# 1.6 Memory Management and Garbage Collection

**Memory management** in C# involves the allocation and deallocation of memory for applications. C# relies on the .NET runtime to manage memory automatically, primarily through garbage collection. However, understanding memory management concepts is crucial for writing efficient and optimized applications.

- **Stack and Heap**:
    - **Stack**: Stores value types and the references to objects. It follows a last-in, first-out (LIFO) order.
    - **Heap**: Stores objects and reference types. The heap has a more complex structure for dynamic memory allocation.
- **Value Types and Reference Types**:
    - **Value Types**: Stored on the stack. Examples include `int`, `char`, `float`, and `struct`.
    - **Reference Types**: Stored on the heap. Examples include `class`, `array`, `delegate`, and `string`.
- **Boxing and Unboxing**:
    - **Boxing**: Converting a value type to a reference type (object). It involves allocating memory on the heap.
    - **Unboxing**: Converting a reference type back to a value type.

```csharp
int number = 42; // Value type on the stack
object boxedNumber = number; // Boxing: value type to reference type
int unboxedNumber = (int)boxedNumber; // Unboxing: reference type to value type
```

**Garbage Collection (GC)** is the process by which the .NET runtime reclaims memory occupied by objects that are no longer in use. The GC automatically handles memory deallocation, freeing developers from manual memory management tasks.

### How Garbage Collection Works

1. **Generations**:
    - The heap is divided into three generations: Gen 0, Gen 1, and Gen 2.
    - Objects are initially allocated in Gen 0. If they survive a garbage collection, they are promoted to Gen 1 and eventually to Gen 2 if they continue to survive.
2. **Garbage Collection Phases**:
    - **Marking**: Identifies which objects are still in use.
    - **Relocating**: Updates references to the remaining objects.
    - **Compacting**: Reclaims memory by moving surviving objects together, reducing fragmentation.
3. **Triggers**:
    - Allocation of a certain amount of memory.
    - Explicit calls to `GC.Collect()` (though generally discouraged).
    - System triggers such as low memory conditions.

```csharp
// Force a garbage collection
GC.Collect();
GC.WaitForPendingFinalizers();
```

- **Minimize Object Allocations**: Avoid unnecessary object creations.
- **Use Structs for Small Data Structures**: Structs are value types and can reduce heap allocations.
- **Dispose Unmanaged Resources**: Implement the `IDisposable` interface for classes that use unmanaged resources.
- **Avoid Long-Lived References**: Keep references as short-lived as possible to allow GC to reclaim memory efficiently.
- **Use StringBuilder for String Manipulations**: Avoid excessive string concatenations.

### Memory Management Tools and Techniques

1. **Profiling Tools**: Use tools like Visual Studio Profiler, JetBrains dotMemory, or ANTS Memory Profiler to identify memory issues.
2. **Weak References**: Use `WeakReference` to reference objects without preventing their garbage collection.

```csharp
WeakReference weakRef = new WeakReference(new SomeClass());
if (weakRef.IsAlive)
{
    SomeClass obj = weakRef.Target as SomeClass;
    // Use obj
}
else
{
    // The object has been garbage collected
}
```