## Dependency Inversion Principle (DIP)
- ### Definition
	- (A) High-level modules should not depend on low-level modules. Both should depend on abstractions.
	- (B) Abstractions should not depend on details. Details should depend on abstractions.
- ### Contrast: Tight Coupling (Opposite of DIP)
  collapsed:: true
	- In tightly coupled designs, high-level modules directly instantiate and use low-level modules.
	- Any change in the low-level implementation (e.g., switching from file storage to a database) requires modifying the high-level code.
	- This makes the system **fragile**, **hard to extend**, and **difficult to test**.
	- **Dependency Inversion** reverses this relationship by introducing an abstraction layer between them, reducing coupling and increasing flexibility.
	  
	  ---
- ### Example in C#
  collapsed:: true
	- ### Without DIP (Tightly Coupled)
	  
	  ```
	  // High-level module depends directly on a low-level module
	  public class FileLogger
	  {
	    public void Log(string message)
	    {
	        Console.WriteLine($"Writing to file: {message}");
	    }
	  }
	  
	  public class OrderProcessor
	  {
	    private FileLogger _logger = new FileLogger(); // direct dependency
	  
	    public void Process()
	    {
	        // Business logic here
	        _logger.Log("Order processed successfully.");
	    }
	  }
	  
	  class Program
	  {
	    static void Main()
	    {
	        var processor = new OrderProcessor();
	        processor.Process();
	    }
	  }
	  ```
	  
	  **Problems:**
	- `OrderProcessor` is tightly coupled to `FileLogger`.
	- If you want to log to a database or console, you must modify the `OrderProcessor` code.
	- Unit testing is difficult because you can’t easily replace the logger with a mock.
	  
	  ---
- ### With DIP (Using Abstraction)
  collapsed:: true
	- ```
	  // Define abstraction
	  public interface ILogger
	  {
	    void Log(string message);
	  }
	  
	  // Low-level modules implement the abstraction
	  public class FileLogger : ILogger
	  {
	    public void Log(string message)
	    {
	        Console.WriteLine($"Writing to file: {message}");
	    }
	  }
	  
	  public class ConsoleLogger : ILogger
	  {
	    public void Log(string message)
	    {
	        Console.WriteLine($"Console: {message}");
	    }
	  }
	  
	  // High-level module depends on abstraction
	  public class OrderProcessor
	  {
	    private readonly ILogger _logger;
	  
	    public OrderProcessor(ILogger logger)
	    {
	        _logger = logger;
	    }
	  
	    public void Process()
	    {
	        // Business logic here
	        _logger.Log("Order processed successfully.");
	    }
	  }
	  
	  class Program
	  {
	    static void Main()
	    {
	        ILogger logger = new ConsoleLogger(); // Can easily switch implementation
	        var processor = new OrderProcessor(logger);
	        processor.Process();
	    }
	  }
	  ```
	  
	  **Benefits:**
	- The `OrderProcessor` no longer depends on the details of logging.
	- You can change or extend logging mechanisms (file, console, database, remote server) without changing the business logic.
	- Easier to test by injecting mock loggers.
	  
	  ---
- ### Top Three “-ilities” Promoted by DIP
  collapsed:: true
	- **Maintainability**
		- Changes to low-level modules don’t affect high-level logic.
		- Code is easier to update when requirements or technologies change.
	- **Testability**
		- Dependencies can be replaced with mock implementations, simplifying unit testing.
	- **Flexibility (Extensibility)**
		- You can add new implementations (e.g., `DatabaseLogger`, `CloudLogger`) without modifying existing high-level classes.
		  
		  ---