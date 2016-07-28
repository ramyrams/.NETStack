[C# Language Basics]

* [Types, Storage, and Variables](#Types, Storage, and Variables)
* [Statements](#Statements)
* [Expressions and Operators](#Expressions and Operators)
* [Method](#Method)
* [Arrays](#Arrays)
* [Conversions](#Conversions)
* [Enumerations](#Enumerations)
* [Exception Handling](#Exception Handling)
* [Structs](#Structs)
* [Namespaces](#Namespaces)
* [Collection](#Collection)
* [Enumerators and Iterators](#Enumerators and Iterators)
* [Preprocessor Directives](#Preprocessor Directives)
* [File I/O](#File I/O)
* [Regular Expressions](#Regular Expressions)
* 
# Types, Storage, and Variables


```cs
int a = 5;             
int b = a + 2; //OK

bool test = true;

// Error. Operator '+' cannot be applied to operands of type 'int' and 'bool'.
int c = a + test;
```

```cs
// Declaration only:
float temperature;
string name;
MyClass myClass;

// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3; //var is just shorthand not new type
int[] source = { 0, 1, 2, 3, 4, 5 };
var query = from item in source
            where item <= limit
            select item;
```		


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


int? aaa = null;
Console.WriteLine(aaa.HasValue);
aaa = 1;
Console.WriteLine(aaa.HasValue);
Console.WriteLine(aaaram.Value);


```


## Generic Types
```cs
List<string> strings = new List<string>();
```	


## Implicit Types
```cs
// i is compiled as an int
var i = 5;

// s is compiled as a string
var s = "Hello";

// a is compiled as int[]
var a = new[] { 0, 1, 2 };

// expr is compiled as IEnumerable<Customer>
// or perhaps IQueryable<Customer>
var expr =
    from c in customers
    where c.City == "London"
    select c;

// anon is compiled as an anonymous type
var anon = new { Name = "Terry", Age = 34 };

// list is compiled as List<int>                             
var list = new List<int>();
```	

## Anonymous Types
```cs
var v = new { Amount = 108, Message = "Hello" };
Console.WriteLine(v.Amount + v.Message);


var productQuery = 
    from prod in products
    select new { prod.Color, prod.Price };
	

var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = "grape", diam = 1 }};
```	

```cs
// Get the type of a specified class.
Type myType1 = Type.GetType("System.Int32");
Console.WriteLine("The full name is {0}.\n", myType1.FullName);
//Output: 
The full name is System.Int32.

// Since NoneSuch does not exist in this assembly, GetType throws a TypeLoadException.
Type myType2 = Type.GetType("NoneSuch", true);
Console.WriteLine("The full name is {0}.", myType2.FullName);
//Output: 
TypeLoadException


object[] values = { "word", true, 120, 136.34, 'a' };
foreach (var value in values)
 Console.WriteLine("{0} - type {1}", value, 
				   value.GetType().Name);
// The example displays the following output:
//       word - type String
//       True - type Boolean
//       120 - type Int32
//       136.34 - type Double
//       a - type Char				   
				   
```


```cs
Class Program
{
static void Main()
{
	// Use type variables.
	// ... Then pass the variables as an argument.
	Type type1 = typeof(string[]);
	Type type2 = "string".GetType();
	Type type3 = typeof(Type);

	Test(type1);
	Test(type2);
	Test(type3);
}

static void Test(Type type)
{
	// Print some properties of the Type formal parameter.
	Console.WriteLine("IsArray: {0}", type.IsArray);
	Console.WriteLine("Name: {0}", type.Name);
	Console.WriteLine("IsSealed: {0}", type.IsSealed);
	Console.WriteLine("BaseType.Name: {0}", type.BaseType.Name);
	Console.WriteLine();
}

Output
IsArray: True
Name: String[]
IsSealed: True
BaseType.Name: Array

IsArray: False
Name: String
IsSealed: True
BaseType.Name: Object

IsArray: False
Name: Type
IsSealed: False
BaseType.Name: MemberInfo
```

```cs
Type t = typeof(String);

MethodInfo substr = t.GetMethod("Substring", new Type[] { typeof(int), typeof(int) });

Object result =  substr.Invoke("Hello, World!", new Object[] { 7, 5 });
Console.WriteLine("{0} returned \"{1}\".", substr, result);
```


# Statements
# Expressions and Operators
# Method
# Arrays


## Arrays in General
```cs
// declare numbers as an int array of any size
int[] numbers; 

// Declare a single-dimensional array 
int[] array1 = new int[5];

// Declare and set array element values
int[] array2 = new int[] { 1, 3, 5, 7, 9 };

// Alternative syntax
int[] array3 = { 1, 2, 3, 4, 5, 6 };

// Declare a two dimensional array
int[,] multiDimensionalArray1 = new int[2, 3];

// Declare and set array element values
int[,] multiDimensionalArray2 = { { 1, 2, 3 }, { 4, 5, 6 } };

// Declare a jagged array
int[][] jaggedArray = new int[6][];

// Set the values of the first array in the jagged array structure
jaggedArray[0] = new int[4] { 1, 2, 3, 4 };
```




## Arrays as Objects
```cs
int[] numbers = { 1, 2, 3, 4, 5 };
int lengthOfNumbers = numbers.Length;

// Declare and initialize an array:
int[,] theArray = new int[5, 10];
System.Console.WriteLine("The array has {0} dimensions.", theArray.Rank);
		
		
Single-Dimensional Arrays
//declare a single-dimensional array of five integers
int[] array = new int[5];

//Array Initialization
int[] array1 = new int[] { 1, 3, 5, 7, 9 };
string[] weekDays = { "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat" };

//It is possible to declare an array variable without initialization, but you must use the new operator when you assign an array to this variable.
int[] array3;
array3 = new int[] { 1, 3, 5, 7, 9 };   // OK
//array3 = {1, 3, 5, 7, 9};   // Error

//Value Type and Reference Type Arrays
SomeType[] array4 = new SomeType[10];
```


## Multidimensional Arrays
```cs
//Arrays can have more than one dimension.
int[,] array = new int[4, 2];

//creates an array of three dimensions, 4, 2, and 3.
int[, ,] array1 = new int[4, 2, 3];

//Array Initialization
// Two-dimensional array.
int[,] array2D = new int[,] { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } };
// The same array with dimensions specified.
int[,] array2Da = new int[4, 2] { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } };
// A similar array with string elements.
string[,] array2Db = new string[3, 2] { { "one", "two" }, { "three", "four" },
                                        { "five", "six" } };

// Three-dimensional array.
int[, ,] array3D = new int[,,] { { { 1, 2, 3 }, { 4, 5, 6 } }, 
                                 { { 7, 8, 9 }, { 10, 11, 12 } } };
// The same array with dimensions specified.
int[, ,] array3Da = new int[2, 2, 3] { { { 1, 2, 3 }, { 4, 5, 6 } }, 
                                       { { 7, 8, 9 }, { 10, 11, 12 } } };
									   
// initialize the array without specifying the rank.
int[,] array4 = { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } };

// assigns a value to a particular array element.
array5[2, 1] = 25;

//gets the value of a particular array element and assigns it to variable elementValue.
int elementValue = array5[2, 1];

//initializes the array elements to default values (except for jagged arrays).
int[,] array6 = new int[10, 10];
```

## Jagged Arrays
```cs
// single-dimensional array that has three elements
int[][] jaggedArray = new int[3][];

//Before you can use jaggedArray, its elements must be initialized. You can initialize the elements like this:
jaggedArray[0] = new int[5];
jaggedArray[1] = new int[4];
jaggedArray[2] = new int[2];


//It is also possible to use initializers to fill the array elements with values
jaggedArray[0] = new int[] { 1, 3, 5, 7, 9 };
jaggedArray[1] = new int[] { 0, 2, 4, 6 };
jaggedArray[2] = new int[] { 11, 22 };

//initialize the array upon declaration l
int[][] jaggedArray2 = new int[][] 
{
    new int[] {1,3,5,7,9},
    new int[] {0,2,4,6},
    new int[] {11,22}
};

//Notice that you cannot omit the new operator from the elements initialization because there is no default initialization for the elements
int[][] jaggedArray3 = 
{
    new int[] {1,3,5,7,9},
    new int[] {0,2,4,6},
    new int[] {11,22}
};

// Assign 77 to the second element ([1]) of the first array ([0]):
jaggedArray3[0][1] = 77;

// Assign 88 to the second element ([1]) of the third array ([2]):
jaggedArray3[2][1] = 88;


int[][,] jaggedArray4 = new int[3][,] 
{
    new int[,] { {1,3}, {5,7} },
    new int[,] { {0,2}, {4,6}, {8,10} },
    new int[,] { {11,22}, {99,88}, {0,9} } 
};

//access individual elements, which displays the value of the element [1,0] of the first array (value 5)
System.Console.Write("{0}", jaggedArray4[0][1, 0]);

//The method Length returns the number of arrays contained in the jagged array.
System.Console.WriteLine(jaggedArray4.Length);


## Using foreach with Arrays
int[] numbers = { 4, 5, 6, 1, 2, 3, -2, -1, 0 };
foreach (int i in numbers)
{
    System.Console.Write("{0} ", i);
}
// Output: 4 5 6 1 2 3 -2 -1 0

//With multidimensional arrays, you can use the same method to iterate through the elements
int[,] numbers2D = new int[3, 2] { { 9, 99 }, { 3, 33 }, { 5, 55 } };
// Or use the short form:
// int[,] numbers2D = { { 9, 99 }, { 3, 33 }, { 5, 55 } };

foreach (int i in numbers2D)
{
    System.Console.Write("{0} ", i);
}
// Output: 9 99 3 33 5 55
```

## Passing Arrays as Arguments
```cs
### Passing Single-Dimensional Arrays As Arguments
//pass an initialized single-dimensional array to a method
int[] theArray = { 1, 3, 5, 7, 9 };
PrintArray(theArray);

//a partial implementation of the print method.
void PrintArray(int[] arr)
{
    // Method code.
}

//initialize and pass a new array in one step
PrintArray(new int[] { 1, 3, 5, 7, 9 });

### Passing Multidimensional Arrays As Arguments

int[,] theArray = { { 1, 2 }, { 2, 3 }, { 3, 4 } };
Print2DArray(theArray);

void Print2DArray(int[,] arr)
{
    // Method code.
}

Print2DArray(new int[,] { { 1, 2 }, { 3, 4 }, { 5, 6 }, { 7, 8 } });


## Passing Arrays Using ref and out
```cs
static void TestMethod1(out int[] arr)
{
    arr = new int[10];   // definite assignment of arr
}

static void TestMethod2(ref int[] arr)
{
    arr = new int[10];   // arr initialized to a different array
}
```


## Implicitly Typed Arrays
```cs
var a = new[] { 1, 10, 100, 1000 }; // int[]
var b = new[] { "hello", null, "world" }; // string[]

// single-dimension jagged array
var c = new[]   
{  
    new[]{1,2,3,4},
    new[]{5,6,7,8}
};

// jagged array of strings
var d = new[]   
{
    new[]{"Luca", "Mads", "Luke", "Dinesh"},
    new[]{"Karen", "Suma", "Frances"}
};


var contacts = new[] 
{
    new {
            Name = " Eugene Zabokritski",
            PhoneNumbers = new[] { "206-555-0108", "425-555-0001" }
        },
    new {
            Name = " Hanying Feng",
            PhoneNumbers = new[] { "650-555-0199" }
        }
};
```

# Conversions
# Enumerations

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

```cs
static void Main()
{
	int x = 10, y = 0;
	x /= y; // Attempt to divide by zero--raises an exception
}

Unhandled Exception: System.DivideByZeroException: Attempted to divide by zero.
at Exceptions_1.Program.Main() in C:\Progs\Exceptions\Program.cs:line 12
```

```cs
try
{
	myObj.Property1 = value;
}
catch(CarIsDeadException e)
{
	// Process CarIsDeadException.
}
catch(ArgumentOutOfRangeException e)
{
	// Process ArgumentOutOfRangeException.
}

catch (InvalidOperationException)
{
	// Use the "throw" keyword to raise an exception. 
	throw new Exception(string.Format("{0} has overheated!", PetName));
}
catch (OverflowException oe)
{
	// Record the fact that the overflow exception occurred.
	EventLog.WriteEntry("MyApplication", oe.Message, EventLogEntryType.Error);
	throw;
}
catch(Exception e)
{
	// Process any other Exception.
}

finally
{
	// Clean up and free any resources here.
	// For example, there could be a method on myCOMObj to allow us to clean
	// up after using the Method1 method.
}
```

## Configuring the State of an Exception

### The TargetSite Property
```cs
static void Main(string[] args)
{
	...
	// TargetSite actually returns a MethodBase object.
	catch(Exception e)
	{
		Console.WriteLine("\n*** Error! ***");
		Console.WriteLine("Member name: {0}", e.TargetSite);
		Console.WriteLine("Class defining member: {0}", 	e.TargetSite.DeclaringType);
		Console.WriteLine("Member type: {0}", e.TargetSite.MemberType);
		Console.WriteLine("Message: {0}", e.Message);
		Console.WriteLine("Source: {0}", e.Source);
	}
	
	Console.WriteLine("\n***** Out of exception logic *****");
	Console.ReadLine();
}

*** Error! ***
Member name: Void Accelerate(Int32)
Class defining member: SimpleException.Car
Member type: Method
Message: Zippy has overheated!
Source: SimpleException
```

### The StackTrace Property
```cs
catch(Exception e)
{
	...
	Console.WriteLine("Stack: {0}", e.StackTrace);
}

Output:
Stack: at SimpleException.Car.Accelerate(Int32 delta)
in c:\MyApps\SimpleException\car.cs:line 65 at SimpleException.Program.Main()
in c:\MyApps\SimpleException\Program.cs:line 21
```

### The HelpLink Property
```cs
// We need to call the HelpLink property, thus we need to
// create a local variable before throwing the Exception object.
Exception ex = new Exception(string.Format("{0} has overheated!", PetName));
ex.HelpLink = "http://www.CarsRUs.com";
throw ex;

catch(Exception e)
{
	...
	Console.WriteLine("Help Link: {0}", e.HelpLink);
}
```

### The Data Property
```cs
Exception ex = new Exception(string.Format("{0} has overheated!", PetName));

// Stuff in custom data regarding the error.
ex.Data.Add("TimeStamp", string.Format("The car exploded at {0}", DateTime.Now));
ex.Data.Add("Cause", "You have a lead foot.");


foreach (DictionaryEntry de in ex.Data)
	Console.WriteLine("-> {0}: {1}", de.Key, de.Value);
```

### System.Exception Base Class
```cs
public class Exception : ISerializable, _Exception
{
	// Public constructors
	public Exception(string message, Exception innerException);
	public Exception(string message);
	public Exception();
	...
	
	// Methods
	public virtual Exception GetBaseException();
	public virtual void GetObjectData(SerializationInfo info,
	StreamingContext context);

	// Properties
	public virtual IDictionary Data { get; }
	public virtual string HelpLink { get; set; }
	public Exception InnerException { get; }
	public virtual string Message { get; }
	public virtual string Source { get; set; }
	public virtual string StackTrace { get; }
	public MethodBase TargetSite { get; }
	...
}
```


### Obtaining information on an exception invoked by a method accessed through reflection

```cs
public static class Reflect
{
	public static void ReflectionException()
	{
		Type reflectedClass = typeof(DebuggingAndExceptionHandling);
		try
		{
			MethodInfo methodToInvoke = reflectedClass.GetMethod("TestInvoke");
			methodToInvoke?.Invoke(null, null);
		}
		catch(Exception e)
		{
			Console.WriteLine(e.ToShortDisplayString());
		}
	}
	
	public static void TestInvoke()
	{
	throw (new Exception("Thrown from invoked method."));
	}
}

Output:
Message: Exception has been thrown by the target of an invocation.
Type: System.Reflection.TargetInvocationException
Source: mscorlib
TargetSite: System.Object InvokeMethod(System.Object, System.Object[], System.Si
gnature, Boolean)
**** INNEREXCEPTION START ****
Message: Thrown from invoked method.
Type: System.Exception
Source: CSharpRecipes
TargetSite: Void TestInvoke()
**** INNEREXCEPTION END ****
```

## a New Exception Type
```cs
public class RemoteComponentException : Exception
{
	public RemoteComponentException() : base()
	{
		HResult = 0x80040321;
	}
	
	public RemoteComponentException(string message) : 	base(message)
	{
		HResult = 0x80040321;
	}
	
	public RemoteComponentException(string message, Exception innerException) : base(message, innerException)
	{
		HResult = 0x80040321;
	}
}
```

### Giving Exceptions the Extra Info with Exception.Data
```cs
try
{
	try
	{
		try
		{
			try
			{
				ArgumentException irritable = new ArgumentException("I'm irritable!");
				irritable.Data["Cause"]="Computer crashed";
				irritable.Data["Length"]=10;
				throw irritable;
			}
			catch (Exception e)
			{
				// See if I can help...
				if(e.Data.Contains("Cause"))
				e.Data["Cause"]="Fixed computer"
				throw;
			}
		}
		catch (Exception e)
		{
			e.Data["Comment"]="Always grumpy you are";
			throw;
		}
	}
	catch (Exception e)
	{
		e.Data["Reassurance"]="Error Handled";
		throw;
	}
}
```

## iterate over the Exception.Data collection
```cs
catch (Exception e)
{
	Console.WriteLine("Exception supporting data:");
	foreach(DictionaryEntry de in e.Data)
	{
		Console.WriteLine("\t{0} : {1}",de.Key,de.Value);
	}
}
```

### Selective About Exception Processing
```cs
private void ProtectedCallTheDatabase(string problem)
{
	try
	{
		CallTheDatabase(problem);
		Console.WriteLine("No error on database call");
	}
	catch (DatabaseException dex) when (dex.Number == -2) // watch for timeouts
	{
		Console.WriteLine(	"DatabaseException catch caught : " +	$"{dex.Message}");
	}
}
```

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



# Enumerators and Iterators
# Preprocessor Directives
# File I/O
# Regular Expressions