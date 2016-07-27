
#TOC 
* [Types, Storage, and Variables](#Types, Storage, and Variables)
* [Classes](#classes)
* [Inheritance](#inheritance)
* [Interfaces](#interfaces)
* [Methods](#methods)
* [Expressions and Operators](#expressions-and-operators)
* [Statements](#statements)
* [Structs](#structs)
* [Enumerations](#enumerations)
* [Arrays](#arrays)
* [Delegates](#delegates)
* [Events](#events)
* [Conversions](#conversions)
* [Generics](#generics)
* [Enumerators and Iterators](#enumerators-and-iterators)
* [Exceptions](#exceptions)
* [Preprocessor Directives](#preprocessor-directives)
* [Reflection and Attributes ](#reflection-and-attributes )
* [Dynamic Binding](#dynamic-binding)
* [Disposal and Garbage Collection](#disposal-and-garbage-collection)
* [Serialization](#serialization)
* [Application Domains](#application-domains)
* [Collections](#collections)
* [Lambda](#lambda)
* [Asynchronous Programming](#asynchronous-programming)
* [Concurrency & Asynchrony](#concurrency-&-Asynchrony)
* [Native and COM Interoperability](#native-and-com-interoperability)
* [Parallel Programming](#parallel-programming)
* [Advanced Threading](#advanced-threading)
* [Security](#security)
* [Reflection and Metadata](#reflection-and-metadata)
* [Networking](#networking)
* [Streams and I/O](#streams-and-I/O)
* [Diagnostics and Code Contracts](#diagnostics-and-code-Contracts)

# Types, Storage, and Variables

```cs

//A variable in C# can never have an uninitialized value.
public class Program
    {
        private static int x;
        private Boolean y;
        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.WriteLine(y);
            Console.ReadKey();
        }
    }

**Output**
0
False
```


## Namespaces
```cs
//Namespaces
System.Security.Cryptography

//fully qualified name
System.Security.Cryptography.RSA rsa = System.Security.Cryptography.RSA.Create();

namespace Outer.Middle.Inner
{
	class Class1 {}
	class Class2 {}
}


namespace Outer
{
	namespace Middle
	{
		namespace Inner
		{
			class Class1 {}
			class Class2 {}
		}
	}
}

//using Directive
using Outer.Middle.Inner;
```

### Rules Within a Namespace
#### Name scoping
```cs
//Names declared in outer namespaces can be used unqualified within inner namespaces.

namespace Outer
	{
	namespace Middle
	{
		class Class1 {}
		
		namespace Inner
		{
			class Class2 : Class1 {}
		}
	}
}
```

```cs
namespace MyTradingCompany
{
	namespace Common
	{
		class ReportBase {}
	}
	
	namespace ManagementReporting
	{
		class SalesReport : Common.ReportBase {}
	}
}
```

#### Name hiding
```cs
//If the same type name appears in both an inner and an outer namespace, the inner name wins.
namespace Outer
{
	class Foo { }
	namespace Inner
	{
		class Foo { }
		class Test
		{
			Foo f1; // = Outer.Inner.Foo
			Outer.Foo f2; // = Outer.Foo
		}
	}
}
```

#### Repeated namespaces
```cs
//You can repeat a namespace declaration, as long as the type names within the namespaces don’t conflict

//Source file 1:
namespace Outer.Middle.Inner
{
	class Class1 {}
}

Source file 2:
namespace Outer.Middle.Inner
{
	class Class2 {}
}
```

#### Nested using directive
```
namespace N1
{
	class Class1 {}
}

namespace N2
{
	using N1;
	class Class2 : Class1 {}
}

namespace N2
{
	class Class3 : Class1 {} // Compile-time error
}
```

### Aliasing Types and Namespaces
```cs
using PropertyInfo2 = System.Reflection.PropertyInfo;
class Program { PropertyInfo2 p; }

//An entire namespace can be aliased, as follows:
using R = System.Reflection;
class Program { R.PropertyInfo p; }
```

### Advanced Namespace Features

#### Extern
```
//Library 1:
// csc target:library /out:Widgets1.dll widgetsv1.cs
namespace Widgets
{
	public class Widget {}
}

//Library 2:
// csc target:library /out:Widgets2.dll widgetsv2.cs
namespace Widgets
{
	public class Widget {}
}

//Application:
// csc /r:Widgets1.dll /r:Widgets2.dll application.cs
using Widgets;
class Test
{
	static void Main()
	{
		Widget w = new Widget();
	}
}


//The application cannot compile, because Widget is ambiguous. 
//Extern aliases can resolve the ambiguity in our application:
// csc /r:W1=Widgets1.dll /r:W2=Widgets2.dll application.cs

extern alias W1;
extern alias W2;
class Test
{
	static void Main()
	{
		W1.Widgets.Widget w1 = new W1.Widgets.Widget();
		W2.Widgets.Widget w2 = new W2.Widgets.Widget();
	}
}
```

#### Namespace alias qualifiers
```
// The global namespace—the root of all namespaces (keyword global)
// The set of extern aliases

namespace N
{
	class A
	{
		public class B {} // Nested type
		static void Main() { new A.B(); } // Instantiate class B
	}
}

namespace A
{
	class B {}
}


namespace N
{
	class A
	{
		static void Main()
		{
			System.Console.WriteLine (new A.B());
			System.Console.WriteLine (new global::A.B());
		}
		public class B {}
	}
}
namespace A
{
	class B {}
}
```

```cs
extern alias W1;
extern alias W2;

class Test
{
	static void Main()
	{
		W1::Widgets.Widget w1 = new W1::Widgets.Widget();
		W2::Widgets.Widget w2 = new W2::Widgets.Widget();
	}
}
```

## Numeric Types
```cs
//Integral literals
int x = 127;
long y = 0x7F;

//Real literals
double d = 1.5;
double million = 1E06;

float f = 4.5F;
decimal d = −1.23M; // Will not compile without the M suffix.

Console.WriteLine ( 1.0.GetType()); // Double (double)
Console.WriteLine ( 1E06.GetType()); // Double (double)
Console.WriteLine ( 1.GetType()); // Int32 (int)
Console.WriteLine ( 0xF0000000.GetType()); // UInt32 (uint)


float f = 1.0F;
double d = 1D;
decimal d = 1.0M;
uint i = 1U;
long i = 1L;
ulong i = 1UL;


// Implicit lossless conversion from int literal to long
long i = 5; 

//you can always add a decimal point to a numeric literal
double x = 4.0;

// Will not compile without the M suffix.
decimal d = −1.23M; 

//Floating-point to integral conversions
//implicitly converted to all floating-point types
int i = 1;
float f = i;

//reverse conversion must be explicit
int i2 = (int)f;

//Integral arithmetic overflow check operators
int a = 1000000;
int b = 1000000;

int c = checked (a * b); // Checks just the expression.

checked 	// Checks all expressions
{ 		// in statement block.
	...
	c = a * b;
	...
}


//Overflow checking for constant expressions
int x = int.MaxValue + 1; // Compile-time error
int y = unchecked (int.MaxValue + 1); // No errors


//Dividing a nonzero number by zero results in an infinite value.
Console.WriteLine ( 1.0 / 0.0); // Infinity
Console.WriteLine (−1.0 / 0.0); // -Infinity
Console.WriteLine ( 1.0 / −0.0); // -Infinity
Console.WriteLine (−1.0 / −0.0); // Infinity


//Dividing zero by zero, or subtracting infinity from infinity, results in a NaN
Console.WriteLine ( 0.0 / 0.0); // NaN
Console.WriteLine ((1.0 / 0.0) − (1.0 / 0.0)); // NaN

Console.WriteLine (0.0 / 0.0 == double.NaN); // False
Console.WriteLine (double.IsNaN (0.0 / 0.0)); // True
Console.WriteLine (object.Equals (0.0 / 0.0, double.NaN)); // True


```

### Numeric Conversions
```cs
int x = 12345; // int is a 32-bit integral
long y = x; // Implicit conversion to 64-bit integral
short z = (short)x; // Explicit conversion to 16-bit integral
```




## Boolean Type


## Characters
```cs
char c = 'A'; // Simple character
char newLine = '\n';
char backSlash = '\\';
char copyrightSymbol = '\u00A9';
char omegaSymbol = '\u03A9';
char newLine = '\u000A';
char backSlash = '\\';
char Null = '\0';
char Alert = '\a'
char Backspace = '\b'
char Formfeed = '\f' 
char Newline= '\n' 
char Carriagereturn = '\r' 
char Horizontaltab = '\t' 
char Verticaltab = '\v' 
```

## Strings 
```cs
string a = "Heat";
string a = "test";
string b = "test";
Console.Write (a == b); // True

string a = "Here's a tab:\t";
string a1 = "\\\\server\\fileshare\\helloworld.cs";


//verbatim string
string a2 = @ "\\server\fileshare\helloworld.cs";

//escaped vs verbatim
string escaped = "First Line\r\nSecond Line";
string verbatim = @"First Line
Second Line";

// Assuming your IDE uses CR-LF line separators:
Console.WriteLine (escaped == verbatim); // True

//String concatenation
string s = "a" + 5; // a5

//include the double-quote character
string xml = @"<customer id=""123""></customer>";
```



# Classes

## Classes
```cs
//public, internal, abstract, sealed, static, unsafe, and partial
class YourClassName
{
}
```

## Fields
```cs
//Static modifier: static
//Access modifiers: public internal private protected
//Inheritance modifier: new
//Unsafe code modifier: unsafe
//Read-only modifier: readonly
//Threading modifier: volatile

class Octopus
{
	string name;
	public int Age = 10;
}
```

## Methods
```cs
Static modifier: static
Access modifiers: public internal private protected
Inheritance modifiers: new virtual abstract override sealed
Partial method modifier: partial
Unmanaged code modifiers: unsafe extern



//Overloading methods
void Foo (int x) {...}
void Foo (double x) {...}
void Foo (int x, float y) {...}
void Foo (float x, int y) {...}

void Foo (int x) {...}
float Foo (int x) {...} // Compile-time error
void Goo (int[] x) {...}
void Goo (params int[] x) {...} // Compile-time error


//Pass-by-value versus pass-by-reference
void Foo (int x) {...}
void Foo (ref int x) {...} // OK so far
void Foo (out int x) {...} // Compile-time error

//Partial methods
partial class PaymentForm // In auto-generated file
{
	...
	partial void ValidatePayment (decimal amount);
}	

partial class PaymentForm // In hand-authored file
{
	...
	partial void ValidatePayment (decimal amount)
	{
		if (amount > 100)
		...
	}
}
```

## Constructors
```cs
Access modifiers: public internal private protected
Unmanaged code modifiers: unsafe extern

//Overloading constructors
public class Wine
{
	public decimal Price;
	public int Year;
	public Wine (decimal price) { Price = price; }
	public Wine (decimal price, int year) : this (price) { Year = year; }
}


public class Class1
{
	Class1() {} // Private constructor
	public static Class1 Create (...)
	{
		// Perform custom logic here to return an instance of Class1
		...
	}
}
```

## Static Constructors
```cs
class Test
{
	static Test() {
		Console.WriteLine ("Type Initialized"); 
	}
}
```

## The this Reference
```cs
public class Panda
{
	public Panda Mate;
	public void Marry (Panda partner)
	{
		Mate = partner;
		partner.Mate = this;
	}
}
```

## Properties
## Properties
```cs
public class Properties
{
	public string Name{}
}
//Output
//Error 'Properties.Properties.Name': property or indexer must have at least one accessor
```

## Get accessor
```cs
public string Name
{
	get
	{
		 return "I am a Name property";
	}
}
```

```cs
public int Age
{
	get
	{
		DateTime dateOfBirth=new DateTime(1984,01,20);
		DateTime currentDate = DateTime.Now;
		int age = currentDate.Year - dateOfBirth.Year;
		return age;
	}
}
```

## Set accessor		
```cs
public int Age
{
	set
	{
		Console.WriteLine("Set Age called " + value);
	}
}	
```

### Auto
```cs
public string Name { get; set; }
public int Age { get;  }
public int Age {  set; }
```

### Readonly
```cs
public int Age { get { return age; } }
```

### Write-Only
```cs
public int Age { set { age = value; } }
```

### Static Properties
```cs
public static int Age
{
	set
	{
		Console.WriteLine("In set static property; value is " + value);
	}
	get
	{
		Console.WriteLine("In get static property");
		return 10;
	}
}
```

### Abstract Propertiesnamespace Properties
```cs

    public abstract class BaseClass
    {
        public abstract int AbsProperty { get; set; }
    }

    public class Properties : BaseClass
    {
        public override int AbsProperty
        {
            get
            {
                return 10;
            }
            set { Console.WriteLine("set called,value is " + value); }
        }
    }

```

### Properties in Inheritance
```cs
namespace Properties
{
  public class PropertiesBaseClass 
    {
        public int Age
        {
            set {}
        }
    }

    public class PropertiesDerivedClass:PropertiesBaseClass
    {
        public int Age
        {
            get { return 32; }
        }
    }
}

namespace Properties
{
    class Program
    {
        static void Main(string[] args)
        {
            PropertiesBaseClass pBaseClass=new PropertiesBaseClass();
            pBaseClass.Age = 10;
            PropertiesDerivedClass pDerivedClass=new PropertiesDerivedClass();
            ((PropertiesBaseClass) pDerivedClass).Age = 15;
            pDerivedClass.Age = 10;
        }
    }
}
```




### CLR property implementation
```cs
public decimal get_CurrentPrice {...}
public void set_CurrentPrice (decimal value) {...}
```
## Indexers


## Index
```cs
static void Main(string[] args)
{
	Indexer indexer=new Indexer();
	indexer[1] = 50;
}
//Output
Compile the code. Error Cannot apply indexing with [] to an expression of type 'Indexers.Indexer'
```

```cs
namespace Indexers
{
    public class Indexer
    {
		public int this[int indexValue]
        {
            set
            {
                Console.WriteLine("I am in set : Value is " + value + " and indexValue is " + indexValue);
            }
             get
            {
                Console.WriteLine("I am in get and indexValue is " + indexValue);
                return 30;
            }
        }
    }
	
	class Program
    {
        static void Main(string[] args)
        {
            Indexer indexer=new Indexer();
            indexer["name"]=20;
            Console.WriteLine(indexer["name"]);
        }
    }
	
}
```
		
		
### Indexers in interfaces
```cs
namespace Indexers
{
    interface IIndexers
    {
        string this[int indexerValue] { get; set; }
    }

    public class IndexerClass:IIndexers
    {
        readonly string[] _nameList = { "AKhil","Bob","Shawn","Sandra" };

        public string this[int indexerValue]
        {
            get
            {
                return _nameList[indexerValue];
            }
            set
            {
                _nameList[indexerValue] = value;
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
           IIndexers iIndexer=new IndexerClass();
            Console.WriteLine(iIndexer[0]);
            Console.WriteLine(iIndexer[1]);
            Console.WriteLine(iIndexer[2]);
            Console.WriteLine(iIndexer[3]);
            Console.ReadLine();

        }
    }
}
```

### Indexers in Abstract class
```cs
namespace Indexers
{
	//AbstractBaseClass
    public abstract class AbstractBaseClass
    {
        public abstract string this[int indexerValue] { get; set; }
    }

	//IndexerClass
    public class IndexerClass:AbstractBaseClass
    {
        readonly string[] _nameList = { "AKhil","Bob","Shawn","Sandra" };

        public override string this[int indexerValue]
        {
            get
            {
                return _nameList[indexerValue];
            }
            set
            {
                _nameList[indexerValue] = value;
            }
        }
    }
}

//Program.cs
class Program
{
	static void Main(string[] args)
	{
	   AbstractBaseClass absIndexer=new IndexerClass();
		Console.WriteLine(absIndexer[0]);
		Console.WriteLine(absIndexer[1]);
		Console.WriteLine(absIndexer[2]);
		Console.WriteLine(absIndexer[3]);
		absIndexer[2] = "Akhil Mittal";
		Console.WriteLine(absIndexer[2]);

		Console.ReadLine();

	}
}
```

### Indexer Overloading
```cs
public class Indexer
{
	public int this[int indexerValue]
	{
		set
		{
			Console.WriteLine("Integer value " + indexerValue + " " + value);
		}
	}

	public int this[string indexerValue]
	{
		set
		{
			Console.WriteLine("String value " + indexerValue + " " + value);
		}
	}

	public int this[string indexerValue, int indexerintValue]
	{
		set
		{
			Console.WriteLine("String and integer value " + indexerValue + " " + indexerintValue + " " + value);
		}
	}
}
	
class Program
{
	static void Main(string[] args)
	{
		Indexer indexer=new Indexer();
		indexer[1] = 30;
		indexer["name"]=20;
		indexer["address",2] = 40;
		Console.ReadLine();
	}
}
```

### Inheritance/Polymorphism in Indexers
```cs
//Indexer.cs
namespace Indexers
{
    public class IndexerBaseClass
    {
        public virtual int this[int indexerValue]
        {
            get
            {
                Console.WriteLine("Get of IndexerBaseClass; indexer value: " + indexerValue);
                return 100;
            }
            set
            {
                Console.WriteLine("Set of IndexerBaseClass; indexer value: " + indexerValue + " set value " + value);
            }

        }
    }
    public class IndexerDerivedClass:IndexerBaseClass
    {
        public override int this[int indexerValue]
        {
            get
            {
                int dValue = base[indexerValue];
                Console.WriteLine("Get of IndexerDerivedClass; indexer value: " + indexerValue + " dValue from base class indexer: " + dValue);
                return 500;
            }
            set
            {
                Console.WriteLine("Set of IndexerDerivedClass; indexer value: " + indexerValue + " set value " + value);
                base[indexerValue] = value;
            }

        }
    }
}

//Program.cs
class Program
{
	static void Main(string[] args)
	{
		IndexerDerivedClass indexDerived=new IndexerDerivedClass();
		indexDerived[2] = 300;
		Console.WriteLine(indexDerived[2]);
		Console.ReadLine();

	}
}
```	

### Implementing an indexer
```cs
class Sentence
{
	string[] words = "The quick brown fox".Split();
	
	public string this [int wordNum] // indexer
	{
		get { return words [wordNum]; }
		set { words [wordNum] = value; }
	}
}

Sentence s = new Sentence();
Console.WriteLine (s[3]); // fox
s[3] = "kangaroo";
Console.WriteLine (s[3]); // kangaroo
```

### Constants
```cs
public class Test
{
	public const string Message = "Hello World";
}
```
### Finalizers
```cs
class Class1
{
	~Class1()
	{
		...
	}
}

//This is actually C# syntax for overriding Object’s Finalize method, 
//and the compiler expands it into the following method declaration:
protected override void Finalize()
{
	...
	base.Finalize();
}
```


## Abstract Classes

### Abstract Classes in Action
* We cannot create an object of abstract class using new keyword. 
* Seems that the class is useless for us as we cannot use it for other practical purposes as we used to do.

```cs
namespace InheritanceAndPolymorphism
{
    public abstract class ClassA
    {  }

    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA classA = new ClassA();
        }
    }
}

//Output
//Compile time error: Cannot create an instance of the abstract class or interface 'InheritanceAndPolymorphism.ClassA'
```

### Non Abstract Method Definition in Abstract Class
```cs
public abstract class ClassA
{
	//add some code to our abstract class:
    public int a;
    public void XXX()
    {    }
}

public class Program
{
    private static void Main(string[] args)
    {
		//we cannot use new if we have already used an abstract modifier.
        ClassA classA = new ClassA();
        Console.ReadKey();
    }
}
Output
Compile time error: Cannot create an instance of the abstract class or interface 'InheritanceAndPolymorphism.ClassA'
```

### Abstract Class Acting as a Base Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }
}

public class ClassB:ClassA
{
}

public class Program
{
    private static void Main(string[] args)
    {
		// A class can be derived from abstract class. 
		// Creating an object of ClassB does not gives us any error.
        ClassB classB = new ClassB();
    }
}
```

### Non Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {

    }

    public void YYY();
}

//A class can be derived from an abstract class.
public class ClassB:ClassA
{

}

public class Program
{
    private static void Main(string[] args)
    {
		//A object of a class derived from an abstract class can be created using new.
        ClassB classB = new ClassB();
        Console.ReadKey();
    }
}

//Output
//Compile time error: 'InheritanceAndPolymorphism.ClassA.YYY()' must declare a body because it is not marked abstract, extern, or partial
```

###  Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compiler error: 'InheritanceAndPolymorphism.ClassB' does not implement  inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
```

### Abstract Method Implementation in Derived Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}


public class ClassB:ClassA
{
    public void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compile time error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
Compile time warning: 'InheritanceAndPolymorphism.ClassB.YYY()' hides inherited member 'InheritanceAndPolymorphism.ClassA.YYY()'.
```


### Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
	public int a;
	public void XXX()
	{
	}

	abstract public void YYY();
}


public class ClassB:ClassA
{
	//If any method as abstract in our abstract class, then derived class must  provide the body for that abstract method
	//unless a body is provided for that abstract method, we cannot create an object of that derived class.
	public override void YYY()
	{
	}
}

public class Program
{
	private static void Main(string[] args)
	{
		ClassB classB = new ClassB();
	}
}
Output
Compiler error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
```	
	
### Abstract Method Implementation in Derived Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Two compile time errors this time:
Compile time error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
Compile time warning: 'InheritanceAndPolymorphism.ClassB.YYY()' hides inherited member 'InheritanceAndPolymorphism.ClassA.YYY()'.

```

```cs
To make a member override that implementation, add the override keyword.
public abstract class ClassA
{
	public int a;
	public void XXX()
	{
	}

   abstract public void YYY();
}

public class ClassB:ClassA
{
	public override void YYY()
	{
	}
}

public class Program
{
	private static void Main(string[] args)
	{
		ClassB classB = new ClassB();
	}
}
```
	
	
### Abstract Method Implementation in Derived Class with Different Return Type
```cs
public abstract class ClassA
{
  public int a;
  public void XXX()
  {
  }

 abstract public void YYY();
}

public class ClassB:ClassA
{
  public override int YYY()
  {
  }
}


public class Program
{
  private static void Main(string[] args)
  {
	  ClassB classB = new ClassB();
  }
}
 
Output
Compile time error: 'InheritanceAndPolymorphism.ClassB.YYY()': return type must be 'void' to match overridden member 'InheritanceAndPolymorphism.ClassA.YYY()'
```
	

```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
   abstract public void YYY1();
   abstract public void YYY2();
   abstract public void YYY3();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Compiler error:
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY3()'
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY2()'
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY1()'
```
	
### Abstract Method in Non Abstract Class
```cs
public class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compiler error: 'InheritanceAndPolymorphism.ClassA.YYY()' is abstract but it is contained in non-abstract class 'InheritanceAndPolymorphism.ClassA'
```

### Abstract Base Method
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
         base.YYY();
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}
Output
Compile time error : Cannot call an abstract base member: 'InheritanceAndPolymorphism.ClassA.YYY()'
```

### Abstract Class Acting as Derived as Well as Base Class
```cs
public class ClassA
{
    public virtual void XXX()
    {
        Console.WriteLine("ClassA XXX");
    }
}

public abstract class ClassB:ClassA
{
    public new abstract void XXX();
}

public class ClassC:ClassB
{
    public override void XXX()
    {
        System.Console.WriteLine("ClassC XXX");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassA classA = new ClassC();
        ClassB classB = new ClassC();
        classA.XXX(); classB.XXX();
    }
}	
Output
ClassA XXX
ClassC XXX
```


### Can Abstract Class be Sealed?
* Abstract class cannot be sealed class.
* Abstract class cannot be a static class.
```cs
public sealed abstract class ClassA
{
    public abstract void XXX()
    {
        Console.WriteLine("ClassA XXX");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
    }
}

Output
Compile time error: 'InheritanceAndPolymorphism.ClassA': an abstract class cannot be sealed or static 
```


## Polymorphism

### Method Overloading or Early Binding or Compile Time Polymorphism
*  C# recognizes the method by its parameters and not only by its name.
```cs
public class Overload
{
  public void DisplayOverload(int a){
	  System.Console.WriteLine("DisplayOverload " + a);
  }
  public void DisplayOverload(string a){
	  System.Console.WriteLine("DisplayOverload " + a);
  }
  public void DisplayOverload(string a, int b){
	  System.Console.WriteLine("DisplayOverload " + a + b);
  }
}
```


```cs
public void DisplayOverload() { }
public int DisplayOverload(){ }

Output
Error: Type 'InheritanceAndPolymorphism.Overload' already defines a member called 'DisplayOverload' with the same parameter types

Point to remember: The return value/parameter type of a method is never the part of method signature if the names of the methods are same. So this is not polymorphism.
Point to remember: Modifiers such as static are not considered as part of method signature.
```

## xx
```cs
private void DisplayOverload(int a) {   }

private void DisplayOverload(out int a)
{
	a = 100;
}

private void DisplayOverload(ref int a) {   }

Output
Error: Cannot define overloaded method 'DisplayOverload' because it differs from another method only on ref and out
```

## Role of Params Parameter in Polymorphism
```cs
//Point to remember: Parameter names should be unique. And also we can not have a parameter name and a declared variable name in the same function as same.

public void DisplayOverload(int a, string a)  {   }

public void Display(int a)
{
	string a;
}

Error1: The parameter name 'a' is a duplicate
Error2: A local variable named 'a' cannot be declared in this scope because it would give a different meaning to 'a', which is already used in a 'parent or current' scope to denote something else

```

```cs
public class Overload
{
	public void Display()
	{
		DisplayOverload(100, "Akhil", "Mittal", "OOP");
		DisplayOverload(200, "Akhil");
		DisplayOverload(300);
	}

	private void DisplayOverload(int a, params string[] parameterArray)
	{
		foreach (string str in parameterArray)
		   Console.WriteLine(str + " " + a);
	}
}

class Program
{
	static void Main(string[] args)
	{
		Overload overload = new Overload();
		overload.Display();
		Console.ReadKey();
	}
}
Error: A parameter array must be the last parameter in a formal parameter list	
```

## 
```cs
Point to Remember: C# is very smart to recognize if the penultimate argument and the params have the same data type.
public class Overload
{
    public void Display()
    {
        DisplayOverload(100, 200, 300);
        DisplayOverload(200, 100);
        DisplayOverload(200);
    }

    private void DisplayOverload(int a, params int[] parameterArray)
    {
        foreach (var i in parameterArray)
            Console.WriteLine(i + " " + a);
    }

}

class Program
{
	static void Main(string[] args)
	{
		Overload overload = new Overload();
		overload.Display();
		Console.ReadKey();
	}
}
Error: The parameter array must be a single dimensional array	
```


```cs
public class Overload
    {
        public void Display()
        {
            string[] names = {"Akhil", "Ekta", "Arsh"};
            DisplayOverload(3, names);
        }

        private void DisplayOverload(int a, params string[] parameterArray)
        {
            foreach (var s in parameterArray)
                Console.WriteLine(s + " " + a);
        }

    }
```

```cs
public class Overload
{
	public void Display()
	{
	   string [] names = {"Akhil","Arsh"};
	   DisplayOverload(2, names, "Ekta");
	}

	private void DisplayOverload(int a, params string[] parameterArray)
	{
		foreach (var str in parameterArray)
			Console.WriteLine(str + " " + a);
	}

}
Output
Error: The best overloaded method match for 'InheritanceAndPolymorphism.Overload.DisplayOverload(int, params string[])' has some invalid arguments
Error:Argument 2: cannot convert from 'string[]' to 'string'

```


```cs
public class Overload
{
	public void Display()
	{
		int[] numbers = {10, 20, 30};
		DisplayOverload(40, numbers);
		Console.WriteLine(numbers[1]);
	}

	private void DisplayOverload(int a, params int[] parameterArray)
	{
		parameterArray[1] = 1000;
	}

}
Output
1000
```

```cs
public class Overload
{
	public void Display()
	{
		int number = 102;
		DisplayOverload(200, 1000, number, 200);
		Console.WriteLine(number);
	}

	private void DisplayOverload(int a, params int[] parameterArray)
	{
		parameterArray[1] = 3000;
	}

}
Output
102
```

```cs
public class Overload
{
	public void Display()
	{
		DisplayOverload(200);
		DisplayOverload(200, 300);
		DisplayOverload(200, 300, 500, 600);
	}

	private void DisplayOverload(int x, int y)
	{
		Console.WriteLine("The two integers " + x + " " + y);
	}

	private void DisplayOverload(params int[] parameterArray)
	{
		Console.WriteLine("parameterArray");
	}

}

Output
parameterArray
The two integers 200 300
parameterArray
```

```cs
public class Overload
{
	public static void Display(params object[] objectParamArray)
	{
		foreach (object obj in objectParamArray)
		{
			Console.Write(obj.GetType().FullName + " ");
		}
		Console.WriteLine();

	}
}

class Program
{
	static void Main(string[] args)
	{
		object[] objArray = { 100, "Akhil", 200.300 };
		object obj = objArray;
		Overload.Display(objArray);
		Overload.Display((object)objArray);
		Overload.Display(obj);
		Overload.Display((object[])obj);
		Console.ReadKey();

	}
}

Output
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
	
```

## Inheritance


```cs
class ClassA
 {
	
 }

class ClassB
{
	public int x = 100;
	public void Display1()
	{
		Console.WriteLine("ClassB Display1");
	}
	public void Display2()
	{
		Console.WriteLine("ClassB Display2");
	}
}

class Program
  {
      static void Main(string[] args)
      {

          ClassA a = new ClassA();
          a.Display1();
      }
  }
Output:
Error: 'InheritanceAndPolymorphism.ClassA' does not contain a definition for 'Display1' and no extension method 'Display1' accepting a first argument of type 'InheritanceAndPolymorphism.ClassA' could be found (are you missing a using directive or an assembly reference?)
  
```

```cs
class ClassA:ClassB
{
}

class ClassB
{
	public int x = 100;
	public void Display1()
	{
		Console.WriteLine("ClassB Display1");
	}
	public void Display2()
	{
		Console.WriteLine("ClassB Display2");
	}
}
	
class Program
{
	static void Main(string[] args)
	{
		ClassA a = new ClassA();
		a.Display1();
		Console.ReadKey();
	}
}
	
Output
ClassB Display1
```

```cs
class ClassA:ClassB
    {
		//No one can stop a derived class to have a method with the same name already declared in its base class.
        public void Display1()
        {
            System.Console.WriteLine("ClassA Display1");
        }
    }

class ClassB
    {
        public int x = 100;
        public void Display1()
        {
            Console.WriteLine("ClassB Display1");
        }
        public void Display2()
        {
            Console.WriteLine("ClassB Display2");
        }
    
	class Program
    {
        static void Main(string[] args)
        {
            ClassA a = new ClassA();
            a.Display1();
            Console.ReadKey();
        }
    }
Output:
ClassA Display1
Warning: 'InheritanceAndPolymorphism.ClassA.Display1()' hides inherited member 'InheritanceAndPolymorphism.ClassB.Display1()'. Use the new keyword if hiding was intended.
	
```

```cs
ClassA:

  class ClassA:ClassB
    {
        public void Display1()
        {
            Console.WriteLine("ClassA Display1");
            base.Display1();
        }
    }

ClassB:

class ClassB
    {
        public int x = 100;
        public void Display1()
        {
            Console.WriteLine("ClassB Display1");
        }
        public void Display2()
        {
            Console.WriteLine("ClassB Display2");
        }
    }
class Program
    {
        static void Main(string[] args)
        {
            ClassA a = new ClassA();
            a.Display1();
            Console.ReadKey();
        }
    }	
	
	Output
	ClassA Display1 
ClassB Display1
```

```cs
/// <summary>
/// ClassB: acting as base class
/// </summary>
class ClassB
 {
     public int x = 100;
     public void Display1()
     {
         Console.WriteLine("ClassB Display1");
     }
     public void Display2()
     {
         Console.WriteLine("ClassB Display2");
     }
 }

 /// <summary>
 /// ClassA: acting as derived class
 /// </summary>
 class ClassA : ClassB
 {
     public void Display1()
     {
         Console.WriteLine("ClassA Display1");
         base.Display2();
     }
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 class Program
 {
     static void Main(string[] args)
     {
         ClassA a = new ClassA();
         a.Display1();
         Console.ReadKey();
     }
 }
 Output
 ClassA Display1
ClassB Display2
```

```cs
/// <summary>
/// ClassB: acting as base class
/// </summary>
class ClassB
 {
     public int x = 100;
     public void Display1()
     {
         Console.WriteLine("ClassB Display1");
     }
 }

 /// <summary>
 /// ClassA: acting as derived class
 /// </summary>
 class ClassA : ClassB
 {
     public void Display2()
     {
         Console.WriteLine("ClassA Display2");
     }
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 class Program
 {
     static void Main(string[] args)
     {
         ClassB b = new ClassB();
         b.Display2();
         Console.ReadKey();
     }
 }
 
 Output

Error: 'InheritanceAndPolymorphism.ClassB' does not contain a definition for 'Display2' and no extension method 'Display2' accepting a first argument of type 'InheritanceAndPolymorphism.ClassB' could be found (are you missing a using directive or an assembly reference?)
Point to remember: Inheritance does not work backwards.
Point to remember: Except constructors and destructors, a class inherits everything from its base class .

```

```cs
 classes defined cannot inherit from special built in classes in C#.
public class ClassW : System.ValueType
  {
  }

  public class ClassX : System.Enum
  {
  }

  public class ClassY : System.Delegate
  {
  }

  public class ClassZ : System.Array
  {
  }
  
  Errors
  'InheritanceAndPolymorphism.ClassW' cannot derive from special class 'System.ValueType'
'InheritanceAndPolymorphism.ClassX' cannot derive from special class 'System.Enum'
'InheritanceAndPolymorphism.ClassY' cannot derive from special class 'System.Delegate'
'InheritanceAndPolymorphism.ClassZ' cannot derive from special class 'System.Array'
  In inheritance in C#, custom classes cannot derive from special built in c# classes like System.ValueType, System.Enum, System.Delegate, System.Array, etc.
```

```cs
public class ClassW
  {
  }

  public class ClassX
  {
  }

  public class ClassY : ClassW, ClassX
  {
  }
  
  Compile time Error: Class 'InheritanceAndPolymorphism.ClassY' cannot have multiple base classes: 'InheritanceAndPolymorphism.ClassW' and 'ClassX'.
  
  So one more Point to remember: A class can only be derived from one class in C#. C# does not support multiple inheritance by means of class*.
  
  *Multiple inheritance in C# can be accomplished by the use of Interfaces
  
```

```cs
//Circular dependency is not allowed in inheritance in C#.
public class ClassW:ClassY
 {
 }

 public class ClassX:ClassW
 {
 }

 public class ClassY :  ClassX
 {
 }
 Error: Circular base class dependency involving 'InheritanceAndPolymorphism.ClassX' and 'InheritanceAndPolymorphism.ClassW'.
 ```
 
```cs
Point to remember:  We can equate an object of a base class to a derived class but not vice versa.
public class ClassB
 {
     public int b = 100;
 }

 public class ClassA:ClassB
 {
     public int a = 100;
 }

 public class Program
 {
     private static void Main(string[] args)
     {
         ClassB classB = new ClassB();
         ClassA classA = new ClassA();
         classA = classB;
         classB = classA;
     }
 }
 Error: Cannot implicitly convert type 'InheritanceAndPolymorphism.ClassB' to 'InheritanceAndPolymorphism.ClassA'. An explicit conversion exists (are you missing a cast?)
 Point to remember:  We can equate an object of a base class to a derived class but not vice versa.
 ```
 
 ```cs
 public class ClassB
    {
        public int b = 100;
    }

    public class ClassA:ClassB
    {
        public int a = 100;
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassB classB = new ClassB();
            ClassA classA = new ClassA();
            classB=classA;
            classA = (ClassA)classB;
        }
    }
	
 ```
  ```cs
  public class ClassB
 {
     public int b = 100;
 }

 public class ClassA // Removed ClassB as base class
 {
     public int a = 100;
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 public class Program
 {
     private static void Main(string[] args)
     {
         ClassB classB = new ClassB();
         ClassA classA = new ClassA();
         classB = (ClassB)classA;
         classA = (ClassA)classB;
     }
 }
 Output
 Cannot convert type 'InheritanceAndPolymorphism.ClassA' to 'InheritanceAndPolymorphism.ClassB'
Cannot convert type 'InheritanceAndPolymorphism.ClassB' to 'InheritanceAndPolymorphism.ClassA' 
 ```
  ```cs
  /// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        int integerA = 10;
        char characterB = 'A';
        integerA = characterB;
        characterB = integerA;
    }
}
Output

Error: Cannot implicitly convert type 'int' to 'char'. An explicit conversion exists (are you missing a cast?)

Point to remember: We cannot implicitly convert an int to char, but char can be converted to int.
 ```

 
##Dynamic Binding/Run Time Polymorphism
```cs
/// <summary>
/// ClassB, acting as a base class
/// </summary>
public class ClassB
{
    public void AAA()
    {
        Console.WriteLine("ClassB AAA");
    }

    public void BBB()
    {
        Console.WriteLine("ClassB BBB");
    }

    public void CCC()
    {
        Console.WriteLine("ClassB CCC");
    }
}

public class ClassA : ClassB
{
    public void AAA()
    {
        Console.WriteLine("ClassA AAA");
    }

    public void BBB()
    {
        Console.WriteLine("ClassA BBB");
    }

    public void CCC()
    {
        Console.WriteLine("ClassA CCC");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassA x = new ClassA();
        ClassB y=new ClassB();
        ClassB z=new ClassA();

        x.AAA(); x.BBB(); x.CCC();
        y.AAA(); y.BBB();y.CCC();
        z.AAA(); z.BBB(); z.CCC();
    }
}
Output
ClassA AAA
ClassA BBB
ClassA CCC
ClassB AAA
ClassB BBB
ClassB CCC
ClassB AAA
ClassB BBB
ClassB CCC
'InheritanceAndPolymorphism.ClassA.AAA()' hides inherited member 'InheritanceAndPolymorphism.ClassB.AAA()'. Use the new keyword if hiding was intended.
'InheritanceAndPolymorphism.ClassA.BBB()' hides inherited member 'InheritanceAndPolymorphism.ClassB.BBB()'. Use the new keyword if hiding was intended.
'InheritanceAndPolymorphism.ClassA.CCC()' hides inherited member 'InheritanceAndPolymorphism.ClassB.CCC()'. Use the new keyword if hiding was intended.
```

```cs


/// <summary>
    /// ClassB, acting as a base class
    /// </summary>
    public class ClassB
    {
        public virtual void AAA()
        {
            Console.WriteLine("ClassB AAA");
        }

        public virtual void BBB()
        {
            Console.WriteLine("ClassB BBB");
        }

        public virtual void CCC()
        {
            Console.WriteLine("ClassB CCC");
        }
    }

    /// <summary>
    /// Class A, acting as a derived class
    /// </summary>
    public class ClassA : ClassB
    {
        public override void AAA()
        {
            Console.WriteLine("ClassA AAA");
        }

        public new void BBB()
        {
            Console.WriteLine("ClassA BBB");
        }

        public void CCC()
        {
            Console.WriteLine("ClassA CCC");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassB y = new ClassB();
            ClassA x = new ClassA();
            ClassB z = new ClassA();

            y.AAA(); y.BBB(); y.CCC();
            x.AAA(); x.BBB(); x.CCC();
            z.AAA(); z.BBB(); z.CCC();

            Console.ReadKey();
        }
    }
```

### Run Time Polymorphism with Three Classes
```cs
/// <summary>
/// ClassB, acting as a base class
/// </summary>
public class ClassB
{
    public  void AAA()
    {
        Console.WriteLine("ClassB AAA");
    }

    public virtual void BBB()
    {
        Console.WriteLine("ClassB BBB");
    }

    public virtual void CCC()
    {
        Console.WriteLine("ClassB CCC");
    }
}

/// <summary>
/// Class A, acting as a derived class
/// </summary>
public class ClassA : ClassB
{
    public virtual void AAA()
    {
        Console.WriteLine("ClassA AAA");
    }

    public new void BBB()
    {
        Console.WriteLine("ClassA BBB");
    }

    public override void CCC()
    {
        Console.WriteLine("ClassA CCC");
    }
}

/// <summary>
/// Class C, acting as a derived class
/// </summary>
public class ClassC : ClassA
{
    public override void AAA()
    {
        Console.WriteLine("ClassC AAA");
    }

    public void CCC()
    {
        Console.WriteLine("ClassC CCC");
    }
}

/// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        ClassB y = new ClassA();
        ClassB x = new ClassC();
        ClassA z = new ClassC();

        y.AAA(); y.BBB(); y.CCC();
        x.AAA(); x.BBB(); x.CCC();
        z.AAA(); z.BBB(); z.CCC();

        Console.ReadKey();
    }
}
Output
ClassB AAA
ClassB BBB
ClassA CCC
ClassB AAA
ClassB BBB
ClassA CCC
ClassC AAA
ClassA BBB
ClassA CCC

Point to remember: If the base class object declared the method virtual and the derived class used the modifier override, the derived class method will get called. Otherwise the base class method will get executed. Therefore for virtual methods, the data type created is decided at run time only.

Point to remember: All the methods not marked with virtual are non virtual, and the method to be called is decided at compile time, depending upon the static data type of the object.

```

```cs
internal class A
{
    public virtual void X()
    {
    }
}

internal class B : A
{
    public new void X()
    {
    }
}

internal class C : B
{
    public override void X()
    {
    }
}

Error: 'InheritanceAndPolymorphism.C.X()': cannot override inherited member 
'InheritanceAndPolymorphism.B.X()' because it is not marked virtual, abstract, or override

```

### Cut Off Relations
```cs
internal class A
{
    public virtual void X()
    {
        Console.WriteLine("Class: A ; Method X");
    }
}

internal class B : A
{
    public new virtual void X()
    {
        Console.WriteLine("Class: B ; Method X");
    }
}

internal class C : B
{
    public override void X()
    {
        Console.WriteLine("Class: C ; Method X");
    }
}

/// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        A a = new C();
        a.X();
        B b = new C();
        b.X();

        Console.ReadKey();
    }
}
Output

Hide   Copy Code
Class: A ; Method X
Class: C ; Method X
If in the above code, we remove the modifier override from X() in class C, we get:

Output

Hide   Copy Code
Class: A ; Method X
Class: B ; Method X

```

### Runtime Polymorphism with Four Classes
```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            Console.WriteLine("ClassB XXX");
        }
    }

    /// <summary>
    /// Class C
    /// </summary>
    public class ClassC : ClassB
    {
        public virtual new void XXX()
        {
            Console.WriteLine("ClassC XXX");
        }
    }

    /// <summary>
    /// Class D
    /// </summary>
    public class ClassD : ClassC
    {
        public override void XXX()
        {
            Console.WriteLine("ClassD XXX");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassD();
            ClassB b = new ClassD();
            ClassC c=new ClassD();
            ClassD d=new ClassD();
           
            a.XXX();
            b.XXX();
            c.XXX();
            d.XXX();

            Console.ReadKey();
        }
    }
	
	Output
	ClassB XXX
ClassB XXX
ClassD XXX
ClassD XXX
```

```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            base.XXX();
            Console.WriteLine("ClassB XXX");
        }
    }

    /// <summary>
    /// Class C
    /// </summary>
    public class ClassC : ClassB
    {
        public override void XXX()
        {
            base.XXX();
            Console.WriteLine("ClassC XXX");
        }
    }

    /// <summary>
    /// Class D
    /// </summary>
    public class ClassD : ClassC
    {
        public override void XXX()
        {
            Console.WriteLine("ClassD XXX");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassB();
            a.XXX();
            ClassB b = new ClassC();
            b.XXX();
            Console.ReadKey();
        }
    }
	
	Output

Hide   Copy Code
ClassA XXX
ClassB XXX
ClassA XXX
ClassB XXX
ClassC XXX

```
### The Infinite Loop
```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            ((ClassA)this).XXX();
            Console.WriteLine("ClassB XXX");
        }
    }

   
    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassB();
            a.XXX();
           
        }
    }
```


# Inheritance
```cs
public class Asset
{
	public string Name;
}

public class Stock : Asset // inherits from Asset
{
	public long SharesOwned;
}

public class House : Asset // inherits from Asset
{
	public decimal Mortgage;
}

```

# Polymorphism
```cs
public static void Display (Asset asset)
{
	System.Console.WriteLine (asset.Name);
}


Stock msft = new Stock ... ;
House mansion = new House ... ;
Display (msft);
Display (mansion);
``

## Upcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Console.WriteLine (a == msft); // True
Console.WriteLine (a.Name); // OK
Console.WriteLine (a.SharesOwned); // Error: SharesOwned undefined
```

## Downcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Stock s = (Stock)a; // Downcast
Console.WriteLine (s.SharesOwned); // <No error>
Console.WriteLine (s == a); // True
Console.WriteLine (s == msft); // True
```

```cs
House h = new House();
Asset a = h; // Upcast always succeeds
Stock s = (Stock)a; // Downcast fails: a is not a Stock
```

## The as operator
```cs
Asset a = new Asset();
Stock s = a as Stock; // s is null; no exception thrown

int shares = ((Stock)a).SharesOwned; // Approach #1
int shares = (a as Stock).SharesOwned; // Approach #2
```

## The is operator
```cs

```




## Virtual Function Members
```cs
```

### Abstract Classes and Abstract Members
```cs
public abstract class Asset
{
	// Note empty implementation
	public abstract decimal NetValue { get; }
	}
	
	public class Stock : Asset
	{
		public long SharesOwned;
		public decimal CurrentPrice;
	
		// Override like a virtual method.
		public override decimal NetValue
		{
			get { return CurrentPrice * SharesOwned; }
		}
	}		
}
```


### Hiding Inherited Members
```cs
public class A { public int Counter = 1; }
public class B : A { public int Counter = 2; }

public class A { public int Counter = 1; }
public class B : A { public new int Counter = 2; }
```

### Sealing Functions and Classes
```cs
public sealed override decimal Liability { get { return Mortgage; } }
```

#### The base Keyword
```cs
public class House : Asset
{
	...
	public override decimal Liability
	{
		get { return base.Liability + Mortgage; }
	}
}
```

### Constructors and Inheritance
```cs
public class Baseclass
{
	public int X;
	public Baseclass () { }
	public Baseclass (int x) { this.X = x; }
}
public class Subclass : Baseclass { }

public class Subclass : Baseclass
{
	public Subclass (int x) : base (x) { }
}
```

### Boxing and Unboxing
```cs
int x = 9;
object obj = x; // Box the int

int y = (int)obj; // Unbox the int
```
### Copying semantics of boxing and unboxing



## Interfaces
```cs
public interface IEnumerator
{
	bool MoveNext();
	object Current { get; }
	void Reset();
}

internal class Countdown : IEnumerator
{
	int count = 11;
	public bool MoveNext () { return count-- > 0 ; }
	public object Current { get { return count; } }
	public void Reset() { throw new NotSupportedException(); }
}

IEnumerator e = new Countdown();
while (e.MoveNext())
	Console.Write (e.Current); // 109876543210
```	
	
### Extending an Interface	
```cs
public interface IUndoable { void Undo(); }
public interface IRedoable : IUndoable { void Redo(); }
```

### Explicit Interface Implementation
```cs
interface I1 { void Foo(); }
interface I2 { int Foo(); }

public class Widget : I1, I2
{
	public void Foo ()
	{
		Console.WriteLine ("Widget's implementation of I1.Foo");
	}
	
	int I2.Foo()
	{
		Console.WriteLine ("Widget's implementation of I2.Foo");
		return 42;
	}
}


Widget w = new Widget();
w.Foo(); // Widget's implementation of I1.Foo
((I1)w).Foo(); // Widget's implementation of I1.Foo
((I2)w).Foo(); // Widget's implementation of I2.Foo
```

### Implementing Interface Members Virtually
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
	public virtual void Undo()
	{
		Console.WriteLine ("TextBox.Undo");
	}

}

public class RichTextBox : TextBox
{
	public override void Undo()
	{
		Console.WriteLine ("RichTextBox.Undo");
	}
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo
((IUndoable)r).Undo(); // RichTextBox.Undo
((TextBox)r).Undo(); // RichTextBox.Undo
```

### Reimplementing an Interface in a Subclass
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
void IUndoable.Undo() { Console.WriteLine ("TextBox.Undo"); }
}
public class RichTextBox : TextBox, IUndoable
{
public new void Undo() { Console.WriteLine ("RichTextBox.Undo"); }
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo Case 2


public class TextBox : IUndoable
{
public void Undo() { Console.WriteLine ("TextBox.Undo"); }
}


RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo 				Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo 	Case 2
((TextBox)r).Undo(); // TextBox.Undo		Case 3
```

### Alternatives to interface reimplementation
```cs
public class TextBox : IUndoable
{
	void IUndoable.Undo() { Undo(); } // Calls method below
	protected virtual void Undo() { Console.WriteLine ("TextBox.Undo"); }
}

public class RichTextBox : TextBox
{
	protected override void Undo() { Console.WriteLine("RichTextBox.Undo"); }
}
```


## Access Modifiers 
```cs
namespace AccessModifiers
{
    class Modifiers
    {
		//Method AAA is not marked with any access modifier which automatically makes it private, that is the default.
		//Method BBB can access AAA but other class can't
        static void AAA()
        {
            Console.WriteLine("Modifiers AAA");
        }

        public static void BBB()
        {
            Console.WriteLine("Modifiers BBB");
            AAA();
        }
    }

     class Program
    {
        static void Main(string[] args)
        {
            Modifiers.BBB();
        }
    }
}
//Output
//Modifiers BBB
//Modifiers AAA

```   

```cs
class Program
{
	static void Main(string[] args)
	{
		Modifiers.AAA();
		Console.ReadKey();
	}
}
//Output
//'AccessModifiers.Modifiers.AAA()' is inaccessible due to its protection level

```


```cs
class Modifiers
{
	protected static void AAA()
	{
		Console.WriteLine("Modifiers AAA");
	}

	public static void BBB()
	{
		Console.WriteLine("Modifiers BBB");
		AAA();
	}
}
	

class Program
{
    static void Main(string[] args)
    {
        Modifiers.AAA();
        Console.ReadKey();
    }
}
//Output
'AccessModifiers.Modifiers.AAA()' is inaccessible due to its protection level	
```

### Modifiers in Inheritance
```cs
//Modifiers Base Class
class ModifiersBase
{
	static void AAA()
	{
		Console.WriteLine("ModifiersBase AAA");
	}
	public static void BBB()
	{
		Console.WriteLine("ModifiersBase BBB");
	}
	protected static void CCC()
	{
		Console.WriteLine("ModifiersBase CCC");
	}
}
	
//Modifiers Derive Class

class ModifiersDerived:ModifiersBase
{
    public static void XXX()
    {
        AAA();
        BBB();
        CCC();
    }
}

//Program Class
class Program
{
    static void Main(string[] args)
    {
        ModifiersDerived.XXX();
        Console.ReadKey();
    }
}
```


### Namespaces with Modifiers
```cs
public namespace AccessModifiers
{
    class Program
    {
        static void Main(string[] args)
        {

        }
    }
}

//Output
Compile time error: A namespace declaration cannot have modifiers or attributes
```


### Private Class
```cs
namespace ConsoleApplication2
{
    private class ModifiersBase
    {
        public static void BBB()
        {
            Console.WriteLine("ModifiersBase BBB");
        }
    }
}	

Output
Compile time error: Elements defined in a namespace cannot be explicitly declared as private, protected, or protected internal
```


### Internal Class and Public Method
```cs
namespace AccessModifiersLibrary
{
    internal class ClassA
    {
        public void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}

//Output
'AccessModifiersLibrary.ClassA' is inaccessible due to its protection level
The type 'AccessModifiersLibrary.ClassA' has no constructors defined
'AccessModifiersLibrary.ClassA' is inaccessible due to its protection level
'AccessModifiersLibrary.ClassA' does not contain a definition for 'MethodClassA' and
no extension method 'MethodClassA' accepting a first argument of type 'AccessModifiersLibrary.ClassA'
could be found (are you missing a using directive or an assembly reference?)
```


### Public Class and Private Method
```cs
AccessModifiersLibrary.ClassA:

namespace AccessModifiersLibrary
{
    public class ClassA
    {
        private void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}


//Output on compilation
'AccessModifiersLibrary.ClassA' does not contain a definition
for 'MethodClassA' and no extension method 'MethodClassA' accepting a first argument
of type 'AccessModifiersLibrary.ClassA' could be found (are you missing a using directive or an assembly reference?)
```


### Public Class and Internal Method
```cs
AccessModifiersLibrary.ClassA:

namespace AccessModifiersLibrary
{
    public class ClassA
    {
        Internal void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}

//Output on compilation
'AccessModifiersLibrary.ClassA' does not contain a definition for 'MethodClassA' and no extension
method 'MethodClassA' accepting a first argument of type 'AccessModifiersLibrary.ClassA' could be
found (are you missing a using directive or an assembly reference?)
```


### Protected Internal
```cs
namespace AccessModifiersLibrary
{
    public class ClassA
    {
        protected internal void MethodClassA()
        {

        }
    }

    public class ClassB:ClassA
    {
        protected internal void MethodClassB()
        {
            MethodClassA();
        }
    }

    public class ClassC
    {
        public void MethodClassC()
        {
            ClassA classA=new ClassA();
            classA.MethodClassA();
        }
    }
}



using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassC classC=new ClassC();
            classC.MethodClassC();
        }
    }
}

//Compiler output
The code successfully compiles with no error.
```


### Sealed Classes

```cs
namespace AccessModifiers
{
    sealed class AAA
    {
        public int x = 100;
        public void MethodA()
        {
            Console.WriteLine("Method A in sealed class");
        }
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            AAA aaa=new AAA();
            Console.WriteLine(aaa.x);
            aaa.MethodA();
            Console.ReadKey();
        }
    }
}
//Compiler Output
//100
//Method A in sealed class
```
	
	
```cs	
 namespace AccessModifiers
{
    sealed class AAA
    {

    }
    class BBB:AAA
    {

    }
    public class Program
    {
        public static void Main(string[] args)
        {
        }
    }
}

//Compiler Output
'AccessModifiers.BBB': cannot derive from sealed type 'AccessModifiers.AAA'	
```


### Constants
```cs
public class Program
 {
     private const int x = 100;
     public static void Main(string[] args)
     {
         Console.WriteLine(x);
         Console.ReadKey();
     }
 }
 Output
 100 
 ```
 
 ```cs
 namespace AccessModifiers
{
    public class Program
    {
        private const int x = y + 100;
        private const int y = z - 10;
        private const int z = 300;

        public static void Main(string[] args)
        {
           System.Console.WriteLine("{0} {1} {2}",x,y,z);
            Console.ReadKey();
        }
    }
}

Output
390 290 300
```

```cs
namespace AccessModifiers
{
    public class Program
    {
        private const int x = y + 100;
        private const int y = z - 10;
        private const int z = x;

        public static void Main(string[] args)
        {
           System.Console.WriteLine("{0} {1} {2}",x,y,z);
            Console.ReadKey();
        }
    }
}
Output
The evaluation of the constant value for 'AccessModifiers.Program.x' involves a circular definition
```

```cs
//A const is a variable whose value once assigned cannot be modified, but its value is determined at compile time only.
namespace AccessModifiers
{
    public class Program
    {
        public const ClassA classA=new ClassA();
        public static void Main(string[] args)
        {
        }
    }

   public class ClassA
    {

    }
}
//Output
Compile time error: 'AccessModifiers.Program.classA' is of type 'AccessModifiers.ClassA'.
A const field of a reference type other than string can only be initialized with null.
```

```cs
public class ClassA
    {
        public const int aaa = 10;
    }
	
	public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA=new ClassA();
            Console.WriteLine(classA.aaa);
            Console.ReadKey();
        }
    }

Output
Compile time error: Member 'AccessModifiers.ClassA.aaa'
cannot be accessed with an instance reference; qualify it with a type name instead 
```

```cs
//Just mark the const as static.
using System;
namespace AccessModifiers
{
    public class ClassA
    {
        public static const int aaa = 10;
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA=new ClassA();
            Console.WriteLine(classA.aaa);
            Console.ReadKey();
        }
    }
}

Output
Compile time error: The constant 'AccessModifiers.ClassA.aaa' cannot be marked static
```

```cs
namespace AccessModifiers
{
    public class ClassA
    {
        public const int xxx = 10;
    }

    public class ClassB:ClassA
    {
        public const int xxx = 100;
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine(ClassA.xxx);
            Console.WriteLine(ClassB.xxx);
            Console.ReadKey();
        }
    }
}
Output
10
100
Compiler Warning: 'AccessModifiers.ClassB.xxx' hides inherited
member 'AccessModifiers.ClassA.xxx'. Use the new keyword if hiding was intended.
```


## Static Fields
```cs
namespace AccessModifiers
{
    public class Program
    {
        private static int x;
        private static Boolean y;
        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.WriteLine(y);
            Console.ReadKey();
        }
    }
}

Output
0
False
```

```cs
namespace AccessModifiers
{
    public class Program
    {
         int x = y + 10;
         int y = x + 5;
        public static void Main(string[] args)
        {

        }
    }
}

Output
Compile time error:
A field initializer cannot reference the non-static field, method, or property 'AccessModifiers.Program.y'
A field initializer cannot reference the non-static field, method, or property 'AccessModifiers.Program.x'
```

### Readonly Fields
```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x = 100;

        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}

Output
100
```

```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x = 100;

        public static void Main(string[] args)
        {
            x = 200;
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}

Output
Compile time error: A static readonly field cannot be assigned to
(except in a static constructor or a variable initializer).
```


```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x;

        static Program()
        {
            x = 100;
            Console.WriteLine("Inside Constructor");
        }

        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}
Inside Constructor
100
```

```cs
namespace AccessModifiers
{
    public class ClassA
    {
        public int readonly x= 100;
    }
    public class Program
    {
      public static void Main(string[] args)
        {
        }
    }
}

Output
Compile time error:
Member modifier 'readonly' must precede the member type and name
Invalid token '=' in class, struct, or interface member declaration
```

# Methods
# Expressions and Operators
# Statements
# Structs
# Enumerations
```cs
namespace Enums
{
    class Program
    {
        static void Main(string[] args)
        {
			Console.WriteLine(Color.Yellow);		//Output: Yellow
			Console.WriteLine((int)Color.Yellow);	//Output: 0
        }
    }

    enum Color
    {
        Yellow,
        Blue,
        Brown,
        Green
    }
}
```

### Underlying Data type & Inheritance

```cs
static void Main(string[] args)
{
	Console.WriteLine((byte)Color.Yellow);	//Output: 0
	Console.WriteLine((byte)Color.Blue);	//Output: 1
}

enum Color:byte
{
	Yellow,
	Blue,
	Brown,
	Green
}


```


### Inheritance in Enum
By default, enum is a sealed class and therefore sticks to all the rules that a sealed class follows, so no class can derive from enum, i.e., a sealed type.
```cs
enum Shades:Color
{

}
//Output
//Compile time error: 'Enums.Derived': cannot derive from sealed type 'Enums.Color'
```

```cs
internal enum Color: System.Enum
{
	Yellow,
	Blue
}
//Output
//Compile time error: Type byte, sbyte, short, ushort, int, uint, long, or ulong expected.

```

### IComparable
```cs
internal enum Color
{
	Yellow,
	Blue,
	Green
}

private static void Main(string[] args)
{
	Console.WriteLine(Color.Yellow.CompareTo(Color.Blue));
	Console.WriteLine((byte)Color.Yellow);
	Console.ReadLine();
}
		
//Output -1
```

### IFormattable
```cs
internal enum Color
{
	Yellow,
	Blue,
	Green
}

private static void Main(string[] args)
{
	System.Console.WriteLine(Color.Format(typeof(Color), Color.Green, "X"));
	System.Console.WriteLine(Color.Format(typeof(Color), Color.Green, "d"));
	Console.ReadLine();
}
//Output		
00000002
2	

```
	
	
### IConvertible	
```cs

enum Color
{
	Yellow,
	Blue,
	Green
}
	
private static void Main(string[] args)
{
	string[] names;
	names = Color.GetNames(typeof (Color));
	foreach (var name in names)
	{
		Console.WriteLine(name);
	}
	Console.ReadLine();
}
		
```	
	
	
	
	
```cs
using System;
namespace Enums
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine((int)Color.Yellow);
            Console.WriteLine((int)Color.Blue);
            Console.WriteLine((int)Color.Brown);
            Console.WriteLine((int)Color.Green);
            Console.ReadLine();
        }
    }

    enum Color
    {
        Yellow =2,
        Blue,
        Brown=9,
        Green,
		Red = Yellow

    }
}
//Output
2
3
9
10

```	

```cs
class Program
    {
        static void Main(string[] args)
        {
            Color.Yellow = 3;
        }
    }

    enum Color
    {
        Yellow = 2,
        Blue
    }

//Output
Compile time error: The left-hand side of an assignment must be a variable, property or indexer
```


```cs
enum Color:byte
    {
        Yellow =300 ,
        Blue,
        Brown=9,
        Green,
    }
::Output
Compile time error: Constant value '300' cannot be converted to a 'byte'


```	

```cs
enum Color
{
	Yellow,
	Blue,
	Brown,
	Green,
	Blue
}
//Output
Compile time error: The type 'Enums.Color' already contains a definition for 'Blue'	
```

### Circular Dependency
```cs
internal enum Color
{
	Yellow=Blue,
	Blue
}

//Output
Compile time error: The evaluation of the constant value for 'Enums.Color.Yellow' involves a circular definition
```
	
###  Diving Deep

```cs
enum Color
{

}

Color color = (Color) -1;

::Output
Compile time error: 
To cast a negative value, you must enclose the value in parentheses
'Enums.Color' is a 'type' but is used like a 'variable'
```


```cs
enum Color
{
  value__
}
//Output
Compile time error: The enumerator name 'value__' is reserved and cannot be used

```	
	
# Arrays

```cs
char[] vowels = new char[5]; // Declare an array of 5 characters

vowels[0] = 'a';
vowels[1] = 'e';
vowels[2] = 'i';
vowels[3] = 'o';
vowels[4] = 'u';
Console.WriteLine (vowels[1]); // e


char[] vowels = new char[] {'a','e','i','o','u'};

//or simply:
char[] vowels = {'a','e','i','o','u'};

//Default Element Initialization
int[] a = new int[1000];
Console.Write (a[123]); // 0

//Multidimensional Arrays
int[,] matrix = new int[3,3];

for (int i = 0; i < matrix.GetLength(0); i++)
	for (int j = 0; j < matrix.GetLength(1); j++)
		matrix[i,j] = i * 3 + j;

//Simplified Array Initialization Expressions
int[,] matrix = new int[,]
{
	{0,1,2},
	{3,4,5},
	{6,7,8}
};

// Jagged arrays
int[][] matrix = new int[3][];

for (int i = 0; i < matrix.Length; i++)
{
	matrix[i] = new int[3]; // Create inner array
	for (int j = 0; j < matrix[i].Length; j++)
	matrix[i][j] = i * 3 + j;
}

//Simplified Array Initialization Expressions
int[][] matrix = new int[][]
{
	new int[] {0,1,2},
	new int[] {3,4,5},
	new int[] {6,7,8,9}
};
```
# Delegates
# Events
# Conversions
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

# Enumerators and Iterators
# Exceptions
# Preprocessor Directives
# Reflection and Attributes
# Dynamic Binding
# Disposal and Garbage Collection
# Serialization
# Application Domains
# Collections
# Lambda
# Asynchronous Programming
# Concurrency & Asynchrony
# Native and COM Interoperability
# Parallel Programming
# Advanced Threading
# Security
# Reflection and Metadata
# Networking
# Streams and I/O
# Diagnostics and Code Contracts

```cs
//Multiple-Variable Declarations
// Variable declarations--some with initializers, some without
int var3 = 7, var4, var5 = 3;
double var6, var7 = 6.52;
```

## Nullable Types
```cs
bool myBool = null;	//you'd get a compiler error.
DateTime myDate = null;	//you'd get a compiler error.

//these statements will compile just fine
bool? myNulableInt = null;
DateTime? myNullableDate = null;


//You can always convert a value type to a nullable type:
DateTime myDate = DateTime.Now;
DateTime? myNullableDate = myDate;

myDate = (DateTime) myNullableDate;


myDate = myNullableDate.Value;

```

## Class
### Declaring Classes & Creating Objects
```cs
public class Customer
{
    //Fields, properties, methods and events go here...
}

Customer object3 = new Customer();
Customer object4 = object3;

```


### Class Inheritance
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}

```cs
public class Employee
{

	//Constants
	//---------
	public const int months = 12, weeks = 52, days = 365;
	const double daysPerWeek = (double)days / (double)weeks;


	//Fields
	//---------
	// private field
	private DateTime date;

	// Instance field (Generally not recommended.)
	public string day;

	// static field 
	public static int NumberOfEmployees;
	
	public static volatile bool finished;
	
	//readonly readonly field
	public readonly int legs = 8, eyes = 2;



	//Property
	//---------
	private static int counter;
	private string name;


	// Auto-Impl Properties for trivial get and set
	public double TotalPurchases { get; set; }

	public abstract double Area
	{
		get;
		set;
	}

	// A read-write instance property:
	public string Name
	{
		get { return name; }
		set { name = value; }
	}

	// A read-only static property:
	public static int Counter
	{
		get { return counter; }
	}

	// A read-write instance property, with calculation
	private double seconds;
	public double Hours
	{
		get { return seconds / 3600; }
		set { seconds = value * 3600; }
	}


	// Public property exposes date field safely.
	public DateTime Date
	{
		get
		{
			return date;
		}
		set
		{
			// Set some reasonable boundaries for likely birth dates.
			if (value.Year > 1900 && value.Year <= DateTime.Today.Year)
			{
				date = value;
			}
			else
				throw new ArgumentOutOfRangeException();
		}

	}

	// Public method also exposes date field safely.
	// Example call: birthday.SetDate("1975, 6, 30");
	public void SetDate(string dateString)
	{
		DateTime dt = Convert.ToDateTime(dateString);

		// Set some reasonable boundaries for likely birth dates.
		if (dt.Year > 1900 && dt.Year <= DateTime.Today.Year)
		{
			date = dt;
		}
		else
			throw new ArgumentOutOfRangeException();
	}

	//Read only
	public TimeSpan GetTimeSpan(string dateString)
	{
		DateTime dt = Convert.ToDateTime(dateString);

		if (dt != null && dt.Ticks < date.Ticks)
		{
			return date - dt;
		}
		else
			throw new ArgumentOutOfRangeException();

	}

	public virtual int TestProperty
	{
		// Notice the accessor accessibility level.
		protected set { }

		// No access modifier is used here.
		get { return 0; }
	}
	
	
	
	
	// A Constructor:
	public Employee()
	{
		// Calculate the employee's number:
		counter = ++counter + NumberOfEmployees;
	}


	// protected method:
	protected void Pedal() { }

	// private field:
	private int wheels = 3;

	// protected internal property:
	protected internal int Wheels
	{
		get { return wheels; }
	}


	public override double GetTopSpeed()
	{
		return 108.4;
	}

}

public class Manager : Employee
{
	private string name;

	// Notice the use of the new modifier:
	public new string Name
	{
		get { return name; }
		set { name = value + ", Manager"; }
	}

	public double side;

	public override double Area
	{
		get
		{
			return side * side;
		}
		set
		{
			side = System.Math.Sqrt(value);
		}
	}

	public override int TestProperty
	{
		// Use the same accessibility level as in the overridden accessor.
		protected set { }

		// Cannot use access modifier here.
		get { return 0; }
	}
}


abstract class Motorcycle
{
	// Anyone can call this.
	public void StartEngine() {/* Method statements here */ }

	// Only derived classes can call this.
	protected void AddGas(int gallons) { /* Method statements here */ }

	// Derived classes can override the base class implementation.
	public virtual int Drive(int miles, int speed) { /* Method statements here */ return 1; }

	// Derived classes must implement this.
	public abstract double GetTopSpeed();
}


class TestEmployee
{
	static void Main()
	{
		
		Employee.NumberOfEmployees = 107;
		Employee e1 = new Employee();
		e1.Name = "Claude Vige";

		System.Console.WriteLine("Employee number: {0}", Employee.Counter);
		System.Console.WriteLine("Employee name: {0}", e1.Name);

		Manager m1 = new Manager();
		// Derived class property.
		m1.Name = "John";
		// Base class property.
		((Employee)m1).Name = "Mary";
	}
}
```


## Constructors 

```cs
public class Taxi
{
    public bool isInitialized;
    public Taxi()
    {
        isInitialized = true;
    }
}

class TestTaxi
{
    static void Main()
    {
        Taxi t = new Taxi();
        Console.WriteLine(t.isInitialized);
    }
}
```


### Prevent a class from being instantiated by making the constructor private, as follows:
```cs
class NLog
{
    // Private Constructor:
    private NLog() { }

    public static double e = Math.E;  //2.71828...
}
```


```cs
public class Employee
{
    public int salary;

    public Employee(int annualSalary)
    {
        salary = annualSalary;
    }

    public Employee(int weeklySalary, int numberOfWeeks)
    {
        salary = weeklySalary * numberOfWeeks;
    }
}

Employee e1 = new Employee(30000);
Employee e2 = new Employee(500, 52);
```


### A constructor can use the base keyword to call the constructor of a base class. 
```cs
public class Manager : Employee
{
    public Manager(int annualSalary)
        : base(annualSalary)
    {
        //Add further instructions here.
    }
}
```


```cs
public Employee(int weeklySalary, int numberOfWeeks)
    : this(weeklySalary * numberOfWeeks)
{
}
```


## Destructors 

### a declaration of a destructor for the class Car:
```csclass Car
{
    ~Car()  // destructor
    {
        // cleanup statements...
    }
}
```

### The destructor implicitly calls Finalize on the base class of the object. 
```cs
protected override void Finalize()
{
    try
    {
        // Cleanup statements...
    }
    finally
    {
        base.Finalize();
    }
}
```

### creates three classes that make a chain of inheritance
```cs
class First
{
    ~First()
    {
        System.Diagnostics.Trace.WriteLine("First's destructor is called.");
    }
}

class Second : First
{
    ~Second()
    {
        System.Diagnostics.Trace.WriteLine("Second's destructor is called.");
    }
}

class Third : Second
{
    ~Third()
    {
        System.Diagnostics.Trace.WriteLine("Third's destructor is called.");
    }
}

class TestDestructors
{
    static void Main()
    {
        Third t = new Third();
    }

}
/* Output (to VS Output Window):
    Third's destructor is called.
    Second's destructor is called.
    First's destructor is called.
*/
```



## Object and Collection Initializers
```cs
class Cat
{
    // Auto-implemented properties.
    public int Age { get; set; }
    public string Name { get; set; }
}

Cat cat = new Cat { Age = 10, Name = "Fluffy" };
```

### Object Initializers with anonymous types
```cs
var pet = new { Age = 10, Name = "Fluffy" };

var productInfos =
    from p in products
    select new { p.ProductName, p.UnitPrice };
```	

### Object initializers with nullable types	
```cs
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };

List<Cat> moreCats = new List<Cat>
{
    new Cat(){ Name = "Furrytail", Age=5 },
    new Cat(){ Name = "Peaches", Age=4 },
    null
};
```


### Access a Collection Class with foreach
```cs
Tokens f = new Tokens("This is a sample sentence.", new char[] {' ','-'});

// Display the tokens.
foreach (string item in f)
{
    System.Console.WriteLine(item);
}
```

## Nested Types
```cs
class Container
{
    class Nested
    {
        Nested() { }
    }
}
```

## Partial Classes and Methods
```cs
public partial class Employee
{
    public void DoWork()
    {
    }
}

public partial class Employee
{
    public void GoToLunch()
    {
    }
}
```

### At compile time, attributes of partial-type definitions are merged.
```cs
[SerializableAttribute]
partial class Moon { }

[ObsoleteAttribute]
partial class Moon { }
```

//For example, consider the following declarations:
```cs
partial class Earth : Planet, IRotate { }
partial class Earth : IRevolve { }

//They are equivalent to the following declarations:
class Earth : Planet, IRotate, IRevolve { }

### Partial Methods

```cs
// Definition in file1.cs
partial void onNameChanged();

// Implementation in file2.cs
partial void onNameChanged()
{
  // method body
}
```

## Anonymous Types

```cs
var v = new { Amount = 108, Message = "Hello" };

// Rest the mouse pointer over v.Amount and v.Message in the following
// statement to verify that their inferred types are int and string.
Console.WriteLine(v.Amount + v.Message);
```

```cs
var productQuery = 
    from prod in products
    select new { prod.Color, prod.Price };

foreach (var v in productQuery)
{
    Console.WriteLine("Color={0}, Price={1}", v.Color, v.Price);
}
```

```cs
var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = "grape", diam = 1 }};
```



## Polymorphism
```cs
public class Shape
{
    // A few example members
    public int X { get; private set; }
    public int Y { get; private set; }
    public int Height { get; set; }
    public int Width { get; set; }

    // Virtual method
    public virtual void Draw()
    {
        Console.WriteLine("Performing base class drawing tasks");
    }
}

class Circle : Shape
{
    public override void Draw()
    {
        // Code to draw a circle...
        Console.WriteLine("Drawing a circle");
        base.Draw();
    }
}
class Rectangle : Shape
{
    public override void Draw()
    {
        // Code to draw a rectangle...
        Console.WriteLine("Drawing a rectangle");
        base.Draw();
    }
}
class Triangle : Shape
{
    public override void Draw()
    {
        // Code to draw a triangle...
        Console.WriteLine("Drawing a triangle");
        base.Draw();
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Polymorphism at work #1: a Rectangle, Triangle and Circle
        // can all be used whereever a Shape is expected. No cast is
        // required because an implicit conversion exists from a derived 
        // class to its base class.
        System.Collections.Generic.List<Shape> shapes = new System.Collections.Generic.List<Shape>();
        shapes.Add(new Rectangle());
        shapes.Add(new Triangle());
        shapes.Add(new Circle());

        // Polymorphism at work #2: the virtual method Draw is
        // invoked on each of the derived classes, not the base class.
        foreach (Shape s in shapes)
        {
            s.Draw();
        }

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }

}

/* Output:
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
 */
 ```
 
### Virtual Members
```cs
public class BaseClass
{
    public virtual void DoWork() { }
    public virtual int WorkProperty
    {
        get { return 0; }
    }
}
public class DerivedClass : BaseClass
{
    public override void DoWork() { }
    public override int WorkProperty
    {
        get { return 0; }
    }
}

DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = (BaseClass)B;
A.DoWork();  // Also calls the new method.

```

### Hiding Base Class Members with New Members
```cs
public class BaseClass
{
    public void DoWork() { WorkField++; }
    public int WorkField;
    public int WorkProperty
    {
        get { return 0; }
    }
}

public class DerivedClass : BaseClass
{
    public new void DoWork() { WorkField++; }
    public new int WorkField;
    public new int WorkProperty
    {
        get { return 0; }
    }
}


DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = (BaseClass)B;
A.DoWork();  // Calls the old method.

```

### Preventing Derived Classes from Overriding Virtual Members
```cs
public class A
{
    public virtual void DoWork() { }
}
public class B : A
{
    public override void DoWork() { }
}

public class C : B
{
    public sealed override void DoWork() { }
}

public class D : C
{
    public new void DoWork() { }
}
```
### Accessing Base Class Virtual Members from Derived Classes
```cs
public class Base
{
    public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
    public override void DoWork()
    {
        //Perform Derived's work here
        //...
        // Call DoWork on base class
        base.DoWork();
    }
}
```


### Versioning with the Override and New Keywords
```cs

class GraphicsClass
{
    public virtual void DrawLine() { }
    public virtual void DrawPoint() { }
    public virtual void DrawRectangle() { }
}


class YourDerivedGraphicsClass : GraphicsClass
{
    public override void DrawRectangle() { }
}


base.DrawRectangle();


class YourDerivedGraphicsClass : GraphicsClass
{
    public new void DrawRectangle() { }
}


```

### Override and Method Selection
```cs
public class Derived : Base
{
    public override void DoWork(int param) { }
    public void DoWork(double param) { }
}

int val = 5;
Derived d = new Derived();
d.DoWork(val);  // Calls DoWork(double).

((Base)d).DoWork(val);  // Calls DoWork(int) on Derived.

```



```cs
// Define the base class, Car. The class defines two methods,
// DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each derived
// class also defines a ShowDetails method. The example tests which version of
// ShowDetails is selected, the base class method or the derived class method.
class Car
{
    public void DescribeCar()
    {
        System.Console.WriteLine("Four wheels and an engine.");
        ShowDetails();
    }

    public virtual void ShowDetails()
    {
        System.Console.WriteLine("Standard transportation.");
    }
}

// Define the derived classes.

// Class ConvertibleCar uses the new modifier to acknowledge that ShowDetails
// hides the base class method.
class ConvertibleCar : Car
{
    public new void ShowDetails()
    {
        System.Console.WriteLine("A roof that opens up.");
    }
}

// Class Minivan uses the override modifier to specify that ShowDetails
// extends the base class method.
class Minivan : Car
{
    public override void ShowDetails()
    {
        System.Console.WriteLine("Carries seven people.");
    }
}
```


## Abstract and Sealed Classes and Class Members

### Abstract Classes and Class Members
```cs

public abstract class A
{
    public abstract void DoWork(int i);
}

```



```cs
public class D
{
    public virtual void DoWork(int i)
    {
        // Original implementation.
    }
}

public abstract class E : D
{
    public abstract override void DoWork(int i);
}

public class F : E
{
    public override void DoWork(int i)
    {
        // New implementation.
    }
}
```


### Sealed Classes and Class Members
```cs
public sealed class D
{
    // Class members here.
}

public class D : C
{
    public sealed override void DoWork() { }
}

```

## Static Classes and Static Class Members
```cs
UtilityClass.MethodA();

```


### Static Members

```cs

public static class TemperatureConverter
{
    public static double CelsiusToFahrenheit(string temperatureCelsius)
    {
        return (temperatureCelsius * 9 / 5) + 32;;
    }

    public static double FahrenheitToCelsius(string temperatureFahrenheit)
    {
        return (fahrenheit - 32) * 5 / 9;;
    }
}

class TestTemperatureConverter
{
    static void Main()
    {
		double F, C = 0;
		F = TemperatureConverter.CelsiusToFahrenheit(Console.ReadLine());
        Console.WriteLine("Temperature in Fahrenheit: {0:F2}", F);
		
        C = TemperatureConverter.FahrenheitToCelsius(Console.ReadLine());
        Console.WriteLine("Temperature in Celsius: {0:F2}", C);
    }
}

```

```cs
public class Automobile
{
    public static int NumberOfWheels = 4;
    public static int SizeOfGasTank
    {
        get
        {
            return 15;
        }
    }
    public static void Drive() { }
    public static event EventType RunOutOfGas;

    // Other non-static fields and properties...
}

Automobile.Drive();
int i = Automobile.NumberOfWheels;

```

## Enumeration Types

```cs
enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };
enum Months : byte { Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec }; 
enum Days {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
enum Days : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
enum Range : long { Max = 2147483648L, Min = 255L };

Days today = Days.Monday;
int dayNumber =(int)today;
Console.WriteLine("{0} is day number #{1}.", today, dayNumber);

Months thisMonth = Months.Dec;
byte monthNumber = (byte)thisMonth;
Console.WriteLine("{0} is month number #{1}.", thisMonth, monthNumber);

// Output:
// Monday is day number #1.
// Dec is month number #11.


public class EnumTest
{
    enum Days { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        int x = (int)Days.Sun;
        int y = (int)Days.Fri;
        Console.WriteLine("Sun = {0}", x);
        Console.WriteLine("Fri = {0}", y);
    }
}
```


```cs
enum MachineState
{
    PowerOff = 0,
    Running = 5,
    Sleeping = 10,
    Hibernating = Sleeping + 5
}
```

### Enumeration Types as Bit Flags

```cs
[Flags]
enum Days2
{
    None = 0x0,
    Sunday = 0x1,
    Monday = 0x2,
    Tuesday = 0x4,
    Wednesday = 0x8,
    Thursday = 0x10,
    Friday = 0x20,
    Saturday = 0x40
}
class MyClass
{
    Days2 meetingDays = Days2.Tuesday | Days2.Thursday;
}


// Initialize with two flags using bitwise OR.
meetingDays = Days2.Tuesday | Days2.Thursday;

// Set an additional flag using bitwise OR.
meetingDays = meetingDays | Days2.Friday;

Console.WriteLine("Meeting days are {0}", meetingDays);
// Output: Meeting days are Tuesday, Thursday, Friday

// Remove a flag using bitwise XOR.
meetingDays = meetingDays ^ Days2.Tuesday;
Console.WriteLine("Meeting days are {0}", meetingDays);
// Output: Meeting days are Thursday, Friday

// Test value of flags using bitwise AND.
bool test = (meetingDays & Days2.Thursday) == Days2.Thursday;
Console.WriteLine("Thursday {0} a meeting day.", test == true ? "is" : "is not");
```

### Using the System.Enum Methods to Discover and Manipulate Enum Values
```cs
string s = Enum.GetName(typeof(Days), 4);
Console.WriteLine(s);

Console.WriteLine("The values of the Days Enum are:");
foreach (int i in Enum.GetValues(typeof(Days)))
    Console.WriteLine(i);

Console.WriteLine("The names of the Days Enum are:");
foreach (string str in Enum.GetNames(typeof(Days)))
    Console.WriteLine(str);
```	

## Indexers 
```cs
class SampleCollection<T>
{
    // Declare an array to store the data elements.
    private T[] arr = new T[100];

    // Define the indexer, which will allow client code
    // to use [] notation on the class instance itself.
    // (See line 2 of code in Main below.)        
    public T this[int i]
    {
        get
        {
            // This indexer is very simple, and just returns or sets
            // the corresponding element from the internal array.
            return arr[i];
        }
        set
        {
            arr[i] = value;
        }
    }
}

// This class shows how client code uses the indexer.
class Program
{
    static void Main(string[] args)
    {
        // Declare an instance of the SampleCollection type.
        SampleCollection<string> stringCollection = new SampleCollection<string>();

        // Use [] notation on the type.
        stringCollection[0] = "Hello, World";
        System.Console.WriteLine(stringCollection[0]);
    }
}
// Output:
// Hello, World.
```


## Delegates

### very basic Delegate
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

### Calling Static Functions
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

### Multicasting
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

## Events

### Simple Event
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


### The Second Change Event Example
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


### Partial Types
```cs
// PaymentFormGen.cs - auto-generated
partial class PaymentForm { ... }

// PaymentForm.cs - hand-authored
partial class PaymentForm { ... }


//Each participant must have the partial declaration; the following is illegal:
partial class PaymentForm {}
class PaymentForm {}

//There are two ways to specify a base class with partial classes:
//• Specify the (same) base class on each participant. For example:
partial class PaymentForm : ModalForm {}
partial class PaymentForm : ModalForm {}

//• Specify the base class on just one participant. For example:
partial class PaymentForm : ModalForm {}
partial class PaymentForm {}
```

### URL
* [2,000 Things You Should Know About C#](https://csharp.2000things.com/index/)
* [Introduction to Object Oriented Programming Concepts ](http://www.codeproject.com/Articles/22769/Introduction-to-Object-Oriented-Programming-Concep)




# Collection

## List<T>
```cs
//To create a list:
var list = new List<int>();

// Creating a list with an initial size
var list = new List<int>(10000);

// Add an item at the end of the list
list.Add(4);
 
// Add an item at index 0
list.Insert(4, 0);
 
// Remove an item from list
list.Remove(1);
 
// Remove the item at index 0
list.RemoveAt(0);
 
// Return the item at index 0
var first = list[0];
 
// Return the index of an item
var index = list.IndexOf(4);
 
// Check to see if the list contains an item
var contains = list.Contains(4);
 
// Return the number of items in the list 
var count = list.Count;
 
// Iterate over all objects in a list
foreach (var item in list)
    Console.WriteLine(item);
	

// Create a list of strings.
var salmons = new List<string>();
salmons.Add("chinook");
salmons.Add("coho");
salmons.Add("pink");
salmons.Add("sockeye");


// Create a list of strings by using a collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };


// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");	// Output: chinook coho pink sockeye
}


// Iterate through the list by index.
for (var index = 0; index < salmons.Count; index++)
{
    Console.Write(salmons[index] + " ");	// Output: chinook coho pink sockeye
}


// Remove an element from the list by specifying the object.
salmons.Remove("coho");





### A lambda expression is placed in the ForEach



var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Remove odd numbers.
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        // Remove the element by specifying
        // the zero-based index in the list.
        numbers.RemoveAt(index);
    }
}

// Iterate through the list.
// A lambda expression is placed in the ForEach method
// of the List(T) object.
numbers.ForEach(
    number => Console.Write(number + " "));
// Output: 0 2 4 6 8



###  List<T>
private static void IterateThroughList()
{
    var theGalaxies = new List<Galaxy>
        {
            new Galaxy() { Name="Tadpole", MegaLightYears=400},
            new Galaxy() { Name="Pinwheel", MegaLightYears=25},
            new Galaxy() { Name="Milky Way", MegaLightYears=0},
            new Galaxy() { Name="Andromeda", MegaLightYears=3}
        };

    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);
    }

    // Output:
    //  Tadpole  400
    //  Pinwheel  25
    //  Milky Way  0
    //  Andromeda  3
}

public class Galaxy
{
    public string Name { get; set; }
    public int MegaLightYears { get; set; }
}
```

## Dictionary<TKey, TValue>
```cs
var dictionary = new Dictionary<int, Customer>();

dictionary.Add(customer.Id, customer);

var dictionary = new Dictionary<int, Customer>
{
     { customer1.Id, customer1 },
     { customer2.Id, customer2 }
}


// Return the customer with ID 1234 
var customer = dictionary[1234];

// Removing an object by its key
dictionary.Remove(1);
 
// Removing all objects
dictionary.Clear();

var count = dictionary.Count; 
 
var containsKey = dictionary.ContainsKey(1);
 
var containsValue = dictionary.ContainsValue(customer1);
 
// Iterate over keys 
foreach (var key in dictionary.Keys)
     Console.WriteLine(dictionary[key]);
 
// Iterate over values
foreach (var value in dictionary.Values)
     Console.WriteLine(value);
 
// Iterate over dictionary
foreach (var keyValuePair in dictionary)
{
     Console.WriteLine(keyValuePair.Key);
     Console.WriteLine(keyValuePair.Value);
}
```

## HashSet<T>
```cs
var hashSet = new HashSet<int>();


// Initialize the set using object initialization syntax 
var hashSet = new HashSet<int>() { 1, 2, 3 };
 
// Add an object to the set
hashSet.Add(4);
 
// Remove an object 
hashSet.Remove(3);
 
// Remove all objects 
hashSet.Clear();
 
// Check to see if the set contains an object 
var contains = hashSet.Contains(1);
 
// Return the number of objects in the set 
var count = hashSet.Count;

// Modify the set to include only the objects present in the set and the other set
hashSet.IntersectWith(another);
 
// Remove all objects in "another" set from "hashSet" 
hashSet.ExceptWith(another);
 
// Modify the set to include all objects included in itself, in "another" set, or both
hashSet.UnionWith(another);
 
var isSupersetOf = hashSet.IsSupersetOf(another);
var isSubsetOf = hashSet.IsSubsetOf(another);
var equals = hashSet.SetEquals(another);
```


## Stack<T>
```cs
var stack = new Stack<string>();
             
// Push items in a stack
stack.Push("http://www.google.com");
 
// Check to see if the stack contains a given item 
var contains = stack.Contains("http://www.google.com");
 
// Remove and return the item on the top of the stack
var top = stack.Pop();
 
// Return the item on the top of the stack without removing it 
var top = stack.Peek();
 
// Get the number of items in stack 
var count = stack.Count;
 
// Remove all items from stack 
stack.Clear();

## Queue<T>
var queue = new Queue<string>();
 
// Add an item to the queue
queue.Enqueue("transaction1");
 
// Check to see if the queue contains a given item 
var contains = queue.Contains("transaction1");
 
// Remove and return the item on the front of the queue
var front = queue.Dequeue();
 
// Return the item on the front without removing it 
var top = queue.Peek();
             
// Remove all items from queue 
queue.Clear();
 
// Get the number of items in the queue
var count = queue.Count;
```

### Hashtable
Hashtable hashList = new Hashtable();
hashList.Add(1, "item#1");
hashList.Add(2, "item#2");
hashList.Add(3, "item#3");

bool result = hashList.IsFixedSize; // false

bool result = hashList.IsReadOnly;

//Keys - It returns ICollection object containing keys of the IDictionary object.
ICollection keys = hashList.Keys;

string[] strKeys = new string[keys.Count];
int index =0;
foreach (int key in keys)
{
   strKeys[index++] = key.ToString();
}

string keysList = string.Join(", ",strKeys); // 3, 2, 1

//Values - It returns ICollection object containing values of the IDictionary object.

ICollection values = hashList.Values;

string[] strValues = new string[values.Count];
int index = 0;
foreach (string value in values)
{
   strValues[index++] = value;
}

string valueList = string.Join(", ", strValues); //item#1, item#2, item#3

hashList.Clear(); // it removes all item from the list.

bool result = hashList.Contains(1); // true


IDictionaryEnumerator dicEnum = hashList.GetEnumerator();

string items = string.Empty;
while (dicEnum.MoveNext())
{

   items += string.Format("{0} : {1}\n", dicEnum.Key, dicEnum.Value);
}

MessageBox.Show(items);

hashList.Remove(2); // remove item which has 2 key


### ArrayList

ArrayList arrayList = new ArrayList();
bool isFixedSize = arrayList.IsFixedSize; // false, because ArrayList is not fixed size list


ArrayList arrayList = new ArrayList();
arrayList.Add(1);
arrayList.Add(2);
arrayList.Add(3);

bool readOnly = arrayList.IsReadOnly; // false, because default array list is not readonly.

// create readonly list from existing list
ArrayList readOnlyList = ArrayList.ReadOnly(arrayList);

bool isNewListReadOnly = readOnlyList.IsReadOnly; // true. now user can't modify this list
												  
arrayList.Clear() 


int itemsCount = arrayList.Count; // 3


//Contains
Person person1 = new Person(1, "test");
Person person2 = new Person(2, "test2");

bool result1 = arrayList.Contains(person1); // true
bool result2 = arrayList.Contains(person2); // false

int result1 = arrayList.IndexOf(person3); // 2,
int result2 = arrayList.IndexOf(person4); // -1. because it does not exist in list
										  
// insert item at index 2.
arrayList.Insert(2, person);

arrayList.Remove(person); // it will remove 2nd item. it will call Equals method to object to find in list.

arrayList.RemoveAt(1); // remove item at index 1




http://cc.davelozinski.com/c-sharp/fastest-collection-for-string-lookups
