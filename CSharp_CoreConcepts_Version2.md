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
*   **Interface**: Defines a contract of what a class *can do*. It can only contain signatures of methods, properties, events, or indexers. A class can implement multiple interfaces. It cannot contain instance state (fields).
*   **Abstract Class**: Provides a base with common functionality that derived classes *share*. It can contain both abstract (unimplemented) and concrete (implemented) members, including fields and constructors. A class can inherit from only one abstract class.

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