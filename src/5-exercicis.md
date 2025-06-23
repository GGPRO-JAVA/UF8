# Exercicis

## Exercicis - Nivell bàsic

### Exercici 1

Una empresa necessita gestionar els vehicles de què disposa. Cada vehicle té unes dades bàsiques, i segons el tipus (cotxe, camió, moto...), hi ha informació i comportaments particulars.

a) Crea una classe Vehicle amb atributs per a la matricula, la marca, el model model i el tipus de vehicle (per exemple, "cotxe" o "moto").  
b) Afig un mètode que mostre tota la informació del vehicle, tenint en compte que, en funció del tipus, s'haurà de mostrar alguna informació pròpia d'eixe tipus (caldrà afegir-ho com a atributs, amb valors aleatoris establits en inicialitzar un objecte):  

- Si el tipus és "camió", també ha de mostrar el pes màxim admissible.
- Si és "moto", ha de mostrar si pot circular per autopista.
- Si és "cotxe", ha de mostrar el nombre de places.

c) En la classe principal, crea vehicles de diversos tipus i mostra’ls per pantalla.  

:::: tip ✏️ Reflexió

Tot i que aquest sistema funciona, **no és una bona solució des del punt de vista de la programació orientada a objectes**. Per què?

Molts alumnes pensen en fer una estructura com aquesta dins de mostrarInfo():

::: tabs
== Java

```java
if (tipus.equals("cotxe")) {
    // Mostrar places
} else if (tipus.equals("camio")) {
    // Mostrar pes màxim
} else if (tipus.equals("moto")) {
    // Mostrar si pot anar per autopista
}
```

:::

Aquesta solució presenta diversos problemes:

- El mètode usat per a mostrar informació (i qualsevol altre que comprove el tipus per a fer una cosa o una altra) coneix massa detalls: ha de saber com es comporten tots els tipus de vehicle.
- La classe Vehicle tindrà atributs que no seran usats per tots els objectes (les motos no necessiten un atribut per al nombre de places ni per al pes màxim admissible).
- Viola el principi d’obert/tancat: si apareix un nou tipus de vehicle (per exemple, bicicleta elèctrica), caldrà modificar tots els mètodes que facen la comprovació de tipus.
- No s’aprofita el polimorfisme: cada objecte hauria de saber com mostrar la seua pròpia informació, no delegar-ho tot a un mètode amb condicions.

Tots aquests problemes seran més greus a mesura que s'afegeixen més tipus de vehicles.
::::

Ara corregirem aquesta estructura fent ús d’herència i classes abstractes.

d) Reestructura el codi:  

- Fes que Vehicle siga una classe abstracta amb els atributs bàsics: matricula, marca i model.
- Declara un mètode abstracte per a mostrar la informació.

e) Crea les subclasses:  

- Cotxe, amb un atribut per al nombre de places.
- Camio, amb un atribut per al pes màxim.
- Moto, amb un atribut que determine si pot anar per autopista.

Cada subclasse ha de sobreescriure el mètode per mostrar la informació corresponent.

f) En la classe principal, crea un llistat de vehicles dels tres tipus i mostra la informació de tots ells mitjançant una única crida al mètode definit en un bucle.  
g) Encapsula el codi.  
h) Afig una classe Concessionari que gestione una col·lecció de vehicles. Inclou mètodes com:  

- Afegir vehicles a la col·lecció
- Mostrar la informació de tots els vehicles
- Fes un recompte de quants vehicles hi ha de cada tipus i mostrar-ho per pantalla.  

i) Fes ús de la classe Concessionari des del main, i prova els seus mètodes.

### Exercici 2

Estàs desenvolupant un sistema per gestionar els productes d’una tenda d’informàtica. Els productes poden ser de diferents tipus (processadors, discos durs, targetes gràfiques, etc.) i alguns comparteixen característiques comunes, com per exemple la capacitat d’emmagatzematge o el consum energètic. Cal tindre en compte, que els distints productes tindran informació sobre particular ells (els discs durs tindran una certa capacitat d'emmagatzemament, per exemple) i, com tenen funcions diferents dins de l'àmbit informàtic, tindran també comportaments (funcions) diferents. Per tant, farem ús de l'herència i crearem una classe base, de la qual heretaran distintes subclasses.

a) Crea una classe ProducteInformatic amb els atributs bàsics següents: un codi identificatiu, un nom i un preu per unitat.  
b) Crea distintes subclasses de ProducteInformatic: DiscDur, GPU i CPU.

- DiscDur tindrà:
  - un atribut enter per a la capacitat (en GB).
  - una cadena per al tipus (HDD o SSD).
  - un enter per a la velocitat de lectura/escriptura.
- GPU tindrà:
  - un atribut enter per a la VRAM.
  - un booleà que indica si té accés a treballar amb IA.
  - un booleà que indica si permet fer *overclock*.
- CPU tindrà:
  - un enter per al nombre de nuclis.
  - un decimal per a la velocitat (en GHz).
  - un booleà que indica si permet fer *overclock*.

c) Implementa el constructor de totes les classes. Assegura't que cada objecte, independentment del producte, té un codi diferent. A més, este serà invariable i no es podrà modificar una vegada queda establit per primera vegada.

Ara volem un mètode que mostre tota la informació d'un producte. Com és una funcionalitat comuna a totes les subclasses, però diferent en cadascuna, caldrà fer ús de la abstracció.

d) Fes que la classe pare siga abstracta, i declara el mètode abstracte encarregat de mostrar tota la informació d'un producte. Implementa el mètode en les subclasses.  

Ara volem assignar diversos comportaments simulats a les subclasses. Perquè si bé la funcionalitat de mostrar informació és comuna, cada dispositiu informàtic pot fer certes funcionalitats que la resta no:

:::: tip ✏️ Reflexió

Podríem **implementar cada mètode en les classes corresponents**, però no seria una pràctica correcta des del punt de vista de la Programació Orientada a Objectes. Particularment, pel que fa al polimorfisme: **no podríem tractar els objectes de forma genèrica a través d'un comportament comú**.

Per tal d'aplicar bones pràctiques, cal fer ús de l'**herència múltiple**.

::: tabs
== Java
En Java, com ja s'ha vist en el tema, no hi ha herència múltiple com a tal, i s'usa el concepte d'**interfície**.
:::

::::

e) Crea les següents funcionalitats:

- Formatejar
- Overclock
- AccelerarIA
- CalcularVelocitat

f) Fes que cada subclasse implemente les funcionalitats corresponents (els comportaments de les funcions ha de ser molt senzill, únicament mostrar un missatge per pantalla):

- DiscDur
  - → Formatejar
- CPU
  - → Overclock
  - → AccelerarIA
- GPU
  - → Overclock
  - → CalcularVelocitat

g) En la classe principal:

- Crea una llista de ProducteInformatic.
- Recorre la llista i mostra la informació de cada producte (codi, nom, preu).
- Fes que s'executen, també, la resta de mètodes que implementen (caldrà comprovar si cada objecte és instància ).

h) Afig un nou comportament Eficient que comprove si un producte (CPU o GPU) és eficient o no. Caldrà afegir un nou atribut en estes classes, que contindrà el consum en wats, i al qual se li assignarà un valor aleatori comprés entre 200 i 700.  

- Es considerarà que una CPU és eficient si el consum per nucli és inferior a 100 wats.
- Es considerarà que una GPU és eficient si el consum per GB de VRAM és inferior a 50 wats.

## Exercicis - Nivell mitjà

### Exercici 3

L'associació *Vida i Natura* és una organització sense ànim de lucre que es dedica al rescat, acollida i adopció d’animals domèstics i exòtics. Disposa de diverses instal·lacions, com ara una zona d’estada per a mamífers, una àrea especial per a aus i una petita consulta veterinària. Com que el nombre d’animals atesos ha crescut molt en els últims mesos, el personal ha decidit informatitzar el registre i el seguiment dels animals. Per a fer-ho, cal desenvolupar una **aplicació que permeta gestionar els animals allotjats en el refugi**.

Els animals que s’atenen habitualment són de **tres espècies**: **gossos**, **gats** i **ocells**. Cada animal té assignat un **identificador únic** (assignat automàticament en incorporar-se al refugi), un **nom**, una **edat** (establida segons la valoració veterinària en el moment de l’entrada), i un indicador del seu estat actual de **vacunació** (poden estar al dia en les vacunes o poden no estar-ho).

Cal tindre en compte que **els gossos i els ocells** són molt diferents uns d'altres en funció de la **raça** a la qual pertanyen i, per tant, caldrà afegir aquesta informació al seu registre. Açò no ocorre amb els gats (perquè, a més a més, la seua raça és complexa de determinar).

Pel seu compte, hi ha **gats** que presenten **problemes de conducta** (agressivitat i hiperactivitat, entre d'altres), cosa que s'haurà de tindre en compte si es volguera adoptar. En aquest sentit, pel que fa als **ocells**, **no tots podran ser adoptats**, perquè alguns són de races salvatges i la legislació en matèria animal ho prohibeix (per a simplificar, aquest serà un paràmetre independent de la raça).

Per últim, dels **ocells** cal tindre en compte la seua **capacitat de vol**, ja que alguns (ja siga per la raça o per alguna condició particular) no poden. Açò es té en compte a l'hora d'entrenar-los per a algunes exhibicions de vol que es porten a cap en el refugi.

A més, cada espècie d’animal pot fer activitats concretes:

- Totes les espècies registrades (gossos, gats i ocells) tenen opció a ser adoptats, però **en un futur podria arribar al refugi alguna nova espècie que** siga 100% salvatge i **no siga apta per a adoptar en ningun cas**. A més, de les espècies actuals, **cal tindre en compte**:
  - Un animal només es pot **adoptar** si té **menys de 10 anys** i està **vacunat**.
  - Els **gossos i els gats** poden ser adoptats únicament amb el compliment de l'**anterior requeriment**.
  - Els **ocells** podran ser adoptats només si són d'una **raça no salvatge**.
  - **Ser adoptat implicarà eixir del refugi**, i mostrar un missatge per pantalla amb un acomiadament.
- Els **gats** poden participar en **sessions de teràpia** amb humans, sempre que **no tinguen problemes de conducta**. Quan un gat du a terme una sessió de teràpia, el programa ho indicarà.
- Els **ocells** poden fer **exhibicions de vol** durant les jornades de portes obertes, sempre que tinguen **capacitat de vol** i que **no siguen salvatges**.

El programa mostrarà un menú que permetrà:

- Mostrar la informació bàsica de tots els animats del refugi (codi, espècie, nom i edat).
- Mostrar tota la informació d'un animal a partir del seu codi.
- Afegir un animal, introduint per pantalla tota la informació necessària segons l'espècie.
- Adoptar un animal: permetrà a l'usuari seleccionar quina espècie d'animal es vol adoptar, mostrarà tot el llistat d'eixa espècie amb el seu codi i permetrà seleccionar-ne un. Una vegada adoptat, l'animal quedarà forma del registre del refugi.
- Donat el codi d'un animal, actualitzar la seua edat (sumar 1).
- Donat el codi d'un animal, actualitzar una determinada informació segons l'espècie:  
  - Si és gos, no hi ha res que actualitzar.
  - Si és gat, es pot actualitzar la seua conducta a la contrària que presente actualment.
  - Si és ocell, es pot actualitzar la seua capacitat de volar a la contrària que presente actualment.
- Començar sessió de teràpia, amb la qual cosa es mostrarà tot el llistat de gats sense problemes de comportament junt amb el seu codi corresponent, i permetrà a l'usuari seleccionar un.
- Realitzar exhibició, que serà molt paregut al cas anterior. Es mostraran tots els ocells no salvatges i amb capacitat de vol, i l'usuari podrà triar-ne un.
- Eixir del programa.

::: tip ANOTACIONS
Per a poder tindre un bon control de tots els animals, resultarà molt úil fer ús d'una estructura que continga tota la informació d'aquests. Una bona opció seria una **estructura clau-valor**, on la clau és l'espècie d'animal i el valor és el llistat dels animals d'eixa espècie.

- Aquesta estructura estarà dins de la classe independent Refugi.
- Tot animal que entre al refugi s'afegirà a aquesta estructura, dins del llistat corresponent a la seua espècie.
- Tot animal que és adoptat s'eliminarà de l'estructura.

És important aplicar bones pràctiques a l'hora de programar, amb un codi coherent, unes classes ben definides i seguint el **principi d'obert/tancat**. Segons aquest principi, **un programa** realitzat amb bones pràctiques **ha d'estar obert a ampliacions però tancat a modificacions**. Per a aconseguir-ho:

- Les subclasses usaran el constructor de la classe pare.
- Cada classe contindrà els mètodes que afectaran a la pròpia classe i als seus objectes.
- S'evitarà, en la mesura en què siga possible, l'ús de mètodes estàtics.

El programa consistirà en un bucle infinit que només acabarà si l'usuari selecciona l'opció corresponent. A aquest bucle se'l coneix com bucle principal del programa, i sol estar directament al mètode principal. El bucle principal executarà, en cada iteració, el mètode encarregat de mostrar el menú i un mètode gestor de funcionalitats. Aquest segon serà l'encarregat d'obtindre la selecció de l'usuari i de cridar a la funció corresponent. Tots aquests poden ser mètodes estàtics de la classe principal.
:::

## Exercicis - Nivell avançat

### Exercici 4

La cooperativa *Cosmolab*, dedicada a la investigació espacial, gestiona diversos projectes interns que estudien la viabilitat de colònies fora del planeta Terra. En l’actualitat, treballen amb diferents prototips d’unitats experimentals que poden simular condicions d’hàbitat en diferents entorns, i necessiten una aplicació que els permeta supervisar en tot moment l’estat d’aquestes unitats. Fins ara, cada equip de recerca portava un registre manual, però amb l’arribada de nous membres s’ha decidit centralitzar tota la gestió.

Tota unitat operativa disposa d’un identificador numèric únic que el distingeix de les altres, i se li assigna un nom. També tenen un temps d'ús (en anys) i l’estat general en què es troba, que pot ser actiu o avariat.

En l’actualitat, hi ha tres tipus de prototips que funcionen de forma estable i que, per tant, han de poder ser registrats i gestionats: les unitats de cultiu, les d’anàlisi atmosfèric i les de generació d’energia. Cadascuna d’elles té característiques pròpies. Les unitats de cultiu estan especialitzades en simulacions de producció vegetal i compten amb un sistema de gestió d’aigua, que pot estar actiu o no, i una capacitat màxima de plantes que poden allotjar, a més del nombre actual de plantes allotjades i de la potencia en watts que consumeix. Les d’anàlisi atmosfèric enregistren el percentatge mitjà d'oxigen i la concentració mitjana de partícules contaminants detectades, en ppm (partícules per milió). Les unitats energètiques generen una certa potència cadascuna (per fer-ho senzill, serà constant).

Les diferents unitats són instal·lades de forma conjunta en zones (zona A, zona B, etc.). D'aquesta forma, cada zona és independent de la resta

Sumat a tot açò, cal tindre en compte que:

- Si el sistema de gestió d'aigua està actiu, el sistema de cultiu consumirà una potència de 100 watts més altres 10 watts per planta.
- En cada unitat de cultiu, el nombre de plantes no pot superar el maxim establit, que serà de 30. El nombre inicial de plantes s'establirà inicialment en 0.
- La potència generada per cada unitat energètica serà aleatòria entre 0.5 kW i 1.5 kW (tindria més sentit incorporar una variabilitat en funció de l'hora, per tal de simular el cicle dia/nit, però ho deixem més senzill).
- Cada zona no podrà tindre més d'una unitat d'anàlisi atmosfèric, i aquests consumiran una potència constant de 300 watts.
- El percentatge mitjà d'oxigen detectat per la unitat d'anàlisi atmosfèric començarà amb un número inicial de 10%, i variarà en funció del número de plantes total de les diverses unitats de cultiu que puga haver en la zona. Cada planta afegirà un valor aleatori comprés entre 0,05% i 0,15% al percentatge mitjà d'oxigen.
- Les partícules contaminants del sistema són degudes, principalment, a elements tòxics que deixen les unitats energètiques. El valor inicial en ppm de les partícules contaminants serà de 0, i anirà augmentant a mesura que es vagen afegint unitats energètiques. D'aquesta forma, aquest nombre augmentarà a raó d'un valor aleatori entre 25 i 75 per cada unitat energètica.

El sistema proporcionarà a l'usuari formes de modificar la composició dels elements de cada zona, amb la possibilitat d'afegir i eliminar unitats, i de variar alguns paràmetres d'aquests. Només es podran fer aquestes modificacions a zones operatives, que són aquelles que tenen, almenys, una unitat de cada tipus i, a més, almenys una unitat de cultiu té el sistema de gestió d'aigua activat. Addicionalment, les unitats d'anàlisi atmosfèric estan limitades a una per zona. Les opcions que el sistema oferirà a l'usuari seran:

- Possibilitat d'afegir noves unitats de cultiu i energètiques.
- En les unitats de cultiu, possibilitat d'augmentar i disminuir el nombre de plantes, dins del límit establit.
- També en les unitats de cultiu, possibilitat d'activar o desactivar el sistema de gestió d'aigua. Per a afegir plantes, el sistema ha d'estar actiu. Mentre hi haja plantes, no es podrà desactivar. Per a eliminar la unitat, caldrà primer deixar el nombre de plantes a 0.
- Anàlisi atmosfèric: es mostra informació sobre el percentatge d'oxigen en l'aire i sobre el nombre mitja de partícules contaminants. En cas de trobar valors fora des valors raonables per a la vida, informarà.
  - Els valors buscats d'oxigen mitjà a l'aire són entre 16% i 21%.
  - Els valors acceptables de partícules contaminants seran mai superiors a 100 ppm.
  - Com cada anàlisi agafa mostres d'aire diferents, sempre cap algun error en les dades. El percentatge d'oxigen pot variar en cada anàlisi de forma aleatoria en ±1% respecte del valor real, i les partícules contaminants poden variar en ±5 ppm.
- Anàlisi energètic: es mostra la informació de la potència disponible en el sistema i de la consumida, amb el detall desglossat per cada elements que en fa ús.
  
  ::: details Exemple d'eixida d'anàlisi energètic

  ```plaintext
  ANÀLISI ENERGÈTIC DEL SISTEMA

  Potència total disponible: 973 W
  Potència total consumida: 790 W

  Distribució del consum:

  Unitat de cultiu 1: 320 W
    -> Sistema de gestió d'aigua actiu: 100 W
    -> Potència consumida per planta (22): 220 W 

  Unitat de cultiu 2:  170 W
    -> Sistema de gestió d'aigua actiu: 100 W
    -> Potència consumida per planta (7): 70 W 

  Unitats d’anàlisi atmosfèrica: 300 W
  ```

  :::

- Solucionar les unitats avariades.

Tant les unitats energètiques com les d'anàlisi atmosfèric es poden avariar, però en cadascuna el mal funcionament tindrà una naturalesa diferent:

- Les unitats energètiques poden, de sobte, oferir fins a un 20% menys de la potència que deurien. Aquest comportament inesperat pot ocórrer en qualsevol moment que l'usuari demane un anàlisi energètic, amb una probabilitat d'avaria del 5% més un 2% addicional per cada any d'ús que tinga. Si la potència oferida cau per baix de la consumida, es considera que es perd la zona.
- Les unitats d'anàlisi atmosfèric poden, de sobte, donar dades completament incorrectes si s'avarien, cosa que pot passar en una probabilitat del 10% més un altre 1% per cada any d'ús, i pot ocórrer cada vegada que l'usuari fa un anàlisi atmosfèric.
- Ambdues situacions es poden solucionar. L'usuari sempre tindrà accés a l'opció que permet solucionar les avaries  en cadascun dels dos tipus d'unitats, però en cas de seleccionar aquesta opció sense que la unitat estiga avariada es mostrarà un missatge informant que ningun mal funcionament ha sigut detectat. En cas de sí haver, es solucionarà.

<!--

## Exercici 1 - Producte

Suposem una classe Producte amb dos atributs:

- String nom
- int quantitat

Implementa aquesta classe amb un constructor (amb paràmetres) a més dels getters i setters dels seus dos atributs. No és necessari comprovar les dades introduïdes.

A continuació, en el programa principal fes el següent:

1. Crea 5 instàncies de la Classe Producte.
2. Crea un llistat i afig les 5 instàncies de Producte al ArrayList.
3. Visualitza el contingut del llistat.
4. Elimina dos element del llistat.
5. Insereix un nou objecte Producte enmig de la llistat.
6. Visualitza de nou el contingut.
7. Elimina tots els productes del llistat.

## Exercici 2 - Astres

Defineix una jerarquia de classes que permeta emmagatzemar dades sobre els planetes i satèl·lits (llunes) que formen part del sistema solar.

Alguns atributs que necessitarem emmagatzemar són:

- Massa del cos.
- Diàmetre mitjà.
- Període de rotació sobre el seu propi eix.
- Període de translació al voltant del cos que orbiten.
- Distancia mitjana a aqueix cos.
- etc.

Defineix les classes necessàries, amb:

- Constructors.
- Mètodes per a recuperar i emmagatzemes atributs.
- Mètodes per a mostrar la informació de l'objecte.

Defineix un mètode que, donat un objecte del sistema solar (planeta o satèl·lit), imprimisca tota la informació que es disposa sobre el mateix (a més de el seu llistat de satèl·lits si els tinguera).

El diagrama UML seria:

![Esquema d'herència](/uf8/Exercici_Astros.jpg)

Una possible solució seria crear un llistat d'objectes, inserir els planetes i satèl·lits (directament mitjançant codi o sol·licitant-los per pantalla) i després mostrar un xicotet menú que permeta a l'usuari imprimir la informació de l'astre que trie.

## Exercici 3 - Mascotes

Implementa una classe anomenada **Inventari** que utilitzarem per a emmagatzemar referències a tots els animals existents en una botiga de mascotes.

Aquesta classe ha de complir amb els següents requisits:

- A la botiga existiran 4 tipus d'animals: gossos, gats, lloros i canaris.
- Els animals han d'emmagatzemar-se en un llistat privat dins de la classe Inventari.
- La classe ha de permetre realitzar les següents accions:
  - Mostrar el llistat d'animals (sols tipus i nom, 1 línia per animal).
  - Mostrar totes les dades d'un animal concret.
  - Mostrar totes les dades de tots els animals.
  - Inserir animals en l'inventari.
  - Eliminar animals de l'inventari.
  - Buidar l'inventari.

Implementa les altres classes necessàries per a la classe Inventari.

El diagrama UML seria:

![Esquema d'herència](/uf8/Exercici_Mascotes.jpg)

## Exercici 4 – Banc

Farem una aplicació que simule el funcionament d'un banc.

Crea una classe **CompteBancari** amb els atributs: **IBAN** i **saldo**. Implementa mètodes per a :

- Consultar els atributs.
- Ingressar diners.
- Retirar diners.
- Traspassar diners d'un compte a una altre.

Per als tres últims mètodes pot utilitzar-se internament un mètode privat més general anomenat **afegir(...)** que afija una quantitat (positiva o negativa) al saldo.

També hi haurà un atribut comú a totes les instàncies anomenat **interesAnualBasic**, que en principi pot ser constant.

La classe ha de ser **abstracta** i ha de tindre un mètode **calcularInteressos()** que es deixarà sense implementar.

També pot ser útil implementar un mètode per a mostrar les dades del compte.

D'aquesta classe heretaran dues subclasses: **CompteCorrent** i **CompteEstalvi**. La diferència entre ambdues serà la manera de calcular els interessos:

- A la primera se li incrementarà el saldo tenint en compte l'interés anual bàsic.
- La segona tindrà una constant de classe anomenada **saldoMinim**. Si no s'arriba a aquest saldo l'interés serà la meitat de l'interés bàsic. Si se supera el saldo mínim l'interés aplicat serà el doble de l'interés anual bàsic.

Implementa una classe principal per a provar el funcionament de les tres classes: Crea diversos comptes bancaris de diferents tipus, prova de realitzar ingressos, retirades i transferències; calcula els interessos i mostra'ls per pantalla; etc.

El diagrama UML seria:

![Esquema d'herència](/uf8/Exercici_Banc.jpg)

## Exercici 5 – Empresa i empleats

Implementarem dues classes que permeten gestionar dades d'empreses i els seus empleats.

Els **empleats** tenen les següents característiques:

- Un empleat té nom, DNI, sou brut (mensual), edat, telèfon i adreça.
- El nom i DNI d'un objecte no pot variar.
- És obligatori que tots els empleats tinguen almenys definit el seu nom, DNI i el sou brut. Les altres dades no són obligatoris.
- Serà necessari un mètode per a imprimir per pantalla la informació d'un empleat.
- Serà necessari un mètode per a calcular el sou net d'un empleat. El sou net es calcula descomptant del sou brut un percentatge que depén de l'IRPF. El percentatge de l'IRPF depén del sou brut anual de l'empleat (sou brut x 12 pagues).**(\*)**

|**Sou brut anual**|**IRPF**|
|-|-|
|Inferior a 12.000€|20%|
|De 12.000€ a 25.000€|30%|
|Més de 25.000€|40%|

Per exemple, un empleat amb un sou brut anual de 17.000 € tindrà un 30% d'IRPF. Per a calcular el seu sou net mensual es descomptarà un 30% al seu sou brut mensual.

Les **empreses** tenen les següents característiques:

- Una empresa té nom i CIF (dades que no poden variar), a més de telèfon, adreça i empleats. Quan es crea una nova empresa aquesta manca d'empleats.
- Seran necessaris mètodes per a:
  - Afegir i eliminar empleats a l'empresa.
  - Mostrar per pantalla la informació de tots els empleats.
  - Mostrar per pantalla el DNI, sou brut i net de tots els empleats.
  - Calcular la suma total de sous bruts de tots els empleats.
  - Calcular la suma total de sous nets de tots els empleats.

**Implementa les classes Emprat i Empresa** amb els atributs oportuns, un constructor, els getters/setters oportuns i els mètodes indicats. Pots afegir més mètodes si ho veus necessari. Aquestes classes no han de realitzar cap mena d'entrada per teclat.

**Implementa també una classe Programa_Principal** per a realitzar proves: crear una o diverses empreses, crear empleats, afegir i eliminar empleats a les empreses, llistar tots els empleats, mostrar el total de sous bruts i nets, etc.

**(\*)** L'IRPF realment és més complex però s'ha simplificat per a no complicar massa aquest exercici.

## Exercici 6 - Vehicles

**És molt aconsellable fer el disseny UML abans de començar a programar**.

Crea diverses classes per a un programari d'una empresa de transport. Implementa la jerarquia de classes necessària per a complir els següents criteris:

- Els vehicles de l'empresa de transport poden ser terrestres, aquàtics i aeris. Els vehicles terrestres poden ser cotxes i motos. Els vehicles aquàtics poden ser vaixells i submarins. Els vehicles aeris poden ser avions i helicòpters.
- Tots els vehicles tenen matrícula i model (dades que no poden canviar). La matrícula dels cotxes terrestres han d'estar formada per 4 números i 3 lletres. La dels vehicles aquàtics per entre 3 i 10 lletres. La dels vehicles aeris per 4 lletres i 6 números.
- Els vehicles terrestres tenen un nombre de rodes (dada que no pot canviar).
- Els vehicles aquàtics tenen eslora (dada que no pot canviar).
- Els vehicles aeris tenen un nombre de seients (dada que no pot canviar).
- Els cotxes poden tindre aire condicionat o no tindre'n.
- Les motos tenen un color.
- Els vaixells poden tindre motor o no tindre'n.
- Els submarins tenen una profunditat màxima.
- Els avions tenen un temps màxim de vol.
- Els helicòpters tenen un nombre d'hèlices.
- No es permeten vehicles genèrics, és a dir, no es deuen poder instanciar objectes que siguen vehicles sense més. Però ha de ser possible instanciar vehicles terrestres, aquàtics o aeris genèrics (és a dir, que no siguen cotxes, motos, vaixells, submarins, avions o helicòpters).
- El disseny ha d'obligar al fet que totes les classes de vehicles tinguen un mètode imprimir() que imprimisca per pantalla la informació del vehicle en una sola línia.

Implementa totes les classes necessàries amb: atributs, constructor amb paràmetres, getters/setters i el mètode imprimir. Utilitza **abstracció** i **herència** de la forma més apropiada.

Implementa també una classe Programa per a fer algunes proves: Instància diversos vehicles de tota mena (cotxes, motos, vaixells, submarins, avions i helicòpters) així com vehicles genèrics (terrestres, aquàtics i aeris). Crea un llistat i afig tots els vehicles. Recorre el llistat i crida al mètode imprimir de tots els vehicles.

## Exercici 7 - Figures

Implementa una **interfície** anomenada **iFigura2D** que declare els mètodes:

- double perimetre(): Per a retornar el perímetre de la figura
- double area(): Per a retornar l'àrea de la figura
- void escalar(double escala): Per a escalar la figura (augmentar o disminuir la seua grandària). Només cal multiplicar els atributs de la figura per l'escala (> 0).
- void imprimir(): Per a mostrar la informació de la figura (atributs, perímetre i àrea) en una sola línia.

Existeixen 4 tipus de figures.

- **Quadrat**: Els seus quatre costats són iguals.
- **Rectangle**: Tenen ample i alt.
- **Triangle**: Tenen ample i alt.
- **Cercle**: Tenen radi.

Crea les 4 classes de figures de manera que implementen la interfície iFigura2D. Defineix els seus mètodes.

Crea una classe ProgramaFiguras en la qual realitzar les següents proves:

1. Crea un llistat de figures.
2. Afig figures de diversos tipus.
3. Mostra la informació de totes les figures.
4. Escala totes les figures amb escala = 2.
5. Mostra de nou la informació de totes les figures.
6. Escala totes les figures amb escala = 0.1.
7. Mostra de nou la informació de totes les figures.

## Exercici 8 - Cas pràctic DawBank

L'empresa <i>LibreCoders</i> us ha contractat per desenvolupar un programari de gestió d'un compte bancari per a la cooperativa de banca ètica i sostenible DawBank. Es tracta d'una aplicació formada per una classe principal DawBank i una altra anomenada CompteBancari.

El programa demanarà les dades necessàries per crear un compte bancari. Si són vàlids, crearà el compte i mostrarà el menú principal per permetre actuar sobre el compte. Després de cada acció es tornarà a mostrar el menú.

1. **Dades del compte**. Mostrarà l'IBAN, el titular i el saldo.
2. **IBAN**. Mostrarà l'IBAN.
3. **Titular**. Mostrarà el titular.
4. **Saldo**. Mostrarà el saldo disponible.
5. **Ingrés**. Demanarà la quantitat a ingressar i realitzarà l'ingrés si és possible.
6. **Retirada**. Demanarà la quantitat a retirar i realitzarà la retirada si és possible.
7. **Moviments**. Mostrarà una llistat amb l'historial de moviments.
8. **Eixir**. Finalitza el programa.

**Classe CompteBancari**  
Un compte bancari té com a dades associades l'IBAN (International Bank Account Number, format per dues lletres i 22 números, per exemple ES6621000418401234567891), el titular (un nom complet), el saldo (diners en euros) i els moviments (històric dels moviments realitzats al compte, un màxim de 100(*) per simplificar).

Quan es cree un compte és obligatori que tinga un IBAN i un titular (que no podran canviar mai). El saldo serà de 0 euros i el compte no tindrà moviments associats.

El saldo només pot variar quan es produeix un ingrés (entra diners al compte) o una retirada (ix diners del compte). En tots dos casos s'haurà de registrar l'operació als moviments. Els ingressos i les retirades només poden ser de valors superiors a zero.

El saldo d'un compte mai no podrà ser inferior a -50(\*) euros. Si es produeix un moviment que deixe el compte amb un saldo negatiu (no inferior a -50) caldrà mostrar el missatge "AVÍS: Saldo negatiu". Si es produeix un moviment superior a 3.000(\*) euros, es mostrarà el missatge "AVÍS: Notificar a hisenda".

No es realitzarà cap mena d'entrada per teclat. L'única eixida per pantalla permesa són els dos missatges d'avís esmentats a dalt, cap altra.

(\*)Aquests valors no poden variar i són iguals per a tots els comptes bancaris.

**Classe DawBank**  
Classe principal amb funció main. Encarregada d'interactuar amb l'usuari, mostrar el menú principal, donar feedback i/o missatges d'error, etc. Utilitzarà la classe CompteBancari. Podeu implementar les funcions que considereu oportunes.

-->