# Java Arrays - Complete Guide

## Table of Contents
1. [Introduction to Arrays](#introduction-to-arrays)
2. [Declaring and Initializing Arrays](#declaring-and-initializing-arrays)
3. [Accessing and Modifying Array Elements](#accessing-and-modifying-array-elements)
4. [Array Length](#array-length)
5. [Iterating Through Arrays](#iterating-through-arrays)
6. [2D Arrays (Multidimensional Arrays)](#2d-arrays-multidimensional-arrays)
7. [Common Array Operations](#common-array-operations)
8. [Arrays Utility Class Methods](#arrays-utility-class-methods)
9. [Common Pitfalls and Best Practices](#common-pitfalls-and-best-practices)

---

## Introduction to Arrays

### What are Arrays?
An **array** is a container object that holds a **fixed number** of values of a **single type**. Arrays are used to store multiple values in a single variable, instead of declaring separate variables for each value.

### Why Use Arrays?
- Store multiple values of the same type efficiently
- Access elements quickly using an index
- Organize data in a structured manner
- Essential for many algorithms and data structures

### Key Characteristics
- **Fixed size**: Once created, the size cannot be changed
- **Zero-indexed**: First element is at index 0
- **Homogeneous**: All elements must be of the same type
- **Reference type**: Arrays are objects in Java

---

## Declaring and Initializing Arrays

### Basic Syntax

```java
// Declaration syntax 1 (preferred)
dataType[] arrayName;

// Declaration syntax 2
dataType arrayName[];
```

### Example: Different Ways to Create Arrays

```java
public class ArrayBasics {
    public static void main(String[] args) {
        // Method 1: Declare and allocate memory separately
        int[] numbers;                  // Declaration
        numbers = new int[5];           // Memory allocation for 5 integers
        
        // Method 2: Declare and allocate in one line
        int[] scores = new int[10];     // Array of 10 integers (all initialized to 0)
        
        // Method 3: Declare and initialize with values
        int[] ages = {18, 25, 30, 45, 60};  // Array with 5 elements
        
        // Method 4: Using new keyword with initialization
        String[] names = new String[] {"Alice", "Bob", "Charlie"};
        
        // Method 5: Anonymous array initialization
        printArray(new int[] {1, 2, 3, 4, 5});
        
        // Different data types
        double[] prices = {19.99, 29.99, 39.99};
        boolean[] flags = {true, false, true, true};
        char[] letters = {'A', 'B', 'C', 'D'};
    }
    
    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}
```

**Output:**
```
1 2 3 4 5
```

**Explanation:**
- **Method 1**: Two-step process - first declare, then allocate memory
- **Method 2**: Combined declaration and allocation - all elements initialized to default values (0 for int)
- **Method 3**: Array literal - most concise way when you know the values
- **Method 4**: Explicit initialization with new keyword
- **Method 5**: Useful when passing arrays to methods directly

---

## Accessing and Modifying Array Elements

### Index-Based Access

```java
public class ArrayAccess {
    public static void main(String[] args) {
        // Create an array
        String[] fruits = {"Apple", "Banana", "Cherry", "Date", "Elderberry"};
        
        // Accessing elements (index starts at 0)
        System.out.println("First fruit: " + fruits[0]);      // Apple
        System.out.println("Second fruit: " + fruits[1]);     // Banana
        System.out.println("Last fruit: " + fruits[4]);       // Elderberry
        
        // Modifying elements
        fruits[1] = "Blueberry";                              // Change Banana to Blueberry
        System.out.println("Modified second fruit: " + fruits[1]);  // Blueberry
        
        // Using variables as indices
        int index = 3;
        System.out.println("Fruit at index " + index + ": " + fruits[index]);  // Date
        
        // Common error: ArrayIndexOutOfBoundsException
        try {
            System.out.println(fruits[10]);  // Index 10 doesn't exist!
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Index out of bounds!");
        }
    }
}
```

**Output:**
```
First fruit: Apple
Second fruit: Banana
Last fruit: Elderberry
Modified second fruit: Blueberry
Fruit at index 3: Date
Error: Index out of bounds!
```

**Explanation:**
- **Index Range**: Valid indices are from 0 to (length - 1)
- **Zero-indexed**: First element is always at index 0
- **Modification**: Use assignment operator to change values
- **Runtime Error**: Accessing invalid indices throws `ArrayIndexOutOfBoundsException`

---

## Array Length

### The length Property

```java
public class ArrayLength {
    public static void main(String[] args) {
        int[] numbers = {10, 20, 30, 40, 50};
        
        // Get array length using .length property (not a method!)
        int size = numbers.length;
        System.out.println("Array length: " + size);           // 5
        
        // Access last element using length
        int lastElement = numbers[numbers.length - 1];
        System.out.println("Last element: " + lastElement);    // 50
        
        // Useful for loops
        System.out.println("All elements:");
        for (int i = 0; i < numbers.length; i++) {
            System.out.println("Index " + i + ": " + numbers[i]);
        }
        
        // Empty array
        int[] empty = new int[0];
        System.out.println("Empty array length: " + empty.length);  // 0
    }
}
```

**Output:**
```
Array length: 5
Last element: 50
All elements:
Index 0: 10
Index 1: 20
Index 2: 30
Index 3: 40
Index 4: 50
Empty array length: 0
```

**Explanation:**
- **length is a property, not a method**: No parentheses needed
- **Immutable**: Array length cannot be changed after creation
- **Last Index Formula**: `array.length - 1`
- **Loop Condition**: Use `i < array.length` to avoid index errors

---

## Iterating Through Arrays

### Different Ways to Loop Through Arrays

```java
public class ArrayIteration {
    public static void main(String[] args) {
        int[] scores = {85, 92, 78, 90, 88};
        
        // Method 1: Traditional for loop (with index)
        System.out.println("Method 1: Traditional for loop");
        for (int i = 0; i < scores.length; i++) {
            System.out.println("Score at index " + i + ": " + scores[i]);
        }
        
        // Method 2: Enhanced for loop (for-each) - Recommended when index not needed
        System.out.println("\nMethod 2: Enhanced for loop");
        for (int score : scores) {
            System.out.println("Score: " + score);
        }
        
        // Method 3: While loop
        System.out.println("\nMethod 3: While loop");
        int index = 0;
        while (index < scores.length) {
            System.out.println("Score: " + scores[index]);
            index++;
        }
        
        // Method 4: Reverse iteration
        System.out.println("\nMethod 4: Reverse iteration");
        for (int i = scores.length - 1; i >= 0; i--) {
            System.out.println("Score: " + scores[i]);
        }
        
        // Calculating sum using loop
        int sum = 0;
        for (int score : scores) {
            sum += score;
        }
        double average = (double) sum / scores.length;
        System.out.println("\nTotal: " + sum);
        System.out.println("Average: " + average);
    }
}
```

**Output:**
```
Method 1: Traditional for loop
Score at index 0: 85
Score at index 1: 92
Score at index 2: 78
Score at index 3: 90
Score at index 4: 88

Method 2: Enhanced for loop
Score: 85
Score: 92
Score: 78
Score: 90
Score: 88

Method 3: While loop
Score: 85
Score: 92
Score: 78
Score: 90
Score: 88

Method 4: Reverse iteration
Score: 88
Score: 90
Score: 78
Score: 92
Score: 85

Total: 433
Average: 86.6
```

**Explanation:**
- **Traditional for loop**: Best when you need the index
- **Enhanced for loop**: Cleaner syntax, use when index not needed
- **While loop**: Useful for complex iteration conditions
- **Reverse iteration**: Start from last element, decrement index

---

## 2D Arrays (Multidimensional Arrays)

### Understanding 2D Arrays

A 2D array is essentially an **array of arrays**. Think of it as a table with rows and columns.

### Declaration and Initialization

```java
public class TwoDArrays {
    public static void main(String[] args) {
        // Method 1: Declare and allocate memory
        int[][] matrix = new int[3][4];  // 3 rows, 4 columns
        
        // Method 2: Initialize with values
        int[][] grid = {
            {1, 2, 3},      // Row 0
            {4, 5, 6},      // Row 1
            {7, 8, 9}       // Row 2
        };
        
        // Method 3: Jagged array (different column sizes)
        int[][] jagged = {
            {1, 2},
            {3, 4, 5, 6},
            {7}
        };
        
        // Accessing elements
        System.out.println("Element at [1][2]: " + grid[1][2]);  // 6
        
        // Modifying elements
        grid[0][0] = 10;
        System.out.println("Modified [0][0]: " + grid[0][0]);    // 10
        
        // Getting dimensions
        int rows = grid.length;           // Number of rows
        int cols = grid[0].length;        // Number of columns in first row
        System.out.println("Rows: " + rows + ", Columns: " + cols);
    }
}
```

**Output:**
```
Element at [1][2]: 6
Modified [0][0]: 10
Rows: 3, Columns: 3
```

### Iterating Through 2D Arrays

```java
public class TwoDArrayIteration {
    public static void main(String[] args) {
        int[][] matrix = {
            {1,  2,  3,  4},
            {5,  6,  7,  8},
            {9, 10, 11, 12}
        };
        
        // Method 1: Nested traditional for loops
        System.out.println("Method 1: Nested for loops");
        for (int i = 0; i < matrix.length; i++) {           // Iterate rows
            for (int j = 0; j < matrix[i].length; j++) {    // Iterate columns
                System.out.print(matrix[i][j] + "\t");
            }
            System.out.println();  // New line after each row
        }
        
        // Method 2: Enhanced for loops
        System.out.println("\nMethod 2: Enhanced for loops");
        for (int[] row : matrix) {           // Each row is an array
            for (int element : row) {        // Each element in the row
                System.out.print(element + "\t");
            }
            System.out.println();
        }
        
        // Practical example: Sum of all elements
        int sum = 0;
        for (int[] row : matrix) {
            for (int element : row) {
                sum += element;
            }
        }
        System.out.println("\nSum of all elements: " + sum);
        
        // Diagonal elements (for square matrices)
        System.out.println("\nDiagonal elements:");
        for (int i = 0; i < Math.min(matrix.length, matrix[0].length); i++) {
            System.out.print(matrix[i][i] + " ");
        }
    }
}
```

**Output:**
```
Method 1: Nested for loops
1	2	3	4	
5	6	7	8	
9	10	11	12	

Method 2: Enhanced for loops
1	2	3	4	
5	6	7	8	
9	10	11	12	

Sum of all elements: 78

Diagonal elements:
1 6 11
```

**Explanation:**
- **First index**: Row number (vertical position)
- **Second index**: Column number (horizontal position)
- **Nested loops**: Outer loop for rows, inner loop for columns
- **Jagged arrays**: Rows can have different lengths
- **row.length**: Gets the number of columns in a specific row

### Practical 2D Array Examples

```java
public class TwoDArrayExamples {
    public static void main(String[] args) {
        // Example 1: Student grades (3 students, 4 subjects)
        int[][] grades = {
            {85, 90, 78, 92},   // Student 1
            {88, 76, 95, 89},   // Student 2
            {92, 88, 84, 90}    // Student 3
        };
        
        // Calculate each student's average
        System.out.println("Student Averages:");
        for (int i = 0; i < grades.length; i++) {
            int sum = 0;
            for (int j = 0; j < grades[i].length; j++) {
                sum += grades[i][j];
            }
            double average = (double) sum / grades[i].length;
            System.out.println("Student " + (i + 1) + ": " + average);
        }
        
        // Example 2: Tic-Tac-Toe board
        char[][] board = {
            {'X', 'O', 'X'},
            {'O', 'X', 'O'},
            {'X', ' ', 'O'}
        };
        
        System.out.println("\nTic-Tac-Toe Board:");
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                System.out.print(board[i][j]);
                if (j < board[i].length - 1) {
                    System.out.print(" | ");
                }
            }
            System.out.println();
            if (i < board.length - 1) {
                System.out.println("---------");
            }
        }
    }
}
```

**Output:**
```
Student Averages:
Student 1: 86.25
Student 2: 87.0
Student 3: 88.5

Tic-Tac-Toe Board:
X | O | X
---------
O | X | O
---------
X |   | O
```

---

## Common Array Operations

### Copying Arrays

```java
import java.util.Arrays;

public class ArrayCopying {
    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4, 5};
        
        // Method 1: Manual copying (not recommended)
        int[] copy1 = new int[original.length];
        for (int i = 0; i < original.length; i++) {
            copy1[i] = original[i];
        }
        
        // Method 2: Arrays.copyOf() - Recommended
        int[] copy2 = Arrays.copyOf(original, original.length);
        
        // Method 3: Arrays.copyOfRange() - Copy a portion
        int[] copy3 = Arrays.copyOfRange(original, 1, 4);  // Copies indices 1, 2, 3
        
        // Method 4: System.arraycopy() - Fast and efficient
        int[] copy4 = new int[original.length];
        System.arraycopy(original, 0, copy4, 0, original.length);
        
        // Method 5: clone() - Creates shallow copy
        int[] copy5 = original.clone();
        
        System.out.println("Original: " + Arrays.toString(original));
        System.out.println("Copy 2: " + Arrays.toString(copy2));
        System.out.println("Copy 3 (partial): " + Arrays.toString(copy3));
        
        // Important: Assignment does NOT create a copy!
        int[] notACopy = original;  // Both variables point to same array
        notACopy[0] = 999;
        System.out.println("Original after modifying 'notACopy': " + Arrays.toString(original));
    }
}
```

**Output:**
```
Original: [1, 2, 3, 4, 5]
Copy 2: [1, 2, 3, 4, 5]
Copy 3 (partial): [2, 3, 4]
Original after modifying 'notACopy': [999, 2, 3, 4, 5]
```

### Comparing Arrays

```java
import java.util.Arrays;

public class ArrayComparison {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {1, 2, 3, 4, 5};
        int[] arr3 = {1, 2, 3, 4, 6};
        
        // Wrong way: Using == (compares references, not content)
        System.out.println("arr1 == arr2: " + (arr1 == arr2));  // false
        
        // Correct way: Using Arrays.equals()
        System.out.println("Arrays.equals(arr1, arr2): " + Arrays.equals(arr1, arr2));  // true
        System.out.println("Arrays.equals(arr1, arr3): " + Arrays.equals(arr1, arr3));  // false
        
        // For 2D arrays: Use Arrays.deepEquals()
        int[][] matrix1 = {{1, 2}, {3, 4}};
        int[][] matrix2 = {{1, 2}, {3, 4}};
        System.out.println("Arrays.deepEquals(matrix1, matrix2): " + Arrays.deepEquals(matrix1, matrix2));  // true
    }
}
```

**Output:**
```
arr1 == arr2: false
Arrays.equals(arr1, arr2): true
Arrays.equals(arr1, arr3): false
Arrays.deepEquals(matrix1, matrix2): true
```

### Finding Elements

```java
public class ArraySearching {
    public static void main(String[] args) {
        int[] numbers = {15, 23, 8, 42, 16, 30, 4};
        
        // Linear search - Find if element exists
        int searchValue = 42;
        boolean found = false;
        int foundIndex = -1;
        
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == searchValue) {
                found = true;
                foundIndex = i;
                break;  // Stop searching once found
            }
        }
        
        if (found) {
            System.out.println(searchValue + " found at index " + foundIndex);
        } else {
            System.out.println(searchValue + " not found");
        }
        
        // Find maximum element
        int max = numbers[0];
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] > max) {
                max = numbers[i];
            }
        }
        System.out.println("Maximum value: " + max);
        
        // Find minimum element
        int min = numbers[0];
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] < min) {
                min = numbers[i];
            }
        }
        System.out.println("Minimum value: " + min);
    }
}
```

**Output:**
```
42 found at index 3
Maximum value: 42
Minimum value: 4
```

---

## Arrays Utility Class Methods

The `java.util.Arrays` class provides many useful static methods for array manipulation.

### Arrays.toString()

```java
import java.util.Arrays;

public class ArraysToString {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        String[] names = {"Alice", "Bob", "Charlie"};
        
        // Convert array to readable string format
        System.out.println("Numbers: " + Arrays.toString(numbers));
        System.out.println("Names: " + Arrays.toString(names));
        
        // For 2D arrays, use deepToString()
        int[][] matrix = {{1, 2, 3}, {4, 5, 6}};
        System.out.println("Matrix: " + Arrays.deepToString(matrix));
    }
}
```

**Output:**
```
Numbers: [1, 2, 3, 4, 5]
Names: [Alice, Bob, Charlie]
Matrix: [[1, 2, 3], [4, 5, 6]]
```

### Arrays.fill()

```java
import java.util.Arrays;

public class ArraysFill {
    public static void main(String[] args) {
        // Fill entire array with a value
        int[] numbers = new int[5];
        Arrays.fill(numbers, 10);
        System.out.println("Filled with 10: " + Arrays.toString(numbers));
        
        // Fill a range of array
        int[] scores = new int[10];
        Arrays.fill(scores, 0, 5, 100);  // Fill indices 0 to 4 with 100
        System.out.println("Partial fill: " + Arrays.toString(scores));
        
        // Fill with different data types
        boolean[] flags = new boolean[5];
        Arrays.fill(flags, true);
        System.out.println("Boolean array: " + Arrays.toString(flags));
        
        String[] words = new String[4];
        Arrays.fill(words, "Hello");
        System.out.println("String array: " + Arrays.toString(words));
    }
}
```

**Output:**
```
Filled with 10: [10, 10, 10, 10, 10]
Partial fill: [100, 100, 100, 100, 100, 0, 0, 0, 0, 0]
Boolean array: [true, true, true, true, true]
String array: [Hello, Hello, Hello, Hello]
```

**Explanation:**
- **Arrays.fill(array, value)**: Fills entire array with specified value
- **Arrays.fill(array, fromIndex, toIndex, value)**: Fills range [fromIndex, toIndex) with value
- **Use cases**: Initializing arrays, resetting values, creating test data

### Arrays.sort()

```java
import java.util.Arrays;

public class ArraysSort {
    public static void main(String[] args) {
        // Sort integer array (ascending order)
        int[] numbers = {5, 2, 8, 1, 9, 3};
        Arrays.sort(numbers);
        System.out.println("Sorted numbers: " + Arrays.toString(numbers));
        
        // Sort string array (lexicographic order)
        String[] names = {"Charlie", "Alice", "Bob", "David"};
        Arrays.sort(names);
        System.out.println("Sorted names: " + Arrays.toString(names));
        
        // Sort a portion of array
        int[] scores = {80, 95, 70, 85, 90, 75};
        Arrays.sort(scores, 1, 4);  // Sort indices 1 to 3
        System.out.println("Partially sorted: " + Arrays.toString(scores));
        
        // Sort in descending order (using wrapper classes)
        Integer[] nums = {5, 2, 8, 1, 9, 3};
        Arrays.sort(nums, (a, b) -> b - a);  // Comparator for descending
        System.out.println("Descending order: " + Arrays.toString(nums));
    }
}
```

**Output:**
```
Sorted numbers: [1, 2, 3, 5, 8, 9]
Sorted names: [Alice, Bob, Charlie, David]
Partially sorted: [80, 70, 85, 95, 90, 75]
Descending order: [9, 8, 5, 3, 2, 1]
```

**Explanation:**
- **Arrays.sort(array)**: Sorts entire array in ascending order
- **Arrays.sort(array, fromIndex, toIndex)**: Sorts specified range
- **Time Complexity**: O(n log n) using Dual-Pivot Quicksort
- **Note**: Changes the original array (in-place sorting)

### Arrays.binarySearch()

```java
import java.util.Arrays;

public class ArraysBinarySearch {
    public static void main(String[] args) {
        // Binary search requires sorted array
        int[] numbers = {2, 5, 8, 12, 16, 23, 38, 45, 56, 67};
        
        // Search for existing element
        int index = Arrays.binarySearch(numbers, 23);
        System.out.println("Index of 23: " + index);
        
        // Search for non-existing element (returns negative value)
        int notFound = Arrays.binarySearch(numbers, 25);
        System.out.println("Search for 25: " + notFound);  // Negative value
        System.out.println("Insertion point: " + (-notFound - 1));
        
        // Search in a range
        int rangeSearch = Arrays.binarySearch(numbers, 2, 6, 12);
        System.out.println("Search in range [2,6): " + rangeSearch);
        
        // String array search
        String[] names = {"Alice", "Bob", "Charlie", "David", "Eve"};
        int nameIndex = Arrays.binarySearch(names, "Charlie");
        System.out.println("Index of Charlie: " + nameIndex);
    }
}
```

**Output:**
```
Index of 23: 5
Search for 25: -7
Insertion point: 6
Search in range [2,6): 3
Index of Charlie: 2
```

**Explanation:**
- **Prerequisite**: Array MUST be sorted before binary search
- **Return value**: Index of element if found
- **If not found**: Returns `-(insertion point) - 1`
- **Time Complexity**: O(log n) - very fast for large arrays

### Arrays.copyOf() and Arrays.copyOfRange()

```java
import java.util.Arrays;

public class ArraysCopy {
    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4, 5};
        
        // Copy entire array
        int[] copy1 = Arrays.copyOf(original, original.length);
        System.out.println("Exact copy: " + Arrays.toString(copy1));
        
        // Copy with different length (truncate)
        int[] copy2 = Arrays.copyOf(original, 3);
        System.out.println("Truncated copy: " + Arrays.toString(copy2));
        
        // Copy with larger length (pads with zeros)
        int[] copy3 = Arrays.copyOf(original, 8);
        System.out.println("Extended copy: " + Arrays.toString(copy3));
        
        // Copy a range (from index 1 to 4, exclusive)
        int[] copy4 = Arrays.copyOfRange(original, 1, 4);
        System.out.println("Range copy [1,4): " + Arrays.toString(copy4));
        
        // Copy from middle to end
        int[] copy5 = Arrays.copyOfRange(original, 2, original.length);
        System.out.println("From index 2 to end: " + Arrays.toString(copy5));
    }
}
```

**Output:**
```
Exact copy: [1, 2, 3, 4, 5]
Truncated copy: [1, 2, 3]
Extended copy: [1, 2, 3, 4, 5, 0, 0, 0]
Range copy [1,4): [2, 3, 4]
From index 2 to end: [3, 4, 5]
```

### Arrays.equals() and Arrays.deepEquals()

```java
import java.util.Arrays;

public class ArraysEquals {
    public static void main(String[] args) {
        // 1D array comparison
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {1, 2, 3, 4, 5};
        int[] arr3 = {1, 2, 3, 4, 6};
        
        System.out.println("arr1 equals arr2: " + Arrays.equals(arr1, arr2));  // true
        System.out.println("arr1 equals arr3: " + Arrays.equals(arr1, arr3));  // false
        
        // Compare ranges
        boolean rangeEquals = Arrays.equals(arr1, 0, 3, arr3, 0, 3);
        System.out.println("First 3 elements equal: " + rangeEquals);  // true
        
        // 2D array comparison (must use deepEquals)
        int[][] matrix1 = {{1, 2}, {3, 4}};
        int[][] matrix2 = {{1, 2}, {3, 4}};
        int[][] matrix3 = {{1, 2}, {3, 5}};
        
        System.out.println("matrix1 deepEquals matrix2: " + Arrays.deepEquals(matrix1, matrix2));  // true
        System.out.println("matrix1 deepEquals matrix3: " + Arrays.deepEquals(matrix1, matrix3));  // false
        
        // Regular equals doesn't work for 2D arrays
        System.out.println("matrix1 equals matrix2 (wrong): " + Arrays.equals(matrix1, matrix2));  // false!
    }
}
```

**Output:**
```
arr1 equals arr2: true
arr1 equals arr3: false
First 3 elements equal: true
matrix1 deepEquals matrix2: true
matrix1 deepEquals matrix3: false
matrix1 equals matrix2 (wrong): false
```

### Arrays.asList()

```java
import java.util.Arrays;
import java.util.List;

public class ArraysAsList {
    public static void main(String[] args) {
        // Convert array to List (fixed-size)
        String[] array = {"Apple", "Banana", "Cherry"};
        List<String> list = Arrays.asList(array);
        
        System.out.println("List: " + list);
        System.out.println("List size: " + list.size());
        
        // Can modify elements
        list.set(1, "Blueberry");
        System.out.println("Modified list: " + list);
        System.out.println("Original array: " + Arrays.toString(array));  // Array also changed!
        
        // Cannot add or remove elements (UnsupportedOperationException)
        try {
            list.add("Date");  // This will throw exception
        } catch (UnsupportedOperationException e) {
            System.out.println("Cannot add elements to fixed-size list");
        }
        
        // Direct creation without array variable
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        System.out.println("Numbers list: " + numbers);
    }
}
```

**Output:**
```
List: [Apple, Banana, Cherry]
List size: 3
Modified list: [Apple, Blueberry, Cherry]
Original array: [Apple, Blueberry, Cherry]
Cannot add elements to fixed-size list
Numbers list: [1, 2, 3, 4, 5]
```

### Arrays.stream()

```java
import java.util.Arrays;

public class ArraysStream {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        
        // Create stream and perform operations
        int sum = Arrays.stream(numbers).sum();
        System.out.println("Sum: " + sum);
        
        double average = Arrays.stream(numbers).average().orElse(0.0);
        System.out.println("Average: " + average);
        
        int max = Arrays.stream(numbers).max().orElse(0);
        System.out.println("Max: " + max);
        
        // Filter and count
        long evenCount = Arrays.stream(numbers).filter(n -> n % 2 == 0).count();
        System.out.println("Even numbers count: " + evenCount);
        
        // Transform and collect
        int[] squared = Arrays.stream(numbers).map(n -> n * n).toArray();
        System.out.println("Squared: " + Arrays.toString(squared));
    }
}
```

**Output:**
```
Sum: 55
Average: 5.5
Max: 10
Even numbers count: 5
Squared: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Complete Arrays Class Methods Summary

```java
import java.util.Arrays;

public class ArraysMethodsSummary {
    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 1, 9};
        
        // 1. Arrays.toString() - Convert to string
        System.out.println("toString: " + Arrays.toString(arr));
        
        // 2. Arrays.fill() - Fill with value
        int[] filled = new int[5];
        Arrays.fill(filled, 7);
        System.out.println("fill: " + Arrays.toString(filled));
        
        // 3. Arrays.sort() - Sort array
        Arrays.sort(arr);
        System.out.println("sort: " + Arrays.toString(arr));
        
        // 4. Arrays.binarySearch() - Find element
        int index = Arrays.binarySearch(arr, 5);
        System.out.println("binarySearch(5): " + index);
        
        // 5. Arrays.copyOf() - Copy array
        int[] copy = Arrays.copyOf(arr, arr.length);
        System.out.println("copyOf: " + Arrays.toString(copy));
        
        // 6. Arrays.copyOfRange() - Copy range
        int[] range = Arrays.copyOfRange(arr, 1, 4);
        System.out.println("copyOfRange(1,4): " + Arrays.toString(range));
        
        // 7. Arrays.equals() - Compare arrays
        boolean equal = Arrays.equals(arr, copy);
        System.out.println("equals: " + equal);
        
        // 8. Arrays.hashCode() - Get hash code
        int hash = Arrays.hashCode(arr);
        System.out.println("hashCode: " + hash);
        
        // 9. Arrays.asList() - Convert to List
        Integer[] nums = {1, 2, 3};
        System.out.println("asList: " + Arrays.asList(nums));
        
        // 10. Arrays.stream() - Create stream
        int sum = Arrays.stream(arr).sum();
        System.out.println("stream().sum(): " + sum);
    }
}
```

---

## Common Pitfalls and Best Practices

### Pitfall 1: ArrayIndexOutOfBoundsException

```java
public class Pitfall1 {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        
        // WRONG: Using <= instead of <
        // for (int i = 0; i <= arr.length; i++) {  // Will throw exception
        //     System.out.println(arr[i]);
        // }
        
        // CORRECT: Use < for upper bound
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    }
}
```

### Pitfall 2: Reference vs Copy

```java
import java.util.Arrays;

public class Pitfall2 {
    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4, 5};
        
        // WRONG: This doesn't create a copy!
        int[] notACopy = original;
        notACopy[0] = 999;
        System.out.println("Original: " + Arrays.toString(original));  // [999, 2, 3, 4, 5]
        
        // CORRECT: Create a proper copy
        int[] realCopy = Arrays.copyOf(original, original.length);
        realCopy[1] = 888;
        System.out.println("Original: " + Arrays.toString(original));  // [999, 2, 3, 4, 5]
        System.out.println("Real Copy: " + Arrays.toString(realCopy));  // [999, 888, 3, 4, 5]
    }
}
```

### Pitfall 3: Comparing Arrays with ==

```java
import java.util.Arrays;

public class Pitfall3 {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        
        // WRONG: Compares references, not content
        System.out.println("arr1 == arr2: " + (arr1 == arr2));  // false
        
        // CORRECT: Use Arrays.equals()
        System.out.println("Arrays.equals: " + Arrays.equals(arr1, arr2));  // true
    }
}
```

### Pitfall 4: Modifying Array Size

```java
public class Pitfall4 {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        
        // Arrays have FIXED size - cannot change
        // arr.length = 5;  // Compilation error - cannot assign to length
        
        // To "resize", create a new array
        int[] larger = new int[5];
        System.arraycopy(arr, 0, larger, 0, arr.length);
        
        // Or use Arrays.copyOf()
        int[] resized = java.util.Arrays.copyOf(arr, 5);
    }
}
```

### Best Practices

```java
import java.util.Arrays;

public class BestPractices {
    public static void main(String[] args) {
        // 1. Use enhanced for loop when index not needed
        int[] numbers = {1, 2, 3, 4, 5};
        for (int num : numbers) {  // Cleaner and less error-prone
            System.out.print(num + " ");
        }
        System.out.println();
        
        // 2. Always validate array bounds
        int index = 10;
        if (index >= 0 && index < numbers.length) {
            System.out.println(numbers[index]);
        }
        
        // 3. Use Arrays utility methods
        System.out.println(Arrays.toString(numbers));  // Better than manual printing
        
        // 4. Consider using ArrayList for dynamic sizing
        // List<Integer> list = new ArrayList<>();  // Can grow/shrink
        
        // 5. Initialize arrays with meaningful values
        int[] scores = new int[5];
        Arrays.fill(scores, -1);  // Use -1 to indicate "no score"
        
        // 6. Use descriptive variable names
        int[] studentGrades = {85, 90, 78};  // Good
        // int[] a = {85, 90, 78};  // Bad
        
        // 7. Document array structure for 2D arrays
        int[][] grid = new int[3][4];  // 3 rows, 4 columns - document this!
    }
}
```

### Performance Tips

```java
import java.util.Arrays;

public class PerformanceTips {
    public static void main(String[] args) {
        int size = 1000000;
        int[] arr = new int[size];
        
        // 1. Arrays.fill() is faster than manual loop
        long start = System.nanoTime();
        Arrays.fill(arr, 5);
        long time1 = System.nanoTime() - start;
        System.out.println("Arrays.fill(): " + time1 + " ns");
        
        start = System.nanoTime();
        for (int i = 0; i < arr.length; i++) {
            arr[i] = 5;
        }
        long time2 = System.nanoTime() - start;
        System.out.println("Manual loop: " + time2 + " ns");
        
        // 2. System.arraycopy() is fastest for copying
        int[] dest = new int[size];
        start = System.nanoTime();
        System.arraycopy(arr, 0, dest, 0, arr.length);
        long time3 = System.nanoTime() - start;
        System.out.println("System.arraycopy(): " + time3 + " ns");
        
        // 3. Cache array length in frequently accessed loops
        int length = arr.length;  // Cache this
        for (int i = 0; i < length; i++) {  // Slightly faster
            // process arr[i]
        }
    }
}
```

---

## Summary

### Key Takeaways

1. **Arrays are fixed-size** - size cannot change after creation
2. **Zero-indexed** - first element is at index 0, last at length-1
3. **Use Arrays class** - provides powerful utility methods
4. **Enhanced for loop** - use when you don't need the index
5. **Arrays.equals()** - always use for comparing array content
6. **Arrays.copyOf()** - use for creating proper copies
7. **Validate bounds** - always check indices before accessing
8. **2D arrays** - use nested loops for iteration

### Quick Reference

| Operation | Method/Syntax |
|-----------|---------------|
| Declare | `int[] arr;` |
| Initialize | `int[] arr = {1, 2, 3};` |
| Access | `arr[index]` |
| Length | `arr.length` |
| Print | `Arrays.toString(arr)` |
| Sort | `Arrays.sort(arr)` |
| Search | `Arrays.binarySearch(arr, value)` |
| Fill | `Arrays.fill(arr, value)` |
| Copy | `Arrays.copyOf(arr, length)` |
| Compare | `Arrays.equals(arr1, arr2)` |
| Convert to List | `Arrays.asList(arr)` |

---

**Happy Coding! 🚀**