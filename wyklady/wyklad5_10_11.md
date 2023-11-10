# cos

jakieś klasy (ważne?)

* `localDate`, `localTime`, `localDateTime`
* `period`, `duration`

## Arraylist

`ArrayList` is a C++-esque vector. `ArrayList` can change
size at runtime. `ArrayList` has two properties:

* **size**      - how many are stored in it right now
* **capacity**  - how many more can be stored

```java
import java.util.ArrayList;
```

## Object

klasa `Object` jest klasą nadrzędną dla każdej klasy Java.
Każda klasa dziedziczy po klasie `Object`. Nawet jeżeli nie
ma konstruktora, to Java doda pusty konstruktor.

```java
ArrayList<String> list4 = new ArrayList<String>();
ArrayList<String> list5 = new ArrayList<>();
```

zauważmy w powyższym przykładzie generyczność - `ArrayList`
może przechowywać dowolne elementy.

ważne metody do `ArrayList`:

* **add()**
* **remove()**
* **set()**
* **isEmpty()**
* **size()**
* **clear()**
* **contains()**

`ArrayList` przechowywuje tylko typy referencyjne. Nie może
przechowywać typów prymitywnych, np. `int`.

```java
ArrayList list = new ArrayList(); //tworzy dla obiektu `Object`
list.add("hawk");
list.add(Boolean.TRUE);
System.out.println(list) // ["hawk", TRUE]
```

# autoboxing i wrapper classes

if we want to have an `ArrayList` of int, we have to use a
wrapper class (you cant have an `ArrayList` of primitives).

```java
Integer.valueOf(1);
```

pakowanie:

```java
Integer intWrapped = 1;
Integer intWrapped = new Integer(1);
Integer intWrapped = Integer.valueof(1); //recommended
```

rozpakowywanie:

```java
int i = intWrapped;
int i = intWrapped.intValue(); //recommended
```

konwersja:

```java
Integer wrapper = Integer.valueOf("123");

int primitive = Integer.parseInt("123");
```

autoboxing example:

```java
List<Double> weights = new ArrayList<>();   //przechowywuje typu `Double`, ale `Object` już nie
weights.add(50.5);                          // [50.5], jest autoboxing
weights.add(new Double(60.0));              // [50.5, 60], NIE MA AUTOBOXINGU!!! (bo dajemy new Double())
weights.remove(50.5);                       // [60], jest autoboxing
double first = weights.get(0);              // first = 60.0, jest autoboxing
```

be careful when autoboxing into `Integer`:

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(1);
numbers.add(2);
numbers.remove(1);
// java jest "leniwa". W powyższej linijce nie zautoboxuje,
// zatem usunie 1 jako prymityw. Czyli usunie numbers[1],
// czyli 2.
// jeśli java nie musi autoboxować, to tego nie zrobi

System.out.println(numbers);    //output: 1
```

**przeciążanie metod** (method overloading) - ważne i trzeba znać.

## sortowanie

```java
//for arrays
java.util.Arrays.sort(myArray);

//for `ArrayList` objects
java.util.Collections.sort(arrayListVariable);
```

# working with dates and times

you will need `java.time` package:

```java
import java.time.*;
```

* `LocalDate` - contains just a date, no time and no time zone
* `LocalTime` - contains just a time, no date and no time zone
* `LocalDateTime` - contains a date and time, no time zone

```java
System.out.println(LocalDate.now());        //tylko data
System.out.println(LocalTime.now());        //tylko czas
System.out.println(LocalDateTime.now());    //data i czas
```

create a date:

```java
LocalDate dateF = LocalDate.of(2022, 1, 20);
LocalDate dateS = LocalDate.of(2022, Month.JANUARY, 20);
//dateF == dateS
```

konstruktory do tych date są `private`, nikt się do nich nie dostanie.

**method chaining**:

```java
//zamiast pisać dużo linijek, można tak:
LocalDateTime dateTime = LocalDateTime.of(date, time).minusDays(1).minusHours(10).minusSeconds(30);
```

these date/time objects are **immutable** (just like strings), so:

```java
LocalDate date = LocalDate.of(2023, 10, 11);
date.plusDays(10);
System.out.println(date) //pokaże 2023, 10, 11
```

if we wanted it to print `2023, 10, 21` we would have to do this:

```java
LocalDate date = LocalDate.of(2023, 10, 11);
date = date.plusDays(10);
System.out.println(date) //pokaże 2023, 10, 21
```

## `Period` class

java has class `Period` to work with periods of time.

```java
import java.time.Period;

Period anually = Period.ofYears(1);
Period quarterly = Period.ofMonths(3);
//etc.
Period everyYearAndAWeek = Period.of(1, 0, 7);
```

## `DateTimeFormatter` class

```java
import java.time.format;
```

jak chcesz to sweatować to wygoogluj, na teście tego nie będzie.