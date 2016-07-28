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

# Statements
# Expressions and Operators
# Method
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
# Conversions
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
# Exception Handling
# Structs
# Namespaces

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
# Collection
# Enumerators and Iterators
# Preprocessor Directives
# File I/O
# Regular Expressions
