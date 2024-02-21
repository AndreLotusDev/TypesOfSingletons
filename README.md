# Singleton Pattern in C#

This repository is dedicated to exploring the Singleton design pattern in C#. The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is particularly useful when managing resources such as database connections or configurations that should be shared across the application.

## Types of Singleton Patterns in C#

There are several ways to implement the Singleton pattern in C#. The most common approaches include:

1. **Basic Singleton** - Ensures a class has only one instance and provides a simple global point of access to it. This implementation is not thread-safe and can cause issues in a multi-threaded environment.

2. **Thread-Safe Singleton** - Enhances the basic Singleton by ensuring that the instance is created safely in a multi-threaded environment. This typically involves locking.

3. **Lazy Singleton** - Utilizes lazy initialization to delay the creation of the instance until it is actually needed. This can improve the application's performance and resource usage.

4. **Static Initialization** - Relies on the CLR (Common Language Runtime) to create the Singleton instance. This approach is thread-safe without using explicit locks, due to static initialization being performed by the CLR.

## Example Implementations

### 1. Basic Singleton

```csharp
public class BasicSingleton
{
    private static BasicSingleton instance;

    private BasicSingleton() {}

    public static BasicSingleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new BasicSingleton();
            }
            return instance;
        }
    }
}
```

### 2. Thread-Safe Singleton

```csharp
public class ThreadSafeSingleton
{
    private static ThreadSafeSingleton instance;
    private static readonly object lockObject = new object();

    private ThreadSafeSingleton() {}

    public static ThreadSafeSingleton Instance
    {
        get
        {
            lock (lockObject)
            {
                if (instance == null)
                {
                    instance = new ThreadSafeSingleton();
                }
            }
            return instance;
        }
    }
}
```

### 3. Lazy Singleton

```csharp
public class LazySingleton
{
    private static readonly Lazy<LazySingleton> lazy =
        new Lazy<LazySingleton>(() => new LazySingleton());

    public static LazySingleton Instance => lazy.Value;

    private LazySingleton() {}
}
```

### 4. Static Initialization

```csharp
public class StaticSingleton
{
    private static readonly StaticSingleton instance = new StaticSingleton();

    static StaticSingleton() {}

    private StaticSingleton() {}

    public static StaticSingleton Instance
    {
        get
        {
            return instance;
        }
    }
}
```

## Conclusion

The Singleton pattern is a powerful tool for ensuring a class has a single instance and a global point of access. Depending on the specific requirements of your application, such as thread safety or lazy initialization, you can choose the appropriate Singleton implementation.
