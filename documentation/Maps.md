# Java Maps - Complete Guide

## Table of Contents
1. [Basic Operations](#basic-operations)
2. [Retrieval Methods](#retrieval-methods)
3. [Conditional Operations](#conditional-operations)
4. [Compute Methods](#compute-methods)
5. [Replace Methods](#replace-methods)
6. [Iteration Methods](#iteration-methods)
7. [Quick Reference Table](#quick-reference-table)

---

## Basic Operations

### put(key, value)
**Description:** Adds or updates a key-value pair in the map. If the key exists, overwrites the old value.

**Syntax:**
```java
V put(K key, V value)
```

**Returns:** Previous value associated with the key, or `null` if key didn't exist

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);     // Adds: Alice -> 85
scores.put("Alice", 90);     // Updates: Alice -> 90
```

---

### remove(key)
**Description:** Removes the key-value pair for the specified key.

**Syntax:**
```java
V remove(Object key)
```

**Returns:** Previous value associated with the key, or `null` if key didn't exist

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.remove("Alice");      // Removes Alice from map
System.out.println(scores);  // {}
```

---

### size()
**Description:** Returns the number of key-value pairs in the map.

**Syntax:**
```java
int size()
```

**Returns:** Number of entries in the map

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);
System.out.println(scores.size());  // 2
```

---

## Retrieval Methods

### get(key)
**Description:** Retrieves the value associated with the given key. Returns `null` if key doesn't exist.

**Syntax:**
```java
V get(Object key)
```

**Returns:** Value associated with the key, or `null`

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
System.out.println(scores.get("Alice"));  // 85
System.out.println(scores.get("Bob"));    // null
```

---

### getOrDefault(key, defaultValue)
**Description:** Retrieves the value for the key, or returns a default value if key doesn't exist. Safer than `get()`.

**Syntax:**
```java
V getOrDefault(Object key, V defaultValue)
```

**Returns:** Value associated with the key, or `defaultValue` if key not found

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
System.out.println(scores.getOrDefault("Alice", 0));  // 85
System.out.println(scores.getOrDefault("Bob", 0));    // 0 (default)
```

---

### containsKey(key)
**Description:** Checks if the map contains the specified key.

**Syntax:**
```java
boolean containsKey(Object key)
```

**Returns:** `true` if key exists, `false` otherwise

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
System.out.println(scores.containsKey("Alice"));  // true
System.out.println(scores.containsKey("Bob"));    // false
```

---

### containsValue(value)
**Description:** Checks if the map contains the specified value. **Note:** This is slower than `containsKey()` as it searches through all values.

**Syntax:**
```java
boolean containsValue(Object value)
```

**Returns:** `true` if value exists, `false` otherwise

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 85);
System.out.println(scores.containsValue(85));   // true
System.out.println(scores.containsValue(100));  // false
```

---

## Conditional Operations

### putIfAbsent(key, value)
**Description:** Adds the key-value pair **only if the key doesn't already exist**. Won't overwrite existing values.

**Syntax:**
```java
V putIfAbsent(K key, V value)
```

**Returns:** Existing value if key was present, `null` if key was absent (and value was added)

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.putIfAbsent("Alice", 90);  // Does nothing (Alice exists)
scores.putIfAbsent("Bob", 92);    // Adds Bob -> 92
System.out.println(scores);       // {Alice=85, Bob=92}
```

---

## Compute Methods

### computeIfAbsent(key, mappingFunction)
**Description:** Computes and adds a value for the key **only if the key is absent**. Perfect for lazy initialization.

**Syntax:**
```java
V computeIfAbsent(K key, Function<K, V> mappingFunction)
```

**Returns:** Current (existing or computed) value associated with the key

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);

// Only runs if key is missing
scores.computeIfAbsent("Bob", k -> 70);      // Adds Bob -> 70
scores.computeIfAbsent("Alice", k -> 100);   // Does nothing (Alice exists)

System.out.println(scores);  // {Alice=85, Bob=70}
```

**Use Case:** Initialize lists in a map of lists
```java
Map<String, List<String>> groups = new HashMap<>();
groups.computeIfAbsent("teamA", k -> new ArrayList<>()).add("Alice");
```

---

### computeIfPresent(key, remappingFunction)
**Description:** Computes a new value for the key **only if the key exists**. Perfect for updating existing entries.

**Syntax:**
```java
V computeIfPresent(K key, BiFunction<K, V, V> remappingFunction)
```

**Returns:** New computed value, or `null` if key didn't exist

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);

// Only runs if key exists
scores.computeIfPresent("Alice", (k, v) -> v + 10);  // Updates Alice to 95
scores.computeIfPresent("Bob", (k, v) -> v + 10);    // Does nothing (Bob absent)

System.out.println(scores);  // {Alice=95}
```

**Use Case:** Apply bonus to existing students only
```java
scores.computeIfPresent("Alice", (k, v) -> v + 5);  // Add 5 bonus points
```

---

### compute(key, remappingFunction)
**Description:** Computes a value for the key **regardless of whether it exists or not**. Can add, update, or remove entries.

**Syntax:**
```java
V compute(K key, BiFunction<K, V, V> remappingFunction)
```

**Returns:** New computed value

**Note:** The current value `v` will be `null` if the key doesn't exist.

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);

// Always runs - v is null if key absent
scores.compute("Alice", (k, v) -> v == null ? 100 : v + 10);  // Updates to 95
scores.compute("Bob", (k, v) -> v == null ? 100 : v + 10);    // Adds Bob -> 100

System.out.println(scores);  // {Alice=95, Bob=100}
```

---

### merge(key, value, remappingFunction)
**Description:** Merges a new value with an existing value using the provided function. **Perfect for counting and accumulation.**

**Syntax:**
```java
V merge(K key, V value, BiFunction<V, V, V> remappingFunction)
```

**Returns:** New merged value

**Behavior:**
- If key is **absent**: Adds `key -> value`
- If key is **present**: Applies function to combine `oldValue` and `newValue`

**Example:**
```java
Map<String, Integer> wordCount = new HashMap<>();

// Count word occurrences
wordCount.merge("java", 1, Integer::sum);  // Adds java -> 1
wordCount.merge("java", 1, Integer::sum);  // Updates java -> 2
wordCount.merge("java", 1, Integer::sum);  // Updates java -> 3

System.out.println(wordCount);  // {java=3}
```

**Common Use Case:** Word frequency counter
```java
String[] words = {"java", "is", "great", "java", "is", "fun"};
Map<String, Integer> frequency = new HashMap<>();
for (String word : words) {
    frequency.merge(word, 1, Integer::sum);
}
// Result: {java=2, is=2, great=1, fun=1}
```

---

## Replace Methods

### replace(key, value)
**Description:** Replaces the value for the key **only if the key exists**. Won't add new entries.

**Syntax:**
```java
V replace(K key, V value)
```

**Returns:** Previous value, or `null` if key didn't exist

**Example:**
```java
Map<String, Double> prices = new HashMap<>();
prices.put("apple", 1.50);

prices.replace("apple", 1.75);   // Updates apple to 1.75
prices.replace("banana", 0.80);  // Does nothing (banana doesn't exist)

System.out.println(prices);  // {apple=1.75}
```

---

### replace(key, oldValue, newValue)
**Description:** Replaces the value **only if the key exists AND the current value matches `oldValue`**. Safe conditional update.

**Syntax:**
```java
boolean replace(K key, V oldValue, V newValue)
```

**Returns:** `true` if replaced, `false` if not

**Example:**
```java
Map<String, Double> prices = new HashMap<>();
prices.put("apple", 1.50);

// Only replaces if current value is 1.50
prices.replace("apple", 1.50, 1.75);  // true - updates to 1.75
prices.replace("apple", 1.50, 2.00);  // false - value is now 1.75, not 1.50

System.out.println(prices);  // {apple=1.75}
```

---

### replaceAll(function)
**Description:** Applies a function to **all entries** in the map to compute new values. Bulk update operation.

**Syntax:**
```java
void replaceAll(BiFunction<K, V, V> function)
```

**Returns:** `void` (modifies map in-place)

**Example:**
```java
Map<String, Double> prices = new HashMap<>();
prices.put("apple", 1.50);
prices.put("banana", 0.80);
prices.put("orange", 2.00);

// Apply 10% discount to all items
prices.replaceAll((item, price) -> price * 0.9);

System.out.println(prices);  
// {apple=1.35, banana=0.72, orange=1.8}
```

---

## Iteration Methods

### entrySet()
**Description:** Returns a set of all key-value pairs (entries) for iteration.

**Syntax:**
```java
Set<Map.Entry<K, V>> entrySet()
```

**Returns:** Set of entries

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);

for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
// Output:
// Alice: 85
// Bob: 92
```

---

### forEach(action)
**Description:** Performs an action for each key-value pair. **Cleaner alternative to `entrySet()` loop.**

**Syntax:**
```java
void forEach(BiConsumer<K, V> action)
```

**Returns:** `void`

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);

scores.forEach((name, score) -> {
    System.out.println(name + ": " + score);
});
// Output:
// Alice: 85
// Bob: 92
```

**With Conditions:**
```java
// Print only students with score > 80
scores.forEach((name, score) -> {
    if (score > 80) {
        System.out.println(name + ": " + score);
    }
});
```

**Calculate Total:**
```java
int[] total = {0};  // Array trick for effectively final
scores.forEach((name, score) -> total[0] += score);
System.out.println("Total: " + total[0]);  // 177
```

---

### keySet()
**Description:** Returns a set of all keys in the map.

**Syntax:**
```java
Set<K> keySet()
```

**Returns:** Set of keys

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);

Set<String> names = scores.keySet();
System.out.println(names);  // [Alice, Bob]
```

---

### values()
**Description:** Returns a collection of all values in the map. **Note:** Returns `Collection`, not `List` (values can duplicate but no guaranteed order).

**Syntax:**
```java
Collection<V> values()
```

**Returns:** Collection of values

**Example:**
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);
scores.put("Charlie", 85);

Collection<Integer> allScores = scores.values();
System.out.println(allScores);  // [85, 92, 85]
```

---

## Quick Reference Table

| **Method** | **Use When** | **Key Behavior** |
|------------|--------------|------------------|
| `put(k, v)` | Adding or updating | Always adds/updates |
| `get(k)` | Retrieving value | Returns `null` if missing |
| `getOrDefault(k, def)` | Safe retrieval | Returns default if missing |
| `containsKey(k)` | Checking existence | Fast key lookup |
| `containsValue(v)` | Checking value exists | Slow - searches all values |
| `remove(k)` | Deleting entry | Removes if exists |
| `putIfAbsent(k, v)` | Add only if new | Won't overwrite existing |
| `computeIfAbsent(k, f)` | Lazy initialization | Only computes if key absent |
| `computeIfPresent(k, f)` | Update existing | Only runs if key exists |
| `compute(k, f)` | Handle both cases | Always runs (`v` is `null` if absent) |
| `merge(k, v, f)` | Counting/accumulation | Combines old and new values |
| `replace(k, v)` | Update if exists | Won't add new entries |
| `replace(k, old, new)` | Safe conditional update | Checks both key and value |
| `replaceAll(f)` | Bulk update | Applies to all entries |
| `entrySet()` | Traditional iteration | Returns all entries |
| `forEach(action)` | Clean iteration | Lambda-based loop |
| `keySet()` | Get all keys | Returns `Set<K>` |
| `values()` | Get all values | Returns `Collection<V>` |

---

## Common Patterns

### Pattern 1: Word Frequency Counter
```java
String text = "java is great and java is fun";
String[] words = text.split(" ");
Map<String, Integer> frequency = new HashMap<>();

for (String word : words) {
    frequency.merge(word, 1, Integer::sum);
}
System.out.println(frequency);  // {java=2, is=2, great=1, and=1, fun=1}
```

### Pattern 2: Shopping Cart
```java
Map<String, Integer> cart = new HashMap<>();
cart.put("apple", 2);
cart.merge("apple", 3, Integer::sum);  // Add 3 more apples
System.out.println(cart);  // {apple=5}
```

### Pattern 3: Grouping (Map of Lists)
```java
Map<String, List<String>> teams = new HashMap<>();
teams.computeIfAbsent("teamA", k -> new ArrayList<>()).add("Alice");
teams.computeIfAbsent("teamA", k -> new ArrayList<>()).add("Bob");
teams.computeIfAbsent("teamB", k -> new ArrayList<>()).add("Charlie");
System.out.println(teams);  // {teamA=[Alice, Bob], teamB=[Charlie]}
```

### Pattern 4: Default Values
```java
Map<String, Integer> config = new HashMap<>();
int timeout = config.getOrDefault("timeout", 30);  // Default 30 seconds
```

---

## Key Differences: The "Compute Family"

```
computeIfAbsent(k, f)    → Only runs if key is ABSENT (adds new entry)
computeIfPresent(k, f)   → Only runs if key is PRESENT (updates existing)
compute(k, f)            → Always runs (handles both cases, v=null if absent)
merge(k, v, f)           → Adds if absent, merges if present (perfect for counting)
```

---

## Performance Notes

- **HashMap:** O(1) average for `get`, `put`, `remove`, `containsKey`
- **containsValue:** O(n) - must search all values
- **Keys must be unique** - duplicates overwrite
- **Values can duplicate** - no restrictions
- **Unordered** - iteration order not guaranteed (use `LinkedHashMap` for insertion order)

---

**End of Maps Guide** - You now have all the essential Map operations! 🎉
