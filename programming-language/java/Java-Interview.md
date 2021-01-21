# Java Interview 


## 1. The JVM

> Explain what is a JVM is and what its benefits and drawbacks are.

A Java program is compiled into bytecode, not machine language (as is the case for example for a C or C++ program). Bytecode is a platform independent instruction set that is executed by an interpreter, which itself is a program, usually written in C++ or C. The JVM is the interpreter for the bytecode generated by the Java compiler. Here are the key advantages and disadvantages of this approach:

* The same bytecode can run unchanged on multiple platforms. (Sim's marketing team referred to this as "write once, rim everywhere".) This approach also greatly reduces the burden of porting a language to a new platform—all that is needed is to implement the interpreter and interface key libraries, e.g., for I/O.
* The primary drawback of using a JVMis the performance hit brought about by the added layer of indirection. Recently, this performance penalty has reduced greatly through the use of just-in-time-compilation, wherein the JVMidentifies at run-time code sections that are most commonly executed, e.g., loops, and generates native machine code for those sections. (Occasionally, because the JVM can use rimtime profiling it can better predict branches, which leads to performance that is actually superior to a statically compiled language.)

Variant: What is the difference between checked and unchecked exceptions? List five commonly used standard exceptions. (Item 58, Effective Java)

## 2. throw vs. throws

> Explain the difference between throw and throws.


**Solution**: Both are keywords related to exception handling.

* The `throw` keyword is used to throw an exception from a method or static block, e.g., if (A. length == 8) throw IllegalArgumentException("Array must not be empty");
* The `throws` keyword is used in method declaration to indicate exceptions that canbepossiblybethrownbythemethod,e.g.,public void binSearchfint[] A, int k) throws IllegalArgumentException. A method that throws checked exceptions (e.g., FileNotFoundException) must declare all of them. Unchecked exceptions, e.g., IllegalArgumentException, that are thrown by the method may be declared optionally.


Variant: What is the difference between checked and unchecked exceptions? List five commonly used standard exceptions. (Item 58, Effective Java)

## 3. final, finally and finalizer 

> Explain the difference between final, finally, and finalizer.

**Solution**: All three are keywords. Despite their textual similarity, they are very different:

* `final` is commonly used to ensure a variable is assigned to just once. (This assignment can take place where it is declared, or in the constructor.) It is also used when declaring a method (static or nonstatic) to indicate that the method cannot be overridden. Finally, if a class is declared to be final, it means that it cannot be subclassed. Violating any of these uses of final is a compile-time error.
* `finally` is used with a try-catch block to specify code that must be executed, regardless of whether an exception was thrown and/or caught. It is commonly used to prevent resource leaks when an exception is thrown, e.g., files not being closed, locks not being released, etc.
* `finalizer` isnonstatic method thateveryclassinheritsfromObject. Itiscalled when the object is garbage collected. Ostensibly, it can be used to avoid leaks by explicitly closing files, nulling out object references, etc. In practice, since the exact time when an object is garbage collected is not under programmer control, these resources should be explicitly deallocated—an overridden finalizer() is a code smell. (Other drawbacks of finalizerO include low performance as well as unexpected behaviors on uncaught exceptions.)

## 4. equals() vs. == 

> Compare and contrast equals() and ==.

**Solution**: First of all, this question only makes sense for reference types—primitive types can only be compared using ==, which does pretty much what you'd expect.

A variable of a reference type holds an address. If x and y are variables of a reference type, then x == y tests if they hold the same address.

Very often, it is the case that objects that are located at distinct places in memory have the same content. In this case, we want to use logical equality. Every object inher¬ its a equals(Object o) method from the Object class. The default implementation is the same as ==. However, it is typically overridden to test logical equality.

The usual recipe is to first test if == holds (to boost performance), then use instanceof to see if the argument has the right type, then cast the argument to the correct type, and finally, for each "significant" field check if the field of the argument matches this' corresponding field.

It's fine to rely on == in some cases, most notably when the class ensures at most one object exists with a given value.

## 5. equals() and hashCode()

> Why should you override hashCodeO when you override equalsO?

**Solution**: As discussed in Problem 22.4 on the preceding page, it is appropriate to override equalsO when objects distinct in memory may be logically equal.

Every object inherits int hashCodeO from Object. The default implementation uses the address of the object to compute the hashcode. Suppose a class A overrides equalsO but not hashCodeO. Let x be added to a HashSet< A > container. Suppose y is distinct but logically equivalent to x, i.e., x.equals(y) returns true. A call to contains(y) in the container will use y.hashCodeO to select the hash bucket to search for y in, which in all likelihood be different from the bucket x was placed in, so the call returns false. (Even if the bucket was the same, the container 's implementation caches the hashcode as a performance optimization, and will return still false.) This problem arises whenever objects are stored in other hash-based collections such as HashMap.

The solution is to overridehashCode() to look at each field that is read in equals(). Note that this principle has to be applied recursively, e.g., if fields are compared using their own equalsO.


## 6. List, ArrayList and LinkedList 

> Explain the difference between List, ArrayList, and LinkedList. 

**Solution**: All three are types that are used to represent sequences.

* List is an interface—a definition that specifies method signatures, but no im¬ plementation of these methods. There are many benefits of using interfaces over classes, such as polymorphism, decoupling implementation from specification, and to specify mixins.
* ArrayList is a class that implements the List interface. It is based on ar¬ rays. It has a couple of methods outside of those in the List interface, such as trimToSizeO, but essentially it just implements List. Because it is imple¬ mented using an array, testing and setting elements is fast (£?(1)), but adding elements to the beginning is slow (0(n) for an array of n elements). (Adding elements to the end is fast because arrays overallocate buffer space.)


* LinkedList is an implementation of the List interface. It is based on the linked list data structure. It has many methods in addition to the List interface, e.g., it implements stack and queue functionality. For a linked list LinkedList insertion at the head or tail takes0(1) time, but getting or setting the fcth element takes 0(k) time.

Variant: Contrast the following code snippets. (Item 25, Effective Java)

``` java
Object[] numArray = new Integer[2]; 
numArray[0] = 42;
numArray[1] = "Hello World!";
```
``` java
List<Object> numArrayList = new ArrayList<Integer>(1); 
numArrayList.add(42);
```

## 7. String vs StringBuilder 


> Compare and contrast String and StringBuilder.

**Solution**: String is Java'sbuilt-in class for representing and operating on strings. It has a variety of constructors, and methods, e.g., for testing substring inclusion, ex¬ tracting substrings, etc. A key feature of Java string objects is that they are immutable. This has many benefits, e.g.,

- threads can safely share strings without fear of data corruption through races, 
- strings can be cached, i.e., an operation can return a reference to an existing
string, and
- strings can be safely added to Sets and Maps without fear of changing content corrupting the hashtable.

The drawback of string immutability is that every time a string has to be modified, a new object has to be created, even for something as simple as changing the first character. If the string is long, this is a time-consuming operation. For example, consider the following program.

``` java 
public static String concat(List<String> strings){ 
	String result =
	for (String s : strings) {
		result += s;
	}
	return result;
}
```

Every update to the result entails creating a new string and copying over the existing characters in the result to the start of the new string. If the string has length n this takes 0(n) time. Since there are n iterations, the time complexity grows as 0(n2).

The StringBuilder class is mutable. Additionally, the constructor overallocates space, which means that adding characters to the end is efficient (until the buffer fills up). The following program is functionally equivalent to the one above, but has 0{n) time complexity.

``` java 
public static String concat (List<String> strings) { StringBuilder result = new Str ingBuilder () ;
for (String s : strings) {
result .append(s) ;
}
return result.toString();
}
```

## 8. Autoboxing

> What does autoboxing refer to?

**Solution**: Types in Java are classified into two categories—primitive types and ref¬ erence types. Leaving aside long/short variants, primitive types are integers, chars, floats, and booleans. All remaining types are reference types—this includes arrays, classes, and interfaces. Variable of these type hold addresses.

Nonstatic methods can only be called on reference types—there simply isn't enough space in a primitive type to store the dispatch table needed to call nonstatic methods. This means that primitive types cannot be directly added, for example, to hash tables or linked lists, since we need to be able to call hashCodeO or equalsO to determine where to put a value, or if a value is already present.

Java uses box-types, e.g., Integer to wrap primitive types, thereby allowing them to be used where objects are expected.

Prior to Java 1.5, conversion between primitive types and corresponding box types wasperformedbycodelikeX = new Integer(x);andx = Integer.intValue(X);, where x is of type int and X is of type Integer. Java 1.5 introduced the concept of autoboxingandauto-unboxing—thecompilertakesanassignmentlikeInteger X = x;, where x is assumed to be of type int and internally translates it to Integer X = Integer .valueOf(x) ; The assignment int x = X; internally becomes x = Integer.intValue(X) ;

Though autoboxing leads to cleaner code, and possibly reducing the number of allocated objects (since Integer.valueOfO can return cached values), it has its disadvantages too. Here are some examples. Autoboxing hides the performance hit brought about by object allocation. It's easy to use == to compare values where equalsO is more appropriate. Since Integers can be null, int x = X; may throw NullPointerException. Conversions, e.g., from Integer to Long don't work as you might expect.


## 9. Static initialization 

> What is a static initializer block?

**Solution**: Static variables are often initialized by one-line assignments, e.g., static int capacity = 16;, or static Foo bar = readFooFromConfigFileO. Occasion¬ ally, the initialization logic is more complex, and depends on the values of other static fields. In this case, a static initialization block is appropriate, e.g.,

``` java 
 private static final Map<String, Integer> monthToOrdinal = new HashMap<>();
// Static initializer block. Executed once, when class is first acccessed . 

static {
	int ordinal = 0;
	String[] months = {"January", "February", "March", "April",
							"May", "June", "July", "August",
							"September", "October", "November","December"}; 

for (String month : months){
	monthToOrdinal.put(month, ordinal++);
	} 
}

```

In this case, we can replace the initializer block with a call to a static function. How¬ ever, when multiple static fields are being initialized, using a static function can lead to performance inefficiency and/or code duplication compared to a static block, e.g., imagine the following program, (Item 5, Effective Java), without a static initializer.

``` java 
private static final Date BOOM_START; 
private static final Date BOOM_END;

static {
	Calendar gmtCal = Calendar.getlnstance(TimeZone.getTimeZone("GMT")); gmtCal.set(1946, Calendar.JANUARY, 1, 0, 0, 0);
	BOOM_START = gmtCal.getTime();
	gmtCal.set(1965, Calendar.JANUARY, 1, 0, 0, 0);
	BOOM_END = gmtCal.getTime();
}
```


One drawback of static initialization blocks is that they are called when the class is first accessed, either to create an instance, or to access a static method or field. This order dependency can lead to unanticipated behaviors.

Variant: Explain the difference between a static and a nonstatic inner class. (Item 22, Effective Java)

## Reference

1. Elements of programming interviews in Java 