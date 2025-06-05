# Referència `this` (Java)

En Java, `this` és una paraula clau especial que representa l'objecte actual de la classe. En altres paraules, quan un mètode s'executa dins d'una instància d'una classe, **this** apunta a aquesta instància concreta.

L'ús de this és especialment útil en casos on cal referenciar atributs o mètodes de l'objecte actual per evitar confusions amb variables locals, reutilitzar constructors, encadenar mètodes i molt més. A continuació, vorem els usos principals de **this**, amb exemples pràctics per entendre millor la seua aplicació.

## 1. Diferenciar atributs d'instància de variables locals

Quan un constructor o un mètode utilitza paràmetres amb el mateix nom que els atributs de la classe, es produeix una ambigüitat. Java donarà preferència a la variable local, la qual cosa impedeix modificar directament l'atribut de l'objecte.

Ací és on entra en joc **this**, per indicar que ens referim a l'atribut de la instància en compte de la variable local.

**Exemple**:

::: tabs
== Java

```java
class Cotxe {
    private String marca;

    public Cotxe(String marca) {
        this.marca = marca; // 'this.marca' és l'atribut, 'marca' és el paràmetre
    }

    public void mostrarMarca() {
        System.out.println("Marca: " + this.marca);
    }
}
```

:::

Sense **this**, la línia `marca = marca;` assignaria el valor de la variable local marca a si mateixa, deixant l'atribut marca sense modificar.

## 2. Cridar un altre constructor dins la mateixa classe (this())

Java permet definir constructors sobrecarregats, és a dir, **múltiples constructors amb diferents conjunts de paràmetres**. Per evitar duplicació de codi, es pot cridar un constructor des d'un altre utilitzant `this()`.

**Exemple**:

:::: tabs
=== Java

::: tabs
== Cotxe.java

```java
class Cotxe {
    private String marca;
    private int any;

    // Constructor principal
    public Cotxe(String marca, int any) {
        this.marca = marca;
        this.any = any;
    }

    // Constructor secundari que reutilitza el principal
    public Cotxe(String marca) {
        this(marca, 2024); // Crida al constructor principal amb l'any predeterminat
    }

    public void mostrarInfo() {
        System.out.println("Marca: " + marca + ", Any: " + any);
    }
}
```

== Classe Principal

```java
public class Main {
    public static void main(String[] args) {
        Cotxe c1 = new Cotxe("Toyota");
        c1.mostrarInfo(); // Marca: Toyota, Any: 2024
    }
}
```

:::
::::

Aquesta ús de `this` evita duplicació de codi: en compte d'assignar manualment els atributs en cada constructor, es reutilitza la lògica existent. A més, millora la mantenibilitat: si es canvia la implementació d'un constructor, no caldrà modificar diversos constructors manualment.

## 3. Retornar l'objecte actual (this) en mètodes encadenats

L'ús de **this** per retornar l'objecte actual permet que els mètodes es puguen encadenar en una sola línia. Aquesta tècnica, coneguda com method chaining, millora la llegibilitat del codi i és àmpliament utilitzada en frameworks i llibreries modernes.

**Exemple**:

:::: tabs
=== Java

::: tabs
== Cotxe.java

```java
class Cotxe {
    private String marca;
    private int any;

    public Cotxe setMarca(String marca) {
        this.marca = marca;
        return this; // Retorna l'objecte actual
    }

    public Cotxe setAny(int any) {
        this.any = any;
        return this;
    }

    public void mostrarInfo() {
        System.out.println("Marca: " + marca + ", Any: " + any);
    }
}
```

== Classe principal

```java
public class Main {
    public static void main(String[] args) {
        Cotxe c = new Cotxe().setMarca("Honda").setAny(2023);
        c.mostrarInfo(); // Marca: Honda, Any: 2023
    }
}
```

:::
::::

Així evitem crides repetitives: no cal assignar cada valor per separat.

## 4. Passar l'objecte actual (this) com a argument

De vegades, volem passar l'objecte actual a un altre mètode o classe perquè aquest puga treballar amb ell. Això es fa mitjançant **this**.

**Exemple**:

:::: tabs
=== Java

::: tabs
== Client.java

```java
class Client {
    public void mostrarCotxe(Cotxe cotxe) {
        System.out.println("Cotxe: " + cotxe);
    }
}
```

== Cotxe.java

```java
class Cotxe {
    private String marca;

    public Cotxe(String marca) {
        this.marca = marca;
    }

    public void mostrarInformacio(Client client) {
        client.mostrarCotxe(this); // Passa l'objecte actual
    }

    @Override
    public String toString() {
        return "Marca: " + marca;
    }
}
```

== Classe principal

```java
public class Main {
    public static void main(String[] args) {
        Client client = new Client();
        Cotxe cotxe = new Cotxe("Ford");

        cotxe.mostrarInformacio(client); // Cotxe: Marca: Ford
    }
}
```

:::
::::

És útil per dos motius principals: en primer lloc, permet passar l'objecte actual sense necessitat de crear referències addicionals. I, en segon lloc, es pot utilitzar en dissenys on una classe treballa amb instàncies d'una altra.

::: warning ATENCIÓ
**No es pot utilitzar `this` dins d'un mètode static** perquè **this** fa referència a l'objecte actual, i els mètodes static pertanyen a la classe en lloc d'una instància concreta.
:::
