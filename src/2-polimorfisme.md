# 2. Polimorfisme

El **polimorfisme** o sobreescriptura de mètodes és la pràctica de definir un mètode en una subclasse amb la mateixa signatura (nom i paràmetres) que un mètode existent en la classe base. Quan una subclasse sobreescriu un mètode, ofereix una implementació específica per a aquell comportament.

Gra­cies a la sobreescriptura i a la selecció dinàmica de mètodes, el sistema decideix en temps d'execució quina versió del mètode ha de cridar-se. Això s'aconsegueix perquè **una referència d'una classe general pot apuntar a un objecte d'una classe derivada**. En conseqüència, **el tipus real de l'objecte determina quin bloc de codi s'executarà**, no el tipus declarat de la variable.

Aquest mecanisme permet implementar el polimorfisme en temps d'execució, que és un pilar fonamental de la programació orientada a objectes. Concretament:

- Una superclasse pot definir un conjunt de mètodes generals.
- Les subclasses poden reutilitzar aquests mètodes tal qual o, si cal, sobreescriure'ls per oferir un comportament específic.
- Quan es crida un mètode mitjançant una referència d'una classe general, el sistema inspecciona en temps d'execució de quina subclasse prové l'objecte i executa la implementació corresponent a eixa classe derivada.

:::: tabs
=== Java

En Java, la selecció dinàmica de mètodes s'aconsegueix mitjançant la sobreescriptura i l'ús de referències a la superclasse:

1. Sobreescriptura de mètodes

   - Quan una subclasse defineix un mètode amb la mateixa signatura que un mètode de la superclasse, aquest mètode s'anomena sobreescrit.
   - L'anotació `@Override` es recomana per assegurar que el mètode coincideix exactament amb el de la classe base.

2. Selecció dinàmica en temps d'execució

   - Es pot declarar una variable del tipus de la superclasse, però assignar-li un objecte d'una subclasse:

        ```java
        Superclasse ref = new Subclasse();
        ```

    - Quan s'invoca un mètode que està sobreescrit per la subclasse, Java triarà automàticament la implementació de la classe concreta (subclasse), tot i que la variable es declare com a tipus general.

        ```java
        ref.metodeSobreescrit();  // Crida la versió definida a Subclasse
        ```

Exemple de polimorfisme:

::: tabs
== Classe Animal

```java
class Animal {
    public void ferSo() {
        System.out.println("L'animal fa un so genèric.");
    }
}
```

== Classe Gos

```java
class Gos extends Animal {
    @Override
    public void ferSo() {
        System.out.println("El gos lladra.");
    }
}
```

== Classe Gat

```java
class Gat extends Animal {
    @Override
    public void ferSo() {
        System.out.println("El gat miola.");
    }
}
```

== Classe principal

```java
public class ExemplePolimorfisme {
    public static void main(String[] args) {
        Animal a1 = new Gos();
        Animal a2 = new Gat();

        a1.ferSo();  // Imprimeix "El gos lladra."
        a2.ferSo();  // Imprimeix "El gat miola."
    }
}
```

:::

En aquest fragment, malgrat que **a1** i **a2** són de tipus **Animal**, en temps d'execució Java resol quina versió de **ferSo()** executar segons el tipus real de l'objecte (Gos o Gat).

::::
