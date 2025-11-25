# Java Lists - Complete Guide

## Table of Contents
1. [Basic Operations](#basic-operations)
2. [Access & Modification](#access--modification)
3. [Search & Query](#search--query)
4. [Bulk Operations](#bulk-operations)
5. [Iteration Methods](#iteration-methods)
6. [Sorting & Transforming](#sorting--transforming)
7. [Sublist & Range Operations](#sublist--range-operations)
8. [Quick Reference Table](#quick-reference-table)

---

## Basic Operations

### add(element)
**Description:** Appends an element to the end of the list.

**Syntax:**
```java
boolean add(E element)
```

**Returns:** `true` (always succeeds for ArrayList)

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
System.out.println(fruits);  // [Apple, Banana]
```

---

### add(index, element)
**Description:** Inserts an element at the specified index. Shifts existing elements to the right.

**Syntax:**
```java
void add(int index, E element)
```

**Returns:** `void`

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add(1, "Orange");  // Insert at index 1
System.out.println(fruits);  // [Apple, Orange, Banana]
```

---

### remove(index)
**Description:** Removes the element at the specified index. Shifts remaining elements to the left.

**Syntax:**
```java
E remove(int index)
```

**Returns:** The element that was removed

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");
String removed = fruits.remove(1);  // Removes "Banana"
System.out.println(removed);  // Banana
System.out.println(fruits);   // [Apple, Orange]
```

---

### remove(object)
**Description:** Removes the first occurrence of the specified element.

**Syntax:**
```java
boolean remove(Object o)
```

**Returns:** `true` if element was found and removed, `false` otherwise

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Apple");
fruits.remove("Apple");  // Removes first "Apple"
System.out.println(fruits);  // [Banana, Apple]
```

---

### clear()
**Description:** Removes all elements from the list.

**Syntax:**
```java
void clear()
```

**Returns:** `void`

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.clear();
System.out.println(fruits);  // []
System.out.println(fruits.size());  // 0
```

---

### size()
**Description:** Returns the number of elements in the list.

**Syntax:**
```java
int size()
```

**Returns:** Number of elements

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
System.out.println(fruits.size());  // 2
```

---

## Access & Modification

### get(index)
**Description:** Returns the element at the specified index.

**Syntax:**
```java
E get(int index)
```

**Returns:** Element at the specified position

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
System.out.println(fruits.get(0));  // Apple
System.out.println(fruits.get(1));  // Banana
```

---

### set(index, element)
**Description:** Replaces the element at the specified index with a new element.

**Syntax:**
```java
E set(int index, E element)
```

**Returns:** The element previously at the specified position

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
String old = fruits.set(1, "Orange");  // Replace Banana with Orange
System.out.println(old);     // Banana
System.out.println(fruits);  // [Apple, Orange]
```

---

## Search & Query

### contains(object)
**Description:** Checks if the list contains the specified element.

**Syntax:**
```java
boolean contains(Object o)
```

**Returns:** `true` if element is found, `false` otherwise

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
System.out.println(fruits.contains("Apple"));   // true
System.out.println(fruits.contains("Orange"));  // false
```

---

### indexOf(object)
**Description:** Returns the index of the **first occurrence** of the element. Returns -1 if not found.

**Syntax:**
```java
int indexOf(Object o)
```

**Returns:** Index of first occurrence, or -1

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Apple");
System.out.println(fruits.indexOf("Apple"));   // 0 (first occurrence)
System.out.println(fruits.indexOf("Orange"));  // -1 (not found)
```

---

### lastIndexOf(object)
**Description:** Returns the index of the **last occurrence** of the element. Returns -1 if not found.

**Syntax:**
```java
int lastIndexOf(Object o)
```

**Returns:** Index of last occurrence, or -1

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Apple");
System.out.println(fruits.lastIndexOf("Apple"));  // 2 (last occurrence)
```

---

### isEmpty()
**Description:** Checks if the list has no elements.

**Syntax:**
```java
boolean isEmpty()
```

**Returns:** `true` if list is empty, `false` otherwise

**Example:**
```java
List<String> fruits = new ArrayList<>();
System.out.println(fruits.isEmpty());  // true
fruits.add("Apple");
System.out.println(fruits.isEmpty());  // false
```

---

## Bulk Operations

### addAll(collection)
**Description:** Adds all elements from another collection to the end of the list.

**Syntax:**
```java
boolean addAll(Collection<? extends E> c)
```

**Returns:** `true` if list changed

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");

List<String> moreFruits = Arrays.asList("Banana", "Orange");
fruits.addAll(moreFruits);

System.out.println(fruits);  // [Apple, Banana, Orange]
```

---

### addAll(index, collection)
**Description:** Inserts all elements from another collection at the specified index.

**Syntax:**
```java
boolean addAll(int index, Collection<? extends E> c)
```

**Returns:** `true` if list changed

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Grape");

List<String> moreFruits = Arrays.asList("Banana", "Orange");
fruits.addAll(1, moreFruits);  // Insert at index 1

System.out.println(fruits);  // [Apple, Banana, Orange, Grape]
```

---

### removeAll(collection)
**Description:** Removes all elements that are contained in the specified collection.

**Syntax:**
```java
boolean removeAll(Collection<?> c)
```

**Returns:** `true` if list changed

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

List<String> toRemove = Arrays.asList("Apple", "Orange");
fruits.removeAll(toRemove);

System.out.println(fruits);  // [Banana]
```

---

### retainAll(collection)
**Description:** Retains only the elements that are contained in the specified collection. Removes everything else.

**Syntax:**
```java
boolean retainAll(Collection<?> c)
```

**Returns:** `true` if list changed

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

List<String> toKeep = Arrays.asList("Apple", "Orange");
fruits.retainAll(toKeep);  // Keep only Apple and Orange

System.out.println(fruits);  // [Apple, Orange]
```

---

### containsAll(collection)
**Description:** Checks if the list contains all elements from the specified collection.

**Syntax:**
```java
boolean containsAll(Collection<?> c)
```

**Returns:** `true` if all elements are present

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

List<String> check = Arrays.asList("Apple", "Banana");
System.out.println(fruits.containsAll(check));  // true

List<String> check2 = Arrays.asList("Apple", "Grape");
System.out.println(fruits.containsAll(check2));  // false (Grape missing)
```

---

## Iteration Methods

### forEach(action)
**Description:** Performs an action for each element in the list.

**Syntax:**
```java
void forEach(Consumer<? super E> action)
```

**Returns:** `void`

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");

fruits.forEach(fruit -> System.out.println(fruit));
// Output:
// Apple
// Banana
```

**With Method Reference:**
```java
fruits.forEach(System.out::println);
```

---

### iterator()
**Description:** Returns an iterator over the elements in the list.

**Syntax:**
```java
Iterator<E> iterator()
```

**Returns:** Iterator object

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");

Iterator<String> it = fruits.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
// Output:
// Apple
// Banana
```

---

### listIterator()
**Description:** Returns a list iterator (bidirectional) starting at the beginning.

**Syntax:**
```java
ListIterator<E> listIterator()
```

**Returns:** ListIterator object

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");

ListIterator<String> it = fruits.listIterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
// Can also go backwards with hasPrevious() and previous()
```

---

## Sorting & Transforming

### sort(comparator)
**Description:** Sorts the list according to the order specified by the comparator.

**Syntax:**
```java
void sort(Comparator<? super E> c)
```

**Returns:** `void` (sorts in-place)

**Example:**
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(5);
numbers.add(2);
numbers.add(8);
numbers.add(1);

numbers.sort(Comparator.naturalOrder());
System.out.println(numbers);  // [1, 2, 5, 8]

numbers.sort(Comparator.reverseOrder());
System.out.println(numbers);  // [8, 5, 2, 1]
```

**Custom Sorting:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Banana");
fruits.add("Apple");
fruits.add("Cherry");

// Sort by length
fruits.sort(Comparator.comparingInt(String::length));
System.out.println(fruits);  // [Apple, Banana, Cherry]
```

---

### replaceAll(operator)
**Description:** Replaces each element with the result of applying the operator to that element.

**Syntax:**
```java
void replaceAll(UnaryOperator<E> operator)
```

**Returns:** `void` (modifies in-place)

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("apple");
fruits.add("banana");

fruits.replaceAll(String::toUpperCase);
System.out.println(fruits);  // [APPLE, BANANA]
```

**With Numbers:**
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);

numbers.replaceAll(n -> n * 2);  // Double each number
System.out.println(numbers);  // [2, 4, 6]
```

---

### removeIf(predicate)
**Description:** Removes all elements that satisfy the given predicate.

**Syntax:**
```java
boolean removeIf(Predicate<? super E> filter)
```

**Returns:** `true` if any elements were removed

**Example:**
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);
numbers.add(4);
numbers.add(5);

numbers.removeIf(n -> n % 2 == 0);  // Remove even numbers
System.out.println(numbers);  // [1, 3, 5]
```

**With Strings:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Apricot");

fruits.removeIf(f -> f.startsWith("A"));
System.out.println(fruits);  // [Banana]
```

---

## Sublist & Range Operations

### subList(fromIndex, toIndex)
**Description:** Returns a view of the portion of the list between `fromIndex` (inclusive) and `toIndex` (exclusive).

**Syntax:**
```java
List<E> subList(int fromIndex, int toIndex)
```

**Returns:** Sublist view (changes reflect in original list)

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");
fruits.add("Grape");

List<String> sub = fruits.subList(1, 3);  // Elements at index 1 and 2
System.out.println(sub);  // [Banana, Orange]

// Modifying sublist affects original
sub.set(0, "Mango");
System.out.println(fruits);  // [Apple, Mango, Orange, Grape]
```

---

## Conversion & Utility

### toArray()
**Description:** Converts the list to an array.

**Syntax:**
```java
Object[] toArray()
T[] toArray(T[] a)
```

**Returns:** Array containing all elements

**Example:**
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");

// Convert to Object array
Object[] arr1 = fruits.toArray();

// Convert to String array (preferred)
String[] arr2 = fruits.toArray(new String[0]);
System.out.println(Arrays.toString(arr2));  // [Apple, Banana]
```

---

### Collections.reverse()
**Description:** Reverses the order of elements in the list. (From `Collections` utility class)

**Syntax:**
```java
Collections.reverse(List<?> list)
```

**Returns:** `void` (reverses in-place)

**Example:**
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);

Collections.reverse(numbers);
System.out.println(numbers);  // [3, 2, 1]
```

---

### Collections.shuffle()
**Description:** Randomly shuffles the elements in the list. (From `Collections` utility class)

**Syntax:**
```java
Collections.shuffle(List<?> list)
```

**Returns:** `void` (shuffles in-place)

**Example:**
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);
numbers.add(4);

Collections.shuffle(numbers);
System.out.println(numbers);  // Random order, e.g., [3, 1, 4, 2]
```

---

## Quick Reference Table

| **Method** | **Use When** | **Key Behavior** |
|------------|--------------|------------------|
| `add(e)` | Adding to end | Appends element |
| `add(i, e)` | Inserting at position | Shifts elements right |
| `get(i)` | Accessing element | Returns element at index |
| `set(i, e)` | Replacing element | Updates and returns old value |
| `remove(i)` | Removing by index | Shifts elements left |
| `remove(obj)` | Removing by value | Removes first occurrence |
| `clear()` | Removing all elements | Empties the list |
| `size()` | Getting count | Returns number of elements |
| `isEmpty()` | Checking if empty | Returns true if size == 0 |
| `contains(obj)` | Checking existence | Searches for element |
| `indexOf(obj)` | Finding position | Returns first index or -1 |
| `lastIndexOf(obj)` | Finding last position | Returns last index or -1 |
| `addAll(col)` | Adding multiple | Appends collection |
| `removeAll(col)` | Removing multiple | Removes all matching |
| `retainAll(col)` | Keeping only specific | Removes non-matching |
| `containsAll(col)` | Checking multiple | True if all present |
| `sort(cmp)` | Ordering elements | Sorts in-place |
| `replaceAll(op)` | Transforming all | Applies function to each |
| `removeIf(pred)` | Conditional removal | Removes matching elements |
| `forEach(action)` | Iterating | Performs action on each |
| `subList(from, to)` | Getting range | Returns view of portion |
| `toArray()` | Converting to array | Returns array copy |

---

## Common Patterns

### Pattern 1: Initialize List with Values
```java
// Method 1: Arrays.asList (fixed-size)
List<String> fruits = Arrays.asList("Apple", "Banana", "Orange");

// Method 2: List.of (immutable, Java 9+)
List<String> fruits = List.of("Apple", "Banana", "Orange");

// Method 3: Mutable ArrayList
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

// Method 4: From another collection
List<String> fruits = new ArrayList<>(Arrays.asList("Apple", "Banana"));
```

---

### Pattern 2: Remove Elements While Iterating
```java
// BAD - ConcurrentModificationException
for (String fruit : fruits) {
    if (fruit.startsWith("A")) {
        fruits.remove(fruit);  // ❌ ERROR!
    }
}

// GOOD - Use removeIf
fruits.removeIf(fruit -> fruit.startsWith("A"));  // ✅

// GOOD - Use Iterator
Iterator<String> it = fruits.iterator();
while (it.hasNext()) {
    if (it.next().startsWith("A")) {
        it.remove();  // ✅
    }
}
```

---

### Pattern 3: Find Element
```java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");

// Check if exists
if (fruits.contains("Apple")) {
    System.out.println("Found!");
}

// Get index
int index = fruits.indexOf("Apple");
if (index != -1) {
    System.out.println("Found at index: " + index);
}
```

---

### Pattern 4: Transform All Elements
```java
List<String> fruits = new ArrayList<>();
fruits.add("apple");
fruits.add("banana");

// Convert to uppercase
fruits.replaceAll(String::toUpperCase);
System.out.println(fruits);  // [APPLE, BANANA]

// Or with lambda
fruits.replaceAll(fruit -> fruit + "!");
System.out.println(fruits);  // [APPLE!, BANANA!]
```

---

### Pattern 5: Filter List
```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.add(3);
numbers.add(4);
numbers.add(5);

// Remove even numbers (in-place)
numbers.removeIf(n -> n % 2 == 0);
System.out.println(numbers);  // [1, 3, 5]

// Create new filtered list (using streams)
List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
```

---

## ArrayList vs LinkedList

| **Feature** | **ArrayList** | **LinkedList** |
|-------------|---------------|----------------|
| **Underlying Structure** | Dynamic array | Doubly-linked list |
| **get(i)** | O(1) - Fast | O(n) - Slow |
| **add(e)** (at end) | O(1) - Fast | O(1) - Fast |
| **add(i, e)** (at index) | O(n) - Slow (shifting) | O(n) - Slow (traversal) |
| **remove(i)** | O(n) - Slow (shifting) | O(n) - Slow (traversal) |
| **Memory** | Less overhead | More overhead (node pointers) |
| **Use When** | Frequent access by index | Frequent add/remove at ends |

**Recommendation:** Use **ArrayList** for most cases. Only use LinkedList if you frequently add/remove at the beginning.

---

## Performance Notes

- **ArrayList:** Best for random access (`get`, `set`) - O(1)
- **Adding at end:** O(1) amortized (may need to resize array)
- **Adding at middle:** O(n) - must shift elements
- **Removing:** O(n) - must shift elements
- **Searching:** O(n) - must check each element
- **contains(), indexOf():** O(n) - linear search
- **Sorting:** O(n log n) with efficient algorithms

---

## Key Differences: List vs Array

| **Feature** | **Array** | **List (ArrayList)** |
|-------------|-----------|----------------------|
| **Size** | Fixed | Dynamic (grows automatically) |
| **Syntax** | `int[] arr = new int[5]` | `List<Integer> list = new ArrayList<>()` |
| **Type** | Primitives or objects | Objects only (use wrappers for primitives) |
| **Methods** | Limited (length property) | Rich API (add, remove, contains, etc.) |
| **Performance** | Faster (no overhead) | Slightly slower (object wrapper) |
| **Flexibility** | Less flexible | More flexible |

---

**End of Lists Guide** - You now have all the essential List operations! 🎉
