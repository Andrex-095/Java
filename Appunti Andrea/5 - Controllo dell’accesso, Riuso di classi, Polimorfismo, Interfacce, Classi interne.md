
_**INDICE**_ :
- [[#Interfaccia]]
- [[#Eredità]]
- [[#Metodi di Override e occultamento]]
- [[#Polimorfismo]]
- [[#Oggetto come Superclasse]]

# Interfaccia 

Un'interfaccia **in Java** è un modello di una classe. Ha costanti statiche e metodi astratti.

L'interfaccia in Java è _un meccanismo per ottenere l'_astrazione_ . Possono esserci solo metodi astratti nell'interfaccia Java, non il corpo del metodo. Viene utilizzata per ottenere l'astrazione e l'_ereditarietà_ multipla in Java .

In altre parole, puoi dire che le interfacce possono avere metodi e variabili astratti. Non possono avere un corpo di metodo.

>[!important] _Definizione JavaSun_
>Nel linguaggio di programmazione Java, _un'interfaccia_ è un tipo di riferimento, simile a una classe, che può contenere _solo_ costanti, firme di metodo, metodi predefiniti, metodi statici e tipi annidati. I corpi dei metodi esistono solo per i metodi predefiniti e i metodi statici. Le interfacce non possono essere istanziate, possono essere _implementate_ solo da classi o _estese_ da altre interfacce.

### Motivi perché utilizzare l'interfaccia

- Viene utilizzato per ottenere astrazione;
- Tramite l'interfaccia, possiamo supportare la funzionalità dell'eredità multipla. 
- Può essere utilizzato per ottenere un accoppiamento allentato. 

### Come dichiarare un'interfaccia

Un'interfaccia viene dichiarata usando la parola chiave **interface**. Fornisce un'astrazione totale, significa che tutti i metodi in un'interfaccia vengono dichiarati con il corpo vuoto e tutti i campi sono pubblici, statici e finali per impostazione predefinita. Una classe che implementa un'interfaccia deve implementare tutti i metodi dichiarati nell'interfaccia.


### Com'è definita un'interfaccia

```Java
public interface GroupedInterface extends Interface1, Interface2, Interface3 {

    // constant declarations
    
    // base of natural logarithms
    double E = 2.718282;
 
    // method signatures
    void doSomething (int i, double x);
    int doSomethingElse(String s);
}
```

Lo specificatore di accesso _public_ indica che l'interfaccia può essere utilizzata da qualsiasi classe in qualsiasi pacchetto. Se non viene è accessibile solo alle classi definite nello stesso pacchetto dell'interfaccia. 


## Implementazione di un'interfaccia

>[!important] Definizione
Per dichiarare una classe che implementa un'interfaccia, includi una clausola `implements` nella dichiarazione della classe. La tua classe può implementare più di un'interfaccia, quindi la parola chiave `implements` è seguita da un elenco separato da virgole delle interfacce implementate dalla classe. Per convenzione, la clausola `implements` segue la clausola `extends`, se ce n'è una.

Consideriamo un'interfaccia che definisce come confrontare le dimensioni degli oggetti
```Java
public interface Relatable {
        
    // this (object calling isLargerThan)
    // and other must be instances of 
    // the same class returns 1, 0, -1 
    // if this is greater than, 
    // equal to, or less than other
    public int isLargerThan(Relatable other);
}
```
Qualsiasi classe può implementare `Relatable`se c'è un modo per confrontare la "dimensione" relativa degli oggetti istanziati dalla classe. Per le stringhe, potrebbe essere il numero di caratteri; per i libri, potrebbe essere il numero di pagine; per gli studenti, potrebbe essere il peso; e così via. Per gli oggetti geometrici planari, l'area sarebbe una buona scelta (vedere la classe `RectanglePlus` che segue), mentre il volume funzionerebbe per gli oggetti geometrici tridimensionali. Tutte queste classi possono implementare il metodo `isLargerThan()`.

Esempio implementazione interfaccia Retable:
```Java
public class RectanglePlus implements Relatable {
	
	public int width = 0;
	public int height = 0;
	public Point origin;

    // four constructors
    public RectanglePlus() {
        origin = new Point(0, 0);
    }
    public RectanglePlus(Point p) {
        origin = p;
    }
    public RectanglePlus(int w, int h) {
        origin = new Point(0, 0);
        width = w;
        height = h;
    }
    public RectanglePlus(Point p, int w, int h) {
        origin = p;
        width = w;
        height = h;
    }

    // a method for moving the rectangle
    public void move(int x, int y) {
        origin.x = x;
        origin.y = y;
    }

    // a method for computing
    // the area of the rectangle
    public int getArea() {
        return width * height;
    }
    
    // a method required to implement
    // the Relatable interface
    public int isLargerThan(Relatable other) {
        RectanglePlus otherRect = (RectanglePlus)other;
        if (this.getArea() < otherRect.getArea())
            return -1;
        else if (this.getArea() > otherRect.getArea())
            return 1;
        else
            return 0;               
    }
}
```


### Utilizzo interfaccia come tipo 

Quando si definisce una nuova interfaccia, si definisce un nuovo tipo di dati di riferimento. È possibile utilizzare nomi di interfaccia ovunque sia possibile utilizzare qualsiasi altro nome di tipo di dati. Se si definisce una variabile di riferimento il cui tipo è un'interfaccia, qualsiasi oggetto assegnato ad essa _deve_ essere un'istanza di una classe che implementa l'interfaccia.

A titolo di esempio, ecco un metodo per trovare l'oggetto più grande in una coppia di oggetti, per _tutti_ gli oggetti istanziati da una classe che implementa `Relatable`:
```Java
public Object findLargest(Object object1, Object object2) {
   Relatable obj1 = (Relatable)object1;
   Relatable obj2 = (Relatable)object2;
   if ((obj1).isLargerThan(obj2) > 0)
      return object1;
   else 
      return object2;
}
```

### Interfacce in evoluzione

Se si vuole modificare un'interfaccia, aggiungendo ad esempio un metodo in più si può fare così
```Java
public interface DoItPlus extends DoIt {

   boolean didItWork(int i, double x, String s);
   
}
```



# Eredità

Le classi possono essere derivate da altre classi, ereditando così campi e metodi da quelle classi. 

>[!important] Definizione 
>Una classe derivata da un'altra classe è chiamata _sottoclasse_. Mentre la classe da cui deriva è detta _superclasse_. 
>In assenza di qualsiasi altra superclasse esplicita, ogni classe è implicitamente una sottoclasse di Object.
>

Nella piattaforma Java, molte classi derivano direttamente da `Object`, altre classi derivano da alcune di quelle classi e così via, formando una gerarchia di classi.

Esempio di Eredità:
```Java
public class Bicycle {
        
    // **the Bicycle class has three _fields_**
    public int cadence;
    public int gear;
    public int speed;
        
    // **the Bicycle class has one _constructor_**
    public Bicycle(int startCadence, int startSpeed, int startGear) {
        gear = startGear;
        cadence = startCadence;
        speed = startSpeed;
    }
        
    // **the Bicycle class has four _methods_**
    public void setCadence(int newValue) {
        cadence = newValue;
    }
        
    public void setGear(int newValue) {
        gear = newValue;
    }
        
    public void applyBrake(int decrement) {
        speed -= decrement;
    }
        
    public void speedUp(int increment) {
        speed += increment;
    }
        
}
```

Una dichiarazione di classe per una _MountainBike_ che è una sottoclasse di _Bicycle_ potrebbe apparire così:
```Java
public class MountainBike extends Bicycle {
        
    // **the MountainBike subclass adds one _field_**
    public int seatHeight;

    // **the MountainBike subclass has one _constructor_**
    public MountainBike(int startHeight,
                        int startCadence,
                        int startSpeed,
                        int startGear) {
        super(startCadence, startSpeed, startGear);
        seatHeight = startHeight;
    }   
        
    // **the MountainBike subclass adds one _method_**
    public void setHeight(int newValue) {
        seatHeight = newValue;
    }   
}
```
Questa classe eredita tutti i campi e i metodi di Bicycle e aggiunge il campo _seatHeight_ e un metodo per impostarlo. È come se avesse scritto una nuova classe da zero. 

## Cosa puoi fare in una sottoclasse

Una sottoclasse eredita tutti i membri _pubblici_ e _protetti_ del suo genitore, indipendentemente dal pacchetto in cui si trova la sottoclasse. Se la sottoclasse è nello stesso pacchetto del suo genitore, eredita anche i membri _privati ​​del pacchetto_ del genitore. Puoi usare i membri ereditati così come sono, sostituirli, nasconderli o integrarli con nuovi membri:

- I campi ereditati possono essere utilizzati direttamente, proprio come qualsiasi altro campo.
- È possibile dichiarare un campo nella sottoclasse con lo stesso nome di quello nella superclasse, _nascondendolo_ così (sconsigliato).
- È possibile dichiarare nuovi campi nella sottoclasse che non sono presenti nella superclasse.
- I metodi ereditati possono essere utilizzati direttamente così come sono.
- È possibile scrivere un nuovo metodo _istanza_ nella sottoclasse che abbia la stessa firma di quello nella superclasse, _sovrascrivendolo_ .
- È possibile scrivere un nuovo metodo _statico_ nella sottoclasse che abbia la stessa firma di quello nella superclasse, _nascondendolo_ così .
- È possibile dichiarare nuovi metodi nella sottoclasse che non sono presenti nella superclasse.
- È possibile scrivere un costruttore di sottoclasse che invochi il costruttore della superclasse, in modo implicito oppure utilizzando la parola chiave `super`.

## Eredità multipla di stato, implementazione e tipo 

Una differenza significativa tra classi e interfacce è che le classi possono avere campi mentre le interfacce no. Inoltre, puoi istanziare una classe per creare un oggetto, cosa che non puoi fare con le interfacce. Un oggetto memorizza il suo stato in campi, che sono definiti nelle classi. Uno dei motivi per cui il linguaggio di programmazione Java non ti consente di estendere più di una classe è per evitare i problemi di _ereditarietà multipla dello stato_ , che è la capacità di ereditare campi da più classi. Ad esempio, supponi di essere in grado di definire una nuova classe che estende più classi. Quando crei un oggetto istanziando quella classe, quell'oggetto erediterà i campi da tutte le superclassi della classe. Cosa succede se metodi o costruttori di diverse superclassi istanziano lo stesso campo? Quale metodo o costruttore avrà la precedenza? Poiché le interfacce non contengono campi, non devi preoccuparti dei problemi che derivano dall'ereditarietà multipla dello stato.

_L'ereditarietà multipla dell'implementazione_ è la capacità di ereditare definizioni di metodi da più classi. Con questo tipo di ereditarietà multipla sorgono problemi, come conflitti di nomi e ambiguità. Quando i compilatori di linguaggi di programmazione che supportano questo tipo di ereditarietà multipla incontrano superclassi che contengono metodi con lo stesso nome, a volte non riescono a determinare a quale membro o metodo accedere o invocare. Inoltre, un programmatore può inconsapevolmente introdurre un conflitto di nomi aggiungendo un nuovo metodo a una superclasse. I metodi predefiniti introducono una forma di ereditarietà multipla dell'implementazione. Una classe può implementare più di un'interfaccia, che può contenere metodi predefiniti con lo stesso nome. Il compilatore Java fornisce alcune regole per determinare quale metodo predefinito utilizza una particolare classe.

# Metodi di Override e occultamento 

## Metodi di Istanza

Un metodo di istanza in una sottoclasse con la stessa firma (nome, più il numero e il tipo dei suoi parametri) e lo stesso tipo di ritorno di un metodo di istanza nella superclasse _sovrascrive_ il metodo della superclasse.

La capacità di una sottoclasse di sovrascrivere un metodo consente a una classe di ereditare da una superclasse il cui comportamento è "abbastanza simile" e quindi di modificare il comportamento in base alle necessità. Il metodo di sovrascrittura ha lo stesso nome, numero e tipo di parametri e tipo di ritorno del metodo che sovrascrive. Un metodo di sovrascrittura può anche restituire un sottotipo del tipo restituito dal metodo sovrascritto. Questo sottotipo è chiamato _tipo di ritorno covariante .

Quando si sovrascrive un metodo, si potrebbe voler usare l'annotazione `@Override` che indica al compilatore che si intende sovrascrivere un metodo nella superclasse. Se, per qualche motivo, il compilatore rileva che il metodo non esiste in una delle superclassi, genererà un errore. 

## Metodi statici

Se una sottoclasse definisce un metodo statico con la stessa firma di un metodo statico nella superclasse, allora il metodo nella sottoclasse _nasconde_ quello nella superclasse.

La distinzione tra nascondere un metodo statico e sovrascrivere un metodo istanza ha implicazioni importanti:

- La versione del metodo di istanza sovrascritto che viene richiamata è quella presente nella sottoclasse.
- La versione del metodo statico nascosto che viene richiamata dipende dal fatto che venga richiamata dalla superclasse o dalla sottoclasse.

**Esempio**, due classi, una _Animal_ che contiene un metodo di istanza e un metodo statico:
```java
public class Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Animal");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Animal");
    }
}
```
La seconda classe è una sottoclasse di Animal, chiamata _Cat_:
```java
public class Cat extends Animal {
    public static void testClassMethod() {
        System.out.println("The static method in Cat");
    }
    public void testInstanceMethod() {
        System.out.println("The instance method in Cat");
    }

    public static void main(String[] args) {
        Cat myCat = new Cat();
        Animal myAnimal = myCat;
        Animal.testClassMethod();
        myAnimal.testInstanceMethod();
    }
}
```

La classe Cat sovrascrive il metodo istanza in Animal e nasconde il metodo statico in Animal. Il metodo main in questa classe crea un'istanza di Cat e invoca `testClassMethod()`sulla classe e `testIstanceMethod()` sull'istanza
L'output sarà:
```Java
Il metodo statico in Animal
Il metodo istanza in Cat
```


# Polimorfismo 

>[!important] Definizione:
>Si riferisce a un principio in biologia in cui un organismo o una specie può avere molte forme o stadi diversi.  
>Questo principio può essere applicato anche alla programmazione orientata agli oggetti e a linguaggi come il linguaggio Java. Le sottoclassi di una classe possono definire i propri comportamenti unici e tuttavia condividere alcune delle stesse funzionalità della classe padre.

Il polimorfismo può essere dimostrato con una piccola modifica alla classe `Bicycle`. Ad esempio, si potrebbe aggiungere un metodo `printDescription` alla classe che visualizza tutti i dati attualmente memorizzati in un'istanza.

```Java
public void printDescription(){
    System.out.println("\nBike is " + "in gear " + this.gear
        + " with a cadence of " + this.cadence +
        " and travelling at a speed of " + this.speed + ". ");
}
```

Per dimostrare le caratteristiche polimorfiche nel linguaggio Java, estendi la classe `Bicycle` con `MountainBike`e a `RoadBike`. Per `MountainBike`, aggiungi un campo  `suspension`, che è un valore `String` che indica se la bici ha un ammortizzatore anteriore, `Front`. Oppure, la bici ha un ammortizzatore anteriore e posteriore, `Dual`. 
Ecco la classe aggiornata:
```Java
public class MountainBike extends Bicycle {
    
    private String suspension;

    public MountainBike(
               int startCadence,
               int startSpeed,
               int startGear,
               String suspensionType){
        super(startCadence,
              startSpeed,
              startGear);
        this.setSuspension(suspensionType);
    }

    public String getSuspension(){
      return this.suspension;
    }

    public void setSuspension(String suspensionType) {
        this.suspension = suspensionType;
    }

    public void printDescription() {
        super.printDescription();
        System.out.println("The " + "MountainBike has a" +
            getSuspension() + " suspension.");
    }
}
```

Poi, crea la classe `RoadBike`. Poiché le bici da strada o da corsa hanno pneumatici sottili, aggiungi un attributo per tracciare la larghezza del pneumatico. Ecco la classe `RoadBike`:
```Java
public class RoadBike extends Bicycle{
    // In millimeters (mm)
    private int tireWidth;

    public RoadBike(int startCadence,
                    int startSpeed,
                    int startGear,
                    int newTireWidth){
        super(startCadence,
              startSpeed,
              startGear);
        this.setTireWidth(newTireWidth);
    }

    public int getTireWidth(){
      return this.tireWidth;
    }

    public void setTireWidth(int newTireWidth){
        this.tireWidth = newTireWidth;
    }

    public void printDescription(){
        super.printDescription();
        System.out.println("The RoadBike" + " has " + getTireWidth() +
            " MM tires.");
    }
}
```

Per riassumere, ci sono tre classi: `Bicycle`, `MountainBike`, e `RoadBike`. Le due sottoclassi sovrascrivono il metodo `printDescription` e stampano informazioni univoche.

Ecco un programma di test che crea tre variabili `Bicycle`. Ogni variabile è assegnata a una delle tre classi di biciclette. Ogni variabile viene quindi stampata.
```java
public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03;

    bike01 = new Bicycle(20, 10, 1);
    bike02 = new MountainBike(20, 10, 5, "Dual");
    bike03 = new RoadBike(40, 20, 8, 23);

    bike01.printDescription();
    bike02.printDescription();
    bike03.printDescription();
  }
}

//Output 
Bike is in gear 1 with a cadence of 20 and travelling at a speed of 10. 

Bike is in gear 5 with a cadence of 20 and travelling at a speed of 10. 
The MountainBike has a Dual suspension.

Bike is in gear 8 with a cadence of 40 and travelling at a speed of 20. 
The RoadBike has 23 MM tires.
```


## Nascondere i campi 

All'interno di una classe, un campo che ha lo stesso nome di un campo nella superclasse nasconde il campo della superclasse, anche se i loro tipi sono diversi. All'interno della sottoclasse, il campo nella superclasse non può essere referenziato tramite il suo semplice nome. Invece, il campo deve essere accessibile tramite `super`, che è trattato nella prossima sezione. In generale, non consigliamo di nascondere i campi poiché rende il codice difficile da leggere.


## Parola chiave Super

### Accesso ai membri della superclasse

Se il tuo metodo sovrascrive uno dei metodi della sua superclasse, puoi invocare il metodo sovrascritto tramite l'uso della parola chiave `super`. Puoi anche usare `super`per fare riferimento a un campo nascosto (anche se nascondere i campi è sconsigliato). Considera questa classe, `Superclass`:
```Java
public class Superclass {

    public void printMethod() {
        System.out.println("Printed in Superclass.");
    }
}
```
Ora una sottoclasse chiamata Sottoclasse, che sovrascrive `printMethod()`:
```Java
public class Subclass extends Superclass {

    // overrides printMethod in Superclass
    public void printMethod() {
        super.printMethod();
        System.out.println("Printed in Subclass");
    }
    public static void main(String[] args) {
        Subclass s = new Subclass();
        s.printMethod();    
    }
}
```


Con `super()`, viene chiamato il costruttore superclasse senza argomenti. Con `super(parameter list)`, viene chiamato il costruttore superclasse con un elenco di parametri corrispondente.

# Oggetto come Superclasse

## Metodo clone()

Se una classe, o una delle sue superclassi, implementa l'interfaccia  `Cloneable`, puoi usare il metodo`clone()` per creare una copia da un oggetto esistente. 
Per creare un clone, scrivi:
```Java
aCloneableObject();
```
L'implementazione di questo metodo  `Object`verifica se l'oggetto su cui `clone()`è stato invocato implementa l'interfaccia `Cloneable`. Se l'oggetto non lo fa, il metodo genera un'eccezione `CloneNotSupportedException`. La gestione delle eccezioni sarà trattata in una lezione successiva. Per il momento, devi sapere che `clone()`deve essere dichiarato come:
```Java
protected Object clone() throws CloneNotSupportedException

or:

public Object clone() throws CloneNotSupportedException
```


## Metodo equals()

Il metodo `equals()` confronta due oggetti per verificarne l'uguaglianza e restituisce `true`se sono uguali. Il metodo `equals()` fornito nella classe `Object` utilizza l'operatore di identità ( `==`) per determinare se due oggetti sono uguali. Per i tipi di dati primitivi, questo fornisce il risultato corretto. Per gli oggetti, tuttavia, non lo fa. Il metodo `equals()` fornito da `Object`verifica se i _riferimenti_ agli oggetti sono uguali, ovvero se gli oggetti confrontati sono esattamente lo stesso oggetto.

Per verificare se due oggetti sono uguali nel senso di _equivalenza_ (contenendo le stesse informazioni), è necessario sovrascrivere il metodo `equals()`. Ecco un esempio di una classe `Book` che sovrascrive `equals()`:
```Java
public class Book {
    String ISBN;
    
    public String getISBN() { 
        return ISBN;
    }
    
    public boolean equals(Object obj) {
        if (obj instanceof Book)
            return ISBN.equals((Book)obj.getISBN()); 
        else
            return false;
    }
}
```

Consideriamo questo codice che verifica l'uguaglianza di due istanze della classe `Book`:
```Java
// Tutorial Swing, 2a edizione 
Libro firstBook = new Book("0201914670"); 
Libro secondBook = new Book("0201914670"); 
if (firstBook.equals(secondBook)) { 
	System.out.println("gli oggetti sono uguali"); 
} else { 
	System.out.println("gli oggetti non sono uguali"); 
}
```


## Metodo finalize()

La classe `Object` fornisce un metodo di callback, `finalize()`, che _può essere_ richiamato su un oggetto quando diventa spazzatura. L'implementazione `Object` di `finalize()`non fa nulla: è possibile eseguire l'override `finalize()`per eseguire la pulizia, ad esempio liberando risorse.

## Metodo getClass()

Il metodo `getClass()` restituisce un oggetto `Class`, che ha metodi che puoi usare per ottenere informazioni sulla classe, come il suo nome ( `getSimpleName()`), la sua superclasse ( `getSuperclass()`) e le interfacce che implementa ( `getInterfaces()`). Ad esempio, il seguente metodo ottiene e visualizza il nome della classe di un oggetto:
```Java
void printClassName(Object obj) {
    System.out.println("The object's" + " class is " +
        obj.getClass().getSimpleName());
}
```

La classe `Class`, nel pacchetto `java.lang`, ha un gran numero di metodi (più di 50). Ad esempio, puoi testare per vedere se la classe è un'annotazione ( `isAnnotation()`), un'interfaccia ( `isInterface()`), o un'enumerazione ( `isEnum()`). Puoi vedere quali sono i campi dell'oggetto ( `getFields()`) o quali sono i suoi metodi ( `getMethods()`), e così via.

## Metodo hasCode()

Il valore restituito `hashCode()`è il codice hash dell'oggetto, ovvero un valore intero generato da un algoritmo di hashing.

Per definizione, se due oggetti sono uguali, _anche il loro codice hash deve_ essere uguale. Se si sovrascrive il metodo `equals()`, si modifica il modo in cui due oggetti vengono equiparati e l'implementazione  `Object`di `hashCode()`non è più valida. Pertanto, se si sovrascrive il  metodo `equals()`, è necessario anche sovrascrivere il metodo `hashCode()`.

## Metodo toString()

Il metodo `Object`'s `toString()`restituisce una rappresentazione dell'oggetto `String`, molto utile per il debug. La rappresentazione di un oggetto `String` dipende interamente dall'oggetto, motivo per cui è necessario eseguire l'override `toString()`nelle classi.

È possibile utilizzare `toString()`insieme `System.out.println()`per visualizzare una rappresentazione testuale di un oggetto. 


## Scrittura di classi e metodi finali 

Puoi dichiarare alcuni o tutti i metodi di una classe _final_ . Utilizzi la parola chiave  `final`in una dichiarazione di metodo per indicare che il metodo non può essere sovrascritto dalle sottoclassi. La classe `Object` fa questo: alcuni dei suoi metodi sono `final`.

Potresti voler rendere un metodo final se ha un'implementazione che non dovrebbe essere modificata ed è fondamentale per lo stato coerente dell'oggetto. Ad esempio, potresti voler rendere final il metodo `getFirstPlayer` in questa classe `ChessAlgorithm`:
```Java
class ChessAlgorithm {
    enum ChessPlayer { WHITE, BLACK }
    ...
    final ChessPlayer getFirstPlayer() {
        return ChessPlayer.WHITE;
    }
    ...
}
```
I metodi chiamati dai costruttori dovrebbero essere generalmente dichiarati final. Se un costruttore chiama un metodo non final, una sottoclasse potrebbe ridefinire quel metodo con risultati sorprendenti o indesiderati.

Nota che puoi anche dichiarare un'intera classe final. Una classe dichiarata final non può essere sottoclassata. Ciò è particolarmente utile, ad esempio, quando si crea una classe immutabile come la classe `String`.

## Metodi e classi astratte

Una _classe astratta_ è una classe dichiarata `abstract`, che può includere o meno metodi astratti. Le classi astratte non possono essere istanziate, ma possono essere sottoclassate.

Un _metodo astratto_ è un metodo dichiarato senza implementazione (senza parentesi graffe e seguito da punto e virgola), in questo modo:
```Java
abstract void moveTo(double deltaX, double deltaY);
```

Se una classe include metodi astratti, allora la classe stessa _deve_ essere dichiarata `abstract`, come in:
```java
public abstract class GraphicObject {
   // declare fields
   // declare nonabstract methods
   abstract void draw();
}
```

Quando una classe astratta viene sottoclassata, la sottoclasse solitamente fornisce implementazioni per tutti i metodi astratti nella sua classe padre. Tuttavia, se non lo fa, allora anche la sottoclasse deve essere dichiarata `abstract`.

### Classi astratte rispetto alle interfacce

Le classi astratte sono simili alle interfacce. Non puoi istanziarle e possono contenere un mix di metodi dichiarati con o senza un'implementazione. Tuttavia, con le classi astratte, puoi dichiarare campi che non sono statici e finali e definire metodi concreti pubblici, protetti e privati. Con le interfacce, tutti i campi sono automaticamente pubblici, statici e finali e tutti i metodi che dichiari o definisci (come metodi predefiniti) sono pubblici. Inoltre, puoi estendere solo una classe, indipendentemente dal fatto che sia astratta o meno, mentre puoi implementare un numero qualsiasi di interfacce.

Cosa dovresti usare, classi astratte o interfacce?

- Prendi in considerazione l'utilizzo di classi astratte se una qualsiasi di queste affermazioni si applica alla tua situazione:
    - Si desidera condividere il codice tra diverse classi strettamente correlate.
    - Ci si aspetta che le classi che estendono la classe astratta abbiano molti metodi o campi in comune, oppure che richiedano modificatori di accesso diversi da public (ad esempio protected e private).
    - Vuoi dichiarare campi non statici o non finali. Ciò ti consente di definire metodi che possono accedere e modificare lo stato dell'oggetto a cui appartengono.
- Prendi in considerazione l'utilizzo delle interfacce se una di queste affermazioni si applica alla tua situazione:
    - Ti aspetti che classi non correlate implementino la tua interfaccia. Ad esempio, le interfacce `Comparable`e `Cloneable` sono implementate da molte classi non correlate.
    - Si desidera specificare il comportamento di un particolare tipo di dati, ma non ci si preoccupa di chi ne implementa il comportamento.
    - Si desidera sfruttare i vantaggi dell'ereditarietà multipla del tipo.

#### Esempio di classe astratta

Per prima cosa, dichiari una classe astratta, `GraphicObject`, per fornire variabili membro e metodi che sono completamente condivisi da tutte le sottoclassi, come la posizione corrente e il metodo `moveTo`. `GraphicObject`dichiara anche metodi astratti per metodi, come `draw`o `resize`, che devono essere implementati da tutte le sottoclassi ma devono essere implementati in modi diversi. La classe `GraphicObject` può apparire più o meno così:
```Java
abstract class GraphicObject {
    int x, y;
    ...
    void moveTo(int newX, int newY) {
        ...
    }
    abstract void draw();
    abstract void resize();
}
```
Ogni sottoclasse non astratta di `GraphicObject`, come `Circle`e `Rectangle`, deve fornire implementazioni per i metodi `draw`e `resize`:
```Java
class Circle extends GraphicObject {
    void draw() {
        ...
    }
    void resize() {
        ...
    }
}
class Rectangle extends GraphicObject {
    void draw() {
        ...
    }
    void resize() {
        ...
    }
}
```

#### Quando una classe astratta implementa un'interfaccia

Nella sezione su `Interfaces`, è stato notato che una classe che implementa un'interfaccia deve implementare _tutti_ i metodi dell'interfaccia. È possibile, tuttavia, definire una classe che non implementa tutti i metodi dell'interfaccia, a condizione che la classe sia dichiarata come `abstract`. Ad esempio,
```Java
abstract class X implements Y {
  // implements all but one method of Y
}

class XX extends X {
  // implements the remaining method in Y
}
```
In questo caso, la classe `X`deve essere `abstract`perché non implementa completamente `Y`, ma la classe `XX`, di fatto, implementa `Y`.