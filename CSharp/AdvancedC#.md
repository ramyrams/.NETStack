# [Advanced C#]
* [Delegates](#delegates)
* [Events](#events)
* [Generics](#generics)
* [Reflection, Attributes and Metadata](#reflection-attributes-and-metadata)
* [Dynamic Binding](#dynamic-binding)
* [Disposal and Garbage Collection](#disposal-and-garbage-collection)
* [Serialization](#serialization)
* [Application Domains](#application-domains)
* [Lambda](#lambda)
* [Threading](#threading)
* [Asynchronous Programming](#asynchronous-programming)
* [Parallel Programming](#parallel-programming)
* [Concurrency & Asynchrony](#concurrency--asynchrony)
* [Native and COM Interoperability](#native-and-com-interoperability)
* [Security](#security)
* [Networking](#networking)
* [Streams and I/O](#streams-and-io)
* [Diagnostics and Code Contracts](#diagnostics-and-code-contracts)
* [Performance Counter](#performance-counter)



# Delegates
# Events
# Generics
* [Generics in C#](http://www.tutorialsteacher.com/csharp/csharp-generics)
* [C# - Generics](https://www.tutorialspoint.com/csharp/csharp_generics.htm)
* [Generic classes](https://www.dotnetperls.com/generic)
* [Generic classes](https://www.codeproject.com/Articles/52991/Generic-Classes)
* [Generics In C#http://www.tutorials.kode-blog.com/generics-in-csharp)
* [C# Generics - Beyond Containers of T](https://accu.org/index.php/journals/1376)
* [Generics and its advantages in C#](http://www.csharpstar.com/generics-and-its-advantages-in-csharp/)
* [Generics with C# - how it works under the hood](http://thibaultlaurens.github.io/microsoft/2013/01/12/generics-with-csharp/)

# Reflection, Attributes and Metadata
# Dynamic Binding
# Disposal and Garbage Collection
# Serialization
* [Introducing Serialization in .NET](https://www.codeproject.com/Articles/20962/Introducing-Serialization-in-NET)
* [.NET Serialization](http://www.codeguru.com/columns/dotnet/article.php/c6595/NET-Serialization.htm)
* [.NET Serialization](http://www.dotneat.net/2009/03/22/NETSerializationUsingBinaryFormaterSoapFormatterAndXmlSerializer.aspx)

# Application Domains
# Lambda
# Threading
# Asynchronous Programming
# Parallel Programming
# Concurrency & Asynchrony
# Native and COM Interoperability
# Security
# Networking
# Streams and I/O
* [File and Stream I/O](https://msdn.microsoft.com/en-us/library/k3352a4t(v=vs.110).aspx)

# Diagnostics and Code Contracts
# Performance Counter 
* [Performance Counters for ASP.NET](https://msdn.microsoft.com/en-us/library/fxk122b4.aspx)
* [An Introduction To Performance Counters](https://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters)
* [.NET Best Practice No: 3:- Using performance counters to gather performance data](https://www.codeproject.com/Articles/42001/NET-Best-Practice-No-Using-performance-counters)
* [Create performance counters using .NET and C#](http://madskristensen.net/post/create-performance-counters-using-net-and-c)
* [Using Performance Counters In The C# Language](http://www.coderslexicon.com/using-performance-counters-in-the-c-language/)
* [Performance Counters in the .NET Framework](https://msdn.microsoft.com/en-us/library/w8f5kw2e(v=vs.110).aspx)
* [PerformanceCounter Class](https://msdn.microsoft.com/en-us/library/system.diagnostics.performancecounter(v=vs.110).aspx)
* [A Simple Performance Counter Application](https://www.codeproject.com/Articles/29986/A-Simple-Performance-Counter-Application)
* [Monitoring Distributed Service Performance in .NET](https://www.codeproject.com/Articles/8403/Monitoring-Distributed-Service-Performance-in-NET)

# Move up 

# Delegates

```cs
class Program
{
    delegate void D(string value);

    static void Main()
    {
	// ... Specify delegate with lambda expression.
	D d = v => Console.WriteLine(v);
	// ... Invoke delegate.
	d.Invoke("cat");
    }
}

Output
cat

```


### 
```cs
using System;

class Program
{
    delegate string UppercaseDelegate(string input);

    static string UppercaseFirst(string input)
    {
	char[] buffer = input.ToCharArray();
	buffer[0] = char.ToUpper(buffer[0]);
	return new string(buffer);
    }

    static string UppercaseLast(string input)
    {
	char[] buffer = input.ToCharArray();
	buffer[buffer.Length - 1] = char.ToUpper(buffer[buffer.Length - 1]);
	return new string(buffer);
    }

    static string UppercaseAll(string input)
    {
	return input.ToUpper();
    }

    static void WriteOutput(string input, UppercaseDelegate del)
    {
	Console.WriteLine("Your string before: {0}", input);
	Console.WriteLine("Your string after: {0}", del(input));
    }

    static void Main()
    {
	// Wrap the methods inside delegate instances and pass to the method.
	WriteOutput("perls", new UppercaseDelegate(UppercaseFirst));
	WriteOutput("perls", new UppercaseDelegate(UppercaseLast));
	WriteOutput("perls", new UppercaseDelegate(UppercaseAll));
    }
}

Output

Your string before: perls
Your string after: Perls
Your string before: perls
Your string after: perlS
Your string before: perls
Your string after: PERLS
```

## Predicate
```cs
class Program
{
    static void Main()
    {
	//
	// This Predicate instance returns true if the argument is one.
	//
	Predicate<int> isOne =
	    x => x == 1;
	//
	// This Predicate returns true if the argument is greater than 4.
	//
	Predicate<int> isGreaterEqualFive =
	    (int x) => x >= 5;

	//
	// Test the Predicate instances with various parameters.
	//
	Console.WriteLine(isOne.Invoke(1));
	Console.WriteLine(isOne.Invoke(2));
	Console.WriteLine(isGreaterEqualFive.Invoke(3));
	Console.WriteLine(isGreaterEqualFive.Invoke(10));
    }
}

Output

True
False
False
True
```

## very basic Delegate
```cs
namespace Akadia.BasicDelegate
{
    // Declaration
    public delegate void SimpleDelegate();

    class TestDelegate
    {
        public static void MyFunc()
        {
            Console.WriteLine("I was called by delegate ...");
        }

        public static void Main()
        {
            // Instantiation
            SimpleDelegate simpleDelegate = new SimpleDelegate(MyFunc);

            // Invocation
            simpleDelegate();
        }
    }
}
```

## Calling Static Functions
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // Test Application to use the defined Delegate
    public class TestApplication
    {
        // Static Function: To which is used in the Delegate. To call the Process()
        // function, we need to declare a logging function: Logger() that matches
        // the signature of the delegate.
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }

        static void Main(string[] args)
        {
            MyClass myClass = new MyClass();

            // Crate an instance of the delegate, pointing to the logging function.
            // This delegate will then be passed to the Process() function.
            MyClass.LogHandler myLogger = new MyClass.LogHandler(Logger);
            myClass.Process(myLogger);
        }
    }
}

Compile an test:

# csc SimpleDelegate2.cs
# SimpleDelegate2.exe
Process() begin
Process() end
```

### Calling Member Functions
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;

        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }

        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }

        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }

    // Main() is modified so that the delegate points to the Logger()
    // function on the fl instance of a FileLogger. When this delegate
    // is invoked from Process(), the member function is called and
    // the string is logged to the appropriate file.
    public class TestApplication
    {
        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");

            MyClass myClass = new MyClass();

            // Crate an instance of the delegate, pointing to the Logger()
            // function on the fl instance of a FileLogger.
            MyClass.LogHandler myLogger = new MyClass.LogHandler(fl.Logger);
            myClass.Process(myLogger);
            fl.Close();
        }
    }
}

Compile an test:

# csc SimpleDelegate3.cs
# SimpleDelegate3.exe
# cat process.log
Process() begin
Process() end
```

## Multicasting
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;

        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }

        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }

        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }

    // Test Application which calls both Delegates
    public class TestApplication
    {
         // Static Function which is used in the Delegate
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }

        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");

            MyClass myClass = new MyClass();

            // Crate an instance of the delegates, pointing to the static
            // Logger() function defined in the TestApplication class and
            // then to member function on the fl instance of a FileLogger.
            MyClass.LogHandler myLogger = null;
            myLogger += new MyClass.LogHandler(Logger);
            myLogger += new MyClass.LogHandler(fl.Logger);

            myClass.Process(myLogger);
            fl.Close();
        }
    }
}
Compile an test:

# csc SimpleDelegate4.cs
# SimpleDelegate4.exe
Process() begin
Process() end
# cat process.log
Process() begin
Process() end
```


# Lambda
```cs
//Input Parameters => Expression/Statement Block;
x => x * 2 
```

### Parameters Type 
```cs
//parameters of the lambda expression can be explicitly or implicitly typed. 
(int p) => p * 4; 	// Explicitly Typed Parameter
q => q * 4; 	// Implicitly Typed Parameter
```

### Use Simple Lambda Expression
```cs
//Lambda Expression which returns a list of numbers greater than 8.
int[] numbers = {1,2,3,4,5,6,7,8,9,10 };   
var  returnedList = numbers.Where(n => (n > 8));
```

### use anonymous method for returning the same list.
```cs
int[] numbers = {1,2,3,4,5,6,7,8,9,10 };
var returnedList = numbers.Where(delegate(int i) { return i > 8; });
```

### Statement Block in Lambda Expression
```cs
//Statement block in the lambda expression. This expression returns a list of numbers less than 4 and greater than 8.
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
```

### Use Lambda with More than One Parameter
```cs
//You can also write lambda which takes more than one parameter. Here is an example of lambda which adds two integer numbers:
delegate int AddInteger(int n1, int n2);

AddInteger addInt = (x, y) => x + y;
int result = addInt(10,4); // return 14
```

### Use Lambda with Zero Parameter
```cs
//Here is an example of lambda which takes no parameter and returns new Guid.
delegate Guid GetNextGuid();

GetNextGuid getNewGuid = () => (Guid.NewGuid());
Guid newguid = getNewGuid();
```

### Use Lambda that Returns Nothing
```cs
//You can also write lambda which returns void. Here is an example that lambda is only showing message and returns nothing.
delegate void ShowMessageDelegate();

ShowMessageDelegate msgdelegate = () => MessageBox.Show("It returns nothing.");
msgdelegate();

var returnedList = numbers.Where(n =>
                           {
                              if (n < 4)
                                  return true;
                              else if (n > 8)
                                  return true;

                               return false;
                           }
                        );
						
						
class Program
{
    static void Main()
    {
		List<int> elements = new List<int>() { 10, 20, 31, 40 };
		// ... Find index of first odd element.
		int oddIndex = elements.FindIndex(x => x % 2 != 0);
		Console.WriteLine(oddIndex);
    }
}

Output
2

Lambda details

x          The argument name.
=>         Separates argument list from result expression.
x % 2 !=0  Returns true if x is not even.
```


```cs
string[] words = { "cherry", "apple", "blueberry" };

// Use method syntax to apply a lambda expression to each element
// of the words array. 
int shortestWordLength = words.Min(w => w.Length);
Console.WriteLine(shortestWordLength);

// Compare the following code that uses query syntax.
// Get the lengths of each word in the words array.
var query = from w in words
            select w.Length;
// Apply the Min method to execute the query and get the shortest length.
int shortestWordLength2 = query.Min();
Console.WriteLine(shortestWordLength2);

// Output: 
// 5
// 5
```



```cs
static void Main(string[] args)
{
    string[] digits = { "zero", "one", "two", "three", "four", "five", 
            "six", "seven", "eight", "nine" };

    Console.WriteLine("Example that uses a lambda expression:");
    var shortDigits = digits.Where((digit, index) => digit.Length < index);
    foreach (var sD in shortDigits)
    {
        Console.WriteLine(sD);
    }

    // Output:
    // Example that uses a lambda expression:
    // five
    // six
    // seven
    // eight
    // nine
}
```

### C# program that uses lambda expressions
```cs
class Program
{
    static void Main()
    {
	//
	// Use implicitly typed lambda expression.
	// ... Assign it to a Func instance.
	//
	Func<int, int> func1 = x => x + 1;
	//
	// Use lambda expression with statement body.
	//
	Func<int, int> func2 = x => { return x + 1; };
	//
	// Use formal parameters with expression body.
	//
	Func<int, int> func3 = (int x) => x + 1;
	//
	// Use parameters with a statement body.
	//
	Func<int, int> func4 = (int x) => { return x + 1; };
	//
	// Use multiple parameters.
	//
	Func<int, int, int> func5 = (x, y) => x * y;
	//
	// Use no parameters in a lambda expression.
	//
	Action func6 = () => Console.WriteLine();
	//
	// Use delegate method expression.
	//
	Func<int, int> func7 = delegate(int x) { return x + 1; };
	//
	// Use delegate expression with no parameter list.
	//
	Func<int> func8 = delegate { return 1 + 1; };
	//
	// Invoke each of the lambda expressions and delegates we created.
	// ... The methods above are executed.
	//
	Console.WriteLine(func1.Invoke(1));
	Console.WriteLine(func2.Invoke(1));
	Console.WriteLine(func3.Invoke(1));
	Console.WriteLine(func4.Invoke(1));
	Console.WriteLine(func5.Invoke(2, 2));
	func6.Invoke();
	Console.WriteLine(func7.Invoke(1));
	Console.WriteLine(func8.Invoke());
    }
}

Output

2
2
2
2
4

2
2

```

# Events

## Simple Event
```cs
namespace Akadia.SimpleEvent
{
    /* ========= Publisher of the Event ============== */
    public class MyClass
    {
        // Define a delegate named LogHandler, which will encapsulate
        // any method that takes a string as the parameter and returns no value
        public delegate void LogHandler(string message);
 
        // Define an Event based on the above Delegate
        public event LogHandler Log;
  
        // Instead of having the Process() function take a delegate
        // as a parameter, we've declared a Log event. Call the Event,
        // using the OnXXXX Method, where XXXX is the name of the Event.
        public void Process()
        {
            OnLog("Process() begin");
            OnLog("Process() end");
        }
 
        // By Default, create an OnXXXX Method, to call the Event
        protected void OnLog(string message)
        {
            if (Log != null)
            {
                Log(message);
            }
        }
    }
 
    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;
 
        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }
 
        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }
 
        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }
 
    /* ========= Subscriber of the Event ============== */
    // It's now easier and cleaner to merely add instances
    // of the delegate to the event, instead of having to
    // manage things ourselves
    public class TestApplication
    {
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }
 
        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");
            MyClass myClass = new MyClass();
 
            // Subscribe the Functions Logger and fl.Logger
            myClass.Log += new MyClass.LogHandler(Logger);
            myClass.Log += new MyClass.LogHandler(fl.Logger);

            // The Event will now be triggered in the Process() Method
            myClass.Process();
 
            fl.Close();
        }
    }
}

Compile an test:

# csc SimpleEvent.cs
# SimpleEvent.exe
Process() begin
Process() end
# cat process.log
Process() begin
Process() end
```


## The Second Change Event Example
```cs
namespace SecondChangeEvent
{
   /* ======================= Event Publisher =============================== */

   // Our subject -- it is this class that other classes
   // will observe. This class publishes one event:
   // SecondChange. The observers subscribe to that event.
   public class Clock
   {
      // Private Fields holding the hour, minute and second
      private int _hour;
      private int _minute;
      private int _second;

      // The delegate named SecondChangeHandler, which will encapsulate
      // any method that takes a clock object and a TimeInfoEventArgs
      // object as the parameter and returns no value. It's the
      // delegate the subscribers must implement.
      public delegate void SecondChangeHandler (
         object clock,
         TimeInfoEventArgs timeInformation
      );

      // The event we publish
      public event SecondChangeHandler SecondChange;

      // The method which fires the Event
      protected void OnSecondChange(
         object clock,
         TimeInfoEventArgs timeInformation
      )
      {
         // Check if there are any Subscribers
         if (SecondChange != null)
         {
            // Call the Event
            SecondChange(clock,timeInformation);
         }
      }

      // Set the clock running, it will raise an
      // event for each new second
      public void Run()
      {
         for(;;)
         {
            // Sleep 1 Second
            Thread.Sleep(1000);

            // Get the current time
            System.DateTime dt = System.DateTime.Now;

            // If the second has changed
            // notify the subscribers
            if (dt.Second != _second)
            {
               // Create the TimeInfoEventArgs object
               // to pass to the subscribers
               TimeInfoEventArgs timeInformation =
                  new TimeInfoEventArgs(
                  dt.Hour,dt.Minute,dt.Second);

               // If anyone has subscribed, notify them
               OnSecondChange (this,timeInformation);
            }

            // update the state
            _second = dt.Second;
            _minute = dt.Minute;
            _hour = dt.Hour;

         }
      }
   }

   // The class to hold the information about the event
   // in this case it will hold only information
   // available in the clock class, but could hold
   // additional state information
   public class TimeInfoEventArgs : EventArgs
   {
      public TimeInfoEventArgs(int hour, int minute, int second)
      {
         this.hour = hour;
         this.minute = minute;
         this.second = second;
      }
      public readonly int hour;
      public readonly int minute;
      public readonly int second;
   }

   /* ======================= Event Subscribers =============================== */

   // An observer. DisplayClock subscribes to the
   // clock's events. The job of DisplayClock is
   // to display the current time
   public class DisplayClock
   {
      // Given a clock, subscribe to
      // its SecondChangeHandler event
      public void Subscribe(Clock theClock)
      {
         theClock.SecondChange +=
            new Clock.SecondChangeHandler(TimeHasChanged);
      }

      // The method that implements the
      // delegated functionality
      public void TimeHasChanged(
         object theClock, TimeInfoEventArgs ti)
      {
         Console.WriteLine("Current Time: {0}:{1}:{2}",
            ti.hour.ToString(),
            ti.minute.ToString(),
            ti.second.ToString());
      }
   }

   // A second subscriber whose job is to write to a file
   public class LogClock
   {
      public void Subscribe(Clock theClock)
      {
         theClock.SecondChange +=
            new Clock.SecondChangeHandler(WriteLogEntry);
      }

      // This method should write to a file
      // we write to the console to see the effect
      // this object keeps no state
      public void WriteLogEntry(
         object theClock, TimeInfoEventArgs ti)
      {
         Console.WriteLine("Logging to file: {0}:{1}:{2}",
            ti.hour.ToString(),
            ti.minute.ToString(),
            ti.second.ToString());
      }
   }

   /* ======================= Test Application =============================== */

   // Test Application which implements the
   // Clock Notifier - Subscriber Sample
   public class Test
   {
      public static void Main()
      {
         // Create a new clock
         Clock theClock = new Clock();

         // Create the display and tell it to
         // subscribe to the clock just created
         DisplayClock dc = new DisplayClock();
         dc.Subscribe(theClock);

         // Create a Log object and tell it
         // to subscribe to the clock
         LogClock lc = new LogClock();
         lc.Subscribe(theClock);

         // Get the clock started
         theClock.Run();
      }
   }
}
```








# Generics

## generic

```cs
using System;
class Test<T>
{
    T _value;

    public Test(T t)
    {
	// The field has the same type as the parameter.
	this._value = t;
    }

    public void Write()
    {
	Console.WriteLine(this._value);
    }
}

class Program
{
    static void Main()
    {
	// Use the generic type Test with an int type parameter.
	Test<int> test1 = new Test<int>(5);
	// Call the Write method.
	test1.Write();

	// Use the generic type Test with a string type parameter.
	Test<string> test2 = new Test<string>("cat");
	test2.Write();
    }
}

Output
5
cat
```

## C# program that uses generic type constraints
```cs
using System;
using System.Data;

/// <summary>
/// Requires type parameter that implements interface IEnumerable.
/// </summary>
class Ruby<T> where T : IDisposable
{
}

/// <summary>
/// Requires type parameter that is a struct.
/// </summary>
class Python<T> where T : struct
{
}

/// <summary>
/// Requires type parameter that is a reference type with a constructor.
/// </summary>
class Perl<V> where V : class, new()
{
}

class Program
{
    static void Main()
    {
	// DataTable implements IDisposable so it can be used with Ruby.
	Ruby<DataTable> ruby = new Ruby<DataTable>();

	// Int is a struct (ValueType) so it can be used with Python.
	Python<int> python = new Python<int>();

	// Program is a class with a parameterless constructor (implicit)
	// ... so it can be used with Perl.
	Perl<Program> perl = new Perl<Program>();
    }
}
```

```cs
public class Stack<T>
{
	int position;
	T[] data = new T[100];
	public void Push (T obj) { data[position++] = obj; }
	public T Pop() { return data[--position]; }
}

Stack<int> stack = new Stack<int>();
stack.Push(5);
stack.Push(10);
int x = stack.Pop(); // x is 10
int y = stack.Pop(); // y is 5
```

#### Generic Constraints
```cs
where T : base-class // Base-class constraint
where T : interface // Interface constraint
where T : class // Reference-type constraint
where T : struct // Value-type constraint (excludes Nullable types)
where T : new() // Parameterless constructor constraint
where U : T // Naked type constraint

class SomeClass {}
interface Interface1 {}

class GenericClass<T,U> where T : SomeClass, Interface1
						where U : new()
{...}
```
#### Subclassing Generic Types
```cs
class Stack<T> {...}
class SpecialStack<T> : Stack<T> {...}

class IntStack : Stack<int> {...}

```

# Reflection, Attributes and Metadata
# Dynamic Binding
# Disposal and Garbage Collection
# Serialization
# Application Domains
# Threading
# Asynchronous Programming
# Parallel Programming
# Concurrency & Asynchrony
# Native and COM Interoperability
# Security
# Networking
# Streams and I/O
# Diagnostics and Code Contracts
