# Info

na następnym wykładzie test, 8:15 wtorek 31 X
test będzie z pierwszych dwóch wykładów
czwartek po tym nie ma zajęc (?) (dni rektorskie)

# identifier names

identifiers - variable, method, class, field

* name must begin with a letter, `$` or `_`
* next characters can also be numbers
* cannot use **the same** name as a java reserved word
* a single underscore (`_`) is not allowed

## reserved words

* `class`
* `int`
* `double`
* `import`
* `public`
* `private`
* `switch`
* `boolean`
* etc.

## naming convention

* classes - `ThisIsMyClass`
* methods, variables, packages - `thisIsMyVariable`
* constants (`static final`) - `THIS_IS_MY_CONSTANT`
* enum values - `color.THIS_IS_MY_COLOR`

constants are declared with keywords `static final`

limit yourself to one declaration per statement/line

# creating objects

```java
Random generator = new Random();
```

creates a new variable with name `generator` of type/class
`Random` by using the constructor with `new` keyword.

```java
public class Phone {
    public Phone() {
        //this is the constructor
    }
}
```

two important things to remember:
* name of the constructor matches the name of the class
* the constructor doesnt have a return type

```java
public void Phone() {
    //THIS IS NOT A CONSTRUCTOR
}
```

## constructor example

```java
public class Chicken {
    int numOfEggs;
    String name;

    public Chicken(int num, String name) {
        this.name = name;
        numEggs = num;
    }
}
```

we use `this.name`, because the parameter of the creator
(`String name`) has the same name as the variable of the
`Chicken` class, `name`. Then we use `this.name` to specify
to the compiler that we are reffering to the variable, and
not the parameter.

since in the assignment:

```java
numEggs = num;
```

the two variable names are different, we do not need to use
`this.` keyword.

if there's no keyword specifying the availability of variables,
then it is `package private`. So for example `numEggs` in the
above example is `package private`, which means its available
through the class, and the classes available in the same package.

# default variable initialization

before you use a variable it has to be defined/initialized,
here are the three types of variables:

## local variables

* are defined within a method.
* must be initialized before use

```java
public void findAnswer(boolean check) {
    int answer;
    int onlyOneBranch;
    if (check) {
        answer = 1;
        onlyOneBranch = 1;
    } else {
        answer = 1;
    }
    print(onlyOneBranch) //DOES NOT COMPILE, because
    //sometimes it wont be initialized
}
```

## instance variables

are initialized automatically, `null` for an object,
and `0/false` fora a primitive.

```java
public void whatTypeIsIt() {
    var name = "Hello"; //String name;
    var size = 7;       //int size;
}
```

`var` means local variable type interference, so the compiler
automatically assigns the type based on the value we put in

```java
public void eat(int piecesOfCheese) {
    int bitesOfCheese = 1;
}
```

the above code has two local variables:
* `bitesOfCheese` - is declared inside the method
* `piecesOfCheese` - method parameter - is local to the method

variables have scopes:

```java
public void eatIfHungry(boolean hungry) {
    if (hungry) {
        int bitesOfCheese = 1;
    }
    print(bitesOfCheese) //DOES NOT COMPILE, variable went out of scope
}
```

## class variables

```java
public class Mouse {

    static int maxLength = 5;   //class variable (same for all mice)
    private int length;         //instance variable (can be different)

    public void grow(int inches) {
        if (length<maxLength) {
            int newSize = length + inches;
            length = newSize;
        }
    }
    
}
```

# variable scope

* **local variables** - in scope from declaration to end of block
* **instance variables** - in scope from declaration until eligible
for garbage collection
* **class variables** - in scope from declaration until program ends

# destroying objects

```java
public class Scope {
    public static void main(String[] args) {
        String one, two;
        one = new String("a");
        two = new String("b");
        one = two;              //both point to "b", so "a" becomes a eligible for garbage collection
        String three = one;     //all 3 variables point to "b"
        one = null;             //two and three point to "b", one doesnt point to anything
    }
}
```

# co to jest klasa

* szablon według którego tworzone są obiekty
* pojęcie opisujące obiekty o zbliżonych właściwościach

klasa składa się z trzech elementów:
* nazwa
* zestaw atrybutów
* operacje, jakie można wykonywać na obiektach i ich atrybutach
(metoda to taka operacja)

cztery własności związane z obiektowością:
* **abstrakcja** - akt lub wynik pominięcia różnic pomiędzy
obiektami powodujący, że można dostrzec podobieństwa. Wynikiem tego
procesu jest klasa.
* **hermetyzacja** - dostęp do zmiennych klasy jest ograniczony.
* **modułowość** - podzielenie kodu, np. na pakiety
* **dziedziczenie** - w javie dziedziczenie jednobazowe, aka.
`podtyp` dziedziczy od `nadtypu`. Najwyższy `nadtyp` jest najbardziej
ogólny. Dziedziczy się zarówno atrybuty (zmienne?) jak i operacje
(metody?)

> !!! poczytać o klasa zapieczętowanych (sealed classes) !!!