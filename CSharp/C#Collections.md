

* System.Collections
  * ArrayList
  * BitArray
  * Hashtable
  * SortedList
  * Queue
  * Stack
  * DictionaryEntry

* System.Collections.Generic
  * Dictionary<TKey,TValue>	
  * LinkedList<T>	
  * List<T>	
  * Queue<T>	
  * Stack<T>
  * SortedDictionary<TKey,TValue>
  * SortedList<TKey, TValue>	
  * SortedSet<T>
  * Comparer<T>	
  * KeyValuePair<TKey, TValue> 
  * EqualityComparer<T>	
  * HashSet<T>	
  * KeyedByTypeCollection<TItem>
  * LinkedListNode<T>	
  * SynchronizedCollection<T>
  * SynchronizedKeyedCollection<K,T>
  * SynchronizedReadOnlyCollection<T>	


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
