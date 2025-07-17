
### Part 1: Core C# Concepts

**1. Difference between `readonly` vs `const`**
*   **`const`**: The value is a compile-time constant. It must be initialized at declaration and cannot be changed. It is implicitly `static`.
*   **`readonly`**: The value is a runtime constant. It can be initialized either at declaration or within the constructor of the class. It can be instance-level or `static`.

**2. What is a `sealed` keyword used for?**
The `sealed` keyword is used to prevent inheritance.
*   When applied to a **class**, it prevents other classes from inheriting from it.
*   When applied to a **method or property**, it prevents that member from being overridden in a derived class.

**3. Name all the access modifiers for types**
The main access modifiers in C# are:
*   `public`: Accessible from anywhere.
*   `private`: Accessible only within the same class or struct.
*   `protected`: Accessible within the same class and by derived classes.
*   `internal`: Accessible only within the same assembly.
*   `protected internal`: Accessible within the same assembly OR by derived classes in other assemblies.
*   `private protected`: Accessible by derived classes within the same assembly.

**4. Difference between `interface` and `abstract class`**
*   **Interface**: Defines a contract of what a class *can do*. It can only contain signatures of methods, properties, events, or indexers. A class can implement multiple interfaces. It cannot contain fields or implemented methods (prior to C# 8.0).
*   **Abstract Class**: Provides a base with common functionality that derived classes *share*. It can contain both abstract (unimplemented) and concrete (implemented) members, including fields and constructors. A class can only inherit from one abstract class.

**5. When is a static constructor called?**
A static constructor is called automatically **before the first instance of the class is created** or **any static members are referenced**. It is called at most once per application domain.

**6. How to create an extension method?**
You create an extension method by defining a `static` method inside a `static` class. The first parameter of the method specifies the type it extends, preceded by the `this` keyword.
```csharp
public static class StringExtensions
{
    public static int WordCount(this string str)
    {
        return str.Split(new char[] { ' ', '.', '?' }, StringSplitOptions.RemoveEmptyEntries).Length;
    }
}
```

**7. Does C# support multiple class inheritance?**
No, C# does not support multiple inheritance for classes. A class can only inherit from a single base class. However, a class can implement multiple interfaces, which is how C# achieves a form of multiple inheritance for behavior contracts.

**8. Explain boxing and unboxing**
*   **Boxing**: The process of converting a value type (like `int`, `char`, `struct`) into a reference type (`object`). This involves creating a new object on the heap and copying the value type's value into it.
*   **Unboxing**: The process of extracting the value type from the object. This requires an explicit cast and can throw an `InvalidCastException` if the object is not of the expected boxed type.

**9. What is heap and stack?**
*   **Stack**: A region of memory that stores value types, method parameters, and pointers to reference types. It operates in a Last-In, First-Out (LIFO) manner and is managed directly by the CPU for very fast access. Memory is automatically reclaimed when a method call ends.
*   **Heap**: A region of memory used for dynamic allocation of reference types (like classes, strings, arrays). Objects on the heap are not deallocated automatically and are managed by the Garbage Collector (GC). Access is slower than the stack.

**10. Difference between `string` and `StringBuilder`**
*   **`string`**: An immutable reference type. Any modification (like concatenation) creates a new string object in memory, which can be inefficient for frequent changes.
*   **`StringBuilder`**: A mutable object designed for efficient string manipulation. It modifies the internal buffer instead of creating new objects, making it much faster for building strings in loops or through multiple appends.

**11. How to create a date with a specific timezone?**
You use the `DateTimeOffset` struct, which represents a point in time relative to UTC.
```csharp
// Represents a specific time in a specific time zone (+5:30)
var timeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("India Standard Time");
var dateTime = new DateTime(2025, 12, 25, 10, 30, 0);
var dateTimeWithZone = new DateTimeOffset(dateTime, timeZoneInfo.GetUtcOffset(dateTime));
```

**12. How to change current culture?**
You change the culture for the current thread by setting the `CurrentCulture` and `CurrentUICulture` properties.
```csharp
using System.Globalization;
using System.Threading;

// For formatting numbers, dates, etc.
Thread.CurrentThread.CurrentCulture = new CultureInfo("fr-FR");

// For retrieving culture-specific resources (e.g., language translations)
Thread.CurrentThread.CurrentUICulture = new CultureInfo("fr-FR");
```

**13. What is the difference between `HashSet<T>` and `Dictionary<TKey, TValue>`?**
*   **`HashSet<T>`**: A collection that contains unique elements. It is optimized for high-performance set operations like union, intersection, and checking for an element's existence (`Contains`). It does not store key-value pairs, only unique values.
*   **`Dictionary<TKey, TValue>`**: A collection of key-value pairs. Each key must be unique. It is optimized for fast lookups of a value based on its key.

**14. What is the purpose of the method `ToLookup`?**
`ToLookup` is a LINQ method that groups the elements of a sequence based on a key selector function. It creates an `ILookup<TKey, TElement>`, which is similar to a `Dictionary<TKey, IEnumerable<TElement>>`. The key differences are that `ToLookup` is immutable after creation and it can represent keys that map to empty collections, whereas a dictionary would not contain the key at all. It executes immediately (it is not deferred).

**15. Does LINQ `Cast<T>` method create a new object?**
No, `Cast<T>` does not create new objects for the elements themselves. It attempts to cast each element in the source collection to the specified type `T`. It returns a new `IEnumerable<T>` sequence that performs these casts as you iterate over it (deferred execution). If an element cannot be cast, it will throw an `InvalidCastException`.

**16. Explain deferred execution in LINQ**
Deferred execution means that a LINQ query is not executed at the point it is defined, but rather when the results are actually enumerated (e.g., in a `foreach` loop or by calling a method like `ToList()`, `ToArray()`, `First()`, or `Count()`). This allows for more efficient query chaining and data processing, as the data is only pulled and processed when it's needed.

**17. How does the `ImmutableList<T>` work?**
`ImmutableList<T>` is a collection where any modification operation (like `Add`, `Remove`) does not change the original list. Instead, it returns a **new** `ImmutableList<T>` instance with the change applied. It achieves this efficiently by sharing the underlying data structure (a binary tree) between the old and new lists, minimizing memory usage and allocation overhead.

---

### Part 2: Concurrency, Collections, and Modern C# Features

**18. What are the benefits of using Frozen Collections?**
Frozen collections (`FrozenDictionary<TKey, TValue>` and `FrozenSet<T>`), introduced in .NET 8, are immutable collections optimized for extremely fast read performance. Once created, they cannot be changed. Their main benefit is significantly faster lookups and enumeration compared to other immutable collections, making them ideal for data that is created once and read many times.

**19. Name thread-safe collections**
These are collections designed for concurrent access from multiple threads, found in the `System.Collections.Concurrent` namespace:
*   `ConcurrentDictionary<TKey, TValue>`
*   `ConcurrentQueue<T>`
*   `ConcurrentStack<T>`
*   `ConcurrentBag<T>`
*   `BlockingCollection<T>`

**20. How to perform a lock for asynchronous code?**
You should not use the `lock` keyword with `await` inside it, as it can lead to deadlocks. Instead, use `SemaphoreSlim`.
```csharp
private readonly SemaphoreSlim _mutex = new SemaphoreSlim(1, 1);

public async Task DoWorkAsync()
{
    await _mutex.WaitAsync(); // Acquire the lock asynchronously
    try
    {
        // Critical section: code that needs exclusive access
        await Task.Delay(1000);
    }
    finally
    {
        _mutex.Release(); // Release the lock
    }
}
```

**21. Name all the ways for creating a new thread**
*   **`Thread` class (explicit thread creation)**: `Thread t = new Thread(MethodName); t.Start();`
*   **`Task.Run` (Task Parallel Library - TPL)**: `Task.Run(() => { ... });` (This is the modern, preferred approach).
*   **`ThreadPool.QueueUserWorkItem`**: `ThreadPool.QueueUserWorkItem(state => { ... });` (Used by TPL behind the scenes).
*   **`BackgroundWorker`**: A legacy component for managing background operations in UI applications.

**22. How to execute multiple async tasks at once?**
Use `Task.WhenAll` to await the completion of multiple tasks concurrently.
```csharp
Task<int> task1 = Method1Async();
Task<string> task2 = Method2Async();
Task task3 = Method3Async();

// Starts all tasks and waits for all of them to complete
await Task.WhenAll(task1, task2, task3);

// You can now safely access the results
int result1 = task1.Result; // or await task1
string result2 = task2.Result; // or await task2
```

**23. Explain Inheritance vs Composition**
*   **Inheritance** (`is-a` relationship): A class derives from a base class, inheriting its public and protected members. It promotes code reuse but creates a tight coupling between the base and derived classes. Example: A `Car` *is a* `Vehicle`.
*   **Composition** (`has-a` relationship): A class contains an instance of another class and delegates work to it. It promotes flexibility and loose coupling. Example: A `Car` *has an* `Engine`. The general principle is to "favor composition over inheritance."

**24. Difference between `class` vs `record` vs `struct`**
*   **`class`**: A reference type. Stored on the heap. Supports inheritance. By default, has reference-based equality (two variables are equal if they point to the same object).
*   **`struct`**: A value type. Stored on the stack (usually). Does not support inheritance (but can implement interfaces). Has value-based equality by default (two structs are equal if their members are equal). Best for small, simple data structures.
*   **`record`**: Can be a reference type (`record class`) or a value type (`record struct`). Primarily for immutable data models. The compiler auto-generates methods for value-based equality (`Equals`, `GetHashCode`), a `ToString()` override, and deconstruction. Supports "with-expressions" for non-destructive mutation.

**25. What are `ref struct`s used for?**
`ref struct`s are value types that are enforced by the compiler to live only on the stack. They can never be boxed, stored on the heap, or be members of a class. They are used for high-performance scenarios to avoid heap allocations, such as `Span<T>` and `ReadOnlySpan<T>`, which provide safe, efficient access to contiguous memory.

**26. Name the two forms of records**
1.  **Positional Records**: A concise syntax where properties are defined in the declaration. The compiler generates a primary constructor and deconstructor.
    ```csharp
    public record Person(string FirstName, string LastName);
    ```
2.  **Nominal Records**: Declared with standard property syntax inside curly braces.
    ```csharp
    public record Person
    {
        public string FirstName { get; init; }
        public string LastName { get; init; }
    }
    ```

**27. What is "with" keyword used for?**
The `with` keyword is used with **records** to create a new record instance by copying an existing instance and modifying some of its properties. This is called **non-destructive mutation**.
```csharp
var person1 = new Person("John", "Doe");
var person2 = person1 with { FirstName = "Jane" }; // person2 is a new record
```

**28. What is the purpose of Primary Constructors?**
Introduced in C# 12 for classes and structs (previously available for records), primary constructors provide a concise way to declare constructor parameters whose values can be used to initialize properties or used within the body of the type. They reduce boilerplate code for simple initialization.
```csharp
public class Person(string name, int age)
{
    public string Name { get; } = name;
    public int Age { get; } = age;
}
```

**29. Explain how Nullable Reference Types work**
This is an opt-in feature (enabled with `<Nullable>enable</Nullable>` in the project file) that helps prevent `NullReferenceException`. The compiler performs static analysis to detect potential null issues.
*   **`string name`**: A non-nullable reference type. The compiler will warn you if you try to assign `null` to it or if it's not initialized.
*   **`string? name`**: A nullable reference type. You are explicitly stating that this variable can be `null`, and the compiler will force you to check for `null` before dereferencing it.

**30. Do switch expressions have any return type limitations?**
Yes. All arms of a switch expression must return values of the same type, or types that have an implicit conversion to a single common type. The compiler must be able to determine a single best common type for the expression.

---

### Part 3: Advanced C# and .NET Framework

**31. What is `yield return` used for?**
`yield return` is used inside a method to create an **iterator**. It allows you to return an `IEnumerable<T>` or `IEnumerator<T>` without creating a collection in memory. The method's execution is paused, and control is returned to the caller. When the caller requests the next item, execution resumes from where it left off. This is a form of deferred execution and is very memory-efficient for large sequences.

**32. How many generations does the Garbage Collector have?**
The .NET Garbage Collector (GC) has three generations:
*   **Generation 0**: Contains newly allocated, short-lived objects. This generation is collected most frequently.
*   **Generation 1**: Contains objects that survived a Gen 0 collection. It acts as a buffer between short-lived and long-lived objects.
*   **Generation 2**: Contains long-lived objects that survived a Gen 1 collection. This generation is collected least frequently.

**33. What is `Interlocked` class used for?**
The `System.Threading.Interlocked` class provides static methods for performing simple atomic operations on variables (e.g., `Increment`, `Decrement`, `Add`, `Exchange`, `CompareExchange`). These operations are guaranteed to be performed as a single, indivisible unit, making them a lightweight and efficient way to handle simple synchronization without needing a full `lock`.

**34. What is the code generated by compiler for auto-properties?**
For an auto-implemented property like `public int MyProperty { get; set; }`, the compiler generates a hidden, private backing field and implements the `get` and `set` accessors to read from and write to that field.
```csharp
// What you write:
public int MyProperty { get; set; }

// What the compiler generates (conceptually):
private int _myPropertyBackingField;
public int get_MyProperty()
{
    return _myPropertyBackingField;
}
public void set_MyProperty(int value)
{
    _myPropertyBackingField = value;
}
```

**35. How is Polymorphism implemented in C#?**
Polymorphism ("many forms") is primarily implemented in C# through:
*   **Method Overriding (Runtime Polymorphism)**: A derived class provides a specific implementation for a method that is already defined in its base class using the `virtual` and `override` keywords. The method that gets called is determined at runtime based on the object's actual type.
*   **Method Overloading (Compile-time Polymorphism)**: A class has multiple methods with the same name but different signatures (parameters). The correct method to call is determined at compile time.

**36. How is Encapsulation implemented in C#?**
Encapsulation is the bundling of data (fields) and the methods that operate on that data into a single unit (a class), while hiding the internal state from the outside world. It is implemented using:
*   **Access Modifiers** (`private`, `protected`, etc.) to hide internal fields.
*   **Properties** (`get`, `set` accessors) to provide controlled, public access to the private fields, allowing for validation or logic to be executed when the data is accessed.

**37. What is the difference between `ref` and `out` parameters?**
Both `ref` and `out` pass arguments by reference, meaning the method can modify the original variable.
*   **`ref`**: The variable **must be initialized** before it is passed to the method. The method can read and modify its value.
*   **`out`**: The variable **does not need to be initialized** before being passed. The method **must assign a value** to the parameter before it returns. It cannot read the value before assigning it.

**38. How does the `using` statement work?**
The `using` statement provides a convenient syntax that ensures an object implementing `IDisposable` is correctly disposed of. The compiler translates a `using` block into a `try...finally` block, where the `Dispose()` method is called in the `finally` block. This guarantees that resources (like file handles, database connections) are released even if an exception occurs.
```csharp
// C# 9 and later can use a using declaration:
using var reader = new StreamReader("file.txt");
// ... code that uses reader ...
// reader.Dispose() is called automatically at the end of the scope
```

**39. What is a delegate and how is it used?**
A delegate is a type-safe function pointer. It's an object that holds a reference to a method (or multiple methods). It is used to:
*   Pass methods as arguments to other methods (callbacks).
*   Implement event handling (e.g., `EventHandler`).
*   Execute methods asynchronously.
*   Serve as the foundation for LINQ expressions and lambda functions.
```csharp
public delegate int MathOperation(int a, int b);

public int Add(int a, int b) => a + b;

// Create a delegate instance and use it
MathOperation op = Add;
int result = op(5, 3); // result is 8
```

**40. Explain method overloading and overriding**
*   **Overloading (Compile-time Polymorphism)**: Creating multiple methods in the same class with the same name but different signatures (number or type of parameters). The compiler decides which version to call based on the arguments provided.
*   **Overriding (Runtime Polymorphism)**: Providing a new implementation in a derived class for a `virtual` method defined in its base class. The method signature must be the same. The version that gets executed depends on the object's type at runtime.

**41. Difference between `IEnumerable` and `IQueryable`**
*   **`IEnumerable`**: Represents a sequence of objects that can be enumerated. When you use LINQ with `IEnumerable` (LINQ to Objects), the filtering and processing logic is executed in your application's memory. It's best for working with in-memory collections.
*   **`IQueryable`**: Represents a query that can be executed against a specific data source (like a SQL database). It holds an **expression tree**, not the data itself. When you use LINQ with `IQueryable` (e.g., LINQ to SQL), the expression tree is translated into the native query language (like SQL) and executed on the data source. This is far more efficient for remote data.

**42. What are expression trees in LINQ?**
An expression tree is a tree-like data structure that represents code 
