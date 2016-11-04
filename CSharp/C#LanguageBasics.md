# C# Language Basics

* [Types, Storage, and Variables](#Types, Storage, and Variables)
* [Default Values](#default-value)
* [Constant, Readonly, Static field](#constant)
* [Statements](#statements)
* [Expressions and Operators](#expressions-and-operators)
* [Method](#method)
* [Arrays](#arrays)
* [Conversions](#conversions)
* [Enumerations](#enumerations)
* [Exception Handling](#exception-handling)
* [Structs](#structs)
* [Namespaces](#namespaces)
* [Preprocessor Directives](#preprocessor-directives)
* [File I/O](#file-i/o)
* [Regular Expressions](#regular-expressions)
* [String Format](#string-format)
* [DateTime](#datatime) 
* [Console](#console)
* [Environment](#environment)

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

# Default Value
```cs
sbyte, byte, short, ushort, int, uint, long, ulong = 0
char = '\x0000'
float = 0.0f
double = 0.0d
decimal = 0.0m
bool = false
object = null
string = null
```

```cs
class Program
{

	static public sbyte theSignedByte;
	static byte theByte;
	static short theShort;
	static ushort theUShort;
	static int theInt;
	static uint theUInt;
	static long theLong;
	static ulong theULong;
	static char theChar;
	static float theFloat;
	static double theDouble;
	static public bool theBool;
	static public decimal theDecimal;
	static string theStr;
	static public object theObj;

	static void Main(string[] args)
	{

		// Acquire the default values for these types and assign to a variable.
		StringBuilder variable1 = default(StringBuilder); // Null
		int variable2 = default(int);	// 0
		bool variable3 = default(bool);	// False
		Program variable4 = default(Program); // Null

		Console.WriteLine("bool: {0}", theBool);
		Console.WriteLine("byte: {0}", theByte);
		Console.WriteLine("char: {0}", theChar);
		Console.WriteLine("decimal: {0}", theDecimal);
		Console.WriteLine("double: {0}", theDouble);
		Console.WriteLine("float: {0}", theFloat);
		Console.WriteLine("int: {0}", theInt);
		Console.WriteLine("long: {0}", theLong);
		Console.WriteLine("object: {0}", theObj);
		Console.WriteLine("short: {0}", theShort);
		Console.WriteLine("signed byte: {0}", theSignedByte);
		Console.WriteLine("string: {0}", theStr);
		Console.WriteLine("unsigned int: {0}", theUInt);
		Console.WriteLine("unsigned long: {0}", theULong);
		Console.WriteLine("unsigned short: {0}", theUShort);

		Console.ReadLine();
		
	}
}
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
int? i = 10;
double? d1 = 3.14;
char? letter = 'a';
int?[] arr = new int?[10];


int? c = null;
// d = c, unless c is null, in which case d = -1.
int d = c ?? -1;

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


# Default Values
* sbyte, byte, short, ushort=0, int, uint, long, ulong = 0
* char = '\x0000'
* float = 0.0f
* double = 0.0d
* decimal = 0.0m
* bool = false
* object = null
* string = null




# Constant
* [Difference Between Const, ReadOnly and Static ReadOnly in C#](http://www.c-sharpcorner.com/uploadfile/c210df/difference-between-const-readonly-and-static-readonly-in-c-sharp/)


* Compile-Time
* Fast
* Type Restrictions:  Primitive types, enums or strings
* Scope: Static
* Value is evaluated at compile time
* We cannot use variables to calculate the constants.
* Constant fields and locals aren't variables
* Constants cannot be modified
* Constants can be of any data type or a null reference.
* Constants are by default state so we cannot use static
* Constants can be use to calculate the constants
* Constants can have any access modifier
* Constants can be accessed by using class name directy without creating instances because by default it is static, it cannot be accessed by using the instance of the class but inside the call without class name.

```cs
const string STATE = "NY";
public const Single PI = 3.14159;
public const Single PI = 22/7;
public const double GRAVITATION = 6.673e-11;

//declare multiple constants
public const int CENTURY = 100, HATRIC = 3, OVER = 6;
public const int c1 = 5;
public const int c2 = c1 + 100;
public const int c3 = c1 + c2;
public const int c4 = c1 + c2 + c3;

//Invalid constants
public const int PI = x;
public const int PI = x/y;
public const double DISCOUNT = (price /100 ) * 3;
const string city = GetFromDB();
```

# ReadOnly 
* Runtime
* Slow
* Type Restrictions: none
* Scope: Instance or Static
* ReadOnly Value is evaluated at run time.
* ReadOnly can be either initialized in declaration or in the constructor
* ReadOnly cannot change the value once constructor is called.
* ReadOnly can be used with any data type
* ReadOnly constants can have any access modifier
* ReadOnly property can be change by using reflection 

```cs
public class Const_VS_Readonly
{
   public readonly char[] I_RO_VALUE = new Char[]{'a', 'b', 'c'};
   public Const_VS_Readonly()
   {
      I_RO_VALUE[0] = 'V'; //perfectly legal and will update the value
      I_RO_VALUE = new char[]{'V'}; //will cause compiler error
   }
}
```


# Static field 
* Static field property and method can directly accessed by using the class name.
* Static field, property and method cannot be accessed by using the instance.
* Static field is shared for entire instances as we already checked with example.
* Can be used where we only want to play on the passed values
* Best example is Math class and it's methods.

```cs
public static int x = 5;
```

# Statements
# Expressions and Operators
# Method
```cs
//Return Type - Method  name - Parameter list
int MyMethod ( int par1, string par2 )
```

### Method Invocations
```cs
//Method name - Empty  parameter list
mc.PrintDateAndTime();

//Return Values
return Expression
```

### Formal Parameters
```cs
public void PrintSum( int x, float y )
{ 
	... Formal parameter declarations
}
```

### Actual Parameters
```cs
PrintSum( 5, someInt );
```

### Reference Parameters
```cs
// Method declaration
void MyMethod( ref int val ) 
{ ... }

int y = 1; // Variable for the actual parameter
MyMethod ( ref y ); // Method call: Include the ref modifier.

//Must use a variable
MyMethod ( ref 3+5 ); // Error!
```

### Output Parameters
```cs
void MyMethod( out int val ) // Method declaration
{ ... }

int y = 1; // Variable for the actual parameter
MyMethod ( out y ); // Method call


public void Add2( out int outValue )
{
int var1 = outValue + 2; // Error! Can't read from an output parameter
} // before it has been assigned to by the method.

//two out parameter
static void MyMethod(out MyClass f1, out int f2)
```

### Parameter Arrays
```cs
void ListInts( params int[] inVals )
{
}

//Method Invocation
ListInts( 10, 20, 30 ); // Three ints

int[] intArray = {1, 2, 3};
ListInts( intArray ); // An array variable


//Expanded Form
void ListInts( params int[] inVals ) { ... } // Method declaration
...
ListInts( ); // 0 actual parameters
ListInts( 1, 2, 3 ); // 3 actual parameters
ListInts( 4, 5, 6, 7 ); // 4 actual parameters
ListInts( 8, 9, 10, 11, 12 ); // 5 actual parameters



class MyClass Parameter array
{ 
	public void ListInts( params int[] inVals )
	{
		if ( (inVals != null) && (inVals.Length != 0))
			for (int i = 0; i < inVals.Length; i++) // Process the array.
			{
				inVals[i] = inVals[i] * 10;
				Console.WriteLine("{0}", inVals[i]); // Display new value.
			}
		}
	}
	class Program
	{
		static void Main()
		{
			int first = 5, second = 6, third = 7; // Declare three ints.
			MyClass mc = new MyClass();
			mc.ListInts( first, second, third ); // Call the method.
			Console.WriteLine("{0}, {1}, {2}", first, second, third);
	}
}
```

### Method Overloading
```cs
//return type is Not part of signature
long AddValues( int a, out int b) { ... }

class B Signature
{ 
	long AddValues( long a, long b) { return a+b; }
	int AddValues( long c, long d) { return c+d; } // Error, same signature
}



class A
{
long AddValues( int a, int b) { return a + b; }
long AddValues( int c, int d, int e) { return c + d + e; }
long AddValues( float f, float g) { return (long)(f + g); }
long AddValues( long h, long m) { return h + m; }
}
```

### Named Parameters
```cs
c.Calc ( c: 2, a: 4, b: 3);


static void Main()
{
	MyClass mc = new MyClass( );
	int r0 = mc.Calc( 4, 3, 2 ); // Positional Parameters
	int r1 = mc.Calc( 4, b: 3, c: 2 ); // Positional and Named Parameters
	int r2 = mc.Calc( 4, c: 2, b: 3 ); // Switch order
	int r3 = mc.Calc( c: 2, b: 3, a: 4 ); // All named parameters
	int r4 = mc.Calc( c: 2, b: 1 + 2, a: 3 + 1 ); // Named parameter expressions
	Console.WriteLine("{0}, {1}, {2}, {3}, {4}", r0, r1, r2, r3, r4);
}
```

### Optional Parameters
```cs
class MyClass Optional parameter
{ 
	//b = Optional parameter, 3 = Default value assignment
	public int Calc( int a, int b = 3 )
	{ 
		return a + b; Default value assignment
	}
}



volume = mc.GetCylinderVolume( 3.0, 4.0 ); // Positional
Console.WriteLine( "Volume = " + volume );

volume = mc.GetCylinderVolume( radius: 2.0 ); // Use default height
Console.WriteLine( "Volume = " + volume );

volume = mc.GetCylinderVolume( height: 2.0 ); // Use default radius
Console.WriteLine( "Volume = " + volume );

volume = mc.GetCylinderVolume( ); // Use both defaults
Console.WriteLine( "Volume = " + volume );
```

### Recursion
```cs
int Factorial(int inValue)
{
	if (inValue <= 1)
		return inValue;
	else
		return inValue * Factorial(inValue - 1); // Call Factorial again.
}
```
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

```cs
string myString = "true";
bool myBool = Convert.ToBoolean(myString);

string newString = "123456789";
int myInt = Convert.ToInt32(newString);

Int64 myInt64 = 123456789;
int myInt = Convert.ToInt32(myInt64);
   
Double myDouble = 42.72;
int myInt = Convert.ToInt32(myDouble);
   
// The integer value is set to 2147483647. 
int myInt = int.MaxValue;
byte myByte = (byte)myInt;
Console.WriteLine("The byte value is {0}.", myByte);
// The value of MyByte is 255, the maximum value of a Byte. 
// No overflow exception is thrown.


// The integer value is set to 2147483647. 
int myInt = int.MaxValue;
byte myByte = checked ((byte) myInt);
Console.WriteLine("The byte value is {0}.", myByte);
// Attempting to convert Int32.MaxValue to a Byte  
// throws an OverflowException.


Double myDouble = 42.72;
int myInt = checked ((int)myDouble);
Console.WriteLine(myInt);
// myInt has a value of 42.

```

```cs
int i;
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"
```

### Implicit Conversions
```cs
// Implicit conversion. num long can
// hold any value an int can hold, and more!
int num = 2147483647;
long bigNum = num;


Derived d = new Derived();
Base b = d; // Always OK.
```

### Explicit Conversions
```cs
class Test
{
    static void Main()
    {
        double x = 1234.7;
        int a;
        // Cast double to int.
        a = (int)x;
        System.Console.WriteLine(a);
    }
}
// Output: 1234
```

```cs
// Create a new derived type.
Giraffe g = new Giraffe();

// Implicit conversion to base type is safe.
Animal a = g;

// Explicit conversion is required to cast back
// to derived type. Note: This will compile but will
// throw an exception at run time if the right-side
// object is not in fact a Giraffe.
Giraffe g2 = (Giraffe) a;
```


### Type Conversion Exceptions at Run Time
```cs
class Animal
{
    public void Eat() { Console.WriteLine("Eating."); }
    public override string ToString()
    {
        return "I am an animal.";
    }
}
class Reptile : Animal { }
class Mammal : Animal { }

class UnSafeCast
{
    static void Main()
    {            
        Test(new Mammal());

        // Keep the console window open in debug mode.
        System.Console.WriteLine("Press any key to exit.");
        System.Console.ReadKey();
    }

    static void Test(Animal a)
    {
        // Cause InvalidCastException at run time 
        // because Mammal is not convertible to Reptile.
        Reptile r = (Reptile)a;
    }

}
```

### implement the casting mechanism in our user-defined classes using conversion operators.
```cs
public class Author
{
    public string First;
    public string Last;
    public string[] BooksArray;
}

public class Writer
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public List<string> Books { get; set; }
}

Author author2 = (Author)writer; //explicit casting 
Author author1 = writer; //implicit casting

public static explicit operator Writer(Author a)
{
    return new Writer
    {
        FirstName = a.First,
        LastName = a.Last,
        Books = a.BooksArray != null ? a.BooksArray.ToList() : null
    };
}


Author a = new Author
{
    First = "Vijaya",
    Last = "Anand",
    BooksArray = new string[] { "book1" }
};
Writer w = (Writer)a; //explicitly casting from Author to Writer.


Author a = new Author
{
    First = "Vijaya",
    Last = "Anand",
    BooksArray = new string[] { "book1" }
};
Writer w = a; //implicitly casting from Author to Writer.
```



## Boxing and Unboxing 
```cs
System.ValueType r = 5;
r++;
Console.WriteLine(r.GetType()) // returns System.Int32; 
```

### Boxing
```cs
int i = 123;
// The following line boxes i.
object o = i;  
```

### Unboxing
```cs
o = 123;
i = (int)o;  // unboxing
```

### Implicit boxing
```cs
Int32 x = 10;
object o = x ;  // Implicit boxing
Console.WriteLine("The Object o = {0}",o); // prints out 10
```

### Explicit Boxing
```cs
Int32 x = 10;
object o = (object) x; // Explicit Boxing
Console.WriteLine("The object o = {0}",o); // prints out 10
```

```cs
Int32 x = 5;
object o = x; // Implicit Boxing
x = o; // Implicit UnBoxing


Int32 x = 5;
object o = x; // Implicit Boxing
x = (Int32)o; // Explicit UnBoxing


Int32 x = 5; // declaring Int32
Int64 y = 0; // declaring Int64 double
object o = x; // Implicit Boxing
y = (Int64)o; // Explicit boxing to double
Console.WriteLine("y={0}",y);

Int32 x = 5; // declaring Int32
Int64 y = 0; // declaring Int64 double
object o = x; // Implicit Boxing
y = (Int64)(Int32)o; // Unboxing and than casting to double
Console.WriteLine("y={0}",y);
```

### Upcasting and Downcasting
```cs
class Base
{
	public int num1 { get; set; }
}
 
class Derived : Base
{
	public int num2 { get; set; }
}
 
class Program
{
	 static void Main(string[] args)
	 {
		 Derived d1 = new Derived();
		 //Upcasting
		 Base b1 = d1;
		 
		 Base b2 = new Base();
		 //Downcasting
		 Derived d2 = (Derived)b2; 
	 }
}
```


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
* No database connection => exception.
* Invalid string format to parse to some type => exception
* Trying to parse JSON and while input isn't actually JSON => exception
* Argument null while object was expected => exception
* Some library has a bug => throws an unexpected exception
* There's a socket connection and it gets disconnected. Then you try to send a message => exception
* Your database can go offline...
* Some file can be locked...
* Some formatting might be not supported...
* Some domain validation might fail...
* Your app should work in offline mode...

* [Exception Handling for C# Beginners](http://www.codeproject.com/Articles/125470/Exception-Handling-for-C-Beginners)


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
catch (SomeException e) when (passesFilter(e))
{
	//filter exception
    // expression following the when keyword evaluates to true,
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

# Creating User-Defined Exceptions
```cs
using System;
namespace UserDefinedException
{
   class TestTemperature
   {
      static void Main(string[] args)
      {
         Temperature temp = new Temperature();
         try
         {
            temp.showTemp();
         }
         catch(TempIsZeroException e)
         {
            Console.WriteLine("TempIsZeroException: {0}", e.Message);
         }
         Console.ReadKey();
      }
   }
}

public class TempIsZeroException: Exception
{
   public TempIsZeroException(string message): base(message)
   {
   }
}

public class Temperature
{
   int temperature = 0;
   public void showTemp()
   {
      if(temperature == 0)
      {
         throw (new TempIsZeroException("Zero Temperature found"));
      }
      else
      {
         Console.WriteLine("Temperature: {0}", temperature);
      }
   }
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
```cs
struct Point
{
	public int X;
	public int Y;
}

class Program
{
	static void Main()
	{
		Point first
		
		first.X = 10; 
		first.Y = 10;
		Console.WriteLine("first: {0}, {1}", first.X, first.Y);
	}
}
```

### Structs Are Value Types
```cs
struct Simple
{
	public int X;
	public int Y;
}

Simple ss = new Simple();
```


```cs
struct Simple
{
	public int X;
	public int Y;
	public Simple(int a, int b) // Constructor with parameters
	{
		X = a;
		Y = b;
	}
}
```

```cs
Simple s1 = new Simple();
Simple s2 = new Simple(5, 10);

struct Simple
{
	public int X;
	public int Y;
}
class Program
{
	static void Main()
	{ 
		//No constructor calls
		Simple s1, s2;
		
		//s1.X, s1.Y Not yet assigned
		Console.WriteLine("{0},{1}", s1.X, s1.Y); // Compiler error

		s2.X = 5; 
		s2.Y = 10;
		Console.WriteLine("{0},{1}", s2.X, s2.Y); // OK
	}
}
```

### Field Initializers Are Not Allowed
```cs
struct Simple
{
	//Not allowed
	public int x = 0; // Compile error
	public int y = 10; // Compile error
} 
```


# Namespaces

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


# Preprocessor Directives

```cs
#define PremiumVersion 	// OK
#define BudgetVersion 	// Space before # OK
# define MediumVersion 	// Space after # K
```

```cs
//Delimited comments are not allowed
#define PremiumVersion /* all bells & whistles */

//End-of-line comments are fine.
#define BudgetVersion // Stripped-down version
```

```cs
# define and #undef Directives
#define PremiumVersion
#define EconomyVersion
...
#undef PremiumVersion
```

```cs
using System; // First line of C# code
#define PremiumVersion // Error
namespace Eagle
{
	#define PremiumVersion // Error
```

```cs
#define AValue
#define BValue

#define AValue // Redefinition is fine.
```




## Conditional Compilation 
```cs
#if !DemoVersion
	...
#endif Expression

#if (LeftHanded && OemVersion) || FullVersion
	...
#endif

#if true // The following code segment will always be compiled.
	...
#endif
```

```cs
#define DemoVersionWithoutTimeLimit
...
const int intExpireLength = 30;
string strVersionDesc = null;
int intExpireCount = 0;


#if DemoVersionWithTimeLimit
	intExpireCount = intExpireLength;
	strVersionDesc = "This version of Supergame Plus will expire in 30 days";

#elif DemoVersionWithoutTimeLimit
	strVersionDesc = "Demo Version of Supergame Plus";
#elif OEMVersion
	strVersionDesc = "Supergame Plus, distributed under license";
#else
	strVersionDesc = "The original Supergame Plus!!";
#endif
```




## Diagnostic Directives
```cs
#define RightHanded
#define LeftHanded

#if RightHanded && LeftHanded
#error Can't build for both RightHanded and LeftHanded
#endif
#warning Remember to come back and clean up this code!
```


## Line Number Directives
```cs
#line integer // Sets line number of next line to value of integer
#line "filename" // Sets the apparent file name
#line default // Restores real line number and file name
#line hidden // Hides the following code from stepping debugger
#line // Stops hiding from debugger
```

```cs
#line 226
x = y + z; // Now considered by the compiler to be line 226
...

#line 330 "SourceFile.cs" // Changes the reported line number and file name
var1 = var2 + var3;
...

#line default // Restores true line numbers and file name
```


## Region Directives

```cs
#region Constructors
MyClass()
{ ...
}
MyClass(string s)
{ ...
}
#endregion
```

##  [#pragma warning Directive]
```cs
#pragma warning disable 618, 414
#pragma warning restore 618
#pragma warning disable
#pragma warning restore
```
# File I/O
# Regular Expressions


# String Format
```cs
//en-US
Console.WriteLine("The current culture is: " + System.Threading.Thread.CurrentThread.CurrentCulture);

int number = 42;
string s = number.ToString("D5"); // 00042
s = String.Format("{0,10:D}", number); // "        42"
Console.WriteLine(s);

// Chenge the default culture to Bulgarian
System.Threading.Thread.CurrentThread.CurrentCulture = new CultureInfo("bg-BG");
Console.WriteLine("Bulgarian price: {0:C}", number); // 42,00 ëâ.

string template = "If I were {0}, I would {1}.";
string sentence1 = String.Format(template, "developer", "know C#");
Console.WriteLine(sentence1);
// If I were developer, I would know C#.

string sentence2 = String.Format(template, "elephant", "weigh 4500 kg");
Console.WriteLine(sentence2);
// If I were elephant, I would weigh 4500 kg.

Decimal pricePerOunce = 17.36m;
String s = String.Format("The current price is {0} per ounce.", pricePerOunce);
// Result: The current price is 17.36 per ounc

decimal temp = 20.4m;
string s1 = String.Format("The temperature is {0}°C.", temp);
Console.WriteLine(s1);

string s2 = String.Format("At {0}, the temperature is {1}°C.", DateTime.Now, 20.4);
// Output similar to: 'At 4/10/2015 9:29:41 AM, the temperature is 20.4°C.'

string s3 = String.Format("It is now {0:d} at {0:t}", DateTime.Now);
// Output similar to: 'It is now 4/10/2015 at 10:04 AM'

DateTime now = DateTime.Now;
Console.WriteLine("Now is {0:d.MM.yyyy HH:mm:ss}.", now);

DateTime dat = new DateTime(2012, 1, 17, 9, 30, 0);
string city = "Chicago";
int temp1 = -16;
string output = String.Format("At {0} in {1}, the temperature was {2} degrees.", dat, city, temp1);

Console.WriteLine(output);
// The example displays the following output:
//    At 1/17/2012 9:30:00 AM in Chicago, the temperature was -16 degrees.   

double value = 123456;
Console.WriteLine(value.ToString("[##-##-##]")); // Displays [12-34-56]

double value1 = .086;
Console.WriteLine(value1.ToString("#0.##%", CultureInfo.InvariantCulture));
// Displays 8.6%  

double number1 = 1234567890;
Console.WriteLine(number1.ToString("(###) ###-####")); // (123) 456-7890

int number2 = 42;
Console.WriteLine(number2.ToString("My Number = #"));  //My Number = 42

decimal value2 = 123.456m;
Console.WriteLine(value2.ToString("C2")); // Displays $123.46

int value5 = 12345;
Console.WriteLine(value5.ToString("D")); // Displays 12345
Console.WriteLine(value5.ToString("D8")); // Displays 00012345

string.Format("{0:Yes;;No}", 1); //Output Yes
string.Format("{0:Yes;;No}", 0); //Output No
```

# Datatime
```cs
DateTime dob = new DateTime(1974, 7, 10, 7, 10, 24);  
Console.WriteLine("Day:{0}", dob.Day);  
Console.WriteLine("Month:{0}", dob.Month);  
Console.WriteLine("Year:{0}", dob.Year);  
Console.WriteLine("Hour:{0}", dob.Hour);  
Console.WriteLine("Minute:{0}", dob.Minute);  
Console.WriteLine("Second:{0}", dob.Second);  
Console.WriteLine("Millisecond:{0}", dob.Millisecond);  
   
Console.WriteLine("Day of Week:{0}", dob.DayOfWeek);  
Console.WriteLine("Day of Year: {0}", dob.DayOfYear);  
Console.WriteLine("Time of Day:{0}", dob.TimeOfDay);  
Console.WriteLine("Tick:{0}", dob.Ticks);  
Console.WriteLine("Kind:{0}", dob.Kind);  


DateTime aDay = DateTime.Now;  
TimeSpan aMonth = new System.TimeSpan(30, 0, 0, 0);  
DateTime aDayAfterAMonth = aDay.Add(aMonth);  
DateTime aDayBeforeAMonth = aDay.Subtract(aMonth);  
Console.WriteLine("{0:dddd}", aDayAfterAMonth);  
Console.WriteLine("{0:dddd}", aDayBeforeAMonth);  


// Add Years and Days  
aDay.AddYears(2);            
aDay.AddDays(12);  
// Add Hours, Minutes, Seconds, Milliseconds, and Ticks  
aDay.AddHours(4.25);  
aDay.AddMinutes(15);  
aDay.AddSeconds(45);             
aDay.AddMilliseconds(200);  
aDay.AddTicks(5000);

DateTime dob = new DateTime(2002, 10, 22);  
Console.WriteLine(dob.IsDaylightSavingTime());  
Console.WriteLine(DateTime.IsLeapYear(dob.Year));   

//Converting String to DateTime
tring dt = "2010-10-04T20:12:45-5:00";  
DateTime newDt = DateTime.Parse(dt);  
Console.WriteLine(newDt.ToString());   

DateTime dob = new DateTime(2002, 10, 22);  
Console.WriteLine("ToString: " + dob.ToString());  
Console.WriteLine("ToBinary: " + dob.ToBinary());  
Console.WriteLine("ToFileTime: " + dob.ToFileTime());  
Console.WriteLine("ToLocalTime: " + dob.ToLocalTime());  
Console.WriteLine("ToLongDateString: " + dob.ToLongDateString());  
Console.WriteLine("ToLongTimeString: " + dob.ToLongTimeString());  
Console.WriteLine("ToOADate: " + dob.ToOADate());  
Console.WriteLine("ToShortDateString: " + dob.ToShortDateString());  
Console.WriteLine("ToShortTimeString: " + dob.ToShortTimeString());  
Console.WriteLine("ToUniversalTime: " + dob.ToUniversalTime());  



DateTime date1 = new DateTime(2008, 3, 1, 7, 0, 0);
Console.WriteLine(date1.ToString());
// For en-US culture, displays 3/1/2008 7:00:00 AM


  DateTime localDate = DateTime.Now;
      String[] cultureNames = { "en-US", "en-GB", "fr-FR",
                                "de-DE", "ru-RU" };

      foreach (var cultureName in cultureNames) {
         var culture = new CultureInfo(cultureName);
         Console.WriteLine("{0}: {1}", cultureName,
                           localDate.ToString(culture));
      }



Console.WriteLine(date1.ToString("d, M", 
                  CultureInfo.InvariantCulture)); 
// Displays 29, 8

Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays 29 August
Console.WriteLine(date1.ToString("d MMMM", 
                  CultureInfo.CreateSpecificCulture("es-MX")));
// Displays 29 agosto   

DateTime date1 = new DateTime(2008, 1, 2, 6, 30, 15);

Console.WriteLine(date1.ToString("dd, MM", 
                  CultureInfo.InvariantCulture)); 

Console.WriteLine(date1.ToString("yyyy"));
// Displays 0001


 String format = "dd MMM yyyy hh:mm tt \"pst\"";
      var dat = new DateTime(2016, 8, 18, 16, 50, 0);
      // Display the result string. 
      Console.WriteLine(dat.ToString(format));

      // Parse a string. 
      String value = "25 Dec 2016 12:00 pm pst";
      DateTime newDate;
      if (DateTime.TryParseExact(value, format, null, 
                                 DateTimeStyles.None, out newDate)) 
         Console.WriteLine(newDate);
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }



Console.WriteLine(value == DateTime.Today);


yesterday
// Add -1 to now.
	return DateTime.Today.AddDays(-1);




//Tomoorow
return DateTime.Today.AddDays(1);


int days = DateTime.DaysInMonth(2014, 9); // September.
	Console.WriteLine(days);

	days = DateTime.DaysInMonth(2014, 2); // February.
	Console.WriteLine(days);


IsLeapYear


ToLocalTime


DateTime current = DateTime.MinValue;

DateTime today = DateTime.Today;

// Get currrent day of week.
	DayOfWeek today = DateTime.Today.DayOfWeek;



DateTime now = DateTime.Now;
	Console.WriteLine(now.ToLongDateString());  // Equivalent to D.
	Console.WriteLine(now.ToLongTimeString());  // Equivalent to T.
	Console.WriteLine(now.ToShortDateString()); // Equivalent to d.
	Console.WriteLine(now.ToShortTimeString()); // Equivalent to t.
	Console.WriteLine(now.ToString());



DateTime now = DateTime.Now;
	for (int i = 0; i < 2; i++)
	{
	    Console.WriteLine(now.ToString("tt "));
	    now = now.AddHours(12);


// create date time 2008-03-09 16:05:07.123
DateTime dt = new DateTime(2008, 3, 9, 16, 5, 7, 123);

String.Format("{0:t}", dt);  // "4:05 PM"                         ShortTime
String.Format("{0:d}", dt);  // "3/9/2008"                        ShortDate
String.Format("{0:T}", dt);  // "4:05:07 PM"                      LongTime
String.Format("{0:D}", dt);  // "Sunday, March 09, 2008"          LongDate
String.Format("{0:f}", dt);  // "Sunday, March 09, 2008 4:05 PM"  LongDate+ShortTime
String.Format("{0:F}", dt);  // "Sunday, March 09, 2008 4:05:07 PM" FullDateTime
String.Format("{0:g}", dt);  // "3/9/2008 4:05 PM"                ShortDate+ShortTime
String.Format("{0:G}", dt);  // "3/9/2008 4:05:07 PM"             ShortDate+LongTime
String.Format("{0:m}", dt);  // "March 09"                        MonthDay
String.Format("{0:y}", dt);  // "March, 2008"                     YearMonth
String.Format("{0:r}", dt);  // "Sun, 09 Mar 2008 16:05:07 GMT"   RFC1123
String.Format("{0:s}", dt);  // "2008-03-09T16:05:07"             SortableDateTime
String.Format("{0:u}", dt);  // "2008-03-09 16:05:07Z"            UniversalSortableDateTime



 DateTime date1 = new DateTime(2009, 8, 1, 0, 0, 0);
      DateTime date2 = new DateTime(2009, 8, 1, 12, 0, 0);
      int result = DateTime.Compare(date1, date2);
      string relationship;

      if (result < 0)
         relationship = "is earlier than";
      else if (result == 0)
         relationship = "is the same time as";         
      else
         relationship = "is later than";

      Console.WriteLine("{0} {1} {2}", date1, relationship, date2);
   }



String s;

s = "2014-08-04 12:00 PM";

DateTime dt = new DateTime();

dt = DateTime.ParseExact(s, "yyyy-MM-dd HH:mm tt", null);




String.Format("{0:y yy yyy yyyy}", dt);  // "8 08 008 2008"   year
String.Format("{0:M MM MMM MMMM}", dt);  // "3 03 Mar March"  month
String.Format("{0:d dd ddd dddd}", dt);  // "9 09 Sun Sunday" day
String.Format("{0:h hh H HH}",     dt);  // "4 04 16 16"      hour 12/24
String.Format("{0:m mm}",          dt);  // "5 05"            minute
String.Format("{0:s ss}",          dt);  // "7 07"            second
String.Format("{0:f ff fff ffff}", dt);  // "1 12 123 1230"   sec.fraction
String.Format("{0:F FF FFF FFFF}", dt);  // "1 12 123 123"    without zeroes
String.Format("{0:t tt}",          dt);  // "P PM"            A.M. or P.M.
String.Format("{0:z zz zzz}",      dt);  // "-6 -06 -06:00"   time zone



// Calculate what day of the week is 36 days from this instant.
System.DateTime today = System.DateTime.Now;
System.TimeSpan duration = new System.TimeSpan(36, 0, 0, 0);
System.DateTime answer = today.Add(duration);
System.Console.WriteLine("{0:dddd}", answer);



		DateTime today = DateTime.Now;
		DateTime answer = today.AddDays(36);



  DateTime dateValue = new DateTime(2013, 9, 15, 12, 0, 0);

      double[] minutes = { .01667, .08333, .16667, .25, .33333, 
                           .5, .66667, 1, 2, 15, 30, 17, 45, 
                           60, 180, 60 * 24 };

      foreach (double minute in minutes)
         Console.WriteLine("{0} + {1} minute(s) = {2}", dateValue, minute, 
                           dateValue.AddMinutes(minute));


 var dat = new DateTime(2015, 12, 31);
      for (int ctr = 0; ctr <= 15; ctr++)
         Console.WriteLine(dat.AddMonths(ctr).ToString("d"));


 Console.WriteLine("{0,2} year(s) from now:   {1:d}", 
                           ctr, baseDate.AddYears(ctr));

http://extensionmethod.net/csharp/datetime

```

# Console
```cs
//Get args using foreach-loop. 
foreach (string value in args){
    Console.WriteLine("foreach: {0}", value);
}
//Get args using for-loop.  
for (int i = 0; i < args.Length; i++) {
    Console.WriteLine("for: {0}", args[i]);
}

int i=10;
Console.WriteLine("Beep number {0}.", i);
Console.Beep();
Console.Beep(196, 1600);

Console.ForegroundColor = ConsoleColor.DarkYellow;
Console.BackgroundColor = ConsoleColor.DarkRed;
Console.WriteLine(("").PadRight(24, '-'));
Console.WriteLine("Grand total:\t{0,8:c}", i);
// Restore the original console colors.
Console.ResetColor();
Console.WriteLine(Console.CapsLock);
Console.WriteLine(Console.NumberLock);

Console.WindowWidth = 40;
Console.WindowHeight = 10;

using (StreamWriter writer = new StreamWriter("C:\\out.txt"))
{
    Console.SetOut(writer);
    Console.WriteLine("This is Console.WriteLine");
}

// Call ReadKey method and store result in local variable.
// ... Then test the result for escape.
ConsoleKeyInfo info = Console.ReadKey();
if (info.Key == ConsoleKey.Escape)
{
    Console.WriteLine("You pressed escape!");
}


string line = Console.ReadLine(); // Get string from user
if (line == "exit") // Check string
{
    break;
}

// ... When the enter key is pressed, the Read method returns the first time.
// ... Then, each call to Read accesses one further character from the input.
int result;
while ((result = Console.Read()) != 0)
{
    Console.WriteLine("{0} = {1}", result, (char)result);
}

Console.Clear();
```

# Environment
```cs
Environment.Exit(0);

//"%WINDIR%", "%HOMEDRIVE%", "%USERNAME%", "%COMPUTERNAME%"
string result = Environment.ExpandEnvironmentVariables("%WINDIR%"); //C:\Windows

// GetCommandLineArgs contains the program path as the first element.
string[] array = Environment.GetCommandLineArgs();

string s = "First line" + Environment.NewLine + "Second line";
//C:\Users\Sam2\Desktop
string path = Environment.GetFolderPath(Environment.SpecialFolder.Desktop);

string[] value1 = Environment.GetLogicalDrives();
Console.WriteLine(Environment.ProcessorCount);
```
