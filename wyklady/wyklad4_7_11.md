# Część druga - operatory

three types of operators:
* unary     (pojedynczy)
* binary    (podwójny)
* ternary   (potrójny)

Operator jest to symbol, który może być zastosowany
do zmiennych lub wartości literalnych, i zwraca wynik.

google operands

### pierwszeństwo/kolejność operatorów

**operator precedence**

jeśli coś jest null to nie sprawdzamy dalej,
jest na to specjalny operator

ternary operator sprawdź jak działa.

`instanceof` jest ważny do rozumienia.

operator rzutowania `(type)`, rzutujemy
na inny typ danych.

### ternary operator

```java
int y=10;
int x;
if (y>5) {
    x = 2*y;
} else {
    x = 3*y;
}
```

```java
int y=10;
int x = (y>5) ? (2*y) : (3*y);
```

powyższe dwa zapisy mają takie samo działanie.

> OCP książka wersja 8/11 - z tego są testy (?)

### pętle/operacje warunkowe

poczytać o dwóch (?) wariacjach `switch`

`for-each` specifically designed for iterating over arrays
and collection objects.

```java
for (datatype instance : collection) {
    //body iterates over
    //every element
}
```

# Core Java API's

class `String`:

```java
String name = "Wiktor";             //java najpierw sprawdzi czy jest
//już taki obiekt w puli, jeśli tak to name przypisze do tego co już jest
String name = new String("Wiktor"); //zawsze tworzony jest nowy obiekt
```

both give you a reference variable of type name
pointing to the `String` object "Wiktor".

java has string concatenation, aka "1" + "2" = "12" when
"1" and "2" are strings.

```java
System.out.println("a" + "b" + 3) //ab3
System.out.println(1 + 2 + "c")   //3c
System.out.println("c" + 1 + 2)   //c12
```


```java
int three = 3;
String four = "4";
System.out.println(1 + 2 + three + four);
//printuje "64"
```

Strings are immutable, so you **CAN'T** (?) do this:

```java
String name = "Wiktor";
name += "Wiktor";       //DOES NOT WORK!!! (?)
```

```java
String s1 = "1";
String s2 = s1.concat("2");
s2.concat("3");
System.out.println(s2); //printuje "12"
```

powyższy kod tworzy trzy zmienne, ale na trzecią
nic nie wskazuje.

```java
String s1 = "1";
String s2 = s1.concat("2");
s2 = s2.concat("3");
System.out.println(s2); //printuje "123"
```

### important methods

* charAt();
* length();
* indexOf();
* substring();
* toLowerCase() / toUpperCase();
* equals()
* equalsIgnoreCase()

`==` porówna czy dwie zmienne wskazują na ten sam obiekt,
a `equals()` sprawdzi czy dwie zmienne wskazują na dwa różne
obiekty, ale o tej samej zawartości.

* startsWith()
* endsWith()
* replace()
* contains()
* trim()
* strip()
* intern()

**method chaining**

```java
String result = "AniMaL    ".trim().toLowerCase().replace('a', 'A');
```

> istnieje klasa `StringBuilder` która się przydaje jak chcemy
> zrobić po kolei parę operacji na jakimś stringu bez tworzenia
> wielu obiektów po kolei.

# arrays

basic array:

```java
int[][] rectangleArray = new int[3][4];
```

java also has jagged arrays, which can be declared like this:

```java
int[][] differentSize = {{1, 6}, {3, 5, 9, 8}, {2, 4, 7}};

// 1 3 2
// 6 5 4
//   9 7
//   8
```

or like this:

```java
int[][] args = new int[4][];
args[0] = new int[5];
args[1] = new int[3];
```

this is how to loop through a jagged array:

```java
int[][] twoD = new int[3][2];

for (int a=0; a<twoD.length(); a++) {
    for (int b=0; b<twoD[a].length(); b++) {
        System.out.print(twoD[a][b] + " ");
    }
    System.out.println();
}
```

or like this:

```java
int[][] twoD = new int[3][2];

for (int[] oneD : twoD) {
    for (int singleNumber : oneD) {
        System.out.print(singleNumber + " ");
    }
    System.out.println();
}
```