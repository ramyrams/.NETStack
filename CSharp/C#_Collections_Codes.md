* [C# Advanced](https://github.com/TelerikAcademy/CSharp-Part-2)

* System.Collections.Generic
  * [List&lt;T&gt;](#listt)
  * [SortedList&lt;TKey,TValue&gt;](#sortedlisttkeytvalue)
  * [Dictionary&lt;TKey,TValue&gt;](#dictionarytkeytvalue)	
  * [SortedDictionary&lt;TKey,TValue&gt;](#sorteddictionarytkeytvalue)
  * [LinkedList&lt;T&gt;](#linkedlistt)	
  * [Queue&lt;T&gt;](#queuet)	
  * [Stack&lt;T&gt;](#stackt)
  * [HashSet&lt;T&gt;](#hashsett)	
  * [SortedSet&lt;T&gt;](#sortedsett)
  * [Comparer&lt;T&gt;]()	
  * [KeyValuePair&lt;TKey,TValue&gt;]() 
  * [EqualityComparer&lt;T&gt;]()	
  * [KeyedByTypeCollection&lt;TItem&gt;]()
  * [LinkedListNode&lt;T&gt;]()	
  * [SynchronizedCollection&lt;T&gt;]()
  * [SynchronizedKeyedCollection&lt;K,T&gt;]()
  * [SynchronizedReadOnlyCollection&lt;T&gt;]()	

* System.Collections
  * ArrayList
  * BitArray
  * Hashtable
  * SortedList
  * Queue
  * Stack
  * DictionaryEntry

* System.Collections.Specialized
  * HybridDictionary
  * ListDictionary
  * StringCollection
  * BitVector32
  * NameValueCollection


* System.Collections.Concurrent
  * ConcurrentQueue<T>	
  * ConcurrentStack<T>
  * ConcurrentBag<T>	
  * ConcurrentDictionary<TKey,TValue>
  * BlockingCollection<T>	
  * OrderablePartitioner<TSource>
  * Partitioner	
  * Partitioner<TSource>	


* System.Collections.ObjectModel
  * ReadOnlyCollection<T>	
  * ReadOnlyObservableCollection<T>
  * KeyedCollection<TKey,TItem>	
  * ObservableCollection<T>	
  * ReadOnlyDictionary<TKey,TValue>	





## List&lt;T&gt;
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

```


# SortedList&lt;TKey,TValue&gt;
```cs
var sortedList = new SortedList<int, string>();
sortedList.Add(1, "one");
sortedList.Add(2, "two");
sortedList.Add(3, "three");
sortedList.Add(4, "four");

// returns true
sortedList.ContainsKey(1);

// returns true
sortedList.ContainsValue("two");

// get index of key
sortedList.IndexOfKey(1);

// get index of value
sortedList.IndexOfValue("two");

// remove by key
sortedList.Remove(3);

// remove by index
sortedList.RemoveAt(2);

// lookup by key
string value = sortedList[2];

// get value by index
string value = sortedList.Values[2];

// get key by index
int key = sortedList.Keys[2];

string value;
if (sortedList.TryGetValue(4, out value))
    //do something

foreach (int key in sortedList.Keys)
{
    Console.WriteLine(key);
}

foreach (string value in sortedList.Values)
{
    Console.WriteLine(value);
}            

//removes all elements
sortedList.Clear();

bool contains1 = sorted.ContainsKey("java");

int value;
if (sorted.TryGetValue("perls", out value))
{
    Console.WriteLine("perls key is = " + value);
}

int index1 = sorted.IndexOfKey("net");
int index2 = sorted.IndexOfValue(3);

```

# Dictionary&lt;TKey,TValue&gt;
```cs
Dictionary<int, string> dic =  new Dictionary<int, string>();
dic.Add(1, "data1");   
dic.Add(0, "data2");   
dic.Add(-1, "data3");

Dictionary<string, int> dic = new Dictionary<string, int>(200);

if (dic.ContainsKey(-1)) }} (dic.ContainsValue("data1")){
string value = dic[-1]; //data3
}

foreach (KeyValuePair<int, string> pair in dic) {
    Console.WriteLine("{0}, {1}", pair.Key, pair.Value);
}
foreach (var pair in dic) {
    Console.WriteLine("{0}, {1}", pair.Key, pair.Value);
}
//get all the keys
List<int> list = new List<int>(dic.Keys);

string[] arr = new string[] { "One", "Two" };
var dict = arr.ToDictionary(item => item, item => true);

dic.Remove(-1); // Removes cat.
dic.Remove(99); // Doesn't remove anything.

dic.Clear();

if (dictionary.TryGetValue(9999, out name)) {  }

```



# SortedDictionary&lt;TKey,TValue&gt;
```cs
SortedDictionary<int, string> sorted = new SortedDictionary<int,string>();
sorted.Add(2, "2");
sorted.Add(3, "3");
sorted.Add(1, "1");
Console.WriteLine("The sorted list of keys are");
foreach (string name in sorted.Keys) {
 Console.WriteLine(name);
}

```

# LinkedList(T)
```cs
LinkedList<String> llist1 = new LinkedList<String>();

LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like" });
llist.AddAfter(llist.Last, new LinkedListNode<string>("dogs"));
llist.AddAfter(llist.Last, "dogs");
llist.AddBefore(llist.First, new LinkedListNode<string>("I"));

LinkedListNode<string> foundNode = llist.Find("like");
llist.AddBefore(foundNode, "I");
llist.Remove(foundNode);

llist.AddFirst("I");
llist.AddFirst(new LinkedListNode<string>("I"));

llist.AddLast("dogs");
llist.AddLast(new LinkedListNode<string>("dogs"));

llist.Clear();
llist.Remove("don't");

llist.RemoveFirst();
llist.RemoveLast();

string[] s = llist.ToArray();

Console.WriteLine(llist.First.Value);
Console.WriteLine(llist.Last.Value);
Console.WriteLine(llist.Count);

```

# Queue(T)
```cs
var queue = new Queue<string>();
Queue<int> queue = new Queue<int>();
Queue<int> queue = new Queue<int>(100);

int[] values = new int[] { 34, 2, 1, 88, 53 };
Queue<int> queue = new Queue<int>(values);

//Adding Items to the Queue
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
queue.Enqueue(33);

//Items can be removed from the queue by using the Clear and Dequeue methods. 
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
queue.Clear();

Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
Console.WriteLine(queue.Dequeue());

//Checking the Queue
// use the Peek method when you want to view the 
//first element in the queue without changing the contents of it.
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
Console.WriteLine(queue.Peek()); //Output: 22

// Get the number of items in the queue
var count = queue.Count;

Console.WriteLine(queue.Contains(6) ? "Yes" : "No");
```

# Stack&lt;T&gt;
```cs
//Creating a Stack
Stack<int> stack = new Stack<int>();

int[] values = new int[] { 34, 2, 1, 88, 53 };
Stack<int> stack = new Stack<int>(values);

//Adding Items to the Stack
Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
stack.Push(46);

Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
Console.WriteLine(stack.Pop());

//Removing Items from the Stack
Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
stack.Clear();
```


# HashSet&lt;T&gt;
```cs
var hashSet1 = new HashSet<string>();            
hashSet1.Add("one");
hashSet1.Add("two");
hashSet1.Add("three");
hashSet1.Add("four");

var hashSet2 = new HashSet<string>();
hashSet2.Add("two");
hashSet2.Add("four");

hashSet1.Contains("three");

// sortedSet1 now contains one, three
hashSet1.ExceptWith(hashSet2);

// sortedSet1 now contains two, four
hashSet1.IntersectWith(hashSet2);

// a subset is a set whose elements are all in another set
hashSet1.IsSubsetOf(hashSet2);

// a superset is a set which contains all elements
// in another set
hashSet1.IsSupersetOf(hashSet2);

// a proper subset is a subset which is not equal
hashSet1.IsProperSubsetOf(hashSet2);

// a proper superset is a superset which is not equal
hashSet1.IsProperSupersetOf(hashSet2);            

// returns bool if both sets contain any of the same items
hashSet1.Overlaps(hashSet2);

// removes the element with value "two"
hashSet1.Remove("two");

// removes all elements that match the predicate
hashSet1.RemoveWhere(v => v == "three");

// returns true if both sets are identical
hashSet1.SetEquals(hashSet2);

// sortedSet1 now contains one, three
// only items which are in one or the other, not both
hashSet1.SymmetricExceptWith(hashSet2);

// sortedSet1 now contains one, two, three, four
// all items in both sets
hashSet1.UnionWith(hashSet2);

// elements are no in any guaranteed order
foreach (string value in hashSet1)
{                
}

// remove all items in both sets
hashSet1.Clear();

//RemoveWhere(Predicate(T) match)
delegate bool Predicate<T>(T obj);

static bool IsEven(int value)
{
    return (value % 2) == 0;
}

HashSet<int> hs = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
hs.RemoveWhere(IsEven);
hs.RemoveWhere(item => { return (item % 2) == 0; });
```

# SortedSet&lt;T&gt;
```cs
var elements = new SortedSet<int>() { 5, 9, 2, 11, 2, 1, 4, 1, 2 };

foreach (int element in elements)  
   Console.Write(string.Format(" {0}", element));
	//Output: 1 2 4 5 9 11   

bool result = elements.Add(17); //1 2 4 5 9 11 17

//Getting a Subset of a SortedSet<T> Collection
var subSet = elements.GetViewBetween(2, 9);
//Output: 2 4 5 9        
//Removing Element(s) from a SortedSet<T> Collection
elements.Remove(1);

// predicate - get event number
elements.RemoveWhere(P => P % 2 == 0);

//Max and Min Values of a SortedSet<T> Collection
int max = elements.Max, min = elements.Min;

//Union(U), Intersection(∩) and Difference(-) operations
var A = new SortedSet<int>() { 1, 2, 3, 4, 5, 11, };
var B = new SortedSet<int>() { 6, 7, 8, 9, 10, 11 };    
var union = A.Union(B);
foreach (int element in union)
   Console.Write(string.Format(" {0}", element));
//Output (AUB): 1 2 3 4 5 11 6 7 8 9 10

var intersection = A.Intersect(B); //Output (A∩B): 11
var difference = A.Except(B); // Output (A-B): 1 2 3 4 5  

//Merging of two SortedSet<T> Collection 
var merged = A.Zip(B, (P, Q) => P + Q);
//7 9 11 13 15 22

//CopyTo Method of SortedSet<T> Collection
var target = new SortedSet<int>() {13, 2, 4, 10, 1, 7 };
int[] array = new int[10];
target.CopyTo(array);
```



#KeyValuePair<TKey,TValue>
```cs
KeyValuePair<int, string> p2 = new KeyValuePair<int, string>(4, "perls");

// Shows a List of KeyValuePairs.
var list = new List<KeyValuePair<string, int>>();
list.Add(new KeyValuePair<string, int>("Cat", 1));
```





# END OF Collection


# ObservableCollection
``` cs
// Make a collection to observe and add a few Person objects.
ObservableCollection<Person> people = new ObservableCollection<Person>()
{
new Person{ FirstName = "Peter", LastName = "Murphy", Age = 52 },
new Person{ FirstName = "Kevin", LastName = "Key", Age = 48 },
};
// Wire up the CollectionChanged event.
people.CollectionChanged += people_CollectionChanged;
// Now add a new item.
people.Add(new Person("Fred", "Smith", 32));

// Remove an item.
people.RemoveAt(0);


static void people_CollectionChanged(object sender, System.Collections.Specialized.NotifyCollectionChangedEventArgs e)
{
   // What was the action that caused the event?
	Console.WriteLine("Action for this event: {0}", e.Action);

	// They removed something. 
	if (e.Action == System.Collections.Specialized.NotifyCollectionChangedAction.Remove)
	{
		Console.WriteLine("Here are the OLD items:");
		foreach (Person p in e.OldItems)
		{
			Console.WriteLine(p.ToString());
		}
		Console.WriteLine();
	}

	// They added something. 
	if (e.Action == System.Collections.Specialized.NotifyCollectionChangedAction.Add)
	{
		// Now show the NEW items that were inserted.
		Console.WriteLine("Here are the NEW items:");
		foreach (Person p in e.NewItems)
		{
			Console.WriteLine(p.ToString());
		}
	}
}

public enum NotifyCollectionChangedAction
{
	Add = 0,
	Remove = 1,
	Replace = 2,
	Move = 3,
	Reset = 4,
}
```


# Collection


## SortedDictionary(TKey, TValue)
```cs
SortedDictionary<string, int> sorted = new SortedDictionary<string, int>();
sorted.Add("one", 1);
sorted.Add("two", 2);
sorted.Add("three", 3);
sorted.Add("four", 4);
sorted.Add("five", 5);
sorted.Add("six", 6);
Console.WriteLine("The sorted list of keys are");
foreach (string name in sorted.Keys)
{
 Console.WriteLine(name);
}
Console.WriteLine();
```


## CollectionBase

```cs
void OnValidate

//The following code snippets can be used within OnValidate to check whether the item is a Timer.
if (value != null && !(value is System.Timers.Timer))
{
 throw new ArgumentException("value must be of type System.Timers.Timer.", "value");
}


// The following code snippets can be used within OnValidate to check whether the object is the value type int.
if (value == null || !(value is int))
{
 throw new ArgumentException("value must be of type int.", "value");
}

//void OnClear() and void OnClearComplete()
OnClear();
InnerList.Clear();
OnClearComplete();


//You could then set the cleared items in the array by doing the following in your OnClear method.
m_clearItems = InnerList.ToArray();

//void OnInsert(int index, Object value) and void OnInsertComplete(int index, Object value)

OnValidate(value);
OnInsert(index, value);
InnerList.Insert(index, value);
try
{
 OnInsertComplete(index, value);
}
catch
{
 InnerList.RemoveAt(index);
 throw;
}


protected override void OnInsertComplete(int index, object value)
{
 try
 {
 base.OnInsertComplete(index, value);
 // Code to do after the insert has completed
 }
 catch
 
 // Undo OnInsert
 throw;
 }
}

void OnRemove(int index, object value) and void OnRemoveComplete(int index, object value)
OnValidate(value);
int index = InnerList.IndexOf(value);
if (index < 0)
{
 throw new ArgumentException("Index out of range");
}
OnRemove(index, value);
InnerList.RemoveAt(index);
try
{
 OnRemoveComplete(index, value);
}
catch
{
 InnerList.Insert(index, value);
 throw;
}


protected override void OnRemoveComplete(int index, object value)
{
 try
 {
 base.OnRemoveComplete(index, value);
 // Code to do after the remove has completed
 }
 catch
 {
 // Undo OnRemove
 throw;
 }
}

void OnSet(int index, object oldValue, object newValue) and void OnSetComplete(int index, object oldValue, object newValue)

OnValidate(value);
object oldValue = InnerList[index];
OnSet(index, oldValue, value);
InnerList[index] = value;
try
{
 OnSetComplete(index, oldValue, value);
}
catch
{
 InnerList[index] = oldValue;
 throw;
}


protected override void OnSetComplete(int index, object oldValue, object newValue)
{
 try
 {
 base.OnSetComplete(index, oldValue, newValue);
 // Code to do after the set has completed
 }
 catch
 
 // Undo OnSet
 throw;
 }
}
```


## DictionaryBase
```cs
void OnValidate(object key, object value)
void OnClear() and void OnClearComplete()

OnClear();
InnerHashtable.Clear();
OnClearComplete();


//void OnGet()
object currentValue =InnerHashtable[key];
OnGet(key, currentValue);
return currentValue;

//void OnInsert(Object key, Object value) and void OnInsertComplete(Object key, Object value)

C#
OnValidate(key, value);
OnInsert(key, value);
InnerHashtable.Add(key, value);
try
{
 OnInsertComplete(key, value);
}
catch
{
 InnerHashtable.Remove(key);
 throw;
}

void OnRemove(Object key, Object value) and void OnRemoveComplete(Object key, Object value)
if (InnerHashtable.Contains(key))
{
 object obj2 = InnerHashtable[key];
 OnValidate(key, obj2);
 OnRemove(key, obj2);
 InnerHashtable.Remove(key);
 try
 {
 OnRemoveComplete(key, obj2);
 }
 catch
 {
 InnerHashtable.Add(key, obj2);
 throw;
 }
}

void OnSet(Object key, object oldValue, object newValue) and void OnSetComplete(Object key, object oldValue, object newValue)
OnValidate(key, value);
bool flag = true;
object oldValue = InnerHashtable[key];
if (oldValue == null)
{
 flag = InnerHashtable.Contains(key);
}
OnSet(key, oldValue, value);
InnerHashtable[key] = value;
try
{
 OnSetComplete(key, oldValue, value);
}
catch
{
 if (flag)
 {
 InnerHashtable[key] = oldValue;
 }
 else
 {
 InnerHashtable.Remove(key);
 }
 throw;
}

```

## HashSet(T)
```cs
HashSet<int> a = new HashSet<int>();

HashSet<int> a = new HashSet<int>( new int [] { 2 , 4, 5 } );

HashSet<string> a = new HashSet<string>(StringComparer.CurrentCultureIgnoreCase);

HashSet<string> a = new HashSet<string>(new string[] {"hi", "hola", "Hi"},  StringComparer.CurrentCultureIgnoreCase);

HashSet<string> hs = new HashSet<string>(StringComparer.CurrentCultureIgnoreCase);
hs.Add("hi");
hs.Add("Hi");
hs.Add("hola");

HashSet<string> hs = new HashSet<string>(StringComparer.CurrentCultureIgnoreCase);
hs.Add("hi");
hs.Add("hola");

HashSet<int> hs = new HashSet<int>(new int[] { 1, 6, 2, 3 });
hs.Remove(6);

//RemoveWhere(Predicate(T) match)
delegate bool Predicate<T>(T obj);

static bool IsEven(int value)
{
 return (value % 2) == 0;
}

HashSet<int> hs = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
hs.RemoveWhere(IsEven);

HashSet<int> hs = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
hs.RemoveWhere(item => { return (item % 2) == 0; });

HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> primes = new HashSet<int>(new int[] { 2, 5, 7 });
HashSet<int> oddPrimes = new HashSet<int>(odds);
oddPrimes.IntersectWith(primes);


HashSet<int> numbers = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
HashSet<int> reversedNumbers = new HashSet<int>(new int[] { 9, 8, 7, 6, 5, 4, 3, 2, 1 });
Console.WriteLine("Evens {0} a proper subset of numbers.",  evens.IsProperSubsetOf(numbers) ? "is" : "is not");
Console.WriteLine("Reversednumbers {0} a proper subset of numbers.",  reversedNumbers.IsProperSubsetOf(numbers) ? "is" : "is not");
 
 
 HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> numbers = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
Console.WriteLine("Evens {0} a subset of numbers.",
 evens.IsSubsetOf(numbers) ? "are" : "are not");
Console.WriteLine("Evens {0} a subset of odds.",
 evens.IsSubsetOf(odds) ? "are" : "are not");
 
 
 HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> numbers = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
Console.WriteLine("Evens {0} a superset of numbers.",
 evens.IsSupersetOf(numbers) ? "are" : "are not");
Console.WriteLine("Numbers {0} a superset of odds.",
 numbers.IsSupersetOf(odds) ? "are" : "are not");
 
 HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> numbers = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
Console.WriteLine("Evens {0} with numbers.",
 evens.Overlaps(numbers) ? "overlaps" : "does not overlap");
Console.WriteLine("Evens {0} with odds.",
 evens.Overlaps(odds) ? "overlaps" : "does not overlap");
 
 HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> numbers = new HashSet<int>(odds);
numbers.UnionWith(evens);


HashSet<int> odds = new HashSet<int>(new int[] { 1, 3, 5, 7, 9 });
HashSet<int> numbers = new HashSet<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
HashSet<int> evens = new HashSet<int>(numbers);
evens.ExceptWith(odds);
 
 
 HashSet<int> evens = new HashSet<int>(new int[] { 2, 4, 6, 8 });
Console.WriteLine("Evens {0} 1.", evens.Contains(1) ? "contains" : "doesn't contain");
Console.WriteLine("Evens {0} 2.", evens.Contains(2) ? "contains" : "doesn't contain");

void TrimExcess()

```

## DictionaryEntry
```cs
// Create hashtable with some keys and values.
Hashtable hashtable = new Hashtable();
hashtable.Add(1, "one");
hashtable.Add(2, "two");
hashtable.Add(3, "three");

// Enumerate the hashtable.
foreach (DictionaryEntry entry in hashtable)
{
    Console.WriteLine("{0} = {1}", entry.Key, entry.Value);
}
```

## BitArray
```cs
//Creating a BitArray
BitArray x = new BitArray(8, false);
x.Set(2, true);
BitArray y = new BitArray(x);


BitArray bits = new BitArray(new bool[] { false, true, false, false });



BitArray bits = new BitArray(new byte[] { 1, 2 });


BitArray bits = new BitArray(4, true);



BitArray bits = new BitArray(4);
bits.Set(0, true);
bits.Set(1, true);


BitArray bits = new BitArray(4);
bits.SetAll(true);



BitArray bits = new BitArray(new byte[] { 3 });
Console.Write("3 is stored as ");
for (int i = bits.Length - 1; i >= 0; --i)
{
 Console.Write(bits.Get(i) ? "1" : "0");
}
Console.WriteLine();




BitArray bits = new BitArray(4);
Console.WriteLine("bit 0 is {0}", bits[0]);
Console.WriteLine("Negating bit 0");
bits[0] = !bits[0];
Console.WriteLine("bit 0 is now {0}", bits[0]);



[Flags()]
public enum FileFlags
{
 IsArchived = 0,
 IsReadOnly = 1,
 IsCompressed = 2,
 IsHidden = 3,
 NUM_FLAGS
}



BitArray bits = FlagsToBitArray(FileFlags.IsCompressed, FileFlags.IsArchived,
 FileFlags.IsHidden);
Console.WriteLine("bits = {0}", FlagsToString(bits));
Console.WriteLine("Keep only IsArchived on if it is on");
bits = bits.And(FlagsToBitArray(FileFlags.IsArchived));
Console.WriteLine("bits = {0}", FlagsToString(bits));



BitArray bits = FlagsToBitArray(FileFlags.IsCompressed, FileFlags.IsArchived,
 FileFlags.IsHidden);
Console.WriteLine("bits = {0}", FlagsToString(bits));
Console.WriteLine("Flip all flags");
bits = bits.Not();
Console.WriteLine("bits = {0}", FlagsToString(bits));



BitArray bits = FlagsToBitArray(FileFlags.IsCompressed, FileFlags.IsArchived,
 FileFlags.IsHidden);
Console.WriteLine("bits = {0}", FlagsToString(bits));
Console.WriteLine("Turning IsReadOnly flag on");
bits = bits.Or(FlagsToBitArray(FileFlags.IsReadOnly));
Console.WriteLine("bits = {0}", FlagsToString(bits));



BitArray bits = new BitArray(new byte[]
 { (byte)'h', (byte)'e', (byte)'l', (byte)'l', (byte)'o' });
BitArray key = new BitArray(new byte[] { 99, 88, 55, 22, 11 });
Console.WriteLine("string = {0}", PrintString(bits));
Console.WriteLine("Encrypting");
bits = bits.Xor(key);
Console.WriteLine("string = {0}", PrintString(bits));
Console.WriteLine("Decrypting");
bits = bits.Xor(key);
Console.WriteLine("string = {0}", PrintString(bits));
```


Queue(T) 
```cs
Queue<int> queue = new Queue<int>();


int[] values = new int[] { 34, 2, 1, 88, 53 };
Queue<int> queue = new Queue<int>(values);


Queue<int> queue = new Queue<int>(100);

//Adding Items to the Queue
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
queue.Enqueue(33);

//Items can be removed from the queue by using the Clear and Dequeue methods. 
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
queue.Clear();


Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
Console.WriteLine(queue.Dequeue());

//Checking the Queue
// use the Peek method when you want to view the first element in the queue without changing the contents of it.
Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
Console.WriteLine(queue.Peek());

Output
22



Queue<int> queue = new Queue<int>(new int [] { 22, 3, 6, 19 });
Console.WriteLine("Does the queue contain a 6? {0}", queue.Contains(6) ? "Yes" : "No");
Console.WriteLine("Does the queue contain a 5? {0}", queue.Contains(5) ? "Yes" : "No");



Queue<int> queue = new Queue<int>(new int[] { 22, 3, 6, 19});
Console.WriteLine("The queue contains {0} items.", queue.Count);

//Cleaning the Queue

```

Stack(T)
```cs
//Creating a Stack
Stack<int> stack = new Stack<int>();

int[] values = new int[] { 34, 2, 1, 88, 53 };
Stack<int> stack = new Stack<int>(values);


Stack<int> stack = new Stack<int>(100);


//Adding Items to the Stack

Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
stack.Push(46);

//Removing Items from the Stack
Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
stack.Clear();


Stack<int> stack = new Stack<int>(new int[] { 6, 87, 13, 29, 7 });
Console.WriteLine(stack.Pop());

//Checking the Stack
Checking the Stack
```

## Dictionary(TKey,TValue)
```cs

//Creating a Dictionary
Dictionary<string, int> dictionary = new Dictionary<string, int>();



Dictionary<string, int> dictionary = new Dictionary<string, int>();
dictionary["one"] = 1;
dictionary["two"] = 2;
dictionary["three"] = 3;



Dictionary<string, int> dictionary = new Dictionary<string, int>
 (StringComparer.CurrentCultureIgnoreCase);
dictionary["one"] = 1;
dictionary["two"] = 2;
dictionary["three"] = 3;
int one = dictionary["One"];



Dictionary<string, int> dictionary = new Dictionary<string, int>(200);


//Adding Items to a Dictionary
Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary.Add(9688, "Barbara Zighetti");
dictionary.Add(9689, "Eric Gruber");



Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";

//Removing Items from a Dictionary


Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
dictionary.Clear();


Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
dictionary.Remove(9689);


Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
try
{
 string name;
 if (dictionary.TryGetValue(9999, out name))
 {
 Console.WriteLine("\"{0}\" is associated with 9999", name);
 }

else
 {
 Console.WriteLine("9999 wasn't found in the dictionary");
 }
}
catch (Exception)
{
 Console.WriteLine("An exception was thrown.");
}




Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
Console.WriteLine("\"{0}\" is associated with 9689", dictionary[9689]);
try
{
 Console.WriteLine("\"{0}\" is associated with 9690", dictionary[9690]);
}
catch (KeyNotFoundException ex)
{
 Console.WriteLine("9890 wasn't found in the dictionary");
}


//Checking the Dictionary
Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
if (dictionary.ContainsKey(9689))
{
 Console.WriteLine("9689 was found in the dictionary");
}
else
{
 Console.WriteLine("9689 was not found in the dictionary");
}
if (dictionary.ContainsKey(9690))
{
 Console.WriteLine("9690 was found in the dictionary");
}
else
{
 Console.WriteLine("9690 was not found in the dictionary");
}




Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
if (dictionary.ContainsValue("Barbara Zighetti"))
{
 Console.WriteLine("\"Barbara Zighetti\" was found in the dictionary");
}
else
{
 Console.WriteLine("\"Barbara Zighetti\" was not found in the dictionary");
}
if (dictionary.ContainsValue("David Wright"))
{
 Console.WriteLine("\"David Wright\" was found in the dictionary");
}
else
{
 Console.WriteLine("\"David Wright\" was not found in the dictionary");
}



Dictionary<int, String> dictionary = new Dictionary<int, String>();
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
Console.WriteLine("The dictionary contains {0} items.", dictionary.Count);




Dictionary<int, String> dictionary = new Dictionary<int, String>();
Dictionary<int, String>.KeyCollection keys = dictionary.Keys;
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
Console.WriteLine("The keys in the dictionary are: ");
Print(keys.ToArray());
Console.WriteLine("Adding [9687,\"David Wright\"]");
dictionary[9687] = "David Wright";
Console.WriteLine("The keys in the dictionary are: ");
Print(keys.ToArray());




Dictionary<int, String> dictionary = new Dictionary<int, String>();
Dictionary<int, String>.ValueCollection values = dictionary.Values;
dictionary[9688] = "Barbara Zighetti";
dictionary[9689] = "Eric Gruber";
Console.WriteLine("The values in the dictionary are: ");
Print(values.ToArray());
Console.WriteLine("Adding [9687,\"David Wright\"]");
dictionary[9687] = "David Wright";
Console.WriteLine("The values in the dictionary are: ");
Print(values.ToArray());
```






## ArrayList


```cs
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
```

## BitArray
```cs


// Create BitArray from the array.
BitArray bitArray = new BitArray(32);

// Set three bits to 1.
bitArray[3] = true;     // You can set the bits with the indexer.
bitArray[5] = true;
bitArray.Set(10, true); // You can set the bits with Set.

// Count returns the total of all bits (1s and 0s).
Console.WriteLine("--- Total bits ---");
Console.WriteLine(bitArray.Count);
	
	
// Creates and initializes several BitArrays.
BitArray myBA1 = new BitArray( 5 );

BitArray myBA2 = new BitArray( 5, false );

byte[] myBytes = new byte[5] { 1, 2, 3, 4, 5 };
BitArray myBA3 = new BitArray( myBytes );

bool[] myBools = new bool[5] { true, false, true, true, false };
BitArray myBA4 = new BitArray( myBools );

int[]  myInts  = new int[5] { 6, 7, 8, 9, 10 };
BitArray myBA5 = new BitArray( myInts );

// Displays the properties and values of the BitArrays.
Console.WriteLine( "myBA1" );
Console.WriteLine( "   Count:    {0}", myBA1.Count );
Console.WriteLine( "   Length:   {0}", myBA1.Length );
Console.WriteLine( "   Values:" );
PrintValues( myBA1, 8 );


//creating two  bit arrays of size 8
BitArray ba1 = new BitArray(8);
BitArray ba2 = new BitArray(8);
byte[] a = { 60 };
byte[] b = { 13 };

//storing the values 60, and 13 into the bit arrays
ba1 = new BitArray(a);
ba2 = new BitArray(b);

//content of ba1
Console.WriteLine("Bit array ba1: 60");

for (int i = 0; i < ba1.Count; i++)
{
Console.Write("{0, -6} ", ba1[i]);
}
Console.WriteLine();

//content of ba2
Console.WriteLine("Bit array ba2: 13");

for (int i = 0; i < ba2.Count; i++)
{
Console.Write("{0, -6} ", ba2[i]);
}
Console.WriteLine();
BitArray ba3 = new BitArray(8);
ba3 = ba1.And(ba2);

//content of ba3
Console.WriteLine("Bit array ba3 after AND operation: 12");

for (int i = 0; i < ba3.Count; i++)
{
Console.Write("{0, -6} ", ba3[i]);
}
Console.WriteLine();
ba3 = ba1.Or(ba2);

//content of ba3
Console.WriteLine("Bit array ba3 after OR operation: 61");

for (int i = 0; i < ba3.Count; i++)
{
Console.Write("{0, -6} ", ba3[i]);
}
Console.WriteLine();

Console.ReadKey();
}

Bit array ba1: 60 
False False True True True True False False 
Bit array ba2: 13
True False True True False False False False 
Bit array ba3 after AND operation: 12
False False True True False False False False 
Bit array ba3 after OR operation: 61
True False True True False False False False 
		
	  
```

## Hashtable
```cs
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

```

## LinkedList(T) 
```cs
LinkedList<String> llist = new LinkedList<String>();



LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like" });
llist.AddAfter(llist.Last, new LinkedListNode<string>("dogs"));


LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like" });
llist.AddAfter(llist.Last, "dogs");



LinkedList<string> llist = new LinkedList<string>(new string[] { "like", "dogs" });
llist.AddBefore(llist.First, new LinkedListNode<string>("I"));


LinkedList<string> llist = new LinkedList<string>(new string[] { "like", "dogs" });
LinkedListNode<string> foundNode = llist.Find("like");
llist.AddBefore(foundNode, "I");


LinkedList<string> llist = new LinkedList<string>(new string[] { "like", "dogs" });
llist.AddFirst("I");



LinkedList<string> llist = new LinkedList<string>(new string[] { "like", "dogs" });
llist.AddFirst(new LinkedListNode<string>("I"));


LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like" });
llist.AddLast("dogs");

LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like" });
llist.AddLast(new LinkedListNode<string>("dogs"));


LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "love", "dogs" });
llist.Clear();


LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "don't", "like", "dogs" });
llist.Remove("don't");




LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "don't", "like", "dogs" });
LinkedListNode<string> removeNode = llist.Find("don't");
llist.Remove(removeNode);



LinkedList<int> llist = new LinkedList<int>(new int[] { 1, 1, 2, 3, 4 });
llist.RemoveFirst();


LinkedList<int> llist = new LinkedList<int>(new int[] { 1, 2, 3, 4, 4 });
llist.RemoveLast();




LinkedList<int> llist = new LinkedList<int>(new int[] { 1, 2, 4, 4, 4, 6 });

Print(llist.ToArray());
llist.Find(4).Value = 3;
llist.FindLast(4).Value = 5;
Print(llist.ToArray());



LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "love", "dogs" });
Console.WriteLine(llist.First.Value);
Console.WriteLine(llist.Last.Value);


LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like", "dogs" });
Console.WriteLine("The list contains {0} nodes.", llist.Count);



LinkedList<string> llist = new LinkedList<string>(new string[] { "I", "like", "dogs" });
Console.WriteLine("Does the list contain \"dogs\"? {0}",
 llist.Contains("dogs") ? "Yes" : "No");
Console.WriteLine("Does the list contain \"cats\"? {0}",
 llist.Contains("cats") ? "Yes" : "No");

```


## Queue
```cs
// Creates and initializes a new Queue.
Queue myQ = new Queue();
myQ.Enqueue("Hello");
myQ.Enqueue("World");
myQ.Enqueue("!");

// Displays the properties and values of the Queue.
Console.WriteLine( "myQ" );
Console.WriteLine( "\tCount:    {0}", myQ.Count );
	   
	   
```
```cs

// 1
// Initialize help requeust Queue
Queue<RequestType> help = new Queue<RequestType>();

// 2
// ASP.NET website records a Text Problem help request.
help.Enqueue(RequestType.TextProblem);

// 3
// ASP.NET website records a Screen Problem help request.
help.Enqueue(RequestType.ScreenProblem);

// 4
// You become available to take a new request.
// You can't help with Mouse problems.
if (help.Count > 0 &&
	help.Peek() != RequestType.MouseProblem)
{
	// 5
	// You solve the request. It was a TextProblem
	help.Dequeue();
}

// 5
// Other parts of your code can access the Queue, testing the elements
// to see if they can process them.

// 6
// ASP.NET website records a Modem Problem help request.
help.Enqueue(RequestType.ModemProblem);
```	


```
// Creates and initializes a new Queue.
Queue myQ = new Queue();
myQ.Enqueue( "The" );
myQ.Enqueue( "quick" );
myQ.Enqueue( "brown" );
myQ.Enqueue( "fox" );

// Displays the Queue.
Console.Write( "Queue values:" );
PrintValues( myQ );

// Removes an element from the Queue.
Console.WriteLine( "(Dequeue)\t{0}", myQ.Dequeue() );

// Displays the Queue.
Console.Write( "Queue values:" );
PrintValues( myQ );

// Removes another element from the Queue.
Console.WriteLine( "(Dequeue)\t{0}", myQ.Dequeue() );

// Displays the Queue.
Console.Write( "Queue values:" );
PrintValues( myQ );

// Views the first element in the Queue but does not remove it.
Console.WriteLine( "(Peek)   \t{0}", myQ.Peek() );

// Displays the Queue.
Console.Write( "Queue values:" );
PrintValues( myQ );
```

## SortedList
```cs
// Creates and initializes a new SortedList.
SortedList mySL = new SortedList();
mySL.Add("Third", "!");
mySL.Add("Second", "World");
mySL.Add("First", "Hello");

-KEY-    -VALUE-
First:    Hello
Second:    World
Third:    !

bool contains1 = sorted.ContainsKey("java");
Console.WriteLine("contains java = " + contains1);

int value;
if (sorted.TryGetValue("perls", out value))
{
	Console.WriteLine("perls key is = " + value);
}
	
int index1 = sorted.IndexOfKey("net");
Console.WriteLine("index of net (key) = " + index1);

int index2 = sorted.IndexOfValue(3);
Console.WriteLine("index of 3 (value) = " + index2);

```

## Stack
```cs
Stack<int> stack = new Stack<int>();
stack.Push(100);
stack.Push(1000);
stack.Push(10000);

// Pop the top element
int pop = stack.Pop();

// Write to the console
Console.WriteLine("--- Element popped from top of Stack ---");
Console.WriteLine(pop);

// Now look at the top element
int peek = stack.Peek();
Console.WriteLine("--- Element now at the top ---");
Console.WriteLine(peek);

// Count the number of elements in the Stack
int count = stack.Count;

Stack.Contains(2); // returns true
myStack.Contains(10); // returns false

// Clear the Stack
stack.Clear();
	
```

## ListDictionary
```cs
// Creates and initializes a new ListDictionary.
ListDictionary myCol = new ListDictionary();
myCol.Add( "Braeburn Apples", "1.49" );
myCol.Add( "Fuji Apples", "1.29" );
myCol.Add( "Gala Apples", "1.49" );
	  
```

## StringCollection
```cs
using System.Collections.Specialized;

// Create and initializes a new StringCollection.
StringCollection myCol = new StringCollection();

// Add a range of elements from an array to the end of the StringCollection.
String[] myArr = new String[] { "RED", "orange", "yellow", "RED", "green", "blue", "RED", "indigo", "violet", "RED" };
myCol.AddRange( myArr );

authorNames.Clear();

int authorLocation = authorNames.IndexOf("Mike Gold");

authorNames.CopyTo(newAuthorList, 0);

	  
```


## BitVector32
```cs
// Creates and initializes a BitVector32 with all bit flags set to FALSE.
      BitVector32 myBV = new BitVector32( 0 );

      // Creates masks to isolate each of the first five bit flags.
      int myBit1 = BitVector32.CreateMask();
      int myBit2 = BitVector32.CreateMask( myBit1 );
	 
// Creates and initializes a BitVector32.
      BitVector32 myBV = new BitVector32( 0 );

      // Creates four sections in the BitVector32 with maximum values 6, 3, 1, and 15.
      // mySect3, which uses exactly one bit, can also be used as a bit flag.
      BitVector32.Section mySect1 = BitVector32.CreateSection( 6 );
      BitVector32.Section mySect2 = BitVector32.CreateSection( 3, mySect1 );
	  
```


## HybridDictionary
```cs
// Creates and initializes a new HybridDictionary.
      HybridDictionary myCol = new HybridDictionary();
      myCol.Add( "Braeburn Apples", "1.49" );
      myCol.Add( "Fuji Apples", "1.29" );
      myCol.Add( "Gala Apples", "1.49" );
	  
```




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

## List<T>

```cs
List<int> a = new List<int>();

List<int> a = new List<int>( new int [] { 2 , 4, 5 } );

List<int> a = new List<int>(100);

List<int> list = new List<int>();
list.Add(2);
list.Add(4);

List<int> list = new List<int>();
list.AddRange( new int []{ 2, 4 });

List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7 });
foreach (int value in list)
{
 	Console.WriteLine(value);
}


List<int> list = new List<int>(new int[] { 1, 6, 2, 3 });
list.Remove(6);


List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8 });
list.Reverse();


List<int> list = new List<int>(new int[] { 1, 2, 3, 7, 6, 5, 4, 8 });
list.Reverse(3, 4);
```



```cs

List<Task> list = new List<Task>();
list.Add(new Task("BACKUP"));
list.Add(new Task("VERFIY"));
list.Add(new Task("MARK_ARCHIVED"));
list.ForEach(ProcessTask);


static void ProcessTask(Task task)
{
 // Nothing to process if the task is null or has already been processed
 if (task == null || task.IsProcessed)
 {
 return;
 }
 // Process the task
 // ...
 // Mark the task as processed
 task.IsProcessed = true;
}



List<int> list = new List<int>(new int[] { 16, 8, 44, 5 });
int sum = 0;
list.ForEach(value =>
 {
 sum += value;
 });





static bool IsEven(int value)
{
 return (value % 2) == 0;
}

List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
list.RemoveAll(IsEven);



List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 });
list.RemoveAll(item => { return (item % 2) == 0; });


List<string> list = new List<string>(new string[] { "red", "blue", "green" });
list.RemoveAt(0);


List<string> list = new List<string>(new string[] { "red", "please", "remove", "me", "blue",
"green" });
list.RemoveRange(1,3);


List<string> list = new List<string>(new string[] { "Adam", "Charlie", "David" });
list.Insert(1, "Bob");



List<string> list = new List<string>(new string[] { "Adam", "Charlie", "David" });
List<string> listToAppend = new List<string>(new string[] { "Bob", "Bobbie", "Bobby" });
list.InsertRange(1, listToAppend);








// Create a random list of 20 integers
Random rnd = new Random();
List<int> items = Enumerable.Repeat(0, 20).Select(i => rnd.Next(100)).ToList();

// Write the new list to the screen
Console.WriteLine("items={0}",ListToString(items));

// Sort the list
QuickSort(items);

// Write the sorted list to the screen
Console.WriteLine("QuickSort(items)={0}", ListToString(items));



List<int> list = new List<int>(new int[] { 16, 8, 44, 5 });
list.Sort();





List<Person> list = new List<Person>();
list.Add(new Person("David","Alexander",44));
list.Add(new Person("Jeff","Hay",32));
list.Add(new Person("Kim","Akers",12));
list.Add(new Person("Michael","Allen",25));
list.Sort(AgeComparison);


static int AgeComparison(Person a, Person b)
{
 if (a.Age < b.Age)
 {
 return -1;
 }
 if (a.Age > b.Age)
 {
 return 1;
 }
 return 0;
}




List<Person> list = new List<Person>();
list.Add(new Person("Julia", "Llyina", 12, false));
list.Add(new Person("David", "Alexander", 44, true));
list.Add(new Person("Michael", "Allen", 25, true));
list.Add(new Person("Andrews", "Lisa", 42, false));
list.Add(new Person("Jeff", "Hay", 32, true));
list.Add(new Person("Kim", "Akers", 28, false));
Person found = list.Find(person =>
 {
 return person.IsMale && person.Age > 40;
 });


//or
Person found = list.Find(FindOver40Males);

static bool FindOver40Males (Person person)
{
 return person.IsMale && person.Age >= 40;
}



int found = list.FindIndex(FindOver40Males);



int found = list.FindIndex(person =>
 {
 return person.IsMale && person.Age > 40;
 });



found = list.FindLastIndex(person =>
{
 return person.IsMale && person.Age > 40;
});




List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8 });
List<int> evens = list.FindAll(value => { return (value % 2) == 0; });



List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8 });
List<int> evens = list.FindAll(IsEven);

static bool IsEven(int value)
{
 return (value % 2) == 0;
}






List<int> list = new List<int>(new int[] { 33, 54, 23, 28, 8, 5, 14} );
int found = list.BinarySearch(5);
Console.WriteLine("The unsorted list is {0}", ListToString(list));
Console.WriteLine("The number 5 is located at {0} in the unsorted list.", found);
list.Sort();
Console.WriteLine("The sorted list is now {0}", ListToString(list));
found = list.BinarySearch(5);
Console.WriteLine("The number 5 is located at {0} in the sorted list.", found);



List<int> list = new List<int>(new int[] { 1, 2, 4, 4, 4, 6, 7});
int firstFour = list.IndexOf(4);
int lastFour = list.LastIndexOf(4);
list[firstFour] = 3;
list[lastFour] = 5;


List<int> list = new List<int>(new int[] { 1, 2, 7, 4, 1, 6, 7});
int extra1 = list.IndexOf(1,3);
int extra7 = list.LastIndexOf(7,3);



List<int> list = new List<int>(new int[] { 1, 2, 6, 4, 2, 6, 7});
int extra6 = list.IndexOf(6,1,6);
int extra2 = list.LastIndexOf(2,5,6);



List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8});
Console.WriteLine("Does the list contain an even number? {0}",
 list.Exists(IsEven) ? "Yes" : "No");

static bool IsEven(int value)
{
 return (value % 2) == 0;
}



List<int> list = new List<int>(new int[] { 1, 2, 3, 4, 5, 6, 7, 8});
List<int> evens = new List<int>(new int[] { 2, 4, 6, 8 });
bool allEvens = list.TrueForAll(IsEven);
Console.WriteLine("Does list contain all even numbers? {0}", allEvens ? "Yes" : "No");
allEvens = evens.TrueForAll(IsEven);
Console.WriteLine("Does evens contain all even numbers? {0}", allEvens ? "Yes" : "No");

```



```cs

static string UnpackPhoneNumber(long phonenumber)
{
 long areacode, exccode, subnum;
 // Get the first 3 digits of the phonenumber
 areacode = Math.Floor(phonenumber / 10000000);
 // Change the phonenumber variable to the last 7 digits
 Math.DivRem(phonenumber, 10000000, out phonenumber);
 // Get the exchange code or first 3 digits
 exccode = phonenumber / 10000;
 // Get the subscriber number from the last 4 digits
 Math.DivRem(phonenumber, 1000, out subnum);
 return string.Format("({0:D3}) {1:D3}-{2:D4}", areacode, exccode, subnum);
}


List<long> list = new List<long>(new long[] { 9015550100, 9015550188, 9015550113 });
List<string> phonenumbers = list.ConvertAll<string>( UnpackPhoneNumber);
```


```cs
List<long> list = new List<long>(new long[] { 9015550100, 9015550188, 9015550113 });
List<string> phonenumbers = list.ConvertAll<string>(item =>
 {
 long areaCode = item / 10000000;
 item -= (areaCode * 10000000);
 long exccode = item / 10000;
 return string.Format("({0:D3}) {1:D3}-{2:D4}", areaCode, exccode,
 item - (exccode * 10000));
 });
```









## HashSet<T>


```cs

//HashSet is an unordered collection containing unique elements
HashSet<int> theSet1 = new HashSet<int>();
theSet1.Add(1);
theSet1.Add(2);
theSet1.Add(2);
// theSet1 contains 1,2

HashSet<int> theSet2 = new HashSet<int>();
theSet2.Add(1);
theSet2.Add(3);
theSet2.Add(4);
// theSet2 contains 1,3,4

theSet1.UnionWith(theSet2);
// theSet1 contains 1,2,3,4


//HashSet’s default Add operation returns a bool letting you know whether the item was added,
bool added = theSet1.Add(2); // added is true
added = theSet1.Add(2); // added is false

```

```cs

class OddEvenComparer : IEqualityComparer<int> {
public OddEvenComparer() {}
	public bool Equals(int x, int y) {
		return (x & 1) == (y & 1);
	}

	public int GetHashCode(int x) {
		return (x & 1);
	}
}

...

// Now use the comparer
HashSet<int> oddEvenSet = new HashSet<int>(new OddEvenComparer());
oddEvenSet.Add(1);
oddEvenSet.Add(3);
oddEvenSet.Add(4);
// oddEventSet contains 1,4; it considered 1 and 3 equal.
```

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





# Enumerators and Iterators

```cs
int[] arr1 = { 10, 11, 12, 13 }; // Define the array.
foreach (int item in arr1) // Enumerate the elements.
	Console.WriteLine("Item value: {0}", item);
```

### IEnumerator Interface
```cs
static void Main()
{
	int[] MyArray = { 10, 11, 12, 13 }; // Create an array.

	IEnumerator ie = MyArray.GetEnumerator();
	
	while ( ie.MoveNext() )
	{ 
		int i = (int) ie.Current;
		Console.WriteLine("{0}", i); // Write it out.
	}
}
```

```cs
public class DaysOfTheWeek : System.Collections.IEnumerable
{

     string[] days = { "Sun", "Mon", "Tue", "Wed", "Thr", "Fri", "Sat" };

     //This is the iterator!!!
     public System.Collections.IEnumerator GetEnumerator()
     {
         for (int i = 0; i < days.Length; i++)
         {
             yield return days[i];
         }
     }

}

class TestDaysOfTheWeek
{
    static void Main()
    {
        // Create an instance of the collection class
        DaysOfTheWeek week = new DaysOfTheWeek();

        // Iterate with foreach - this is using the iterator!!! When the compiler
        //detects your iterator, it will automatically generate the Current, 
        //MoveNext and Dispose methods of the IEnumerator or IEnumerator<T> interface
        foreach (string day in week)
        {
            System.Console.Write(day + " ");
        }
    }
}
// Output: Sun Mon Tue Wed Thr Fri Sat
```




### IEnumerable Interface
```cs
class MyColors: IEnumerable
{
	string[] Colors = { "Red", "Yellow", "Blue" };
	public IEnumerator GetEnumerator()
	{
		return new ColorEnumerator(Colors);
	} 
}
```

### Iterators 
```cs
namespace UsingIterators
{
    class Program
    {
        static void Main()
        {
            // Using a simple iterator.
            ListClass listClass1 = new ListClass();

            foreach (int i in listClass1)
            {
                System.Console.Write(i + " ");
            }
            // Output: 0 1 2 3 4 5 6 7 8 9
            System.Console.WriteLine();


            // Using a named iterator.
            ListClass test = new ListClass();

            foreach (int n in test.SampleIterator(1, 10))
            {
                System.Console.Write(n + " ");
            }
            // Output: 1 2 3 4 5 6 7 8 9 10
            System.Console.WriteLine();


            // Using multiple yield statements.
            foreach (string element in new TestClass())
            {
                System.Console.Write(element);
            }
            // Output: With an iterator, more than one value can be returned.
            System.Console.WriteLine();

        }
    }

    class ListClass : System.Collections.IEnumerable
    {

        public System.Collections.IEnumerator GetEnumerator()
        {
            for (int i = 0; i < 10; i++)
            {
                yield return i;
            }
        }

        // Implementing the enumerable pattern
        public System.Collections.IEnumerable SampleIterator(int start, int end)
        {
            for (int i = start; i <= end; i++)
            {
                yield return i;
            }
        }
    }

    class TestClass : System.Collections.IEnumerable
    {
        public System.Collections.IEnumerator GetEnumerator()
        {
            yield return "With an iterator, ";
            yield return "more than one ";
            yield return "value can be returned";
            yield return ".";
        }
    }
}
```

## List<T>
```cs
var list = new List<string>();
list.Add("one");
list.Add("two");
list.Add("three");
list.AddRange(new[] {"four", "five", "six"});
 
//insert item at index 2
list.Insert(2, "seven");
 
//removes first occurrence of "seven"
list.Remove("seven"); //returns true
 
//removes all occurrences of "seven"
list.RemoveAll(s => s == "seven");
 
//checks is list contains two
list.Contains("two"); //returns true
 
//finds the first item which matches predicate
string value = list.Find(s => s == "three");
 
//finds all items which match predicate
List<string> values = list.FindAll(s => s == "three");
 
//gets a range of the list
List<string> range = list.GetRange(2, 3);      
 
//in-place sort of list
list.Sort();
 
//performs a binary search of a sorted list to find index of item
int index = list.BinarySearch("three"); // must sort first!
 
//removes all elements
list.Clear();
```

## SortedList<TKey,TValue>
```cs
var sortedList = new SortedList<int, string>();
sortedList.Add(1, "one");
sortedList.Add(2, "two");
sortedList.Add(3, "three");
sortedList.Add(4, "four");
 
// returns true
sortedList.ContainsKey(1);
 
// returns true
sortedList.ContainsValue("two");
 
// get index of key
sortedList.IndexOfKey(1);
 
// get index of value
sortedList.IndexOfValue("two");
 
// remove by key
sortedList.Remove(3);
 
// remove by index
sortedList.RemoveAt(2);
 
// lookup by key
string value = sortedList[2];
 
// get value by index
string value = sortedList.Values[2];
 
// get key by index
int key = sortedList.Keys[2];
 
string value;
if (sortedList.TryGetValue(4, out value))
    //do something
 
foreach (int key in sortedList.Keys)
{
    Console.WriteLine(key);
}
 
foreach (string value in sortedList.Values)
{
    Console.WriteLine(value);
}            
 
//removes all elements
sortedList.Clear();
```

## Dictionary<TKey,TValue>
```cs
var dictionary = new Dictionary<int, string>();
dictionary.Add(1, "one");
dictionary.Add(2, "two");
dictionary.Add(3, "three");
dictionary.Add(4, "four");
 
// returns true
dictionary.ContainsKey(1);
 
// returns true
dictionary.ContainsValue("two");
 
// remove by key
dictionary.Remove(3);
 
// lookup by key
string indexedValue = dictionary[4];
 
string value;
if (dictionary.TryGetValue(4, out value))
    //do something
 
foreach (int key in dictionary.Keys)
{
}
 
foreach (string value in dictionary.Values)
{
}
 
//removes all elements
dictionary.Clear();
```


## SortedDictionary<TKey,TValue>
```cs
var sortedDictionary = new SortedDictionary<int, string>();
sortedDictionary.Add(1, "one");
sortedDictionary.Add(2, "two");
sortedDictionary.Add(3, "three");
sortedDictionary.Add(4, "four");
 
// returns true
sortedDictionary.ContainsKey(1);
 
// returns true
sortedDictionary.ContainsValue("two");            
 
// remove by key
sortedDictionary.Remove(3);            
 
// lookup by key
string value = sortedDictionary[2];
 
string value;
if (sortedDictionary.TryGetValue(4, out value))
    //do something
 
// sorted by key
foreach (int key in sortedDictionary.Keys)
{
    Console.WriteLine(key);
}
 
// sorted by key
foreach (string value in sortedDictionary.Values)
{
    Console.WriteLine(value);
}            
 
//removes all elements
sortedDictionary.Clear();
```

## LinkedList<T>
```cs
var linkedList = new LinkedList<string>();
 
// add node to front of list
linkedList.AddFirst("one");            
 
// add node to end of list
var nodeThree = linkedList.AddLast("three");
 
// add node before given node
linkedList.AddBefore(nodeThree, "two");
 
// add node after given node
linkedList.AddAfter(nodeThree, "four");
 
// iterate list printing one, two, three, four
foreach (string value in linkedList)
{
    Console.WriteLine(value);
}
 
// find first node with value "two"
var nodeTwo = linkedList.Find("two");
 
// find last node with value "three"
nodeThree = linkedList.FindLast("three");
 
// get first node in list
var firstNode = linkedList.First;
 
// get last node in list
var lastNode = linkedList.Last;
 
// remove the first node with value "two"
linkedList.Remove("two");
 
// remove first node in list
linkedList.RemoveFirst();
 
// remove last node in list
linkedList.RemoveLast();
 
// remove all items from list
linkedList.Clear();
```

## SortedSet<T>
```cs
var sortedSet1 = new SortedSet<string>();            
sortedSet1.Add("one");
sortedSet1.Add("two");
sortedSet1.Add("three");
sortedSet1.Add("four");
 
var sortedSet2 = new SortedSet<string>();
sortedSet2.Add("two");
sortedSet2.Add("four");
 
sortedSet1.Contains("three");
 
// sortedSet1 now contains one, three
sortedSet1.ExceptWith(sortedSet2);
 
// sortedSet1 now contains two, four
sortedSet1.IntersectWith(sortedSet2);
 
// a subset is a set whose elements are all in 
// another set
sortedSet1.IsSubsetOf(sortedSet2);
 
// a superset is a set which contains all elements
// in another set
sortedSet1.IsSupersetOf(sortedSet2);
 
// a proper subset is a subset which is not equal
sortedSet1.IsProperSubsetOf(sortedSet2);
 
// a proper superset is a superset which is not equal
sortedSet1.IsProperSupersetOf(sortedSet2);            
 
// returns bool if both sets contain any of the same items
sortedSet1.Overlaps(sortedSet2);
 
// removes the element with value "two"
sortedSet1.Remove("two");
 
// removes all elements that match the predicate
sortedSet1.RemoveWhere(v => v == "three");
 
// returns true if both sets are identical
sortedSet1.SetEquals(sortedSet2);
 
// sortedSet1 now contains one, three
// only items which are in one or the other, not both
sortedSet1.SymmetricExceptWith(sortedSet2);
 
// sortedSet1 now contains one, two, three, four
// all items in both sets
sortedSet1.UnionWith(sortedSet2);
 
// returns all items between the given values
SortedSet<string> result = sortedSet1.GetViewBetween("two", "four");
 
// elements are in sorted order
foreach (string value in sortedSet1)
{                
}
 
// remove all items in both sets
sortedSet1.Clear();
```

## HashSet<T>
```cs
var hashSet1 = new HashSet<string>();            
hashSet1.Add("one");
hashSet1.Add("two");
hashSet1.Add("three");
hashSet1.Add("four");
 
var hashSet2 = new HashSet<string>();
hashSet2.Add("two");
hashSet2.Add("four");
 
hashSet1.Contains("three");
 
// sortedSet1 now contains one, three
hashSet1.ExceptWith(hashSet2);
 
// sortedSet1 now contains two, four
hashSet1.IntersectWith(hashSet2);
 
// a subset is a set whose elements are all in 
// another set
hashSet1.IsSubsetOf(hashSet2);
 
// a superset is a set which contains all elements
// in another set
hashSet1.IsSupersetOf(hashSet2);
 
// a proper subset is a subset which is not equal
hashSet1.IsProperSubsetOf(hashSet2);
 
// a proper superset is a superset which is not equal
hashSet1.IsProperSupersetOf(hashSet2);            
 
// returns bool if both sets contain any of the same items
hashSet1.Overlaps(hashSet2);
 
// removes the element with value "two"
hashSet1.Remove("two");
 
// removes all elements that match the predicate
hashSet1.RemoveWhere(v => v == "three");
 
// returns true if both sets are identical
hashSet1.SetEquals(hashSet2);
 
// sortedSet1 now contains one, three
// only items which are in one or the other, not both
hashSet1.SymmetricExceptWith(hashSet2);
 
// sortedSet1 now contains one, two, three, four
// all items in both sets
hashSet1.UnionWith(hashSet2);
 
// elements are no in any guaranteed order
foreach (string value in hashSet1)
{                
}
 
// remove all items in both sets
hashSet1.Clear();
```

## Queue<T>
```cs
var queue = new Queue<string>();
 
// pushes an item on the end of the queue
queue.Enqueue("one");
queue.Enqueue("two");
queue.Enqueue("three");
queue.Enqueue("four");
 
// returns true
queue.Contains("four");
 
// takes the item off the front of the queue
string item = queue.Dequeue();
 
// gets the item off the front of the queue
// without removing it
string peekItem = queue.Peek();
 
// remove all items from the queue
queue.Clear();
```

## Stack<T>
```cs
var stack = new Stack<string>();
// puts an item on the top of the stack
stack.Push("one");
stack.Push("two");
stack.Push("three");
stack.Push("four");
 
// removes an item from the top of the stack
string item = stack.Pop();
 
// gets the item on the top of the stack 
// without removing it
string peekedItem = stack.Peek();
 
// returns true if item is in stack
stack.Contains("two");
 
// removes all items from the stack
stack.Clear();
```

## ConcurrentQueue
```cs
//Enqueue takes a single parameter which is the item to add to the ConcurrentQueue:
var cq = new ConcurrentQueue<string>();
cq.Enqueue("test");

//Now we can dequeue this same item by calling TryDequeue.
string value;
if (cq.TryDequeue(out value))
{
    Console.WriteLine(value);
}

//This is called "TryPeek" and works the same as "TryDequeue":
string value;
if (cq.TryPeek(out value))
{
    Console.WriteLine(value);
}


cq.Enqueue("test");
string value;
if (!cq.IsEmpty)
{
    cq.TryDequeue(out value);
    Console.WriteLine(value);
}
```

## ConcurrentBag
```cs
var cb = new ConcurrentBag<string>();
cb.Add("test");

string val;
if (cb.TryTake(out val))
{
    Console.WriteLine(val);
}

string val;
if (cb.TryPeek(out val))
{
    Console.WriteLine(val);
}

var cb = new ConcurrentBag<string>();
Task.Factory.StartNew(() =>
{                
    for (int i = 0; i < 1000; i++)
    {
        cb.Add("test");
    }
    cb.Add("Last");
});
 
Task.Factory.StartNew(() => {
    foreach (string item in cb)
    {
        Console.WriteLine(item);
    }
}).Wait();
```

## ConcurrentStack
```cs
var cs = new ConcurrentStack<string>();
cs.Push("test");


string value;
if (cs.TryPop(out value))
{
    Console.WriteLine(value);
}

string value;
if (cs.TryPeek(out value))
{
    Console.WriteLine(value);
}

cs.PushRange(new[] { "test1", "test2", "test3" });


var cs = new ConcurrentStack<string>();
cs.PushRange(new [] {"item1", "item2", "item3", "item4", "item5"});
 
string[] values = new string[4];
int num = cs.TryPopRange(values);
if (num > 0)
{
    for (int i = 0; i < num; i++)
    {
        Console.WriteLine(values[i]);
    }
}

var cs = new ConcurrentStack<string>();
cs.PushRange(new [] {"item1", "item2", "item3", "item4", "item5"});
 
string[] values = new string[4];
int num = cs.TryPopRange(values, 2, 2);
if (num > 0)
{
    for (int i = 2; i < num + 2; i++)
    {
        Console.WriteLine(values[i]);
    }
}


if (!cs.IsEmpty)
{
    string value;
    cs.TryPop(out value);
    Console.WriteLine(value);
}
```

## BlockingCollection 
```cs
var queue = new Queue<string>();
Task.Factory.StartNew(() =>
{
    while (true)
    {
        queue.Enqueue("value");
    }
});


Task.Factory.StartNew(() =>
{
    while (true)
    {
        if (queue.Count > 0)
        {
            string value = queue.Dequeue();
            Console.WriteLine("Worker 1: " + value);
        }
    }
     
});
 
Task.Factory.StartNew(() =>
{
    while (true)
    {                    
        if (queue.Count > 0)
        {
            string value = queue.Dequeue();
            Console.WriteLine("Worker 2: " + value);
        }
    }
     
});


var queue = new ConcurrentQueue<string>();
Task.Factory.StartNew(() =>
{
    while (true)
    {
        queue.Enqueue("value" + count);
        count++;                    
    }
});
 
Task.Factory.StartNew(() =>
{
    while (true)
    {
        string value;
        if (queue.TryDequeue(out value))
        {
            Console.WriteLine("Worker 1: " + value);
        }
    }
});
 
Task.Factory.StartNew(() =>
{
    while (true)
    {
        string value;
        if (queue.TryDequeue(out value))
        {
            Console.WriteLine("Worker 2: " + value);
        }
         
    }
});




var blockingCollection = new BlockingCollection<string>();
Task.Factory.StartNew(() =>
{
    while (true)
    {
        blockingCollection.Add("value" + count);
        count++;                    
    }
});
 
Task.Factory.StartNew(() =>
{
    while (true)
    {                    
        Console.WriteLine("Worker 1: " + blockingCollection.Take());
    }
});
 
Task.Factory.StartNew(() =>
{
    while (true)
    {
        Console.WriteLine("Worker 2: " + blockingCollection.Take());
    }
});



Task.Factory.StartNew(() =>
{
    foreach (string value in blockingCollection.GetConsumingEnumerable())
    {
        Console.WriteLine("Worker 1: " + value);
    }                
});
```


## SortedSet
```cs
var elements = new SortedSet<int>() { 5, 9, 2, 11, 2, 1, 4, 1, 2 };

foreach (int element in elements)  
   Console.Write(string.Format(" {0}", element));
Output: 1 2 4 5 9 11   



bool result = elements.Add(17);
foreach (int element in elements)  
           Console.Write(string.Format(" {0}", element)); 
Output: 1 2 4 5 9 11 17

//Getting a Subset of a SortedSet<T> Collection
var subSet = elements.GetViewBetween(2, 9);
foreach (int element in subSet)  
           Console.Write(string.Format(" {0}", element));
Output: 2 4 5 9		   

var subSet = elements.GetViewBetween(2, 9);
bool result = subSet.Add(7);
foreach (int element in elements)  
   Console.Write(string.Format(" {0}", element)); 
Output: 1 2 4 5 7 9 11   

//Removing Element(s) from a SortedSet<T> Collection
elements.Remove(1);

foreach (int element in elements)
   Console.Write(string.Format(" {0}", element));
Output: 2 4 5 9 11   

// predicate 
elements.RemoveWhere(P => P % 2 == 0);
 foreach (int element in elements)
    Console.Write(string.Format(" {0}", element));
	
//Max and Min Values of a SortedSet<T> Collection
Console.Write(string.Format("Max: {0}, Min: {1}", elements.Max, elements.Min)); 

//Union(U), Intersection(∩) and Difference(-) operations
var A = new SortedSet<int>() { 1, 2, 3, 4, 5, 11, };
var B = new SortedSet<int>() { 6, 7, 8, 9, 10, 11 };	

var union = A.Union(B);
foreach (int element in union)
   Console.Write(string.Format(" {0}", element));
Output (AUB): 1 2 3 4 5 11 6 7 8 9 10

var intersection = A.Intersect(B);
foreach (int element in intersection)
   Console.Write(string.Format(" {0}", element));

Output (A∩B): 11


var difference = A.Except(B);
foreach (int element in difference)
   Console.Write(string.Format(" {0}", element));
 Output (A-B): 1 2 3 4 5  
 
//Merging of two SortedSet<T> Collection 
var merged = A.Zip(B, (P, Q) => P + Q);

foreach (int element in merged)
   Console.Write(string.Format(" {0}", element));
   
//CopyTo Method of SortedSet<T> Collection
It is a very useful method. It has three constructors - CopyTo(T()), CopyTo(T(), Int32) & CopyTo(T(), Int32, Int32).

CopyTo(T()): It copies the complete SortedSet<T> to a compatible one-dimensional array, starting at the beginning of the target array.
var target = new SortedSet<int>() {13, 2, 4, 10, 1, 7 };

int[] array = new int[10];

target.CopyTo(array);

for (int n = 0; n < array.Length; ++n)
   Console.Write(string.Format("Index: {0}, Value: {1}<br />", n, array[n]));

```   
