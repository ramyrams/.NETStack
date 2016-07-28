
# Delegates

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
# Lambda
# Threading
# Asynchronous Programming
# Parallel Programming
# Concurrency & Asynchrony
# Native and COM Interoperability
# Security
# Networking
# Streams and I/O
# Diagnostics and Code Contracts
