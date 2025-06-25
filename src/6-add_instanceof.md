# L'operador `instanceof`  (Java)

L'operador `instanceof` en Java és fonamental en la programació orientada a objectes perquè permet determinar si un objecte pertany a una determinada classe o a una de les seves subclasses. Això és especialment útil en situacions en què es treballa amb referències de tipus més genèric i es vol verificar la seva instància concreta per aplicar-hi un tractament especialitzat.

## 1. Com funciona?

Quan s'aplica `instanceof`, el compilador comprova en temps d'execució si l'objecte en qüestió pertany a la jerarquia de classes especificada. Això és particularment rellevant quan es treballa amb herència i polimorfisme, ja que permet garantir la seguretat a l'hora de fer conversions de tipus (`casting`). Si el tipus de l'objecte coincideix amb la classe indicada o alguna de les seves subclasses, l'expressió retorna `true`; en cas contrari, retorna `false`.

## 2. Aplicacions pràctiques

1. **Verificació de tipus abans d'un `cast`**: Evita errors en temps d'execució, com `ClassCastException`, garantint que només es realitzen conversions segures.
2. **Implementació de comportaments específics segons el tipus d'objecte**: Permet definir respostes diferents per a objectes que comparteixen una mateixa superclasse o interfície.
3. **Gestió de col·leccions heterogènies**: Quan es treballa amb estructures de dades que contenen diferents tipus d'objectes, `instanceof` permet distingir-los i tractar-los de manera adequada.
4. **Verificació d'implementació d'interfícies**: Assegura que una instància compleix un contracte específic abans d'invocar els seus mètodes.

## 3. Conclusions

L'operador `instanceof` és una eina valuosa en la programació amb Java que permet garantir la seguretat i correcció del codi quan es treballa amb jerarquies de classes i interfícies. No obstant això, s'ha d'usar amb criteri, usant estructures de codi clares i flexibles. Quan s'aplica adequadament, `instanceof` facilita la gestió de tipus en col·leccions d'objectes, permet conversions segures i contribueix a una programació més robusta i mantinguda.

Tot i que `instanceof` és una eina poderosa, cal utilitzar-la amb precaució per evitar un disseny deficient del codi. Un ús excessiu pot indicar una mala estructuració de les classes, que es podria solucionar amb tècniques com el polimorfisme. En molts casos, és preferible definir mètodes abstractes o interfaces per garantir que els objectes es comportin de manera adequada sense necessitat de comprovar manualment el seu tipus.

## 4. Exemples

## 4.1. Exemple 1

Exemple bàsic:

::: tabs
== Java

```java
class Animal {}

class Gos extends Animal {}

public class ExempleInstanceof {
    public static void main(String[] args) {
        Animal a = new Animal();
        Gos g = new Gos();

        System.out.println(a instanceof Animal); // true
        System.out.println(g instanceof Gos);    // true
        System.out.println(g instanceof Animal); // true (perquè Gos hereta de Animal)
        System.out.println(a instanceof Gos);    // false (un Animal no és necessàriament un Gos)
    }
}
```

:::

## 4.2. Exemple 2

L'operador també funciona amb interfícies i classes abstractes.

::: tabs
== Java

```java
interface Mascota {}

class Gat implements Mascota {}

public class ExempleInterficie {
    public static void main(String[] args) {
        Gat g = new Gat();
        System.out.println(g instanceof Mascota); // true
    }
}
```

:::

## 4.3. Exemple 3

Quan **instanceof** es fa servir amb una referència null, sempre retorna false.

::: tabs
== Java

```java
Gos g = null;
System.out.println(g instanceof Gos); // false
```

:::

## 4.4. Exemple 4

L'operador **instanceof** s'utilitza sovint per comprovar el tipus d'objecte abans de fer un cast segur:

::: tabs
== Java

```java
public class ExempleCasting {
    static void comprovarAnimal(Animal a) {
        if (a instanceof Gos) {
            Gos g = (Gos) a; // Cast segur
            System.out.println("L'Animal és un Gos!");
        } else {
            System.out.println("L'Animal no és un Gos.");
        }
    }

    public static void main(String[] args) {
        Animal a1 = new Gos();
        Animal a2 = new Animal();

        comprovarAnimal(a1); // L'Animal és un Gos!
        comprovarAnimal(a2); // L'Animal no és un Gos.
    }
}
```

:::

## 4.5. Exemple complet

:::: tabs
=== Java

::: tabs
== Electric.java

```java
// Interfície per a vehicles elèctrics
public interface Electric {
    void carregarBateria();
}
```

== Vehicle.java

```java
// Classe base Vehicle
abstract class Vehicle {
    protected String matricula;

    public Vehicle(String matricula) {
        this.matricula = matricula;
    }

    public abstract void aparcar();
    
    public String getMatricula() {
        return matricula;
    }
}
```

== Cotxe.java

```java
// Classe Cotxe que hereta de Vehicle
class Cotxe extends Vehicle {
    private int nombrePortes;

    public Cotxe(String matricula, int nombrePortes) {
        super(matricula);
        this.nombrePortes = nombrePortes;
    }

    @Override
    public void aparcar() {
        System.out.println("El cotxe amb matrícula " + matricula + " s'ha aparcat en una plaça estàndard.");
    }
}
```

== Moto.java

```java
// Classe Moto que hereta de Vehicle
class Moto extends Vehicle {
    private boolean téBastidor;

    public Moto(String matricula, boolean téBastidor) {
        super(matricula);
        this.téBastidor = téBastidor;
    }

    @Override
    public void aparcar() {
        System.out.println("La moto amb matrícula " + matricula + " s'ha aparcat en una zona de motos.");
    }
}
```

== Camio.java

```java
// Classe Camió que hereta de Vehicle i implementa Electric
class Camio extends Vehicle implements Electric {
    private int capacitatCarga;

    public Camio(String matricula, int capacitatCarga) {
        super(matricula);
        this.capacitatCarga = capacitatCarga;
    }

    @Override
    public void aparcar() {
        System.out.println("El camió amb matrícula " + matricula + " s'ha aparcat en una plaça gran.");
    }

    @Override
    public void carregarBateria() {
        System.out.println("El camió elèctric amb matrícula " + matricula + " està carregant la bateria.");
    }
}
```

== Classe principal

```java
// Classe principal amb ús de instanceof
public class Aparcament {
    public static void main(String[] args) {
        Vehicle[] vehicles = {
            new Cotxe("1234-ABC", 4),
            new Moto("5678-XYZ", true),
            new Camio("9101-QWE", 5000)
        };

        for (Vehicle v : vehicles) {
            v.aparcar();
            
            // Comprovar si el vehicle és elèctric abans de fer cast
            if (v instanceof Electric) {
                Electric e = (Electric) v; // Cast segur
                e.carregarBateria();
            }
        }
    }
}
```

:::
::::
