# info

**WYKŁADY ZACZYNAJĄ SIĘ O 8:15**

mail:
tomasz.gorski@ug.edu.pl

konsultacje są po wykładzie, przez ~1.5h

co 3 tygodnie na wykładzie sprawdzianik, ~30min
każde ćwiczenia będą na ocenę

Jeżeli masz >3+ na koniec z wykładu i ćwiczeń, to nie
musisz pisać egzaminu

# część pierwsza

* **javac** - converts `.java` files to `.class` files
* **java** - launcher, lauches the `JVM` and executes the program

`obiekt` to `instancja` `klasy`

```java
public class Animal {

    //zmienna instancji
    private String name;

    //konstruktor klasy
    //nazwa konstruktora jest tożsama z nazwą klasy
    //konstruktor nie zwraca żadnego typu danych
    public Animal(String name) {
        //this oznacza przypisanie zmiennej name z linijki
        //wyzej do danej instancji
        this.name = name;
    }

    //metody instancji
    //typ void
    public void setName(String newName) {
        name = newName;
    }

    //typ string
    public String getName() {
        return name;
    }
}
```

zmiana na poziomie `instancji` dotyczy konkretnego obiektu.

```java
//deklarujemy se zwierzaka
//wywołanie konstruktora klasy Animal
Animal myObject = new Animal("Plimpus");
```

pełna deklaracja metody to `sygnatura` metody.
wartości podstawowe (np. `int`) piszemy małą literą, a klasy:
`String`, `Animal` etc.

w jednym pliku jest jedna publiczna klasa, i ten plik powinien
sie tak samo nazywać.

```java
public class Zoo {
    public static void main(String[] args) {

    }
}
```

keyword `static` oznacza że jest to metoda klasy.
zapisy:

```java
String[] args
```

i

```java
String... args
```

są tożsame. Ten pakiet `args` jest tablicą obiektów:
`java.lang.String`. Cała zawartość pakietu `java.lang` jest
importowana do każdego programu w javie.

java klasy daje do `packages`. Można mieć dwie klasy o takiej
samej nazwie, jeżeli są w dwóch innych `packages`. W danym pakiecie
możemy upublicznić jakąś metodę bądź zrobić żeby była `private`.

```java
import java.util.Random;

public class importExample {
    public static void main(String[] args) {
        Random r = new Random();
        //print something
    }
}
```

słowo kluczowe `import` w przypadku wyżej importuje jedną klasę.
Można zrobić tak:

```java
import java.util.*;
```

co zimportuje nam wszystkie klasy z package'u o nazwie `util`.
Trzeba uważać, bo jeżeli `java.util.*` będzie miało dependencje na
jakiś innych package'ach, to wtedy `import` ich nie weźmie automatycznie.

klasy w pakiecie `java.lang` są importowane automatycznie.

Jeżeli piszemy pełne ścieżki, to nie musimy importować:

```java
import java.util.Date;
public class Conflicts {
    Date date;
    java.sql.Date sqlDate;
}
```

tworzenie własnego package (?):

```java
package packageA;
public class ClassA {

}
```

`PIC` - kolejność w pliku javy, aka:
* `package`
* `import`
* `class`

```java
package packageB;
import packageA.ClassA;
public class classB {
    public static void main(String[] args) {
        classA a;
        //print
    }
}
```

jak nie ma keyword `static`, to są to zmienne instancji.

# część druga

typów `podstawowych`/`prymitywnych` jest osiem:

* `boolean` - 0/1
* `byte`    - 8 bit
* `short`   - 16 bit
* `int`     - 32 bit
* `long`    - 64 bit
* `float`   - 32 bit floating point
* `double`  - 64 bit floating point
* `char`    - 16 bit unicode

wszystkie te typy są pisane małą literą (np. `short`, nie `Short`).
w javie dla tych typów są typy opakowywujące te typy, aka.
`wrapper classes` - poczytaj o tym, jak i o `autoboxing`.

```java
today = new java.util.Date();
greeting = new String("How are you");
```

czyli `today` jest reference do obiektu typu `date`. Na wykładzie był
obrazek, a tutaj go nie ma

do zmiennej referencyjnej możemy przypisać wartość `null`,
wtedy nie odnosi się ona do żadnego obiektu. Czyli np:

```java
today = new java.util.Date();
today = null;
```

? i wtedy garbage collector się zacznie tym zajmować.

sposób nazywania zmiennych:

```java
String zooName;
int numberOfAnimals;
```

niezależnie od tego czy nasza zmienna to typ prymitywny, czy
jest obiektem jakiejś klasy to sposób w jaki ją nazywamy jest
taki sam (`camelCase`)