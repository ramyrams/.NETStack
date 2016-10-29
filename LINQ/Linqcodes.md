
# LINQ

https://www.dotnetperls.com/linq
http://linqsamples.com/linq-to-objects/conversion/AsEnumerable

## Lambda Expressions
```cs
( ArgumentsToProcess ) => { StatementsToProcessThem }

// C# lambda expression.
List<int> evenNumbers = list.FindAll(i => (i % 2) == 0);

//Lambda Expression Demonstrating Explicit Argument Types
Func<int, int, int> add = (int x, int y) => x + y;
Console.WriteLine(add(3, 4));


Action<double> print = amount => Console.WriteLine(“{0:c}”, amount); 
Action<double> michiganSalesTax = amount => print(amount *= 1.06);

var amounts = new double[]{ 10.36, 12.00, 134};

Array.ForEach<double>(amounts, michiganSalesTax);

Console.ReadLine();


```


## Extension Methods
```cs
namespace ExtensionMethods
{
    public static class MyExtensions
    {
        public static int WordCount(this String str)
        {
            return str.Split(new char[] { ' ', '.', '?' }, 
                             StringSplitOptions.RemoveEmptyEntries).Length;
        }
    }   
}


using ExtensionMethods;
string s = "Hello Extension Methods";
int i = s.WordCount();


```

## Partial Classes and Methods
```cs
namespace PM
{
    partial class A
    {
        partial void OnSomethingHappened(string s);
    }

    // This part can be in a separate file. 
    partial class A
    {
        // Comment out this method and the program 
        // will still compile. 
        partial void OnSomethingHappened(String s)
        {
            Console.WriteLine("Something happened: {0}", s);
        }
    }
}
```

## Anonymous Type
```cs

//Anonymous Types1
var student = new { Name = "Mary Jones", Age = 19, Major = "History" };
Console.WriteLine("{0}, Age {1}, Major: {2}", student.Name, student.Age, student.Major);

//Anonymous Types2
string Major = "History";
var student = new { Age = 19, Other.Name, Major };

//Anonymous Types3
var student = new { Age = Age, Name = Other.Name, Major = Major };

// Array of objects of an anonymous type
var students = new[] 
{
    new { LName="Jones", FName="Mary", Age=19, Major="History" },
    new { LName="Smith", FName="Bob", Age=20, Major="CompSci" },
    new { LName="Fleming", FName="Carol", Age=21, Major="History" }
};

//Adding Methods to Anonymous Types
Func<string, string, string> Concat1 = delegate(string first, string last)
{
	return last + “, “ + first;
};

var dena = new {First=”Dena”, Last=”Swanson”, Concat=Concat1};
Console.WriteLine(dena.Concat(dena.First, dena.Last));


```



## Basic
```cs
// Data source
int[] numbers = { 2, 12, 5, 15 };

// Define and store the query.
IEnumerable<int> lowNums = from n in numbers
                            where n < 10
                            select n;
// Execute the query.
foreach (var x in lowNums) 
  Console.Write("{0}, ", x);
  
  
//Projecting New Data Types
var nameDesc = from p in products select new { p.Name, p.Description };  

return nameDesc; // Nope!   //static var GetProjectedSubset(ProductInfo[] products)

// Map set of anonymous objects to an Array object.
return nameDesc.ToArray();  //static Array GetProjectedSubset(ProductInfo[] products)


```



##LINQ As a Better Venn Diagramming Tool
```cs

List<string> myCars = new List<String> {"Yugo", "Aztec", "BMW"};
List<string> yourCars = new List<String>{"BMW", "Saab", "Aztec" };


var carDiff =(from c in myCars select c)
	.Except(from c2 in yourCars select c2);


Console.WriteLine("Here is what you don't have, but I do:");

foreach (string s in carDiff)
	Console.WriteLine(s); // Prints Yugo.


// Get the common members.
var carIntersect = (from c in myCars select c)
.Intersect(from c2 in yourCars select c2);

Console.WriteLine("Here is what we have in common:");
foreach (string s in carIntersect)
Console.WriteLine(s); // Prints Aztec and BMW.




// Get the union of these containers.
var carUnion = (from c in myCars select c)
.Union(from c2 in yourCars select c2);
Console.WriteLine("Here is everything:");
foreach (string s in carUnion)
Console.WriteLine(s); // Prints all common members.




var carConcat = (from c in myCars select c)
.Concat(from c2 in yourCars select c2);
// Prints: Yugo Aztec BMW BMW Saab Aztec.
foreach (string s in carConcat)
Console.WriteLine(s);

```


## LINQ Aggregation Operations
```cs
double[] winterTemps = { 2.0, -21.3, 8, -4, 0, 8.2 };

// Various aggregation examples.
Console.WriteLine("Max temp: {0}",
(from t in winterTemps select t).Max());

Console.WriteLine("Min temp: {0}",
(from t in winterTemps select t).Min());

Console.WriteLine("Avarage temp: {0}",
(from t in winterTemps select t).Average());

Console.WriteLine("Sum of all temps: {0}",
(from t in winterTemps select t).Sum());


```



## With & Without LINQ
```cs
// Assume we have an array of strings.
string[] currentVideoGames = { "Morrowind", "Uncharted 2", "Fallout 3", "Daxter", "System Shock 2" };
string[] gamesWithSpaces = new string[5];

for (int i = 0; i < currentVideoGames.Length; i++)
{
    if (currentVideoGames[i].Contains(" "))
        gamesWithSpaces[i] = currentVideoGames[i];
}

// Now sort them.
Array.Sort(gamesWithSpaces);

// Print out the results.
foreach (string s in gamesWithSpaces)
{
    if (s != null)
        Console.WriteLine("Item: {0}", s);
}

//With Linq
// Build a query expression to find the items in the array that have an embedded space.
IEnumerable<string> subset = from g in currentVideoGames
                            where g.Contains(" ") orderby g select g;
                            
// Print out the results.
foreach (string s in subset)
Console.WriteLine("Item: {0}", s);


```




## Method Syntax and Query Syntax
```cs
int[] numbers = { 2, 5, 28, 31, 17, 16, 42 };

// Query syntax
var numsQuery = from n in numbers 
                where n < 20
                select n;
// Method syntax
var numsMethod = numbers.Where(x => x < 20);

// Combined
int numsCount = (from n in numbers 
                    where n < 20
                    select n).Count();

foreach (var x in numsQuery)
    Console.Write("{0}, ", x);  //output: 2, 5, 17, 16,

foreach (var x in numsMethod)
    Console.Write("{0}, ", x);  //output: 2, 5, 17, 16,

Console.WriteLine(numsCount);   //output: 4

```

## Query Variables


int[] numbers = { 2, 5, 28 };
IEnumerable<int> lowNums = from n in numbers // Returns an enumerator
                            where n < 20
                            select n;
                            
int numsCount = (from n in numbers // Returns an int
                    where n < 20
                    select n).Count();


## From Clause
```cs

var groupA = new[] { 3, 4, 5, 6 };
var groupB = new[] { 6, 7, 8, 9 };

var someInts =  from a in groupA     // Required first from clause
                from b in groupB    // First clause of query body
                where a > 4 && b <= 8
                select new {a, b, sum = a + b}; //Object of anonymous type

foreach (var a in someInts)
    Console.WriteLine(a);

//Output        
{ a = 5, b = 6, sum = 11 }
{ a = 5, b = 7, sum = 12 }
{ a = 5, b = 8, sum = 13 }
{ a = 6, b = 6, sum = 12 }
{ a = 6, b = 7, sum = 13 }
{ a = 6, b = 8, sum = 14 }

```

## Let Clause
```cs
var groupA = new[] { 3, 4, 5, 6 };
var groupB = new[] { 6, 7, 8, 9 };

var someInts =  from a in groupA
                from b in groupB
                let sum = a + b //Store result in new variable.
                where sum == 12
                select new {a, b, sum};

foreach (var a in someInts)
    Console.WriteLine(a);

//Output
{ a = 3, b = 9, sum = 12 }
{ a = 4, b = 8, sum = 12 }
{ a = 5, b = 7, sum = 12 }
{ a = 6, b = 6, sum = 12 }
```


## Join Clause
```cs
var query = from s in students
            join c in studentsInCourses on s.StID equals c.StID
            where c.CourseName == "History"
            select s.LastName;
```







## Where Clause
```cs
var groupA = new[] { 3, 4, 5, 6 };
var groupB = new[] { 6, 7, 8, 9 };

var someInts =  from int a in groupA
                from int b in groupB
                let sum = a + b
                where sum >= 11 // Condition 1
                where a == 4    // Condition 2
                select new {a, b, sum};

foreach (var a in someInts)
    Console.WriteLine(a);

//Output
{ a = 4, b = 7, sum = 11 }
{ a = 4, b = 8, sum = 12 }
{ a = 4, b = 9, sum = 13 }



// Find the fast BMWs!
var fastCars = from c in myCars where c.Speed > 90 && c.Make == "BMW" select c;


```


## Applying LINQ Queries to Nongeneric Collections
```cs
// Transform ArrayList into an IEnumerable<T>-compatible type.
var myCarsEnum = myCars.OfType<Car>();

// Create a query expression targeting the compatible type.
var fastCars = from c in myCarsEnum where c.Speed > 55 select c;
```

## Filtering Data Using OfType<T>()
```cs
// Extract the ints from the ArrayList.
ArrayList myStuff = new ArrayList();

myStuff.AddRange(new object[] { 10, 400, 8, false, new Car(), "string data" });

var myInts = myStuff.OfType<int>();

// Prints out 10, 400, and 8.
foreach (int i in myInts)
{
  Console.WriteLine("Int value: {0}", i);
}
```

## orderby Clause
```cs
var query = from student in students
            orderby student.Age ← Order by Age.
            select student;
```






## group Clause
```cs
var students = new[] // Array of objects of an anonymous type
{
    new { LName="Jones", FName="Mary", Age=19, Major="History" },
    new { LName="Smith", FName="Bob", Age=20, Major="CompSci" },
    new { LName="Fleming", FName="Carol", Age=21, Major="History" }
};

var query = from student in students
            group student by student.Major;
foreach (var s in query) // Enumerate the groups.
{
    Console.WriteLine("{0}", s.Key);  //Grouping key

    foreach (var t in s) // Enumerate the items in the group.
    Console.WriteLine(" {0}, {1}", t.LName, t.FName);
}

//Output
History
    Jones, Mary
    Fleming, Carol
CompSci
    Smith, Bob

```




## into Clause
```cs
var groupA = new[] { 3, 4, 5, 6 };
var groupB = new[] { 4, 5, 6, 7 };

var someInts =  from a in groupA
                join b in groupB on a equals b
                into groupAandB // Query continuation
                from c in groupAandB
                select c;

foreach (var a in someInts)
    Console.Write("{0} ", a);
```




## Standard Query Operators
```cs

int[] numbers = new int[] {2, 4, 6};
int total = numbers.Sum();
int howMany = numbers.Count();


int[] intArray = new int[] { 3, 4, 5, 6, 7, 9 };

// Method syntax
var count1 = Enumerable.Count(intArray); 
var firstNum1 = Enumerable.First(intArray); 

// Extension syntax
var count2 = intArray.Count(); 
var firstNum2 = intArray.First(); 

Console.WriteLine("Count: {0}, FirstNumber: {1}", count1, firstNum1);
Console.WriteLine("Count: {0}, FirstNumber: {1}", count2, firstNum2);

//Output
Count: 6, FirstNumber: 3
Count: 6, FirstNumber: 3

```


## Query Expressions
```cs
var numbers = new int[] { 2, 6, 4, 8, 10 };
int howMany = (from n in numbers
                where n < 7
            select n).Count();  // Query expression and Operator

Console.WriteLine("Count: {0}", howMany);

//Output 
Count: 3
```



## Delegates As Parameters
```cs
int[] intArray = new int[] { 3, 4, 5, 6, 7, 9 };
var countOdd = intArray.Count(n => n % 2 == 1); //Lambda expression identifying the odd values
Console.WriteLine("Count of odd numbers: {0}", countOdd);

//Output
Count of odd numbers: 4
```


## Lambda Expression Parameter
```cs
int[] intArray = new int[] { 3, 4, 5, 6, 7, 9 };

Func<int, bool> myDel = delegate(int x)     //Anonymous method
                        {
                            return x % 2 == 1;
                        };
var countOdd = intArray.Count(myDel);

Console.WriteLine("Count of odd numbers: {0}", countOdd);
```

## Deferred Execution
```cs

```

##Chaining Query Operators
```cs
string[] names = { "Tom", "Dick", "Harry", "Mary", "Jay" };
IEnumerable<string> query = names
.Where (n => n.Contains ("a"))
.OrderBy (n => n.Length)
.Select (n => n.ToUpper());
foreach (string name in query) Console.WriteLine (name);


//Output
JAY
MARY
HARRY
```


## Natural Ordering
```cs
int[] numbers = { 10, 9, 8, 7, 6 };
IEnumerable<int> firstThree = numbers.Take (3); // { 10, 9, 8 }


IEnumerable<int> lastTwo = numbers.Skip (3); // { 7, 6 }

IEnumerable<int> reversed = numbers.Reverse(); // { 6, 7, 8, 9, 10 }


int firstNumber = numbers.First(); // 10
int lastNumber = numbers.Last(); // 6
int secondNumber = numbers.ElementAt(1); // 9
int secondLowest = numbers.OrderBy(n=>n).Skip(1).First(); // 7

//aggregation
int count = numbers.Count(); // 5;
int min = numbers.Min(); // 6;


//quantifiers
bool hasTheNumberNine = numbers.Contains (9); // true
bool hasMoreThanZeroElements = numbers.Any(); // true
bool hasAnOddElement = numbers.Any (n => n % 2 != 0); // true

```

## Deferred Execution
The extra number that we sneaked into the list after constructing the query is
included in the result, because it’s not until the foreach statement runs that any
filtering or sorting takes place. This is called deferred or lazy execution.
```cs

var numbers = new List<int>();
numbers.Add (1);

IEnumerable<int> query = numbers.Select (n => n * 10); // Build query

numbers.Add (2); // Sneak in an extra element

foreach (int n in query)
Console.Write (n + "|"); // 10|20|









int[] numbers = { 10, 20, 30, 40, 1, 2, 3, 8 };

// Get numbers less than ten.
var subset = from i in numbers where i < 10 select i;

**// LINQ statement evaluated here!**
foreach (var i in subset)
    Console.WriteLine("{0} < 10", i);


// Change some data in the array.
numbers[0] = 4;

**// Evaluated again!**
foreach (var j in subset)
    Console.WriteLine("{0} < 10", j);

```

## Reevaluation
Deferred execution has another consequence: a deferred execution query is reevaluated when you re-enumerate.

```cs
var numbers = new List<int>() { 1, 2 };
IEnumerable<int> query = numbers.Select (n => n * 10);

foreach (int n in query) Console.Write (n + "|"); // 10|20|
numbers.Clear();

foreach (int n in query) Console.Write (n + "|"); // <nothing>

```


## Captured Variables
lambda expressions capture outer variables, the query will honor the value of the those variables at the time the query runs
```cs
int[] numbers = { 1, 2 };
int factor = 10;
IEnumerable<int> query = numbers.Select (n => n * factor);
factor = 20;
foreach (int n in query) Console.Write (n + "|"); // 20|40|

```



## Captured Variables
```cs


```



## Immediate Execution
```cs
int[] numbers = { 10, 20, 30, 40, 1, 2, 3, 8 };

// Get data RIGHT NOW as int[].
int[] subsetAsIntArray = (from i in numbers where i < 10 select i).ToArray<int>();

// Get data RIGHT NOW as List<int>.
List<int> subsetAsListOfInts = (from i in numbers where i < 10 select i).ToList<int>();

```


## Using Enumerable / Lambda Expressions
```cs

string[] currentVideoGames = {"Morrowind", "Uncharted 2",
"Fallout 3", "Daxter", "System Shock 2"};
// Build a query expression using extension methods
// granted to the Array via the Enumerable type.
var subset = currentVideoGames.Where(game => game.Contains(" "))
.OrderBy(game => game).Select(game => game);
// Print out the results.
foreach (var game in subset)
Console.WriteLine("Item: {0}", game);
Console.WriteLine();


// Break it down!
var gamesWithSpaces = currentVideoGames.Where(game => game.Contains(" "));
var orderedGames = gamesWithSpaces.OrderBy(game => game);
var subset = orderedGames.Select(game => game);




//Using Anonymous Methods
// Build the necessary Func<> delegates using anonymous methods.
Func<string, bool> searchFilter =
delegate(string game) { return game.Contains(" "); };
Func<string, string> itemToProcess = delegate(string s) { return s; };
// Pass the delegates into the methods of Enumerable.
var subset = currentVideoGames.Where(searchFilter)
.OrderBy(itemToProcess).Select(itemToProcess);
// Print out the results.
foreach (var game in subset)
Console.WriteLine("Item: {0}", game);
Console.WriteLine();


//"***** Using Raw Delegates *****"
// Build the necessary Func<> delegates.
Func<string, bool> searchFilter = new Func<string, bool>(Filter);
Func<string, string> itemToProcess = new Func<string,string>(ProcessItem);
// Pass the delegates into the methods of Enumerable.
var subset = currentVideoGames
.Where(searchFilter).OrderBy(itemToProcess).Select(itemToProcess);
// Print out the results.
foreach (var game in subset)
Console.WriteLine("Item: {0}", game);
Console.WriteLine();





```

## LINQ Operators

### Filtering
* Where - Returns a subset of elements that satisfy a given condition 
* Take - Returns the first count elements and discards the rest 
* Skip - Ignores the first count elements and returns the rest
* TakeWhile - Emits elements from the input sequence until the predicate is false 
* SkipWhile - Ignores elements from the input sequence until the predicate is false, and then emits the rest
* Distinct - Returns a sequence that excludes duplicates 

```cs

string[] names = { "Tom", "Dick", "Harry", "Mary", "Jay" };

//Where
IEnumerable<string> query = names.Where (name => name.EndsWith ("y"));
// Result: { "Harry", "Mary", "Jay" }

//Take and Skip
//there are 100 matches. The following returns the first 20:
IQueryable<Book> query = dataContext.Books
.Where (b => b.Title.Contains ("mercury"))
.OrderBy (b => b.Title)
.Take (20);


//The next query returns books 21 to 40:
IQueryable<Book> query = dataContext.Books
.Where (b => b.Title.Contains ("mercury"))
.OrderBy (b => b.Title)
.Skip (20).Take (20);


//TakeWhile and SkipWhile
int[] numbers = { 3, 5, 2, 234, 4, 1 };
var takeWhileSmall = numbers.TakeWhile (n => n < 100); // { 3, 5, 2 }


int[] numbers = { 3, 5, 2, 234, 4, 1 };
var skipWhileSmall = numbers.SkipWhile (n => n < 100); // { 234, 4, 1 }

//Distinct
char[] distinctLetters = "HelloWorld".Distinct().ToArray();
string s = new string (distinctLetters); // HeloWrd

```



## Projecting
* Select - Transforms each input element with the given lambda expression 
* SelectMany - Transforms each input element, and then flattens and concatenates the resultant subsequences

```cs
IEnumerable<string> query = from f in FontFamily.Families
select f.Name;


//SelectMany
string[] fullNames = { "Anne Williams", "John Fred Smith", "Sue Green" };
IEnumerable<string> query = fullNames.SelectMany (name => name.Split());
foreach (string name in query)
Console.Write (name + "|"); // Anne|Williams|John|Fred|Smith|Sue|Green|



from c in dataContext.Customers
where c.Purchases.Any (p => p.Price > 1000)
select new {
c.Name,
Purchases = from p in c.Purchases
where p.Price > 1000
select new { p.Description, p.Price }
};
```

## Joining
* Join - Applies a lookup strategy to match elements from two collections, emitting a flat result set
* GroupJoin - As above, but emits a hierarchical result set 
* Zip  - Enumerates two sequences in step (like a zipper), applying a function over each element pair
 
```cs
//join
IQueryable<string> query =
from c in dataContext.Customers
join p in dataContext.Purchases on c.ID equals p.CustomerID
select c.Name + " bought a " + p.Description;

//GroupJoin
//An into clause translates to GroupJoin only when it appears directly after a join clause.
IEnumerable<IEnumerable<Purchase>> query =
from c in customers
join p in purchases on c.ID equals p.CustomerID
into custPurchases
select custPurchases; // custPurchases is a sequence

//Zip
int[] numbers = { 3, 5, 7 };
string[] words = { "three", "five", "seven", "ignored" };
IEnumerable<string> zip = numbers.Zip (words, (n, w) => n + "=" + w);

//Output
3=three
5=five
7=seven


```

## Ordering
* OrderBy, ThenBy - Sorts a sequence in ascending order 
* OrderByDescending, ThenByDescending - Sorts a sequence in descending order 
* Reverse - Returns a sequence in reverse order

```cs
IEnumerable<string> query = names.OrderBy (s => s.Length);
IEnumerable<string> query = names.OrderBy (s => s.Length);

IEnumerable<string> query = names.OrderBy (s => s.Length).ThenBy (s => s);

names.OrderBy (s => s.Length).ThenBy (s => s[1]).ThenBy (s => s[0]);

dataContext.Purchases.OrderByDescending (p => p.Price).ThenBy (p => p.Description);
```


## Grouping
* GroupBy -  Groups a sequence into subsequences
```cs
IEnumerable<IGrouping<string,string>> query = files.GroupBy (file => Path.GetExtension (file));
```

## Set Operators
Concat - Returns a concatenation of elements in each of the two sequences 
Union - Returns a concatenation of elements in each of the two sequences, excluding duplicates
Intersect - Returns elements present in both sequences 
Except - Returns elements present in the first, but not the second sequence EXCEPT
```cs
//Concat and Union
int[] seq1 = { 1, 2, 3 }, seq2 = { 3, 4, 5 };
IEnumerable<int> concat = seq1.Concat (seq2), // { 1, 2, 3, 3, 4, 5 }
union = seq1.Union (seq2); // { 1, 2, 3, 4, 5 }


//Intersect and Except
IEnumerable<int>
commonality = seq1.Intersect (seq2), // { 3 }
difference1 = seq1.Except (seq2), // { 1, 2 }
difference2 = seq2.Except (seq1); // { 4, 5 }




```


## Conversion Methods
OfType - Converts IEnumerable to IEnumerable<T>, discarding wrongly typed elements
Cast - Converts IEnumerable to IEnumerable<T>, throwing an exception if there are any wrongly typed elements
ToArray - Converts IEnumerable<T> to T[]
ToList - Converts IEnumerable<T> to List<T>
ToDictionary -  Converts IEnumerable<T> to Dictionary<TKey,TValue>
ToLookup - Converts IEnumerable<T> to ILookup<TKey,TElement>
AsEnumerable - Downcasts to IEnumerable<T>
AsQueryable - Casts or converts to IQueryable<T>

```cs
//OfType and Cast
ArrayList classicList = new ArrayList(); // in System.Collections
classicList.AddRange ( new int[] { 3, 4, 5 } );
IEnumerable<int> sequence1 = classicList.Cast<int>();


```

## Element Operators
* First, FirstOrDefault  - Returns the first element in the sequence, optionally satisfying a predicate
* Last, LastOrDefault - Returns the last element in the sequence, optionally satisfying a predicate
* Single, SingleOrDefault  - Equivalent to First/First OrDefault, but throws an exception if there is more than one match
* ElementAt, ElementAtOrDefault - Returns the element at the specified position 
* DefaultIfEmpty  - Returns a single-element sequence whose value is default(TSource) if the sequence has no elements

```cs
//First, Last, and Single
int[] numbers = { 1, 2, 3, 4, 5 };
int first = numbers.First(); // 1
int last = numbers.Last(); // 5
int firstEven = numbers.First (n => n % 2 == 0); // 2
int lastEven = numbers.Last (n => n % 2 == 0); // 4

int firstBigError = numbers.First (n => n > 10); // Exception
int firstBigNumber = numbers.FirstOrDefault (n => n > 10); // 0


int onlyDivBy3 = numbers.Single (n => n % 3 == 0); // 3
int divBy2Err = numbers.Single (n => n % 2 == 0); // Error: 2 & 4 match
int singleError = numbers.Single (n => n > 10); // Error
int noMatches = numbers.SingleOrDefault (n => n > 10); // 0
int divBy2Error = numbers.SingleOrDefault (n => n % 2 == 0); // Error

//ElementAt
int[] numbers = { 1, 2, 3, 4, 5 };
int third = numbers.ElementAt (2); // 3
int tenthError = numbers.ElementAt (9); // Exception
int tenth = numbers.ElementAtOrDefault (9); // 0
```

## Aggregation Methods
* Count, LongCount - Returns the number of elements in the input sequence, optionally satisfying a predicate
* Min, Max  - Returns the smallest or largest element in the sequence
* Sum, Average  - Calculates a numeric sum or average over elements in the sequence
* Aggregate - Performs a custom aggregation

```cs
//Count and LongCount
int digitCount = "pa55w0rd".Count (c => char.IsDigit (c)); // 3

//Min and Max
int[] numbers = { 28, 32, 14 };
int smallest = numbers.Min(); // 14;
int largest = numbers.Max(); // 32;

//Sum and Average
decimal[] numbers = { 3, 4, 8 };
decimal sumTotal = numbers.Sum(); // 15
decimal average = numbers.Average(); // 5 (mean value)

```


## Quantifiers
* Contains - Returns true if the input sequence contains the given element 
* Any  - Returns true if any elements satisfy the given predicate 
* All  - Returns true if all elements satisfy the given predicate 
* SequenceEqual  - Returns true if the second sequence has identical elements to the input sequence


```cs
bool hasAThree = new int[] { 2, 3, 4 }.Contains (3); // true;

bool hasAThree = new int[] { 2, 3, 4 }.Any (n => n == 3); // true;
bool hasABigNumber = new int[] { 2, 3, 4 }.Any (n => n > 10); // false;
bool hasABigNumber = new int[] { 2, 3, 4 }.Where (n => n > 10).Any();

dataContext.Customers.Where (c => c.Purchases.All (p => p.Price < 100));


foreach (int i in Enumerable.Range (5, 3))
Console.Write (i + " "); // 5 6 7


foreach (int i in Enumerable.Repeat (5, 3))
Console.Write (i + " "); // 5 5 5

```



## Generation Methods
* Empty - Creates an empty sequence
* Repeat - Creates a sequence of repeating elements
* Range - Creates a sequence of integers

```cs
//Empty
foreach (string s in Enumerable.Empty<string>())
Console.Write (s); // <nothing>


//Range and Repeat
foreach (int i in Enumerable.Range (5, 3))
Console.Write (i + " "); // 5 6 7

foreach (int i in Enumerable.Repeat (5, 3))
Console.Write (i + " "); // 5 5 5
```






# LINQ to XML

## DOM
```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<customer id="123" status="archived">
<firstname>Joe</firstname>
<lastname>Bloggs</lastname>
</customer>

```

## X-DOM
```cs
string xml = @"<customer id='123' status='archived'>
<firstname>Joe</firstname>
<lastname>Bloggs<!--nice name--></lastname>
</customer>";
XElement customer = XElement.Parse (xml);
```




## Loading and Parsing
```cs

XDocument fromWeb = XDocument.Load ("http://albahari.com/sample.xml");
XElement fromFile = XElement.Load (@"e:\media\somefile.xml");
XElement config = XElement.Parse (
@"<configuration>
<client enabled='true'>
<timeout>30</timeout>
</client>
</configuration>");

foreach (XElement child in config.Elements())
Console.WriteLine (child.Name); // client
XElement client = config.Element ("client");
bool enabled = (bool) client.Attribute ("enabled"); // Read attribute

Console.WriteLine (enabled); // True
client.Attribute ("enabled").SetValue (!enabled); // Update attribute
int timeout = (int) client.Element ("timeout"); // Read element
Console.WriteLine (timeout); // 30
client.Element ("timeout").SetValue (timeout * 2); // Update element
client.Add (new XElement ("retries", 3)); // Add new elememt
Console.WriteLine (config); // Implicitly call config.ToString()

//Output
<configuration>
<client enabled="false">
<timeout>60</timeout>
<retries>3</retries>
</client>
</configuration



```




## Functional Construction
```cs
XElement customer =
new XElement ("customer", new XAttribute ("id", 123),
new XElement ("firstname", "joe"),
new XElement ("lastname", "bloggs",
new XComment ("nice name")
)
);
```


## Automatic Deep Cloning
```cs
var address = new XElement ("address",
new XElement ("street", "Lawley St"),
new XElement ("town", "North Beach")
);
var customer1 = new XElement ("customer1", address);
var customer2 = new XElement ("customer2", address);
customer1.Element ("address").Element ("street").Value = "Another St";
Console.WriteLine (
customer2.Element ("address").Element ("street").Value); // Lawley St
```


## FirstNode, LastNode, and Nodes
```cs
var bench = new XElement ("bench",
new XElement ("toolbox",
new XElement ("handtool", "Hammer"),
new XElement ("handtool", "Rasp")
),
new XElement ("toolbox",
new XElement ("handtool", "Saw"),
new XElement ("powertool", "Nailgun")
),
new XComment ("Be careful with the nailgun")
);
foreach (XNode node in bench.Nodes())
Console.WriteLine (node.ToString (SaveOptions.DisableFormatting) + ".");

//Output
<toolbox><handtool>Hammer</handtool><handtool>Rasp</handtool></toolbox>.
<toolbox><handtool>Saw</handtool><powertool>Nailgun</powertool></toolbox>.
<!--Be careful with the nailgun-->.

```


## Updating an X-DOM
```cs
XElement settings = new XElement ("settings");
settings.SetElementValue ("timeout", 30); // Adds child node
settings.SetElementValue ("timeout", 60); // Update it to 60


XElement items = new XElement ("items",
new XElement ("one"),
new XElement ("three")
);
items.FirstNode.AddAfterSelf (new XElement ("two"));


XElement items = XElement.Parse ("<items><one/><two/><three/></items>");
items.FirstNode.ReplaceWith (new XComment ("One was here"));



```


## Working with Values
```cs
//Setting Values
var e = new XElement ("date", DateTime.Now);
e.SetValue (DateTime.Now.AddDays(1));
Console.Write (e.Value); // 2007-03-02T16:39:10.734375+09:00

//Getting Values
XElement e = new XElement ("now", DateTime.Now);
DateTime dt = (DateTime) e;
XAttribute a = new XAttribute ("resolution", 1.234);
double res = (double) a;


//Values and Mixed Content Nodes
XElement summary = new XElement ("summary",
new XText ("An XAttribute is "),
new XElement ("bold", "not"),
new XText (" an XNode")
);

//Automatic XText Concatenation
var e = new XElement ("test", new XText ("Hello"), new XText ("World"));
Console.WriteLine (e.Value); // HelloWorld
Console.WriteLine (e.Nodes().Count()); // 2






```

## Documents and Declarations
```cs
var doc = new XDocument (
new XElement ("test", "data")
);

Console.WriteLine (doc.Root.Name.LocalName); // html
XElement bodyNode = doc.Root.Element (ns + "body");
Console.WriteLine (bodyNode.Document == doc); // True


var doc = new XDocument (
new XDeclaration ("1.0", "utf-16", "yes"),
new XElement ("test", "data")
);
doc.Save ("test.xml");


//Writing a declaration to a string
var doc = new XDocument (
new XDeclaration ("1.0", "utf-8", "yes"),
new XElement ("test", "data")
);
var output = new StringBuilder();
var settings = new XmlWriterSettings { Indent = true };
using (XmlWriter xw = XmlWriter.Create (output, settings))
doc.Save (xw);
Console.WriteLine (output.ToString());

//Output
<?xml version="1.0" encoding="utf-16" standalone="yes"?>
<test>data</test>




```



## Updating an X-DOM
```cs
```


