# 3. Classes abstractes

Una **classe abstracta** és una classe que **declara l'existència d'alguns mètodes però no la seua implementació** (és a dir, conté la capçalera del mètode però no el seu codi). Els mètodes sense implementar són mètodes abstractes.

Les classes abstractes poden contindre:

- **Mètodes abstractes**: declaracions de mètodes sense codi associat. Són com una promesa que les subclasses han de complir implementant-ne el comportament concret.
- **Mètodes no abstractes**: mètodes amb implementació completa, que poden ser compartits per totes les subclasses.

::: warning ATENCIÓ
**Una classe abstracta no es pot instanciar**, però **sí es pot heretar**. Les subclasses hauran d'implementar obligatòriament el codi dels mètodes abstractes (llevat que també es declaren com a abstractes).
:::

Les classes abstractes són útils quan necessitem definir una forma generalitzada de classe que serà compartida per les subclasses, deixant part del codi en la classe abstracta (mètodes "normals") i delegant una altra part en les subclasses (mètodes abstractes).

::: warning ATENCIÓ
**No poden declarar-se constructors o mètodes estàtics abstractes.**
:::

La finalitat principal d'una classe abstracta és crear una classe heretada a partir d'ella. Per això, en la pràctica és obligatori aplicar herència (si no, la classe abstracta no serveix per a res). El cas contrari és una classe final, que no pot heretar-se com ja hem vist. Per tant, **una classe no pot ser abstract i final al mateix temps**.

Per exemple, aquesta classe abstracta Principal ten dos mètodes: un concret i un altre abstracte.

::: tabs
== Java

```java
public abstract class Principal {
  // Mètode concret amb implementació
  public void metodeConcret() {
    ...
  }
  // Mètode abstracte sense implementació
  public abstract void metodeAbstracte();
}
```

:::

Aquesta subclasse hereta de Principal tots dos mètodes, però està obligada a implementar el codi del mètode abstracte.

::: tabs
== Java

```java
class Secundària extends Principal {
  // Implementació concreta
  public void metodeAbstracte() {
    ...
  }
}
```

:::
