# UIL Computer Science Java Study Guide 2025–2026

This guide is based on the UIL Computer Science Java Topic List 2025–2026. Java SE 25 is the official platform, but UIL questions usually focus on core Java syntax, behavior, data structures, algorithms, logic, and problem solving.

Use this guide in two ways:

1. **Written test mastery:** know exact Java behavior, output, precedence, data limits, Boolean logic, base conversion, and algorithm analysis.
2. **Programming contest mastery:** be able to implement clean, fast Java solutions using arrays, collections, recursion, dynamic programming, greedy methods, graphs, geometry, and string processing.

---

## 1. Primitive Types, Literals, and Casting

### Java primitive types

| Type | Size | Range / Meaning | Default value |
|---|---:|---|---|
| `byte` | 8-bit signed | -128 to 127 | 0 |
| `short` | 16-bit signed | -32768 to 32767 | 0 |
| `int` | 32-bit signed | -2,147,483,648 to 2,147,483,647 | 0 |
| `long` | 64-bit signed | about ±9.22e18 | 0L |
| `float` | 32-bit IEEE 754 | about 6–7 decimal digits | 0.0f |
| `double` | 64-bit IEEE 754 | about 15–16 decimal digits | 0.0 |
| `char` | 16-bit unsigned Unicode code unit | 0 to 65535 | '\u0000' |
| `boolean` | JVM-dependent | `true` or `false` | false |

Local variables do **not** receive default values. They must be initialized before use.

```java
int x;              // local variable
// System.out.println(x); // compile error: x might not have been initialized
```

Instance/static fields do receive default values.

### Integer literals

```java
int a = 42;      // decimal
int b = 0b1010;  // binary = 10
int c = 012;     // octal = 10
int d = 0xA;     // hexadecimal = 10
long e = 123L;
```

Underscores may separate digits but cannot be at the beginning, end, or next to a decimal point.

```java
int n = 1_000_000;
double d = 3.141_592;
```

### Floating-point literals

```java
double a = 3.14;
double b = 1e3;     // 1000.0
float c = 3.14f;
```

### Character literals

```java
char c = 'A';       // numeric value 65
char newline = '\n';
char quote = '\'';
```

`char` participates in arithmetic as an integer.

```java
System.out.println('A' + 1);      // 66
System.out.println((char)('A'+1)); // B
```

### Widening vs narrowing casts

Widening happens automatically if no precision-dangerous conversion is required:

```java
int i = 5;
long l = i;
double d = l;
```

Narrowing requires a cast:

```java
double x = 9.9;
int y = (int)x; // 9, truncates toward zero
```

Important examples:

```java
System.out.println((int)3.99);   // 3
System.out.println((int)-3.99);  // -3
System.out.println((byte)128);   // -128 due to overflow wraparound
```

Arithmetic with `byte`, `short`, and `char` promotes operands to `int`.

```java
byte a = 1, b = 2;
// byte c = a + b; // compile error: a + b is int
byte c = (byte)(a + b);
```

Compound assignment includes an implicit cast.

```java
byte x = 1;
x += 2;      // allowed, equivalent to x = (byte)(x + 2)
// x = x + 2; // compile error
```

---

## 2. Arithmetic Operators and String Concatenation

### Operators

| Operator | Meaning |
|---|---|
| `+` | addition or string concatenation |
| `-` | subtraction |
| `*` | multiplication |
| `/` | division |
| `%` | remainder |
| `++` | increment by 1 |
| `--` | decrement by 1 |

### Integer division

If both operands are integers, Java performs integer division and truncates toward zero.

```java
System.out.println(7 / 2);    // 3
System.out.println(-7 / 2);   // -3
System.out.println(7.0 / 2);  // 3.5
```

### Remainder `%`

The sign of the remainder follows the dividend.

```java
System.out.println(7 % 3);    // 1
System.out.println(-7 % 3);   // -1
System.out.println(7 % -3);   // 1
```

Identity: `a == (a / b) * b + (a % b)` for integer `b != 0`.

### String concatenation

If either operand of `+` is a `String`, Java concatenates.

```java
System.out.println(1 + 2 + "3"); // "33"
System.out.println("1" + 2 + 3); // "123"
System.out.println("1" + (2 + 3)); // "15"
```

---

## 3. Assignment, Increment, and Decrement

### Assignment operators

```java
x = 5;
x += 3; // x = x + 3
x -= 2;
x *= 4;
x /= 2;
x %= 3;
```

Compound assignment evaluates the left side once and includes an implicit cast.

### Pre-increment vs post-increment

```java
int x = 5;
System.out.println(++x); // increments first, prints 6
System.out.println(x++); // prints 6, then increments to 7
```

Common UIL trap:

```java
int a = 3;
int b = a++ + ++a;
// a++ contributes 3, then a becomes 4
// ++a makes a 5 and contributes 5
// b = 8, a = 5
```

Avoid writing code like this in real programs, but know how to trace it for UIL.

---

## 4. Operator Precedence and Evaluation Order

High to low, common UIL operators:

1. postfix: `expr++`, `expr--`
2. unary: `++expr`, `--expr`, `+`, `-`, `!`, `~`, casts
3. multiplicative: `*`, `/`, `%`
4. additive: `+`, `-`
5. shift: `<<`, `>>`, `>>>`
6. relational: `<`, `<=`, `>`, `>=`, `instanceof`
7. equality: `==`, `!=`
8. bitwise AND: `&`
9. bitwise XOR: `^`
10. bitwise OR: `|`
11. logical AND: `&&`
12. logical OR: `||`
13. ternary: `?:`
14. assignment: `=`, `+=`, `-=`, etc.

Most binary operators evaluate left to right. Assignment operators associate right to left.

```java
int a, b, c;
a = b = c = 5; // all become 5
```

---

## 5. Boolean Expressions and Logical Operators

### Relational/equality operators

```java
== != < <= > >=
```

Use `==` for primitives. Use `.equals()` for most object content comparisons.

### Logical operators

| Operator | Meaning | Short-circuit? |
|---|---|---|
| `&&` | logical AND | yes |
| `||` | logical OR | yes |
| `!` | logical NOT | n/a |
| `&` | boolean AND or bitwise AND | no when boolean |
| `|` | boolean OR or bitwise OR | no when boolean |
| `^` | XOR | no |

Short-circuit means the right side may not run.

```java
int x = 0;
if (x != 0 && 10 / x > 1) { } // safe
// if (x != 0 & 10 / x > 1) { } // division by zero
```

XOR is true exactly when operands differ.

```java
true ^ false  // true
true ^ true   // false
```

---

## 6. Bitwise Operators

Bitwise operators operate on integer bits.

| Operator | Meaning |
|---|---|
| `&` | bitwise AND |
| `|` | bitwise OR |
| `^` | bitwise XOR |
| `~` | bitwise NOT / complement |
| `<<` | left shift |
| `>>` | signed right shift |
| `>>>` | unsigned right shift |

### Complement

For signed integers, `~x == -x - 1`.

```java
System.out.println(~0);  // -1
System.out.println(~5);  // -6
System.out.println(~-1); // 0
```

### Shifts

```java
x << n   // multiply by 2^n if no overflow
x >> n   // signed divide by 2^n, rounding down for negatives
x >>> n  // fills with zeros on the left
```

Example:

```java
System.out.println(5 << 1);  // 10
System.out.println(8 >> 2);  // 2
System.out.println(-8 >> 1); // -4
```

For `int`, Java uses only the low 5 bits of the shift count, so shifting by 32 is same as shifting by 0.

---

## 7. Branching: `if`, `if/else`, Ternary, `switch`, `break`

### `if` and `else`

An `else` attaches to the nearest unmatched `if`.

```java
if (a)
    if (b)
        System.out.println("X");
    else
        System.out.println("Y"); // belongs to if (b)
```

### Ternary operator

```java
int max = a > b ? a : b;
```

Only one of the second or third expressions is evaluated.

### `switch`

Traditional switch:

```java
switch (grade) {
    case 'A':
        System.out.println("great");
        break;
    case 'B':
    case 'C':
        System.out.println("ok");
        break;
    default:
        System.out.println("study");
}
```

Without `break`, execution falls through.

Modern switch expression:

```java
String result = switch (n) {
    case 1 -> "one";
    case 2, 3 -> "small";
    default -> "other";
};
```

UIL may mostly use classic switch, but know both.

---

## 8. Loops

### `while`

```java
while (condition) {
    // repeats while condition is true
}
```

### `do/while`

Runs body at least once.

```java
do {
    x++;
} while (x < 10);
```

### `for`

```java
for (int i = 0; i < n; i++) {
    System.out.println(i);
}
```

Execution order:

1. initialization once
2. condition check
3. body
4. update
5. repeat from condition

### Enhanced for loop

```java
for (int value : arr) {
    System.out.println(value);
}
```

Enhanced for gives a copy of primitive values, so assigning to `value` does not modify the array.

```java
for (int value : arr) value = 0; // arr unchanged
```

For object references, you can mutate the object but not replace the collection element by reassigning the loop variable.

### `break`, `continue`, `return`

- `break`: exits nearest loop or switch.
- `continue`: skips to next loop iteration.
- `return`: exits the method.

---

## 9. Output: `print`, `println`, `printf`

```java
System.out.print("Hi");      // no newline
System.out.println("Hi");    // newline after output
System.out.printf("%d %.2f %s%n", 5, 3.14159, "ok");
```

Common format specifiers:

| Specifier | Meaning |
|---|---|
| `%d` | integer decimal |
| `%f` | floating point |
| `%.2f` | floating point rounded to 2 decimals |
| `%s` | string |
| `%c` | character |
| `%n` | platform-independent newline |

Escape sequences:

```java
\n   newline
\t   tab
\\   backslash
\"   double quote
\'   single quote
```

Example:

```java
System.out.println("A\nB");
// A
// B
```

---

## 10. Parsing, Scanner, and Files

### Parsing strings

```java
int x = Integer.parseInt("123");
double d = Double.parseDouble("3.14");
String[] parts = "a,b,c".split(",");
```

`String.split` uses a regular expression, so special regex characters must be escaped.

```java
"a.b.c".split("\\.");
"a|b|c".split("\\|");
```

### Scanner basics

```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
double d = sc.nextDouble();
String word = sc.next();      // next token
String line = sc.nextLine();  // rest of current line
```

Common trap: after `nextInt()`, the newline remains. Call `nextLine()` once to consume it before reading a full line.

### Reading from a file

UIL programming problems often use file names given in the statement.

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(new File("input.dat"));
        while (sc.hasNext()) {
            String s = sc.next();
            System.out.println(s);
        }
    }
}
```

---

## 11. User-Defined Classes

### Class anatomy

```java
public class Student {
    private String name;
    private int grade;
    public static final int MAX_GRADE = 12;
    private static int count = 0;

    public Student(String name, int grade) {
        this.name = name;
        this.grade = grade;
        count++;
    }

    public String getName() { return name; }
    public int getGrade() { return grade; }
    public void setGrade(int grade) { this.grade = grade; }
    public static int getCount() { return count; }
}
```

### Instance vs static

- Instance variables belong to each object.
- Static variables belong to the class.
- Static methods cannot directly access instance variables without an object.

### Constructors

- Same name as class.
- No return type.
- If no constructor is written, Java provides a no-argument default constructor.
- If any constructor is written, Java does not provide the default one.

### Overloading vs overriding

Overloading: same method name, different parameter list, same class or inherited.

```java
void f(int x) {}
void f(double x) {}
void f(int x, int y) {}
```

Overriding: subclass provides a new implementation with same signature.

```java
class Animal { void speak() { System.out.println("?"); } }
class Dog extends Animal { @Override void speak() { System.out.println("woof"); } }
```

### `final`

- `final` local variable: cannot be reassigned.
- `final` method: cannot be overridden.
- `final` class: cannot be extended.
- `static final` field: class constant.

```java
public static final double PI = 3.14159;
```

---

## 12. Object-Oriented Principles

### Encapsulation

Hide data with `private` fields and expose controlled access through public methods.

### Inheritance

```java
class Vehicle { }
class Car extends Vehicle { }
```

A subclass inherits accessible fields/methods from a superclass.

### Abstract classes

```java
abstract class Shape {
    abstract double area();
    void print() { System.out.println(area()); }
}
```

Cannot instantiate abstract classes directly.

### Interfaces

```java
interface Drawable {
    void draw();
}
class Circle implements Drawable {
    public void draw() { }
}
```

Interface methods are public by default. Modern Java interfaces may have `default` and `static` methods.

### Polymorphism

A superclass/interface reference can refer to a subclass object.

```java
Animal a = new Dog();
a.speak(); // Dog's overridden method runs
```

Field access is based on reference type, but overridden method calls are based on actual object type.

---

## 13. Supertypes, Subtypes, and Casting

### Upcasting

Always safe.

```java
Dog d = new Dog();
Animal a = d;
```

### Downcasting

Requires explicit cast and may fail at runtime.

```java
Animal a = new Dog();
Dog d = (Dog)a; // ok

Animal b = new Cat();
// Dog bad = (Dog)b; // ClassCastException
```

Use `instanceof`:

```java
if (a instanceof Dog dog) {
    dog.fetch();
}
```

---

## 14. Comparing Reference Types

### `==` vs `.equals()`

- `==` compares whether two references point to the same object.
- `.equals()` compares logical equality if the class overrides it.

```java
String a = new String("hi");
String b = new String("hi");
System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

String literals may be interned:

```java
String x = "hi";
String y = "hi";
System.out.println(x == y); // often true due to interning
```

### `Comparable.compareTo`

```java
class Student implements Comparable<Student> {
    int score;
    public int compareTo(Student other) {
        return this.score - other.score; // ascending, but beware overflow
    }
}
```

Better:

```java
return Integer.compare(this.score, other.score);
```

Contract:

- negative: this comes before other
- zero: equal order
- positive: this comes after other

---

## 15. Enumerated Data Types

```java
enum Direction { NORTH, SOUTH, EAST, WEST }

Direction d = Direction.NORTH;
switch (d) {
    case NORTH -> System.out.println("up");
    default -> System.out.println("other");
}
```

Useful methods:

```java
Direction.values();
Direction.valueOf("NORTH");
d.name();
d.ordinal(); // zero-based position; avoid relying on it for logic
```

---

## 16. Arrays

### 1D arrays

```java
int[] a = new int[5];       // [0,0,0,0,0]
int[] b = {1, 2, 3};
System.out.println(b.length); // 3
```

Indexes run `0` to `length - 1`.

```java
for (int i = 0; i < a.length; i++) {
    a[i] = i * i;
}
```

Arrays are objects. Passing an array to a method passes a copy of the reference, so the method can modify elements.

### 2D arrays and arrays of arrays

```java
int[][] grid = new int[3][4];
int[][] jagged = new int[3][];
jagged[0] = new int[2];
jagged[1] = new int[5];
```

`grid.length` = number of rows. `grid[r].length` = columns in row `r`.

### Initializing named arrays

```java
int[] nums;
nums = new int[]{1, 2, 3};
```

You cannot write `nums = {1,2,3};` after declaration.

---

## 17. Generic Collections

Import:

```java
import java.util.*;
```

### Interfaces

- `Collection<E>`: general group of elements.
- `List<E>`: ordered, index-based, duplicates allowed.
- `Set<E>`: no duplicates.
- `Map<K,V>`: key-value pairs.
- `Queue<E>`: FIFO-style interface.

### `ArrayList`

```java
ArrayList<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.get(0);       // a
list.set(1, "c");
list.remove(0);    // removes a
list.size();
list.contains("c");
```

Removing while iterating by index can skip elements if not careful. Iterate backward or use an iterator.

### `LinkedList`

Can act as list, queue, or deque. Good for adding/removing ends, but random access is slow.

### `Stack`

Legacy class:

```java
Stack<Integer> st = new Stack<>();
st.push(5);
st.peek();
st.pop();
st.empty();
```

For programming contests, `ArrayDeque<Integer>` is often better, but UIL list includes `Stack`.

### `Queue` and `PriorityQueue`

```java
Queue<Integer> q = new LinkedList<>();
q.add(1);
q.offer(2);
q.remove(); // removes head, throws if empty
q.poll();   // removes head, returns null if empty
q.peek();
```

Priority queue removes smallest by natural order unless comparator changes it.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5); pq.add(1); pq.add(3);
System.out.println(pq.poll()); // 1
```

Max heap:

```java
PriorityQueue<Integer> max = new PriorityQueue<>(Collections.reverseOrder());
```

### `HashSet` and `TreeSet`

```java
Set<String> hs = new HashSet<>(); // unordered, average O(1)
Set<String> ts = new TreeSet<>(); // sorted, O(log n)
```

### `HashMap` and `TreeMap`

```java
Map<String,Integer> map = new HashMap<>();
map.put("a", 1);
map.get("a");
map.getOrDefault("b", 0);
map.containsKey("a");
map.remove("a");
```

Frequency map:

```java
map.put(s, map.getOrDefault(s, 0) + 1);
```

`TreeMap` keeps keys sorted and supports methods like `firstKey`, `lastKey`, `lowerKey`, `higherKey`.

---

## 18. Regular Expressions: `Pattern` and `Matcher`

Regex describes text patterns.

```java
Pattern p = Pattern.compile("[A-Z]+\\d+");
Matcher m = p.matcher("ABC123");
System.out.println(m.matches()); // true
```

Useful regex syntax:

| Regex | Meaning |
|---|---|
| `.` | any char except newline |
| `\d` | digit |
| `\D` | non-digit |
| `\w` | word char `[A-Za-z0-9_]` |
| `\s` | whitespace |
| `[abc]` | a, b, or c |
| `[^abc]` | not a/b/c |
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 |
| `{m,n}` | between m and n |
| `^` | beginning |
| `$` | end |
| `(abc)` | group |
| `a|b` | alternation |

Because Java strings use backslashes too, regex backslashes must be doubled:

```java
"\\d+" // regex \d+
```

Find all matches:

```java
Matcher m = Pattern.compile("\\d+").matcher("a12b345");
while (m.find()) {
    System.out.println(m.group()); // 12, then 345
}
```

---

## 19. Sorting and Searching Library Methods

### `Arrays.sort`

```java
int[] a = {3,1,2};
Arrays.sort(a); // [1,2,3]

String[] s = {"bob", "ann"};
Arrays.sort(s);
```

For object arrays with comparator:

```java
Arrays.sort(arr, (x, y) -> x.length() - y.length());
```

### `Collections.sort`

```java
ArrayList<Integer> list = new ArrayList<>(List.of(3,1,2));
Collections.sort(list);
Collections.sort(list, Collections.reverseOrder());
```

Modern style:

```java
list.sort(Comparator.naturalOrder());
```

### Binary search

```java
int idx = Arrays.binarySearch(a, key);
```

Requires sorted array/list. If not found, returns `-(insertionPoint) - 1`.

---

## 20. Java Standard Library Essentials

### `String`

Strings are immutable.

Common methods:

```java
s.length();
s.charAt(i);
s.substring(start);        // start inclusive
s.substring(start, end);    // end exclusive
s.indexOf("x");
s.lastIndexOf("x");
s.contains("x");
s.equals(t);
s.equalsIgnoreCase(t);
s.compareTo(t);
s.toUpperCase();
s.toLowerCase();
s.trim();
s.replace("a", "b");
s.split(",");
```

### Wrapper classes

```java
Integer.parseInt("5");
Double.parseDouble("3.5");
Integer.MAX_VALUE;
Integer.MIN_VALUE;
Double.POSITIVE_INFINITY;
```

Autoboxing converts between primitive and wrapper:

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(5); // int boxed to Integer
int x = list.get(0); // unboxed
```

Beware `Integer` comparison with `==`; use `.equals()` unless intentionally checking same object.

### `Character`

```java
Character.isDigit(c);
Character.isLetter(c);
Character.isUpperCase(c);
Character.toLowerCase(c);
```

### `Math`

```java
Math.abs(x);
Math.max(a,b);
Math.min(a,b);
Math.pow(a,b);
Math.sqrt(x);
Math.round(x);
Math.floor(x);
Math.ceil(x);
Math.random(); // [0.0, 1.0)
```

`Math.abs(Integer.MIN_VALUE)` overflows and returns `Integer.MIN_VALUE`.

### `Random`

```java
Random r = new Random();
r.nextInt(10); // 0 to 9
r.nextDouble(); // [0.0,1.0)
```

### `Assert`

```java
assert x > 0;
```

Assertions are disabled unless the JVM runs with `-ea`.

---

## 21. Lambda Expressions and Functional Interfaces

A functional interface has exactly one abstract method.

```java
@FunctionalInterface
interface Op {
    int apply(int a, int b);
}

Op add = (a, b) -> a + b;
System.out.println(add.apply(2,3));
```

Common Java functional interfaces:

```java
Predicate<T>     // boolean test(T t)
Function<T,R>    // R apply(T t)
Consumer<T>      // void accept(T t)
Supplier<T>      // T get()
Comparator<T>    // int compare(T a, T b)
```

Sorting with lambda:

```java
list.sort((a, b) -> Integer.compare(a.score, b.score));
list.sort(Comparator.comparingInt(x -> x.score));
```

Variables captured by lambdas must be final or effectively final.

---

# Data Structures

## 22. Arrays and Lists

Array:

- Fixed size.
- O(1) random access.
- Insert/delete in middle costs O(n).

ArrayList:

- Resizable array.
- O(1) average append.
- O(1) get/set.
- O(n) insert/delete middle.

Linked list:

- Nodes connected by references.
- O(1) add/remove if node known.
- O(n) search/index access.

---

## 23. Stacks and Queues

### Stack: LIFO

Operations: push, pop, peek.

Applications:

- matching parentheses
- DFS
- expression evaluation
- undo behavior

Parentheses example:

```java
boolean balanced(String s) {
    Stack<Character> st = new Stack<>();
    for (char c : s.toCharArray()) {
        if (c == '(') st.push(c);
        else if (c == ')') {
            if (st.empty()) return false;
            st.pop();
        }
    }
    return st.empty();
}
```

### Queue: FIFO

Operations: add/offer, remove/poll, peek.

Applications:

- BFS
- simulations
- scheduling

---

## 24. Linked Lists

Basic singly linked node:

```java
class Node {
    int val;
    Node next;
    Node(int val) { this.val = val; }
}
```

Traversal:

```java
for (Node cur = head; cur != null; cur = cur.next) {
    System.out.println(cur.val);
}
```

Insert after node:

```java
Node x = new Node(10);
x.next = cur.next;
cur.next = x;
```

Delete after node:

```java
cur.next = cur.next.next;
```

---

## 25. Trees, BSTs, AVL, Red-Black Trees

### Tree vocabulary

- Root: top node.
- Parent/child: connected nodes.
- Leaf: node with no children.
- Height: longest path down to a leaf.
- Depth: distance from root.

### Binary tree traversals

For node N, left L, right R:

- Preorder: N L R
- Inorder: L N R
- Postorder: L R N
- Level-order: BFS by levels

### Binary Search Tree

For each node:

- left subtree values < node value
- right subtree values > node value, depending on duplicate policy

Search/insert average O(log n), worst O(n) if unbalanced.

Inorder traversal of BST gives sorted order.

### AVL Tree

Self-balancing BST. Balance factor = height(left) - height(right), must be -1, 0, or 1. Uses rotations after insert/delete.

### Red-Black Tree

Self-balancing BST with color rules. Java `TreeSet` and `TreeMap` are red-black-tree based. Guarantees O(log n) search/insert/delete.

---

## 26. Heaps and Priority Queues

A binary heap is a complete binary tree with heap property.

Min-heap: parent <= children. Max-heap: parent >= children.

Array representation:

- parent of index `i`: `(i - 1) / 2`
- left child: `2*i + 1`
- right child: `2*i + 2`

Operations:

- peek min/max: O(1)
- insert: O(log n)
- remove min/max: O(log n)

Java `PriorityQueue` is a min-heap by default.

---

## 27. Hash Tables

Hash table maps keys to buckets using `hashCode()`.

Average operations O(1), worst O(n). Good hashing matters.

If overriding `.equals()`, also override `.hashCode()` consistently.

```java
@Override public boolean equals(Object o) { ... }
@Override public int hashCode() { return Objects.hash(a, b); }
```

HashMap does not maintain sorted order.

---

## 28. Graphs

A graph has vertices/nodes and edges.

Types:

- directed vs undirected
- weighted vs unweighted
- cyclic vs acyclic
- connected vs disconnected

Adjacency list:

```java
ArrayList<Integer>[] g = new ArrayList[n];
for (int i = 0; i < n; i++) g[i] = new ArrayList<>();
g[u].add(v);
g[v].add(u); // if undirected
```

Weighted edge class:

```java
class Edge {
    int to, w;
    Edge(int to, int w) { this.to = to; this.w = w; }
}
```

---

## 29. Tries

A trie stores strings by prefixes. Good for dictionary/prefix search.

```java
class TrieNode {
    TrieNode[] child = new TrieNode[26];
    boolean word;
}
```

Insert/search are O(length of word).

---

## 30. Disjoint Set Union / Union-Find

Tracks connected components.

```java
class DSU {
    int[] parent, size;
    DSU(int n) {
        parent = new int[n]; size = new int[n];
        for (int i = 0; i < n; i++) { parent[i] = i; size[i] = 1; }
    }
    int find(int x) {
        if (parent[x] != x) parent[x] = find(parent[x]);
        return parent[x];
    }
    boolean union(int a, int b) {
        int ra = find(a), rb = find(b);
        if (ra == rb) return false;
        if (size[ra] < size[rb]) { int t = ra; ra = rb; rb = t; }
        parent[rb] = ra;
        size[ra] += size[rb];
        return true;
    }
}
```

With path compression and union by size/rank, operations are almost O(1).

Applications: Kruskal MST, connected components, cycle detection in undirected graphs.

---

## 31. Segment Trees and Fenwick Trees

### Fenwick Tree / Binary Indexed Tree

Supports prefix sums and point updates in O(log n).

```java
class BIT {
    long[] bit;
    BIT(int n) { bit = new long[n + 1]; }
    void add(int idx, long delta) { // idx is 0-based input
        for (idx++; idx < bit.length; idx += idx & -idx) bit[idx] += delta;
    }
    long sumPrefix(int idx) { // sum 0..idx
        long res = 0;
        for (idx++; idx > 0; idx -= idx & -idx) res += bit[idx];
        return res;
    }
    long rangeSum(int l, int r) {
        return sumPrefix(r) - (l == 0 ? 0 : sumPrefix(l - 1));
    }
}
```

### Segment tree

Supports range queries and updates in O(log n). More flexible than Fenwick trees: can handle min, max, sum, gcd, etc.

---

# Sorting and Searching

## 32. Canonical Sorts

| Sort | Best | Average | Worst | Stable? | Notes |
|---|---:|---:|---:|---|---|
| Selection | O(n²) | O(n²) | O(n²) | no | few swaps |
| Insertion | O(n) | O(n²) | O(n²) | yes | good nearly sorted |
| Bubble | O(n) with early stop | O(n²) | O(n²) | yes | mostly educational |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | yes | needs extra space |
| Quick sort | O(n log n) | O(n log n) | O(n²) | usually no | randomized pivot helps |
| Radix sort | O(k n) | O(k n) | O(k n) | yes if stable counting passes | non-comparison sort |

### Selection sort idea

Repeatedly find minimum in unsorted part and swap it into place.

### Insertion sort idea

Build sorted prefix by inserting each new item into correct position.

### Merge sort idea

Divide array in half, sort halves, merge sorted halves.

### Quick sort idea

Choose pivot, partition smaller/larger, recursively sort parts.

---

## 33. Sequential and Binary Search

Sequential search checks every element: O(n).

Binary search requires sorted data: O(log n).

```java
int binarySearch(int[] a, int target) {
    int lo = 0, hi = a.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (a[mid] == target) return mid;
        if (a[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

---

# Recursion, Dynamic Programming, and Greedy Algorithms

## 34. Recursion

A recursive method calls itself. It needs:

1. Base case.
2. Progress toward base case.

```java
int fact(int n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);
}
```

Trace recursion with a call stack. Each call has its own local variables.

Common recursive patterns:

- factorial
- Fibonacci
- binary search
- tree traversal
- DFS
- backtracking/permutations

---

## 35. Dynamic Programming

UIL says DP applies only to the programming contest, not written tests.

DP is used when a problem has:

- overlapping subproblems
- optimal substructure

### Memoization: top-down

```java
long[] memo = new long[100];
long fib(int n) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    return memo[n] = fib(n-1) + fib(n-2);
}
```

### Tabulation: bottom-up

```java
long[] dp = new long[n+1];
dp[0] = 0; dp[1] = 1;
for (int i = 2; i <= n; i++) dp[i] = dp[i-1] + dp[i-2];
```

Classic DP types:

- counting ways
- min/max cost
- knapsack
- longest increasing subsequence
- grid paths
- edit distance

---

## 36. Greedy Algorithms

A greedy algorithm makes the locally best choice and hopes/proves it is globally optimal.

Examples:

### Activity selection

Sort activities by finishing time. Repeatedly choose the next activity that starts after the last chosen activity ends.

### Fractional knapsack

Sort by value/weight ratio and take as much as possible of highest ratio items. Works only because fractions are allowed.

### Huffman coding

Repeatedly combine two lowest-frequency nodes using a priority queue. Produces optimal prefix code.

Greedy warning: many problems look greedy but require DP. Always justify the greedy choice.

---

# Graph Algorithms

## 37. BFS

Breadth-first search explores by distance layers. In unweighted graphs, BFS finds shortest path length.

```java
int[] dist = new int[n];
Arrays.fill(dist, -1);
Queue<Integer> q = new LinkedList<>();
dist[start] = 0;
q.add(start);
while (!q.isEmpty()) {
    int u = q.remove();
    for (int v : g[u]) {
        if (dist[v] == -1) {
            dist[v] = dist[u] + 1;
            q.add(v);
        }
    }
}
```

Time: O(V + E).

## 38. DFS

Depth-first search explores as deep as possible.

```java
boolean[] vis = new boolean[n];
void dfs(int u) {
    vis[u] = true;
    for (int v : g[u]) if (!vis[v]) dfs(v);
}
```

Applications: connected components, cycle detection, topological sort, flood fill.

Time: O(V + E).

## 39. Dijkstra’s Algorithm

Finds shortest paths from one source in a graph with nonnegative edge weights.

```java
long[] dist = new long[n];
Arrays.fill(dist, Long.MAX_VALUE / 4);
PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[0]));
dist[src] = 0;
pq.add(new long[]{0, src});
while (!pq.isEmpty()) {
    long[] cur = pq.poll();
    long d = cur[0]; int u = (int)cur[1];
    if (d != dist[u]) continue;
    for (Edge e : g[u]) {
        if (dist[e.to] > d + e.w) {
            dist[e.to] = d + e.w;
            pq.add(new long[]{dist[e.to], e.to});
        }
    }
}
```

Time: O((V + E) log V).

## 40. Kruskal’s Algorithm

Finds a minimum spanning tree using DSU.

1. Sort edges by weight.
2. Add edge if it connects two different components.
3. Stop after V - 1 edges.

Works for undirected weighted graphs.

## 41. Prim’s Algorithm

Builds MST by growing from a start node, always adding cheapest edge from tree to outside.

Uses priority queue. Time: O(E log V).

## 42. Topological Sort

Orders vertices in a directed acyclic graph so every edge u -> v has u before v.

Kahn’s algorithm:

```java
int[] indeg = new int[n];
for each edge u->v: indeg[v]++;
Queue<Integer> q = new LinkedList<>();
for (int i=0;i<n;i++) if (indeg[i]==0) q.add(i);
ArrayList<Integer> order = new ArrayList<>();
while (!q.isEmpty()) {
    int u = q.remove();
    order.add(u);
    for (int v : g[u]) if (--indeg[v] == 0) q.add(v);
}
boolean hasCycle = order.size() < n;
```

## 43. Cycle Detection

Undirected DFS: if you see a visited neighbor that is not the parent, there is a cycle.

Directed DFS: use states:

- 0 = unvisited
- 1 = currently visiting
- 2 = done

Seeing an edge to state 1 means cycle.

---

# Computational Geometry

## 44. Points, Distance, and Cross Product

```java
class Pt {
    long x, y;
    Pt(long x, long y) { this.x = x; this.y = y; }
}

long cross(Pt a, Pt b, Pt c) {
    return (b.x - a.x) * (c.y - a.y) - (b.y - a.y) * (c.x - a.x);
}
```

`cross(a,b,c)` tells turn direction from AB to AC:

- positive: counterclockwise
- negative: clockwise
- zero: collinear

Distance squared avoids floating point:

```java
long dist2(Pt a, Pt b) {
    long dx = a.x - b.x, dy = a.y - b.y;
    return dx*dx + dy*dy;
}
```

## 45. Line Segment Intersection

Two segments intersect if their orientations straddle each other, with special handling for collinear points.

```java
boolean onSegment(Pt a, Pt b, Pt p) {
    return cross(a,b,p) == 0 &&
           Math.min(a.x,b.x) <= p.x && p.x <= Math.max(a.x,b.x) &&
           Math.min(a.y,b.y) <= p.y && p.y <= Math.max(a.y,b.y);
}
```

## 46. Convex Hull

Convex hull is the smallest convex polygon containing all points.

Common algorithm: monotonic chain.

1. Sort points by x, then y.
2. Build lower hull with cross products.
3. Build upper hull.
4. Combine.

Time: O(n log n).

## 47. Closest Pair of Points

Brute force is O(n²). Divide-and-conquer solves in O(n log n):

1. Sort by x.
2. Recursively solve left and right.
3. Check a vertical strip around the middle.

For UIL programming, small constraints may allow O(n²); always check input size.

---

# Probabilistic Algorithms

## 48. Monte Carlo Pi Estimate

Randomly sample points in square [-1,1] x [-1,1]. Fraction inside unit circle approximates area ratio π/4.

```java
double estimatePi(int trials) {
    Random r = new Random();
    int inside = 0;
    for (int i = 0; i < trials; i++) {
        double x = 2*r.nextDouble() - 1;
        double y = 2*r.nextDouble() - 1;
        if (x*x + y*y <= 1) inside++;
    }
    return 4.0 * inside / trials;
}
```

## 49. Randomized Quicksort

Choose a random pivot to make worst-case input unlikely. Expected O(n log n).

## 50. Reservoir Sampling

Choose k random items from a stream of unknown length using O(k) memory. For k = 1:

```java
String chosen = null;
int count = 0;
while (sc.hasNext()) {
    String item = sc.next();
    count++;
    if (rand.nextInt(count) == 0) chosen = item;
}
```

Each item is chosen with probability 1/n.

## 51. Floyd’s Cycle Detection

Also called tortoise and hare. Detects cycle in linked list or repeated function sequence.

```java
Node slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow == fast) return true;
}
return false;
```

---

# Algorithm Analysis

## 52. Big-O Notation

Big-O describes asymptotic upper bound growth.

Common growth from fastest to slowest:

```text
O(1) < O(log n) < O(n) < O(n log n) < O(n^2) < O(n^3) < O(2^n) < O(n!)
```

Rules:

- Drop constants: O(3n) = O(n).
- Drop lower-order terms: O(n² + n) = O(n²).
- Sequential blocks add; nested loops multiply.

Examples:

```java
for (int i=0;i<n;i++) { }              // O(n)
for (int i=0;i<n;i++)
    for (int j=0;j<n;j++) { }          // O(n^2)
for (int i=1;i<n;i*=2) { }             // O(log n)
for (int i=0;i<n;i++)
    for (int j=1;j<n;j*=2) { }         // O(n log n)
```

### Best, worst, average

- Best case: fastest possible input.
- Worst case: slowest possible input.
- Average case: expected over input distribution.

### Space complexity

Count extra memory used, not necessarily input size unless asked for total memory.

### Exact statement counts

Trace loops carefully. Example:

```java
int count = 0;
for (int i = 0; i < n; i++)
    for (int j = 0; j <= i; j++)
        count++;
```

Inner loop runs `i + 1` times. Total = `1 + 2 + ... + n = n(n+1)/2`.

---

# Number Systems and Digital Logic

## 53. Base Conversion and Arithmetic

Base b uses digits 0 to b-1.

### Convert base b to decimal

`1011₂ = 1*2³ + 0*2² + 1*2¹ + 1*2⁰ = 11`.

`2A₁₆ = 2*16 + 10 = 42`.

### Convert decimal to base b

Repeatedly divide by b and record remainders upward.

42 to binary:

```text
42 / 2 = 21 r0
21 / 2 = 10 r1
10 / 2 = 5  r0
5 / 2  = 2  r1
2 / 2  = 1  r0
1 / 2  = 0  r1
=> 101010₂
```

### Binary/hex shortcut

Group binary digits in groups of 4 from right.

```text
1010 1111₂ = AF₁₆
```

### Binary arithmetic

Addition:

```text
  1011
+ 0110
=10001
```

Remember carries.

---

## 54. Two’s Complement 8-bit Integers

8-bit signed range: -128 to 127.

Positive numbers are ordinary binary.

Negative number process:

1. Write positive magnitude in 8 bits.
2. Flip bits.
3. Add 1.

Example: -5

```text
 5 = 00000101
flip = 11111010
+1   = 11111011
```

Convert 8-bit two’s complement to decimal:

- If leading bit is 0, normal binary.
- If leading bit is 1, value is negative. Either invert/add 1 to find magnitude or use weights with MSB = -128.

Example:

```text
11111011
MSB is 1, negative.
Invert: 00000100
Add 1: 00000101 = 5
=> -5
```

Using weights:

```text
11111011 = -128 + 64 + 32 + 16 + 8 + 0 + 2 + 1 = -5
```

Overflow wraps modulo 256 for 8-bit examples.

```text
127 + 1 = 01111111 + 00000001 = 10000000 = -128
```

---

## 55. Boolean Simplification

UIL notation may use:

- `A*B` = AND
- `A+B` = OR
- `A⊕B` or `AÅB` = XOR
- overbar or prime = NOT

Core identities:

| Identity | Rule |
|---|---|
| Identity | `A + 0 = A`, `A * 1 = A` |
| Null | `A + 1 = 1`, `A * 0 = 0` |
| Idempotent | `A + A = A`, `A * A = A` |
| Complement | `A + A' = 1`, `A * A' = 0` |
| Double negation | `(A')' = A` |
| Commutative | `A+B=B+A`, `AB=BA` |
| Associative | `(A+B)+C=A+(B+C)` |
| Distributive | `A(B+C)=AB+AC`, `A+BC=(A+B)(A+C)` |
| Absorption | `A + AB = A`, `A(A+B)=A` |
| De Morgan | `(AB)' = A' + B'`, `(A+B)' = A'B'` |

XOR identities:

```text
A ⊕ 0 = A
A ⊕ 1 = A'
A ⊕ A = 0
A ⊕ A' = 1
A ⊕ B = A'B + AB'
```

Use truth tables when unsure.

---

## 56. Polish Notation: Prefix, Infix, Postfix

- Infix: operator between operands: `A + B`
- Prefix / Polish: operator before operands: `+ A B`
- Postfix / Reverse Polish: operator after operands: `A B +`

Example:

```text
Infix:   (A + B) * C
Prefix:  * + A B C
Postfix: A B + C *
```

Postfix evaluation uses a stack:

1. If operand, push.
2. If operator, pop right operand, pop left operand, apply, push result.

Example:

```text
2 3 4 * + = 2 + (3*4) = 14
```

---

## 57. Finite State Machines

An FSM has:

- finite set of states
- input alphabet
- transition function
- start state
- accepting/final states

Used to recognize patterns/languages.

Example: recognize binary strings with even number of 1s.

States:

- E: even number of 1s, start and accepting
- O: odd number of 1s

Transitions:

- on 0: stay same
- on 1: switch E/O

---

## 58. Languages and Grammars

A formal language is a set of strings over an alphabet.

### Grammar components

- Terminals: actual symbols in strings.
- Nonterminals: variables/categories.
- Start symbol.
- Productions/rules.

### BNF example

```text
<expr> ::= <term> | <expr> "+" <term>
<term> ::= <factor> | <term> "*" <factor>
<factor> ::= <number> | "(" <expr> ")"
```

### Chomsky hierarchy basics

| Type | Language class | Machine model |
|---|---|---|
| Type 3 | regular | finite automaton |
| Type 2 | context-free | pushdown automaton |
| Type 1 | context-sensitive | linear bounded automaton |
| Type 0 | recursively enumerable | Turing machine |

Regular languages can be described by regex/FSM. Context-free languages can handle nested structures like balanced parentheses.

---

## 59. Design Patterns

### Singleton

Ensures only one instance exists.

```java
class Singleton {
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() {}
    public static Singleton getInstance() { return INSTANCE; }
}
```

### Factory

Creates objects without exposing exact construction logic.

```java
interface Animal { void speak(); }
class Dog implements Animal { public void speak(){} }
class Cat implements Animal { public void speak(){} }

class AnimalFactory {
    static Animal make(String type) {
        return switch (type) {
            case "dog" -> new Dog();
            case "cat" -> new Cat();
            default -> throw new IllegalArgumentException();
        };
    }
}
```

### Strategy

Encapsulates interchangeable algorithms.

```java
interface SortStrategy { void sort(int[] a); }
class QuickSortStrategy implements SortStrategy { public void sort(int[] a) { } }
class MergeSortStrategy implements SortStrategy { public void sort(int[] a) { } }
```

---

## 60. Multithreading and Concurrency Basics

Thread: independent path of execution.

Create a thread:

```java
Thread t = new Thread(() -> System.out.println("run"));
t.start(); // begins new thread
```

Do not call `run()` directly if you intend a new thread; `run()` is just a normal method call.

### Race condition

Occurs when multiple threads access shared data and result depends on timing.

```java
count++; // not atomic
```

### `synchronized`

Ensures only one thread enters critical section for the same lock.

```java
synchronized void inc() { count++; }
```

### Deadlock

Two or more threads wait forever for locks held by each other.

### Volatile

`volatile` improves visibility of changes between threads, but does not make compound operations like `x++` atomic.

---

## 61. Functional Programming Features in Java

Functional programming emphasizes functions as values, immutability, and transformations.

Java features:

- lambdas
- method references
- functional interfaces
- streams

Example stream:

```java
List<Integer> nums = List.of(1,2,3,4);
int sumEvenSquares = nums.stream()
    .filter(x -> x % 2 == 0)
    .mapToInt(x -> x * x)
    .sum();
```

Method reference:

```java
list.forEach(System.out::println);
```

UIL may ask conceptual questions or lambda syntax/output questions.

---

## 62. Digital Electronics and Logic Gates

Logic gates implement Boolean operations.

| Gate | Boolean expression | Output true when |
|---|---|---|
| NOT | `A'` | A is false |
| AND | `A*B` | both true |
| OR | `A+B` | at least one true |
| XOR | `A⊕B` | exactly one true |
| NAND | `(A*B)'` | not both true |
| NOR | `(A+B)'` | neither true |
| NXOR/XNOR | `(A⊕B)'` | both same |

Truth table for two inputs:

| A | B | AND | OR | XOR | NAND | NOR | XNOR |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 | 0 | 1 |

NAND and NOR are universal gates: any Boolean circuit can be built from only NAND gates or only NOR gates.

---

# UIL Written Test First 15 Questions: Targeted Mastery

The topic list says the first 15 written questions follow a predictable pattern. Master these for fast points.

1. **Number bases:** convert binary/octal/decimal/hex; do base arithmetic.
2. **Literal math:** evaluate `3 + 4 * 2`, integer division, `%`.
3. **Output:** know `print`, `println`, `printf`, escapes.
4. **String methods:** `length`, `substring`, `charAt`, `indexOf`, `compareTo`.
5. **Simple Boolean logic:** Java `&&`, `||`, `!`, `^`, short-circuit.
6. **Math methods:** `abs`, `max`, `min`, `pow`, `sqrt`, `round`, `floor`, `ceil`.
7. **Variable expressions:** trace variable values and assignments.
8. **Conditionals:** `if`, `if/else`, `switch`; dangling else; fall-through.
9. **Output loop:** trace loop variable and printed output exactly.
10. **1D primitive arrays:** indexes, length, default values, loops.
11. **Input concepts:** `Scanner`, `File`, token vs line input.
12. **Accumulation loops:** sum, product, count, min/max.
13. **Order of operations:** full precedence list.
14. **Data types:** sizes, min/max, overflow, `~` complement.
15. **ArrayList generics:** `ArrayList<Integer>`, `add`, `get`, `set`, `remove`, `size`.

---

# Programming Contest Templates

## Basic file template

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(new File("input.dat"));
        while (sc.hasNextLine()) {
            String line = sc.nextLine();
            System.out.println(line);
        }
    }
}
```

## Fast scanner template

For very large input, use `BufferedInputStream`.

```java
static class FastScanner {
    private final InputStream in;
    private final byte[] buffer = new byte[1 << 16];
    private int ptr = 0, len = 0;
    FastScanner(InputStream is) { in = is; }
    private int read() throws IOException {
        if (ptr >= len) {
            len = in.read(buffer);
            ptr = 0;
            if (len <= 0) return -1;
        }
        return buffer[ptr++];
    }
    String next() throws IOException {
        StringBuilder sb = new StringBuilder();
        int c;
        do { c = read(); } while (c <= ' ' && c != -1);
        while (c > ' ') {
            sb.append((char)c);
            c = read();
        }
        return sb.length() == 0 ? null : sb.toString();
    }
    int nextInt() throws IOException { return Integer.parseInt(next()); }
    long nextLong() throws IOException { return Long.parseLong(next()); }
}
```

---

# How to Study for Mastery

## Daily written-test drill

1. Trace 5 Java output snippets.
2. Convert 5 numbers between bases.
3. Simplify 3 Boolean expressions.
4. Do 2 Big-O analyses.
5. Review one library class deeply.

## Weekly programming drill

Solve problems in this order:

1. File input/output and formatting.
2. Strings and parsing.
3. Arrays and ArrayLists.
4. Maps/Sets frequency counting.
5. Sorting and custom comparators.
6. Recursion/backtracking.
7. BFS/DFS.
8. Greedy.
9. Dynamic programming.
10. Dijkstra/MST/DSU.
11. Geometry.

## Tracing strategy for written questions

For code-output questions:

1. Make a variable table.
2. Mark loop iterations.
3. Remember integer division and `%`.
4. Handle `++x` vs `x++` exactly.
5. Evaluate string concatenation left to right.
6. Track whether `print` adds a newline.
7. Do not assume arrays/objects are copied unless explicitly cloned.

## Contest debugging checklist

- Did you use the exact file name?
- Did you handle all lines/cases?
- Are indices 0-based or 1-based?
- Did you confuse `next()` and `nextLine()`?
- Did you use integer division accidentally?
- Could values overflow `int`?
- Did you sort before binary search?
- Did you reset variables for each test case?
- Did you print exact capitalization/spaces?

---

# Essential Complexity Cheat Sheet

| Operation | Complexity |
|---|---:|
| Array access | O(1) |
| Array search unsorted | O(n) |
| Array binary search sorted | O(log n) |
| ArrayList get/set | O(1) |
| ArrayList add end | amortized O(1) |
| ArrayList insert/remove middle | O(n) |
| LinkedList get by index | O(n) |
| Stack push/pop/peek | O(1) |
| Queue add/remove/peek | O(1) typical |
| HashSet/HashMap add/get/contains | average O(1) |
| TreeSet/TreeMap add/get/contains | O(log n) |
| PriorityQueue add/poll | O(log n) |
| PriorityQueue peek | O(1) |
| BFS/DFS | O(V + E) |
| Dijkstra with PQ | O((V + E) log V) |
| Kruskal | O(E log E) |
| Prim with PQ | O(E log V) |
| Sorting comparison-based | O(n log n) typical best possible |

---

# Final Advice

To master UIL Computer Science, you need two different skills:

1. **Exact Java knowledge** for the written test. UIL loves tiny details: integer division, operator precedence, escape sequences, object equality, data type overflow, short-circuit behavior, and loop tracing.
2. **Algorithmic implementation speed** for programming. Build templates for input, sorting, BFS, DFS, maps, DSU, Dijkstra, and geometry so you can write them without hesitation.

If you can explain every section in this guide, trace Java code without running it, and implement the major algorithms from memory, you will be prepared for the full topic list.
