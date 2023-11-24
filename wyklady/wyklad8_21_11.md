> costam poprawa tabelki była

static vs instance - calling method in the same class

```java
public class Nova {

    public static void metodaKlasy() {
        drugaMetodaKlasy();
        int value = new Nowa().metodaInstancji();
    }

    public static void drugaMetodaKlasy() {

    }

    public int metodaInstancji() {
        int value = 1;
        return value;
    }

    public void innaMetodaInstancji() {
        metodaKlasy();
        int value = metodaInstancji();
    }

}
```

static vs instance - calling method from another class

```java
public class Druga {

    public static void metodaKlasyDruga() {}

    public void metodaInstancjiDruga() {}

}
```

then we can call those methods like this:

```java
public class Inna {

    public static void metodaKlasy() {
        Druga.metodaKlasyDruga();       //klasy, recommended
        Druga zmienna = new Druga();
        zmienna.metodaKlasyDruga();
        zmienna.metodaInstancjiDruga(); //instancji
    }

    public void metodaInstancji() {
        Druga.metodaKlasyDruga();       //klasy
        Druga zmienna = new Druga();    //instancji
        zmienna.metodaInstancjiDruga();
    }

}
```

# constants

like this:

```java
public class Initializers {
    public static final int MAX_NUM_STUDENTS = 15;
}
```

static imports:

* standard imports are for importing classes
* static imports are for importing static members of classes
(both methods and variables)

<--- z tego będzie pytanie!!!

```java
import static java.util.Arrays.asList;  //static import
public class Imports {
    public static void main(String[] args) {
        List<Strings> list = asList("one", "two");  //no Arrays
        //List is an interface
    }
}
```

pod zmienną interfejsu (`list`) można przypisać obiekt dowolnej
klasy, która ten interfejs implementuje.

Java is a `pass-by-value` language. This means a copy of the
variable is made and the method receives that copy. Assignments
made in the method do not affect the caller.

```java
public static void main(String[] args) {
    int num = 4;                //4
    newNumber(num);
    System.out.println(num);    //still 4
}

public static void newNumber(int num) {
    num = 8;
}
```

```java
public static void main(String[] args) {
    String name = "Wiktor";
    changeName(name);
    System.out.println(name);   //prints Wiktor, NOT InneImię
}

public static void changeName(String name) {
    name = "InneImię";
}
```

when we call the `changeName()` method, a copy of the
reference variable called `name` is made. That copy is
pointing to the same `"Wiktor"` object. We then create a new
`"InneImię"` object, and the `name` variable that's in the
method is now pointing to that one, but the name variable
from main method is still pointing to `""Wiktor` object.

```java
public static void main(String[] args) {
    StringBuilder name = new StringBuilder("My");   //My
    add(name);
    System.out.println(name);       //My uniform
}


public static void add(StringBuilder s) {
    s.append(" uniform");
}
```

# method overloading

nazwa metody musi być taka sama, a metody te muszą różnić
się listą parametrów. Przeciążanie metod zachodzi w tej
samej klasie.

```java
public void fly(int numMiles) {}
public void fly(short numFeet) {}
public boolean fly() { return false; }
void fly(int numMiles, short numFeet) {}
publlic void fly(short numFeet, int numMiles) throws Exception {}
```

```java
public void fly(int numMiles) {
    System.out.println("int");
}

public void fly(short numFeet) {
    System.out.println("short");
}

public static void main(String[] args) {
    fly(1);             //prints int
    fly((short)1);      //prints short
    fly((short)1 + 2)   //prints int
}
```

```java
public class ReferenceTypes {
    public void fly(String s) { System.out.println("string"); }
    public void fly(Object o) { System.out.println("object"); }

    public static void main(String[] args) {
        ReferenceTypes r = new ReferenceTypes();
        r.fly("test");  //prints string
        r.fly(56);      //prints object
    }
}
```

java chooses in order of:
* exact match by type
* larger primitive type
* autoboxed type
* varargs

# creating constructors

java tworzy domyślny bezargumentowy konstruktor tylko wtedy,
kiedy my żadnego konstruktora nie napiszemy.

```java
public class Hampter {
    private String color;
    private int weight;

    public Hampter(int weight) {
        this.weight = weight;
        color = "brown";
    }

    public Hampter(int weight, String color) {
        this.weight = weight;
        this.color = color;
    }
}
```

instead of this:

```java
    public Hampter(int weight) {
        this.weight = weight;
        color = "brown";
    }
```

we could do this:


```java
    public Hampter(int weight) {
        this(weight, "brown");
    }
```

in the first non-commented line use `this` keyword as if it were a method,
to continue constructing by calling another constructor.

final instance variables must be assigned exactly once, either in the
line of declaration, in an instance initializer or in the constructor.

> modyfikatory dostępu będą na sprawdzianie
> poczytać o wyrażeniach lambda, third execution, interfejs `predicate`