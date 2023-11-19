# methods and encapsulation

deklaracja metody:

```java
public final void nap(int minutes) throws InterruptedException {
    //method body
} 
```

* **public** - access modifier
* **final** - optional specifier
* **void** - return type
* **nap** - method name
* **throws** - exception (optional)

method call:

```java
nap(10);
```

## access modifiers

**private** - method can only be called from within the same class

**default** - also known as `package-private`, the method can only
be called from classes in the same package.

**protected** - the method can only be called from classes in the same
package or subclasses.

**public** - the method can be called from any class.

```java
public void walk1() {}
default void walk2() {} //DOES NOT COMPILE
void public walk2() {} //DOES NOT COMPILE
void walk4() {}
```

`walk2` nie skompiluje się w klasie, skompiluje się w ramach interfejsu.

## optional specifiers

**static** - used for class methods

**abstract** - used when not providing a method body

**final** - used when a method is not allowed to be overridden by a subclass

**???** `overloading` vs `overwriting` **???**

Only the constructor has no return type, all other methods must have
a return type (`void` is a return type!)

```java
int integerMethod() {
    return 9;
}

int longMethod() {
    return 9L;      //DOES NOT COMPILE, 9L might not fit into int data type
}
```

optional exception list:

```java
public void oneException() throws IllegalArgumentException {}

public void twoExceptions() throws IllegalArgumentException,
    InterruptedException {}
```

the calling method can either throw the same exceptions, or handle them.

## vararg parameter

its like an array, and it must be the last element in a method parameter
list. This implies that a method can only have one `vararg` parameter.

```java
public void walk1(int... nums) {}
public void walk2(int start, int... nums) {}

public void walk3(int... nums, int start) {}    //DOES NOT COMPILE
public void walk4(int... start, int... nums) {} //DOES NOT COMPILE
```

`varargs` usage example:

```java
public static void walk(int start, int... nums) {
    System.out.println(nums.length());
}

public static void main(String[] args) {
    walk(1);                    //0
    walk(1, 2);                 //1
    walk(1, 2, 4, 5, 6)         //4
    walk(1, new int[] {4, 5})   //2
}
```

class Gosling `extends` Bird, which means it is a subclass of Bird.
It inherits from it. Bird is the more general class, while Gosling
is "specialized".

```java
package pond.shore;

public class Bird {
    protected String text = "floating"; //protected access
    protected void floatInWater() {     //protected access
        System.out.println(text);
    }
}
```

now we can use `extends` like this:

```java
package pond.goose;
immport pond.shore.Bird;    //from a different package

public class Gosling extends Bird {

    public void swim() {
        floatInWater();             //we can use this
        System.out.println(text);   //we can use this
    }

}
```

if variable `text` or method `floatInWater()` were private, then
the code in class Gosling wouldn't work, because we wouldn't have
access.

> are there tables in markdown?

a method in _ can | private  |  default           | protected   |   public
access a _ member |          |  (package-private) |             |
------------------|----------|--------------------|-------------|---------
the same class    | Yes      |  Yes               | Yes         |   Yes
------------------|----------|--------------------|-------------|---------
another class in  | No       |  Yes               | Yes         |   Yes
the same package  |          |                    |             |
------------------|----------|--------------------|-------------|---------
a subclass in a   | No       |  No                | Yes         |   Yes
different package |          |                    |             |
------------------|----------|--------------------|-------------|---------
an unrelated class| No       |  No                | No          |   Yes
in a different    |          |                    |             |
package           |          |                    |             |


lets say we have a class like this:

```java
public class Koala {
    public static int count = 0;
    public static void show() {
        System.out.println(count);
    }
}
```

now look at this:

```java
Koala.count = 4;
Koala koala1 = new Koala();
Koala koala2 = new Koala();

koala1.count = 6;
koala2.count = 5;

System.out.println(Koala.count; //prints 5
```

a `static` member cannot call an instance member.


Type             |  Calling                 | Legal? |   How?
-----------------|--------------------------|--------|------------------------------
Static method    |  Another static method   | Yes    |   Using the classname
                 |  or variable             |        |
-----------------|--------------------------|--------|------------------------------
Static method    |  An instance method      | No     |
                 |  or variable             |        |
-----------------|--------------------------|--------|------------------------------
Instance method  |  A static method         | Yes    |   Using the classname or
                 |  or variable             |        |   a reference variable
-----------------|--------------------------|--------|------------------------------
Instance method  |  Another instance method | Yes    |   Using a reference variable
                 |  or variable             |        |


