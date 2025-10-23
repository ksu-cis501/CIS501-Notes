### Definition
	- The **Strategy Pattern** is a **behavioral design pattern** that enables selecting an algorithm’s behavior **at runtime**.
	- It defines a **family of algorithms**, encapsulates each one in its own class, and makes them **interchangeable**.
	- This pattern lets the algorithm **vary independently** from the clients that use it.
	- The key idea is **delegation**: instead of hardcoding the behavior inside a class, the class delegates it to a “strategy” object that implements a common interface.
	  
	  ---
- ### Contrast: The Opposite (Non-Strategy) Approach
  collapsed:: true
	- Without the Strategy Pattern, different algorithms or behaviors are often managed using **conditional statements** (`if`, `switch`, etc.) inside a single class.
	- This creates **rigid**, **hard-to-maintain** code — changing or adding a new algorithm often requires **modifying existing code**, violating the **Open/Closed Principle**.
	- Strategy, in contrast, **adds new behaviors without modifying existing ones**, promoting flexibility and cleaner design.
	  
	  ---
- ### Example Without Strategy
  collapsed:: true
	- ```
	  using System;
	  
	  class PaymentProcessor
	  {
	    public void ProcessPayment(string method, double amount)
	    {
	        if (method == "CreditCard")
	        {
	            Console.WriteLine($"Processing ${amount} with Credit Card...");
	        }
	        else if (method == "PayPal")
	        {
	            Console.WriteLine($"Processing ${amount} with PayPal...");
	        }
	        else if (method == "Crypto")
	        {
	            Console.WriteLine($"Processing ${amount} with Cryptocurrency...");
	        }
	        else
	        {
	            Console.WriteLine("Invalid payment method.");
	        }
	    }
	  }
	  
	  class Program
	  {
	    static void Main()
	    {
	        var processor = new PaymentProcessor();
	        processor.ProcessPayment("CreditCard", 100);
	        processor.ProcessPayment("PayPal", 250);
	    }
	  }
	  ```
	- #### Problems:
	- The `PaymentProcessor` class **depends directly** on every algorithm.
	- Adding a new payment method requires **editing** this class (violates Open/Closed Principle).
	- Harder to **test** and **extend**.
	- Lots of **conditional logic**.
	  
	  ---
- ### Improved Version Using the Strategy Pattern
  collapsed:: true
	- ```
	  using System;
	  
	  // Step 1: Define the strategy interface
	  interface IPaymentStrategy
	  {
	    void Pay(double amount);
	  }
	  
	  // Step 2: Create concrete strategy classes
	  class CreditCardPayment : IPaymentStrategy
	  {
	    public void Pay(double amount) => 
	        Console.WriteLine($"Processing ${amount} with Credit Card...");
	  }
	  
	  class PayPalPayment : IPaymentStrategy
	  {
	    public void Pay(double amount) => 
	        Console.WriteLine($"Processing ${amount} with PayPal...");
	  }
	  
	  class CryptoPayment : IPaymentStrategy
	  {
	    public void Pay(double amount) => 
	        Console.WriteLine($"Processing ${amount} with Cryptocurrency...");
	  }
	  
	  // Step 3: Create the context class
	  class PaymentProcessor
	  {
	    private IPaymentStrategy _strategy;
	  
	    public void SetStrategy(IPaymentStrategy strategy)
	    {
	        _strategy = strategy;
	    }
	  
	    public void ProcessPayment(double amount)
	    {
	        _strategy.Pay(amount);
	    }
	  }
	  
	  // Step 4: Client code
	  class Program
	  {
	    static void Main()
	    {
	        var processor = new PaymentProcessor();
	  
	        processor.SetStrategy(new CreditCardPayment());
	        processor.ProcessPayment(100);
	  
	        processor.SetStrategy(new PayPalPayment());
	        processor.ProcessPayment(250);
	    }
	  }
	  ```
	- #### 💡 Improvements:
		- New payment types can be added **without modifying** existing code.
		- `PaymentProcessor` is **decoupled** from the specific algorithms.
		- Each strategy is **isolated**, easier to test and maintain.
		- Behavior can change **dynamically at runtime**.
		  
		  ---
- ### Top 3  *-illities*  Supported by the Strategy Pattern
  collapsed:: true
	- **Flexibility** – Algorithms can be swapped or extended without touching the client code.
	- **Maintainability** – Each algorithm lives in its own class, making debugging and updates easier.
	- **Reusability** – Strategies can be reused across different contexts and applications.
	  
	  ---