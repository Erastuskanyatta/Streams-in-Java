### Getting Started with Streams in Java
Streams are one of the most powerful features of Java. They allow developers process a collection of data in a declarative manner. This makes code clean and concise.

A stream is a collection of objects that can be piped together to generate a certain outcome.

Streams are created from either collection, arrays, or an arbitrary number of objects.

### Prerequisites
For this tutorial, it is advisable to have:
1. Basic knowledge of Java programming 
1. An  `IDEA` of your choice installed. In this tutorial I will be using [IntelliJ IDEA](https://www.jetbrains.com/idea/).


### Table of content
1. [Imperative Vs Fuctional Programmimg](#1-imperative-vs-fuctional-programmimg)
2. [Creating a stream](#2-creating-a-stream)
3. [ Mapping Elements](#3-mapping-elements)
4. [Filtering Elements](#4-filtering-elements)
5. [Sorting Streams](#5-sorting-streams)

#### Why use Streams?
1. *Mimimum code Error*.  Streams are performed out in a step by step manner therefore preventing unnecessary bugs and code error.
2. *Code is more Intuitive*. A code that have streams is easy to understand whats going on and does not require too much thinking.
3. *Verbose code*. This is a type of code that need more /longer words to describe what is going on. By using stream, you can chope off some codes making the code less verbose.

### 1. Imperative Vs Fuctional Programmimg
Before we start looking at the streams, we need to understand the kind of problem they solve. 

Let's say we have a `class book` which have the `title`, the `author` of the book and the number of `pages`.

In this `class book`, we want to count the number of books title that have more than 600 pages.

To perform this task, let's create a new directory `Streams` in the IntelliJ IDEA.  Create a `book.java` class and `main.java` class in `/Streams`, and add the following code snippets respectively.

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

>Note: To generate the constructor in the snippet above, right click and select the `generate` option. In `/generate/constructor`, choose the fields you want the constructor to initialize and hit ok. In our case we will select all.

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

In the main class, we have created a list of books called `books`. We  have used `List.of();` to initialize 4 books.

To get the number of books with more than 600 pages, we have used the `Imperative programming` method.

Imperative programming is a style of programming where we have statement that specifys how the number of books should be counted.

To process the collection of data in a declarative/ functional programming approach, we use the `Streams`. Fuctional programming brings in some additional concepts.

In main class, add the code snippet below after `count++` increament.  The snippet is written in fuctional programming approach..

```java
...
// declarative/ functional programming approach
var count1 = books.stream()
                .filter(book -> book.getPages() > 600)
                .count();
...                
```
In the above example(declarative programming), we have used a stream object that has several methods, eg `filter(predicate)` which filters data based on the condition given. i.e. (`book -> book.getPages() > 600`)
>Note. A pridicate is a fuction that takes an object and returns a boolean.

`.cout()` method is used to count the number of movies.

Unlike imperative programming, in fuctional Programmimg we don't have statements like int count = 0; or count++;. This makes our code cleaner and easy to understand. 

### 2. Creating a stream
We have looked at the problem that streams solve. Let's now focuse on creating a stream.

Streams can be created in different ways. These include:
>1. From collection. 

>2. From arrays.

>3. From an arbitrary number of objects.

#### From collection.
In `/Streams` directory create `howToCreateStream.java` class and add the snippet below:

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
Replace the code snippet in howToCreateStream.java with the one below:

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

If we have an array, called cars for instance, our snippet would be as shown below:

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

To execute the snippet, right click on the file and select `Run`.

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
 `.foreach` request new number from stream and prints it.

On executing the snippet, you will get an infinite random numbers generated.

To prevent this, we can call the `limit()` method and define the random numbers we want to generate.

For instance lets generate 5 random numbers:

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
This is the transformation of stream object to new objects. This is done using the `map()` and `flatMap()` methods.

In book.java class, let's us generate another getter called `getAuthor()` that returns the authors of the book. This will be as shown below;

```java
 ---
  public String getAuthor() {
        return author;
    }
 ---
```

In the main class, where we have a list of books, let's create a stream of authors.  Replace the code in the main class with the one below;

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

The .map() get the books object and extract the author.

On running the snippet above, you will get the following output:

```bash
Paul
james
Rich
Ann
```

### 4. Filtering Elements

### 5. Sorting Elements


### Wrapping up

### Further reading
[Java Streams](https://www.baeldung.com/java-streams)


