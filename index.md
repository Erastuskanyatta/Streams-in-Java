Streams are one of the powerful features of [Java](https://www.java.com/en/). 
They allow developers to process a collection of data in a declarative manner. This makes code clean and concise.

A stream is a collection of objects that can be piped together to generate a particular outcome.

Streams are created from either collection, arrays, or an arbitrary number of objects.

### Prerequisites
For this tutorial, the reader would need to have:
- Basic knowledge of Java programming 
- An  `IDEA`  installed. I will be using [IntelliJ IDEA](https://www.jetbrains.com/idea/).


### Table of content
- [Imperative Vs Fuctional Programmimg](#1-imperative-vs-fuctional-programmimg)
- [Creating a stream](#2-creating-a-stream)
- [ Mapping Elements](#3-mapping-elements)
- [Obtaining Unique Elements](#4-obtaining-unique-elements)


#### Why use Streams?
1. *Minimum code Error*. Streams are performed step-by-step, preventing unnecessary bugs and code errors.
2. *Code is more Intuitive*. A code with streams is easy to understand and does not require much thinking.
3. *Verbose code*. This type of code needs more /longer words to describe what is going on. By using stream, you can chope off some codes making the code less verbose.

### 1. Imperative Vs Fuctional Programmimg
Before we start looking at the streams, we need to understand the kind of problem they solve. 

Let's say we have a `class book` with the `title,` the `author` of the book, and the number of `pages.`

We want to count the number of books titles with more than 600 pages in this 'class book.'

Let's create a new directory, `Streams` in the IntelliJ IDEA, to perform this task. Create a `book.java` class and `main.java` class in `/Streams,` and add the following code snippets, respectively.

```java
public class book {
    private String title;
    private String author;
    private int pages;
    
    // generating a Constructor
    public book(String title, String author, int pages) { 
        this.title = title;
        this.author = author;
        this.pages = pages;
    }
    // generating a getter
    public int getPages() {
        return pages;
    }
}
``` 

>Note: To generate the constructor in the snippet above, right-click and select the `generate` option. In `/generate/constructor,` choose the fields you want the constructor to initialize and hit ok. In our case, we will select all.

```java
import java.util.List;
public class main {
    public static void show(){
        List<book> books= List.of(
                new book("x", "Paul", 578),
                new book("y", "James", 800),
                new book("z", "Rich", 400),
                new book("v", "Ann", 600)
        );
        // The type of code below is called imperative programming
        int count = 0; // initializing count to zero
        for( var book : books) // looping over the collection of books.
            if(book.getPages() > 600) //condition statement
                count++;
    }
}
```

We have created a list of `books` in the main class. We have used `List.of();` to initialize four books.

We have used the' Imperative programming' method to get books with more than 600 pages.

Imperative programming is a style of programming where we have a statement that specifies how the number of books should be counted.

We use the `Streams` to process data collection in a declarative/ functional programming approach. Functional programming brings in some additional concepts.

Add the code snippet below after the `count++` increment in the main class. The snippet is written in a functional programming approach.

```java
...
// declarative/ functional programming approach
var count1 = books.stream()
                .filter(book -> book.getPages() > 600)
                .count();
...                
```

In the above example(declarative programming), we have used a stream object with several methods, e.g.,` filter(predicate),` which filters data based on the given condition. i.e. (`book -> book.getPages() > 600`)
>Note. A predicate is a function that takes an object and returns a boolean.

`.cout()` method counts the number of movies.

Unlike imperative programming, in functional programming, we don't have statements like int count = 0; or count++;.  This makes our code cleaner and easy to understand. 

### 2. Creating a stream
We have looked at the problem that streams solve. Let's now focus on creating a stream.

Streams are created in different ways. These include:
>1. From collection. 

>2. From arrays.

>3. From an arbitrary number of objects.

#### From collection.
In the `/Streams` directory, create the `howToCreateStream.java` class and add the snippet below:

```java
import java.util.Collection;
public class howToCreateStream {
    public static void show(){
        Collection<Integer> p = null;
        p.stream();

    }
}
```

#### From arrays.
Replace the code snippet in `howToCreateStream.java` with the one below:

```java
mport java.util.ArrayList;
import java.util.Collection;
public class howToCreateStream {
    public static void show(){
        var list = new ArrayList<>(); //creating an array list
        list.stream(); //  getting array list
    }
}
```

In this snippet, we have first created an array list.

If we have an array called cars, for instance, our snippet would be as shown below:

```java
import java.util.Arrays;
public class howToCreateStream {
    public static void main(String [] args){
        String[] cars = { "BMW", "Toyota", "Nissan"};
        Arrays.stream(cars)
                .forEach(n -> System.out.println(n));
    }
}
```

Right-click on the file and select `Run` to execute the snippet.

The output of the snippet will be:

```bash
BMW
Toyota
Nissan
```

#### From an arbitrary number of objects.
To understand how this work, let's look at the snippet below:

```java
import java.util.stream.Stream;
public class howToCreateStream {
    public static void main(String [] args){
        var stream = Stream.generate(() -> Math.random());
        stream
                .forEach(n -> System.out.println(n)); 
    }
```

 The `Math.random()` object generates infinite random numbers.
 `.foreach` request a new number from the stream and prints it.

On executing the snippet, you will get an infinite random number generated.

To prevent this, we can call the `limit()` method and define the random numbers we want to generate.

For instance, let's generate five random numbers:

```java
import java.util.stream.Stream;
public class howToCreateStream {
    public static void main(String [] args){
        var stream = Stream.generate(() -> Math.random());
        stream
                .limit(5) //set the limit of random numbers to generate
                .forEach(n -> System.out.println(n)); //to terminate the stream
    }
}
```

The output of the snippet will be:

```bash
0.6114976782845492
0.5602715647461322
0.7918521867890812
0.4306881679048976
0.10413495837663422
```

### 3. Mapping Elements
This is the transformation of stream objects to new objects. This is done using the `map()` and `flatMap()` methods.

In book.java class, let's generate another getter called `getAuthor()` that returns the book's authors. This will be as shown below;

```java
 ---
  public String getAuthor() {
        return author;
    }
 ---
```

In the main class, where we have a list of books, let's create a stream of authors. Replace the code in the main class with the one below;

```java
import java.util.List;
public class main {
    public static void main(String [] args){
        List<book> books= List.of(
                new book("x", "Paul", 578),
                new book("y", "james", 800),
                new book("z", "Rich", 400),
                new book("v", "Ann", 600)
        );
        books.stream() 
                .map(movies -> movies.getAuthor())
                .forEach(author-> System.out.println(author));
    }
}
```

The `books.stream()` object creates a stream from the list of books.

The `.map()` get the book's object and extract the author.

The output of the snippet will be:

```bash
Paul
james
Rich
Ann
```

Let's now use the `flatMap()`. 

Replace the code snippet in the main class with the one below:

```java
import java.util.List;
import java.util.stream.Stream;

public class main {
    public static void main(String [] args){
        var stream = Stream.of(List.of("mango", "orange" , "passion"),
                List.of("mango-juice", "sprite", "crest"));
        stream.forEach(list-> System.out.println(list));
    }
```

Output:

```bash
[mango, orange, passion]
[mango-juice, sprite, crest]
```

We have created a stream using the `Stream.of()` method in the above example. We have passed two list-objects. i,e list of `fruits` and `drinks.`

What if we don't want to work with the list? What if we're going to work with individual fruits and drinks? 🤔 This is where the flatMap() comes to the rescue.

Replace the code snippet in the main class with the one below:

```java
import java.util.List;
import java.util.stream.Stream;
public class main {
    public static void main(String [] args){
        var stream = Stream.of(List.of("mango", "orange" , "passion"),
                List.of("mango-juice", "sprite", "crest"));
        stream
                .flatMap(list -> list.stream()) 
                .forEach(n -> System.out.println(n));
    }
}
```

The output of the snippet will be:

```bash
mango
orange
passion
mango-juice
sprite
crest
```

In the snippet, we have used the .flatMap() method to convert the list of objects to a stream of individual objects. 

### 4. Obtaining Unique Elements
The `.distinct()` method removes duplicate elements from the stream. 

Let's run the snippet below to understand this concept.

```java
import java.util.List;
public class main {
    public static void main(String [] args){
        var books =List.of(
                new book("w", "Paul", 900),
                new book("x", "Paul", 578),
                new book("y", "James", 900),
                new book("z", "Rich", 400),
                new book("v", "Ann", 900)
        );
        books.stream() //returning a stream of books
                .map(n -> n.getPages()) //returning a stream of integers
                .forEach(System.out::println);
    }
}
```

The output of the snippet will be:

```bash
900
578
900
400
900
```

In the output, we have a duplicate of 900. To get a unique 900, let's add  `.distinct()` method before the `forEach()` method.

```java
import java.util.List;
public class main {
    public static void main(String [] args){
        var books =List.of(
                new book("w", "Paul", 900),
                new book("x", "Paul", 578),
                new book("y", "James", 900),
                new book("z", "Rich", 400),
                new book("v", "Ann", 900)
        );
        books.stream() //returning a stream of books
                .map(n -> n.getPages()) //returning a stream of integers
                .distinct() // new
                .forEach(System.out::println);
    }
}
```

On rerunning, we get the output below:

```bash
900
578
400
```

### Wrapping up
In this tutorial, we have looked at the basic concepts of streams. For instance, we have seen how to create a stream from a collection. Java streams represent a data pipeline and the functions used to manipulate the data.

Happy Learning!

### Further reading
1. [Primitive Type Streams in Java 8](https://www.baeldung.com/java-8-primitive-streams)
2. [Iterable to Stream in Java](https://www.baeldung.com/java-8-primitive-streams)


