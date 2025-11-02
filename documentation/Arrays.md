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

## Arrays of Objects

### Understanding Object Arrays

Object arrays store references to objects rather than primitive values. Each element in an object array is a reference to an object of the specified class.

### Creating and Using Object Arrays

```java
// Define a simple Person class
class Person {
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class ObjectArrays {
    public static void main(String[] args) {
        // Method 1: Declare and allocate memory
        Person[] people = new Person[3];
        
        // Initialize each element
        people[0] = new Person("Alice", 25);
        people[1] = new Person("Bob", 30);
        people[2] = new Person("Charlie", 35);
        
        // Method 2: Declare and initialize together
        Person[] team = {
            new Person("David", 28),
            new Person("Eve", 32),
            new Person("Frank", 27)
        };
        
        // Accessing object properties
        System.out.println("First person's name: " + people[0].name);
        System.out.println("First person's age: " + people[0].age);
        
        // Iterating through object array
        System.out.println("\nAll people:");
        for (Person person : people) {
            System.out.println(person);
        }
        
        // Modifying object properties
        people[1].age = 31;
        System.out.println("\nModified: " + people[1]);
        
        // Important: Array stores references
        Person[] copy = people;  // Both reference same objects
        copy[0].name = "Alicia";
        System.out.println("Original array affected: " + people[0]);
    }
}
```

**Output:**
```
First person's name: Alice
First person's age: 25

All people:
Alice (25)
Bob (30)
Charlie (35)

Modified: Bob (31)
Original array affected: Alicia (25)
```

**Explanation:**
- **Reference Storage**: Array elements hold references, not the objects themselves
- **Null Values**: Uninitialized elements are `null` by default
- **Shallow Copy**: Copying array copies references, not objects
- **Memory**: Objects are stored in heap, array holds references

### Practical Object Array Examples

```java
import java.util.Arrays;

// Student class for examples
class Student {
    String name;
    int rollNumber;
    double gpa;
    
    Student(String name, int rollNumber, double gpa) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.gpa = gpa;
    }
    
    @Override
    public String toString() {
        return String.format("%s (Roll: %d, GPA: %.2f)", name, rollNumber, gpa);
    }
}

public class StudentArrayExample {
    public static void main(String[] args) {
        // Create array of students
        Student[] students = {
            new Student("Alice", 101, 3.8),
            new Student("Bob", 102, 3.5),
            new Student("Charlie", 103, 3.9),
            new Student("David", 104, 3.6),
            new Student("Eve", 105, 3.7)
        };
        
        // Display all students
        System.out.println("All Students:");
        for (Student student : students) {
            System.out.println(student);
        }
        
        // Find student with highest GPA
        Student topStudent = students[0];
        for (int i = 1; i < students.length; i++) {
            if (students[i].gpa > topStudent.gpa) {
                topStudent = students[i];
            }
        }
        System.out.println("\nTop Student: " + topStudent);
        
        // Calculate average GPA
        double totalGPA = 0;
        for (Student student : students) {
            totalGPA += student.gpa;
        }
        double averageGPA = totalGPA / students.length;
        System.out.println("Average GPA: " + String.format("%.2f", averageGPA));
        
        // Filter students with GPA > 3.7
        System.out.println("\nStudents with GPA > 3.7:");
        for (Student student : students) {
            if (student.gpa > 3.7) {
                System.out.println(student);
            }
        }
        
        // Sort students by GPA (using Arrays.sort with comparator)
        Arrays.sort(students, (s1, s2) -> Double.compare(s2.gpa, s1.gpa));
        System.out.println("\nStudents sorted by GPA (descending):");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```

**Output:**
```
All Students:
Alice (Roll: 101, GPA: 3.80)
Bob (Roll: 102, GPA: 3.50)
Charlie (Roll: 103, GPA: 3.90)
David (Roll: 104, GPA: 3.60)
Eve (Roll: 105, GPA: 3.70)

Top Student: Charlie (Roll: 103, GPA: 3.90)
Average GPA: 3.70

Students with GPA > 3.7:
Alice (Roll: 101, GPA: 3.80)
Charlie (Roll: 103, GPA: 3.90)

Students sorted by GPA (descending):
Charlie (Roll: 103, GPA: 3.90)
Alice (Roll: 101, GPA: 3.80)
Eve (Roll: 105, GPA: 3.70)
David (Roll: 104, GPA: 3.60)
Bob (Roll: 102, GPA: 3.50)
```

### String Arrays

```java
public class StringArrays {
    public static void main(String[] args) {
        // String arrays are object arrays
        String[] fruits = {"Apple", "Banana", "Cherry", "Date"};
        
        // Common String array operations
        System.out.println("Length of first fruit: " + fruits[0].length());
        System.out.println("First fruit uppercase: " + fruits[0].toUpperCase());
        
        // Search for specific string
        String searchFor = "Banana";
        boolean found = false;
        for (String fruit : fruits) {
            if (fruit.equals(searchFor)) {
                found = true;
                break;
            }
        }
        System.out.println(searchFor + " found: " + found);
        
        // Concatenate all strings
        String combined = "";
        for (String fruit : fruits) {
            combined += fruit + " ";
        }
        System.out.println("Combined: " + combined.trim());
        
        // Using String.join()
        String joined = String.join(", ", fruits);
        System.out.println("Joined: " + joined);
    }
}
```

**Output:**
```
Length of first fruit: 5
First fruit uppercase: APPLE
Banana found: true
Combined: Apple Banana Cherry Date
Joined: Apple, Banana, Cherry, Date
```

---

## Working with Different Data Types

### Boolean Arrays

```java
import java.util.Arrays;

public class BooleanArrays {
    public static void main(String[] args) {
        // Create boolean array
        boolean[] flags = new boolean[5];  // All initialized to false by default
        System.out.println("Default boolean array: " + Arrays.toString(flags));
        
        // Initialize with values
        boolean[] answers = {true, false, true, true, false};
        System.out.println("Answer array: " + Arrays.toString(answers));
        
        // Set all to true
        Arrays.fill(flags, true);
        System.out.println("All true: " + Arrays.toString(flags));
        
        // Count true values
        int trueCount = 0;
        for (boolean answer : answers) {
            if (answer) {
                trueCount++;
            }
        }
        System.out.println("Number of true values: " + trueCount);
        
        // Toggle boolean values
        for (int i = 0; i < answers.length; i++) {
            answers[i] = !answers[i];  // Flip true to false and vice versa
        }
        System.out.println("Toggled: " + Arrays.toString(answers));
        
        // Check if all are true
        boolean allTrue = true;
        for (boolean answer : answers) {
            if (!answer) {
                allTrue = false;
                break;
            }
        }
        System.out.println("All true: " + allTrue);
        
        // Check if any is true
        boolean anyTrue = false;
        for (boolean answer : answers) {
            if (answer) {
                anyTrue = true;
                break;
            }
        }
        System.out.println("Any true: " + anyTrue);
    }
}
```

**Output:**
```
Default boolean array: [false, false, false, false, false]
Answer array: [true, false, true, true, false]
All true: [true, true, true, true, true]
Number of true values: 3
Toggled: [false, true, false, false, true]
All true: false
Any true: true
```

### Float and Double Arrays

```java
import java.util.Arrays;

public class FloatingPointArrays {
    public static void main(String[] args) {
        // Float array
        float[] prices = {19.99f, 29.99f, 39.99f, 49.99f};
        System.out.println("Prices (float): " + Arrays.toString(prices));
        
        // Double array - more precision
        double[] temperatures = {98.6, 100.4, 97.8, 99.2, 98.3};
        System.out.println("Temperatures (double): " + Arrays.toString(temperatures));
        
        // Calculate sum of doubles
        double sum = 0.0;
        for (double temp : temperatures) {
            sum += temp;
        }
        System.out.println("Total temperature: " + sum);
        
        // Calculate average
        double average = sum / temperatures.length;
        System.out.println("Average temperature: " + String.format("%.2f", average));
        
        // Find max temperature
        double max = temperatures[0];
        for (double temp : temperatures) {
            if (temp > max) {
                max = temp;
            }
        }
        System.out.println("Maximum temperature: " + max);
        
        // Find min temperature
        double min = temperatures[0];
        for (double temp : temperatures) {
            if (temp < min) {
                min = temp;
            }
        }
        System.out.println("Minimum temperature: " + min);
        
        // Round all values
        double[] roundedTemps = new double[temperatures.length];
        for (int i = 0; i < temperatures.length; i++) {
            roundedTemps[i] = Math.round(temperatures[i]);
        }
        System.out.println("Rounded temperatures: " + Arrays.toString(roundedTemps));
        
        // Compare float and double precision
        float floatValue = 0.1f + 0.1f + 0.1f;
        double doubleValue = 0.1 + 0.1 + 0.1;
        System.out.println("Float precision: " + floatValue);
        System.out.println("Double precision: " + doubleValue);
    }
}
```

**Output:**
```
Prices (float): [19.99, 29.99, 39.99, 49.99]
Temperatures (double): [98.6, 100.4, 97.8, 99.2, 98.3]
Total temperature: 494.3
Average temperature: 98.86
Maximum temperature: 100.4
Minimum temperature: 97.8
Rounded temperatures: [99.0, 100.0, 98.0, 99.0, 98.0]
Float precision: 0.3
Double precision: 0.30000000000000004
```

### Byte, Short, and Long Arrays

```java
import java.util.Arrays;

public class IntegerTypesArrays {
    public static void main(String[] args) {
        // Byte array (-128 to 127)
        byte[] bytes = {10, 20, 30, 40, 50};
        System.out.println("Byte array: " + Arrays.toString(bytes));
        System.out.println("Byte range: " + Byte.MIN_VALUE + " to " + Byte.MAX_VALUE);
        
        // Short array (-32,768 to 32,767)
        short[] shorts = {1000, 2000, 3000, 4000};
        System.out.println("\nShort array: " + Arrays.toString(shorts));
        System.out.println("Short range: " + Short.MIN_VALUE + " to " + Short.MAX_VALUE);
        
        // Long array (very large numbers)
        long[] distances = {384400L, 149600000L, 778500000L};  // Moon, Sun, Jupiter distances in km
        System.out.println("\nLong array: " + Arrays.toString(distances));
        System.out.println("Long range: " + Long.MIN_VALUE + " to " + Long.MAX_VALUE);
        
        // Converting between types
        int[] ints = new int[bytes.length];
        for (int i = 0; i < bytes.length; i++) {
            ints[i] = bytes[i];  // Byte to int (widening)
        }
        System.out.println("\nConverted byte to int: " + Arrays.toString(ints));
    }
}
```

**Output:**
```
Byte array: [10, 20, 30, 40, 50]
Byte range: -128 to 127

Short array: [1000, 2000, 3000, 4000]
Short range: -32768 to 32767

Long array: [384400, 149600000, 778500000]
Long range: -9223372036854775808 to 9223372036854775807

Converted byte to int: [10, 20, 30, 40, 50]
```

### Character Arrays

```java
import java.util.Arrays;

public class CharArrays {
    public static void main(String[] args) {
        // Character array
        char[] letters = {'H', 'e', 'l', 'l', 'o'};
        System.out.println("Char array: " + Arrays.toString(letters));
        
        // Print as string
        System.out.println("As string: " + new String(letters));
        
        // Vowels and consonants
        char[] alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".toCharArray();
        System.out.println("Alphabet length: " + alphabet.length);
        
        // Count vowels
        char[] vowels = {'A', 'E', 'I', 'O', 'U'};
        int vowelCount = 0;
        for (char ch : alphabet) {
            for (char vowel : vowels) {
                if (ch == vowel) {
                    vowelCount++;
                    break;
                }
            }
        }
        System.out.println("Vowel count: " + vowelCount);
        
        // Character operations
        char[] word = {'j', 'a', 'v', 'a'};
        System.out.println("Original: " + new String(word));
        
        // Convert to uppercase
        for (int i = 0; i < word.length; i++) {
            word[i] = Character.toUpperCase(word[i]);
        }
        System.out.println("Uppercase: " + new String(word));
    }
}
```

**Output:**
```
Char array: [H, e, l, l, o]
As string: Hello
Alphabet length: 26
Vowel count: 5
Original: java
Uppercase: JAVA
```

---

## Converting Data to Arrays

### Converting Numbers to Arrays

```java
import java.util.Arrays;

public class NumberToArray {
    public static void main(String[] args) {
        // Method 1: Convert integer to digit array
        int number = 12345;
        String numStr = String.valueOf(number);
        int[] digitArray = new int[numStr.length()];
        
        for (int i = 0; i < numStr.length(); i++) {
            digitArray[i] = Character.getNumericValue(numStr.charAt(i));
        }
        System.out.println("Number: " + number);
        System.out.println("Digit array: " + Arrays.toString(digitArray));
        
        // Method 2: Using mathematical operations
        int num = 6789;
        int temp = num;
        int length = String.valueOf(num).length();
        int[] digits = new int[length];
        
        for (int i = length - 1; i >= 0; i--) {
            digits[i] = temp % 10;  // Get last digit
            temp /= 10;              // Remove last digit
        }
        System.out.println("\nNumber: " + num);
        System.out.println("Digit array: " + Arrays.toString(digits));
        
        // Method 3: Convert double to array
        double decimal = 3.14159;
        String decimalStr = String.valueOf(decimal);
        String[] parts = decimalStr.split("\\.");
        
        System.out.println("\nDecimal: " + decimal);
        System.out.println("Integer part: " + parts[0]);
        System.out.println("Fractional part: " + parts[1]);
        
        // Convert each part to digit array
        int[] integerDigits = new int[parts[0].length()];
        for (int i = 0; i < parts[0].length(); i++) {
            integerDigits[i] = Character.getNumericValue(parts[0].charAt(i));
        }
        System.out.println("Integer digits: " + Arrays.toString(integerDigits));
        
        // Method 4: Float to array
        float floatNum = 98.6f;
        String floatStr = String.valueOf(floatNum);
        char[] floatChars = floatStr.toCharArray();
        System.out.println("\nFloat: " + floatNum);
        System.out.println("As char array: " + Arrays.toString(floatChars));
    }
}
```

**Output:**
```
Number: 12345
Digit array: [1, 2, 3, 4, 5]

Number: 6789
Digit array: [6, 7, 8, 9]

Decimal: 3.14159
Integer part: 3
Fractional part: 14159
Integer digits: [3]

Float: 98.6
As char array: [9, 8, ., 6]
```

### Converting Strings to Arrays

```java
import java.util.Arrays;

public class StringToArray {
    public static void main(String[] args) {
        String text = "Hello World";
        
        // Method 1: Convert string to char array
        char[] charArray = text.toCharArray();
        System.out.println("String: " + text);
        System.out.println("Char array: " + Arrays.toString(charArray));
        
        // Method 2: Split string into word array
        String sentence = "Java is awesome and powerful";
        String[] words = sentence.split(" ");
        System.out.println("\nSentence: " + sentence);
        System.out.println("Word array: " + Arrays.toString(words));
        System.out.println("Number of words: " + words.length);
        
        // Method 3: Split by comma (CSV format)
        String csv = "Apple,Banana,Cherry,Date,Elderberry";
        String[] fruits = csv.split(",");
        System.out.println("\nCSV: " + csv);
        System.out.println("Fruit array: " + Arrays.toString(fruits));
        
        // Method 4: Split by multiple delimiters
        String data = "John:25,Jane:30,Bob:35";
        String[] entries = data.split(",");
        System.out.println("\nData: " + data);
        for (String entry : entries) {
            String[] parts = entry.split(":");
            System.out.println("Name: " + parts[0] + ", Age: " + parts[1]);
        }
        
        // Method 5: Convert to byte array
        String message = "Hello";
        byte[] byteArray = message.getBytes();
        System.out.println("\nMessage: " + message);
        System.out.println("Byte array: " + Arrays.toString(byteArray));
        
        // Method 6: Split each character
        String code = "12345";
        String[] digitStrings = code.split("");
        System.out.println("\nCode: " + code);
        System.out.println("Digit strings: " + Arrays.toString(digitStrings));
        
        // Convert to int array
        int[] digitInts = new int[code.length()];
        for (int i = 0; i < code.length(); i++) {
            digitInts[i] = Integer.parseInt(digitStrings[i]);
        }
        System.out.println("Digit ints: " + Arrays.toString(digitInts));
    }
}
```

**Output:**
```
String: Hello World
Char array: [H, e, l, l, o,  , W, o, r, l, d]

Sentence: Java is awesome and powerful
Word array: [Java, is, awesome, and, powerful]
Number of words: 5

CSV: Apple,Banana,Cherry,Date,Elderberry
Fruit array: [Apple, Banana, Cherry, Date, Elderberry]

Data: John:25,Jane:30,Bob:35
Name: John, Age: 25
Name: Jane, Age: 30
Name: Bob, Age: 35

Message: Hello
Byte array: [72, 101, 108, 108, 111]

Code: 12345
Digit strings: [, 1, 2, 3, 4, 5]
Digit ints: [0, 1, 2, 3, 4, 5]
```

### Converting Arrays Back to Other Types

```java
import java.util.Arrays;
import java.util.stream.Collectors;

public class ArrayToOtherTypes {
    public static void main(String[] args) {
        // Method 1: Int array to number
        int[] digits = {1, 2, 3, 4, 5};
        int number = 0;
        for (int digit : digits) {
            number = number * 10 + digit;
        }
        System.out.println("Digit array: " + Arrays.toString(digits));
        System.out.println("As number: " + number);
        
        // Method 2: Char array to string
        char[] chars = {'H', 'e', 'l', 'l', 'o'};
        String text = new String(chars);
        System.out.println("\nChar array: " + Arrays.toString(chars));
        System.out.println("As string: " + text);
        
        // Method 3: String array to single string
        String[] words = {"Java", "is", "awesome"};
        String sentence = String.join(" ", words);
        System.out.println("\nWord array: " + Arrays.toString(words));
        System.out.println("As sentence: " + sentence);
        
        // Method 4: Using StringBuilder
        String[] parts = {"Hello", "World", "!"};
        StringBuilder sb = new StringBuilder();
        for (String part : parts) {
            sb.append(part).append(" ");
        }
        System.out.println("\nParts: " + Arrays.toString(parts));
        System.out.println("Combined: " + sb.toString().trim());
        
        // Method 5: Byte array to string
        byte[] bytes = {72, 101, 108, 108, 111};
        String message = new String(bytes);
        System.out.println("\nByte array: " + Arrays.toString(bytes));
        System.out.println("As string: " + message);
        
        // Method 6: Double array to formatted string
        double[] prices = {19.99, 29.99, 39.99};
        System.out.println("\nPrices: " + Arrays.toString(prices));
        System.out.print("Formatted: ");
        for (int i = 0; i < prices.length; i++) {
            System.out.printf("$%.2f", prices[i]);
            if (i < prices.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println();
        
        // Method 7: Array to comma-separated string
        Integer[] numbers = {10, 20, 30, 40, 50};
        String csv = Arrays.stream(numbers)
                          .map(String::valueOf)
                          .collect(Collectors.joining(","));
        System.out.println("\nNumber array: " + Arrays.toString(numbers));
        System.out.println("As CSV: " + csv);
    }
}
```

**Output:**
```
Digit array: [1, 2, 3, 4, 5]
As number: 12345

Char array: [H, e, l, l, o]
As string: Hello

Word array: [Java, is, awesome]
As sentence: Java is awesome

Parts: [Hello, World, !]
Combined: Hello World !

Byte array: [72, 101, 108, 108, 111]
As string: Hello

Prices: [19.99, 29.99, 39.99]
Formatted: $19.99, $29.99, $39.99

Number array: [10, 20, 30, 40, 50]
As CSV: 10,20,30,40,50
```

### Practical Conversion Examples

```java
import java.util.Arrays;

public class PracticalConversions {
    public static void main(String[] args) {
        // Example 1: Parse CSV data
        String csvData = "John,25,Engineer;Jane,30,Doctor;Bob,35,Teacher";
        String[] records = csvData.split(";");
        
        System.out.println("Parsing CSV data:");
        for (String record : records) {
            String[] fields = record.split(",");
            System.out.println("Name: " + fields[0] + 
                             ", Age: " + fields[1] + 
                             ", Profession: " + fields[2]);
        }
        
        // Example 2: Convert phone number to digits
        String phoneNumber = "(123) 456-7890";
        String digitsOnly = phoneNumber.replaceAll("[^0-9]", "");
        int[] phoneDigits = new int[digitsOnly.length()];
        
        for (int i = 0; i < digitsOnly.length(); i++) {
            phoneDigits[i] = Character.getNumericValue(digitsOnly.charAt(i));
        }
        System.out.println("\nPhone: " + phoneNumber);
        System.out.println("Digits: " + Arrays.toString(phoneDigits));
        
        // Example 3: Convert binary string to boolean array
        String binaryString = "10110010";
        boolean[] binaryArray = new boolean[binaryString.length()];
        
        for (int i = 0; i < binaryString.length(); i++) {
            binaryArray[i] = binaryString.charAt(i) == '1';
        }
        System.out.println("\nBinary string: " + binaryString);
        System.out.println("Boolean array: " + Arrays.toString(binaryArray));
        
        // Example 4: Parse grades from string
        String gradeInput = "85 92 78 90 88";
        String[] gradeStrings = gradeInput.split(" ");
        int[] grades = new int[gradeStrings.length];
        
        for (int i = 0; i < gradeStrings.length; i++) {
            grades[i] = Integer.parseInt(gradeStrings[i]);
        }
        
        System.out.println("\nGrade input: " + gradeInput);
        System.out.println("Grade array: " + Arrays.toString(grades));
        
        // Calculate average
        double sum = 0;
        for (int grade : grades) {
            sum += grade;
        }
        System.out.println("Average: " + (sum / grades.length));
    }
}
```

**Output:**
```
Parsing CSV data:
Name: John, Age: 25, Profession: Engineer
Name: Jane, Age: 30, Profession: Doctor
Name: Bob, Age: 35, Profession: Teacher

Phone: (123) 456-7890
Digits: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]

Binary string: 10110010
Boolean array: [true, false, true, true, false, false, true, false]

Grade input: 85 92 78 90 88
Grade array: [85, 92, 78, 90, 88]
Average: 86.6
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