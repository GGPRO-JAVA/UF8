# 4. Interfícies

Una interfície és una **declaració d'atributs i mètodes sense implementació** (sense definir el codi dels mètodes). S'utilitzen per a definir el conjunt mínim d'atributs i mètodes de les classes que implementen aquesta interfície. En certa manera, és paregut a una classe abstracta amb tots els seus membres abstractes.

Si una classe és una plantilla per a crear objectes, **una interfície és una plantilla per a crear classes**.

>[!IMPORTANT]<strong>IMPORTANT!</strong>
>**Una interfície és una declaració d'atributs i mètodes sense implementació.**

Mitjançant la construcció d'una interfície, es pretén especificar què caracteritza a una col·lecció d'objectes i, igualment, especificar quin comportament han de reunir els objectes que vulguen entrar dins d’eixa categoria o col·lecció.

En una interfície també es poden declarar constants que defineixen el comportament que han de suportar els objectes que vulguen implementar aqueixa interfície. La sintaxi típica d'una interfície és la següent:

::: tabs
== Java

```java
public interface Nom {
  //Declaració d'atributs i mètodes (sense definir codi)
}
```

:::

**Una interfície defineix un tipus**, és a dir, serveix per indicar que una variable, un paràmetre o un valor de retorn pertany a un tipus que compleix certes característiques. Fins i tot quan no conté cap mètode (allò que s’anomena “interfície buida”), estem establint un tipus concret que permet al compilador i al programador entendre la finalitat d’aquells objectes.

Les interfícies, encara que estiguen buides, són molt valuoses perquè faciliten el manteniment i l’extensió de les aplicacions. Quan definim un comportament comú, podem fer que totes les classes que l’implementen segueixen el mateix patró: si en el futur volem afegir-hi un nou mètode o una nova propietat, només caldrà actualitzar la interfície i forçar que totes les classes adaptin la seua implementació. Això fa que el codi siga més fàcil de mantenir i evolutiu davant d’exigències canviants.

A més, el fet de disposar d’una interfície permet crear **variables polimòrfiques**: podem declarar una variable amb el nom de la interfície i assignar-hi objectes de qualsevol classe que la implementi. En temps d’execució, la invocació de mètodes es pot fer de manera polimòrfica, tractant diferents classes de manera uniforme.

En la pràctica, una interfície buida pot servir com a “etiqueta” que identifica un conjunt heterogeni d’objectes. Per exemple, si definim una interfície sense cap mètode, qualsevol classe que l’implementi queda automàticament dins del grup que aquella interfície representa.

>[!IMPORTANT]<strong>IMPORTANT</strong>
>Cal tindre en compte que:
>
>- **Una interfície no es pot instanciar en objectes**, només serveix per a implementar classes.
>- **Una classe pot implementar diverses interfícies** (separades per comes).
>- **Una classe que implementa una interfície ha de proporcionar implementació per a tots i cadascun dels mètodes** definits en la interfície.
>- **Les classes que implementen una interfície que té definides constants poden usar-les en qualsevol part del codi** de la classe, simplement indicant el seu nom.

>***Exemple d'interfícies: Ús d'interfícies***
>
>:::: tabs
>=== Java
>
>::: tabs
>== Interfície
>
>```java
>public interface Accio {
>    void executar(); 
>}
>```
>
>== Classe X
>
>```java
>public class X implements Accio {
>    @Override
>    public void executar() {
>        System.out.println("X executa una acció concreta.");
>    }
>}
>```
>
>== Classe Y
>
>```java
>public class Y implements Accio {
>    @Override
>    public void executar() {
>        System.out.println("Y executa una altra acció diferent.");
>    }
>}
>```
>
>== Classe principal
>
>```java
>public class Programa2 {
>    public static void main(String[] args) {
>        // Ara Accio ja defineix un mètode executar(), i totes les classes
>        // que la implementen han d'oferir la seua versió concreta.
>        Accio a = new X();
>        Accio b = new Y();
>
>        a.executar();  // Imprimeix: X executa una acció concreta.
>        b.executar();  // Imprimeix: Y executa una altra acció diferent.
>    }
>}
>```
>
>::::

>***Exemple d'interfícies: Ús d'interfícies buides***
>:::: tabs
>=== Java
>
>::: tabs
>== Interfície buida
>
>```java
>// Interfície buida que marca classes serialitzables
>public interface SerializableMarca {}
>```
>
>== Classe Persona
>
>```java
>public class Persona implements SerializableMarca {
>    private String nom;
>    private int edat;
>
>    public Persona(String nom, int edat) {
>        this.nom = nom;
>        this.edat = edat;
>    }
>
>    public String toString() {
>        return nom + " (" + edat + " anys)";
>    }
>}
>```
>
>== Classe principal
>
>```java
>public class Programa {
>    public static void main(String[] args) {
>        Persona p = new Persona("Joana", 28);
>
>        // Verifiquem si l'objecte implementa SerializableMarca
>        if (p instanceof SerializableMarca) {
>            System.out.println("Persona serialitzable: " + p);
>            // Ací podríem cridar el procés de serialització
>        } else {
>            System.out.println("No pot ser serialitzada.");
>        }
>    }
>}
>```
>
>::::

## 4.1 Exemple complet

En aquest exemple crearem una interfície Figura i posteriorment la implementarem en vàries classes. Per a crear una interfície hem de punxar amb el botó dret sobre el paquet on la vulguem crear i després NEW > Java Interface.

Veurem un exemple simple de definició i ús de interfície a Java. Les classes que usarem i les seues relacions es mostren en l'esquema:

![Esquema exemple 6](/uf8/esquema_exemple6.jpg)

:::: tabs
=== Java

En aquest exemple **la interfície Figura defineix un tipus de dada**. Per això podem crear un ArrayList de figures on inserim quadrats, cercles, rectangles, etc. (polimorfisme).

Això ens permet donar-li un tractament comú a totes les figures: Mitjançant un bucle while recorrem la llista de figures i cridem al mètode area() que serà diferent per a cada classe de figura.


::: tabs
== Interfície Figura

![Classe Figura](/uf8/figura.jpg)

== Subclasses

![Exemple6](/uf8/exemple6.jpg)

== Classe principal

![Exemple6 Main](/uf8/Exemple6_main.jpg)

== Eixida

![Eixida exemple 6](/uf8/eixida_exemple6.jpg)

::::
