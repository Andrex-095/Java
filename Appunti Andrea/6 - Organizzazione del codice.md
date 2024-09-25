
# _**INDICE**_

- [[#Proprietà]]
- [[#Variabili d'ambiente]]
- [[#Pacchetti]]
	- [[#Creazione di un pacchetto]]
	- [[#Denominazione del pacchetto]]
		- [[#Convenzione di denominazione]]
	- [[#Utilizzo dei membri del pacchetto]]
		- [[#Riferimento a un membro del pacchetto tramite il suo nome qualificato]]
		- [[#Importazione di un membro del pacchetto]]
		- [[#Importazione di un pacchetto intero]]
		- [[#Ambiguità del nome]]
		- [[#L'istruzione di importazione statica]]




# Proprietà

_Le proprietà_ sono valori di configurazione gestiti come _coppie chiave/valore_ . In ogni coppia, la chiave e il valore sono entrambi valori `String`. La chiave identifica e viene utilizzata per recuperare il valore, proprio come un nome di variabile viene utilizzato per recuperare il valore della variabile. Ad esempio, un'applicazione in grado di scaricare file potrebbe utilizzare una proprietà denominata "download.lastDirectory" per tenere traccia della directory utilizzata per l'ultimo download.

Per gestire le proprietà, crea istanze di [`java.util.Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html). Questa classe fornisce metodi per quanto segue:
- caricamento di coppie chiave/valore in un oggetto `Properties` da un flusso,
- recuperare un valore dalla sua chiave,
- elencando le chiavi e i loro valori,
- enumerando i tasti, e
- salvataggio delle proprietà in un flusso.

Per un'introduzione ai flussi, fare riferimento alla sezione Flussi di I/O nella lezione I/O di base.

`Properties`estende [`java.util.Hashtable`](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html). Alcuni dei metodi ereditati da `Hashtable`supportano le seguenti azioni:
- testare se una particolare chiave o valore è presente nell'oggetto `Properties`,
- ottenere il numero corrente di coppie chiave/valore,
- rimuovendo una chiave e il suo valore,
- aggiungendo una coppia chiave/valore all'elenco `Properties`,
- enumerando i valori o le chiavi,
- recuperare un valore tramite la sua chiave, e
- scoprire se l'oggetto `Properties` è vuoto.


# Argomenti della riga di comando 

Un'applicazione Java può accettare qualsiasi numero di argomenti dalla riga di comando. Ciò consente all'utente di specificare informazioni di configurazione quando l'applicazione viene avviata.

L'utente immette argomenti della riga di comando quando richiama l'applicazione e li specifica dopo il nome della classe da eseguire. Ad esempio, supponiamo che un'applicazione Java chiamata `Sort`ordina le righe in un file. Per ordinare i dati in un file denominato `friends.txt`, un utente dovrebbe immettere: `java Sort friends.txt`

Quando un'applicazione viene avviata, il sistema runtime passa gli argomenti della riga di comando al metodo principale dell'applicazione tramite un array di `String`. Nell'esempio precedente, gli argomenti della riga di comando sono passati all'applicazione in un array  `Sort` che contiene un singolo `String`: `"friends.txt"`.

# Variabili d'ambiente

Molti sistemi operativi utilizzano _variabili di ambiente_ per passare informazioni di configurazione alle applicazioni. Come le proprietà nella piattaforma Java, le variabili di ambiente sono coppie chiave/valore, dove sia la chiave che il valore sono stringhe. Le convenzioni per l'impostazione e l'utilizzo delle variabili di ambiente variano tra i sistemi operativi e anche tra gli interpreti della riga di comando. Per imparare come passare le variabili di ambiente alle applicazioni sul tuo sistema, fai riferimento alla documentazione del tuo sistema.

## Interrogazione delle variabili di ambiente

Sulla piattaforma Java, un'applicazione usa `System.getenv`per recuperare i valori delle variabili di ambiente. Senza un argomento, `getenv` restituisce un'istanza di sola lettura di `java.util.Map`, dove le chiavi della mappa sono i nomi delle variabili di ambiente e i valori della mappa sono i valori delle variabili di ambiente. Ciò è dimostrato nell'esempio `EnvMap` :
```Java
import java.util.Map;

public class EnvMap {
    public static void main (String[] args) {
        Map<String, String> env = System.getenv();
        for (String envName : env.keySet()) {
            System.out.format("%s=%s%n",
                              envName,
                              env.get(envName));
        }
    }
}
```

Con un argomento `String`, `getenv` restituisce il valore della variabile specificata. Se la variabile non è definita, `getenv`restituisce `null`. L'esempio  `Env` usa `getenv` questo modo per interrogare variabili di ambiente specifiche, specificate sulla riga di comando:
```Java
public class Env {
    public static void main (String[] args) {
        for (String env: args) {
            String value = System.getenv(env);
            if (value != null) {
                System.out.format("%s=%s%n",
                                  env, value);
            } else {
                System.out.format("%s is"
                    + " not assigned.%n", env);
            }
        }
    }
}
```


# Pacchetti

Viene spiegato come raggruppare classi e interfacce in pacchetti, come utilizzare le classi presenti nei pacchetti e come organizzare il file system in modo che il compilatore possa trovare i file sorgente.

Per rendere i tipi più facili da trovare e utilizzare, per evitare conflitti di denominazione e per controllare l'accesso, i programmatori raggruppano gruppi di tipi correlati in pacchetti.

>[!important] Definizione:  
>Un _pacchetto_ è un raggruppamento di tipi correlati che forniscono protezione di accesso e gestione dello spazio dei nomi. Nota che _i tipi_ si riferiscono a classi, interfacce, enumerazioni e tipi di annotazione. Le enumerazioni e i tipi di annotazione sono tipi speciali di classi e interfacce, rispettivamente, quindi _i tipi_ sono spesso indicati in questa lezione semplicemente come _classi e interfacce_.

I tipi che fanno parte della piattaforma Java sono membri di vari pacchetti che raggruppano classi per funzione: le classi fondamentali sono in `java.lang`, le classi per la lettura e la scrittura (input e output) sono in `java.io`, e così via. Puoi anche mettere i tuoi tipi in pacchetti.

Supponiamo di scrivere un gruppo di classi che rappresentano oggetti grafici, come cerchi, rettangoli, linee e punti. 
Scrivi anche un'interfaccia, `Draggable`, che le classi implementano se possono essere trascinate con il mouse.

```Java
//_in the Draggable.java file_
public interface Draggable {
    ...
}

//_in the Graphic.java file_
public abstract class Graphic {
    ...
}

//_in the Circle.java file_
public class Circle extends Graphic
    implements Draggable {
    . . .
}

//_in the Rectangle.java file_
public class Rectangle extends Graphic
    implements Draggable {
    . . .
}

//_in the Point.java file_
public class Point extends Graphic
    implements Draggable {
    . . .
}

//_in the Line.java file_
public class Line extends Graphic
    implements Draggable {
    . . .
}
```

È opportuno raggruppare queste classi e l'interfaccia in un pacchetto per diversi motivi, tra cui i seguenti:  

- Tu e altri programmatori potete facilmente stabilire che questi tipi sono correlati.
- Tu e gli altri programmatori sapete dove trovare i tipi che possono fornire funzioni correlate alla grafica.
- I nomi dei tipi non entreranno in conflitto con i nomi dei tipi presenti in altri pacchetti perché il pacchetto crea un nuovo spazio dei nomi.
- È possibile consentire ai tipi all'interno del pacchetto di avere accesso illimitato l'uno all'altro, limitando comunque l'accesso ai tipi esterni al pacchetto.

## Creazione di un pacchetto

Per creare un pacchetto, si sceglie un nome per il pacchetto (le convenzioni di denominazione sono illustrate nella prossima sezione) e si inserisce un'istruzione `package`con quel nome all'inizio di _ogni file sorgente_ che contiene i tipi (classi, interfacce, enumerazioni e tipi di annotazione) che si desidera includere nel pacchetto.

L'istruzione package (ad esempio, `package graphics;`) deve essere la prima riga nel file sorgente. Può esserci una sola istruzione package in ogni file sorgente e si applica a tutti i tipi nel file.

>[!important] Nota:  
>Se inserisci più tipi in un singolo file sorgente, solo uno può essere `public`, e deve avere lo stesso nome del file sorgente. Ad esempio, puoi definire `public class Circle` nel file `Circle.java`, definire `public interface Draggable` nel file `Draggable.java`, definire `public enum Day` nel file `Day.java`, e così via.  
> Puoi includere tipi non pubblici nello stesso file come tipo pubblico (ciò è fortemente sconsigliato, a meno che i tipi non pubblici non siano piccoli e strettamente correlati al tipo pubblico), ma solo il tipo pubblico sarà accessibile dall'esterno del pacchetto. Tutti i tipi non pubblici di livello superiore saranno _package private_ .
  
Se inserisci l'interfaccia grafica e le classi elencate nella sezione precedente in un pacchetto chiamato `graphics`, avrai bisogno di sei file sorgente, come questo:

```Java
//_in the Draggable.java file_
package graphics;
public interface Draggable {
    . . .
}

//_in the Graphic.java file_
package graphics;
public abstract class Graphic {
    . . .
}

//_in the Circle.java file_
package graphics;
public class Circle extends Graphic
    implements Draggable {
    . . .
}

//_in the Rectangle.java file_
package graphics;
public class Rectangle extends Graphic
    implements Draggable {
    . . .
}

//_in the Point.java file_
package graphics;
public class Point extends Graphic
    implements Draggable {
    . . .
}

//_in the Line.java file_
package graphics;
public class Line extends Graphic
    implements Draggable {
    . . .
}
```

Se non usi un'istruzione `package`, il tuo tipo finisce in un pacchetto senza nome. In generale, un pacchetto senza nome è solo per applicazioni piccole o temporanee o quando stai appena iniziando il processo di sviluppo. Altrimenti, classi e interfacce appartengono a pacchetti con nome.

## Denominazione del pacchetto 

Con programmatori in tutto il mondo che scrivono classi e interfacce usando il linguaggio di programmazione Java, è probabile che molti programmatori useranno lo stesso nome per tipi diversi. Infatti, l'esempio precedente fa proprio questo: definisce una classe `Rectangle` quando c'è già una classe `Rectangle` nel pacchetto `java.awt`. Tuttavia, il compilatore consente a entrambe le classi di avere lo stesso nome se sono in pacchetti diversi. Il nome completamente qualificato di ciascuna classe `Rectangle` include il nome del pacchetto. Vale a dire, il nome completamente qualificato della classe  `Rectangle` nel pacchetto `graphics` è `graphics.Rectangle`, e il nome completamente qualificato della classe `Rectangle` nel pacchetto `java.awt` è `java.awt.Rectangle`.

Questo funziona bene a meno che due programmatori indipendenti non usino lo stesso nome per i loro pacchetti. Cosa impedisce questo problema? Convenzione.

### Convenzione di denominazione

I nomi dei pacchetti sono scritti tutti in minuscolo per evitare conflitti con i nomi delle classi o delle interfacce.

Le aziende utilizzano il loro nome di dominio Internet invertito per iniziare i nomi dei loro pacchetti, ad esempio `com.example.mypackage` per un pacchetto denominato `mypackage`creato da un programmatore presso `example.com`.

I conflitti di nomi che si verificano all'interno di una singola azienda devono essere gestiti per convenzione all'interno dell'azienda stessa, ad esempio includendo il nome della regione o del progetto dopo il nome dell'azienda (ad esempio, `com.example.region.mypackage`).

I pacchetti nel linguaggio Java stesso iniziano con `java.`o`javax.`

In alcuni casi, il nome di dominio Internet potrebbe non essere un nome di pacchetto valido. Ciò può verificarsi se il nome di dominio contiene un trattino o un altro carattere speciale, se il nome del pacchetto inizia con una cifra o un altro carattere che è illegale utilizzare come inizio di un nome Java, o se il nome del pacchetto contiene una parola chiave Java riservata, come "int". In questo caso, la convenzione suggerita è di aggiungere un trattino basso. Ad esempio:![[Pasted image 20240917105823.png]]


## Utilizzo dei membri del pacchetto

I tipi che compongono un pacchetto sono noti come _membri del pacchetto_ .

Per utilizzare un membro `public` del pacchetto dall'esterno del suo pacchetto, è necessario effettuare una delle seguenti operazioni:
- Fare riferimento al membro con il suo nome completo qualificato
- Importa il membro del pacchetto
- Importa l'intero pacchetto del membro

Ognuno di essi è adatto a situazioni diverse, come spiegato nelle sezioni seguenti.

###  Riferimento a un membro del pacchetto tramite il suo nome qualificato

Finora, la maggior parte degli esempi in questo tutorial ha fatto riferimento ai tipi con i loro nomi semplici, come `Rectangle`e `StackOfInts`. Puoi usare il nome semplice di un membro del pacchetto se il codice che stai scrivendo è nello stesso pacchetto di quel membro o se quel membro è stato importato.

Tuttavia, se si sta tentando di utilizzare un membro da un pacchetto diverso e tale pacchetto non è stato importato, è necessario utilizzare il nome completo del membro, che include il nome del pacchetto. Ecco il nome completo della classe `Rectangle` dichiarata nel pacchetto `graphics` nell'esempio precedente.

`graphics.Rectangle`

È possibile utilizzare questo nome qualificato per creare un'istanza di `graphics.Rectangle`:

`graphics.Rectangle myRect = new graphics.Rectangle();`

I nomi qualificati vanno bene per un uso poco frequente. Quando un nome viene usato ripetutamente, tuttavia, digitare ripetutamente il nome diventa noioso e il codice diventa difficile da leggere. In alternativa, puoi _importare_ il membro o il suo pacchetto e quindi usare il suo nome semplice.

### Importazione di un membro del pacchetto

Per importare un membro specifico nel file corrente, inserisci un'istruzione `import`all'inizio del file prima di qualsiasi definizione di tipo ma dopo l'istruzione `package`, se ce n'è una. Ecco come importeresti la classe `Rectangle` dal pacchetto `graphics` creato nella sezione precedente.

`import graphics.Rectangle;`

Ora puoi fare riferimento alla classe `Rectangle` tramite il suo nome semplice.

`Rectangle myRectangle = new Rectangle();`

Questo approccio funziona bene se si usano solo pochi membri del pacchetto `graphics`. Ma se si usano molti tipi da un pacchetto, si dovrebbe importare l'intero pacchetto.

### Importazione di un pacchetto intero

Per importare tutti i tipi contenuti in un particolare pacchetto, utilizzare l'istruzione `import` con il `(*)`carattere jolly asterisco.

`import graphics.*;`

Ora è possibile fare riferimento a qualsiasi classe o interfaccia nel pacchetto `graphics` tramite il suo semplice nome.

`Circle myCircle = new Circle();`
`Rectangle myRectangle = new Rectangle();`

L'asterisco nell'istruzione `import`può essere utilizzato solo per specificare tutte le classi all'interno di un pacchetto, come mostrato qui. Non può essere utilizzato per abbinare un sottoinsieme delle classi in un pacchetto. Ad esempio, quanto segue non corrisponde a tutte le classi nel pacchetto `graphics` che iniziano con `A`.

>[!important] Nota:
>Un'altra forma meno comune di `import`consente di importare le classi nidificate pubbliche di una classe di chiusura. Ad esempio, se la classe `graphics.Rectangle` contenesse classi nidificate utili, come `Rectangle.DoubleWide`e `Rectangle.Square`, potresti importare `Rectangle`e le sue classi nidificate utilizzando le _due_ istruzioni seguenti.
>import graphics.Rectangle;
>import graphics.Rectangle.*;
>Siate consapevoli che la seconda istruzione import _non_ importerà `Rectangle`.  
  Un'altra forma meno comune di `import`, l' _istruzione import statica_ , sarà discussa alla fine di questa sezione.

### Ambiguità del nome

Se un membro in un pacchetto condivide il suo nome con un membro in un altro pacchetto ed entrambi i pacchetti sono importati, devi fare riferimento a ciascun membro tramite il suo nome qualificato. Ad esempio, il pacchetto `graphics` ha definito una classe denominata `Rectangle`. Il pacchetto `java.awt` contiene anche una classe `Rectangle`. Se entrambi `graphics`e `java.awt`sono stati importati, quanto segue è ambiguo.

`Rectangle rect;`

In una situazione del genere, devi usare il nome completo del membro per indicare esattamente quale classe `Rectangle` desideri. Ad esempio,

`graphics.Rectangle rect;`

### L'istruzione di importazione statica

Ci sono situazioni in cui hai bisogno di un accesso frequente ai campi finali statici (costanti) e ai metodi statici di una o due classi. Aggiungere ripetutamente un prefisso al nome di queste classi può causare codice disordinato. L' istruzione _static import_ ti offre un modo per importare le costanti e i metodi statici che vuoi usare in modo da non dover aggiungere un prefisso al nome della loro classe.

La classe `java.lang.Math` definisce la costante `PI` e molti metodi statici, inclusi metodi per calcolare seni, coseni, tangenti, radici quadrate, massimi, minimi, esponenti e molti altri. Ad esempio,

```java
public static final double PI = 3.141592653589793;
public static double cos(double a){
    ...
}
```
Di solito, per utilizzare questi oggetti di un'altra classe, si antepone il nome della classe, come segue.

`double r = Math.cos(Math.PI * theta);`

Puoi usare l'istruzione static import per importare i membri statici di java.lang.Math in modo da non dover aggiungere il prefisso al nome della classe, `Math`. I membri statici di `Math`possono essere importati singolarmente:

```java
import static java.lang.Math.PI  ;
```

o come gruppo 

```Java
import static java.lang.Math.*
```

Una volta importati, i membri statici possono essere utilizzati senza qualificazione. Ad esempio, il frammento di codice precedente diventerebbe:

`double r = cos(PI * theta);`

Ovviamente, puoi scrivere le tue classi che contengono costanti e metodi statici che usi frequentemente, e poi usare l'istruzione static import. Ad esempio,
`import static mypackage.MyConstants.*;`


## Gestione dei file sorgente e di classe

Molte implementazioni della piattaforma Java si basano su file system gerarchici per gestire file sorgente e di classe, sebbene _la Java Language Specification_ non lo richieda. La strategia è la seguente.

Inserisci il codice sorgente per una classe, interfaccia, enumerazione o tipo di annotazione in un file di testo il cui nome è il nome semplice del tipo e la cui estensione è `.java`. Ad esempio:
```Java
//in the Rectangle.java file 
package graphics;
public class Rectangle {
   ... 
}
```
Quindi, inserisci il file sorgente in una directory il cui nome riflette il nome del pacchetto a cui appartiene il tipo:
`.....\graphics\Rectangle.java`

Il nome qualificato del membro del pacchetto e il nome del percorso al file sono paralleli, presupponendo che il separatore del nome file di Microsoft Windows sia la barra rovesciata (per UNIX, utilizzare la barra).

- **nome della classe** –`graphics.Rectangle`
- **percorso del file** –`graphics\Rectangle.java`

Come dovresti ricordare, per convenzione un'azienda usa il suo nome di dominio Internet invertito per i nomi dei suoi pacchetti. L'azienda Example, il cui nome di dominio Internet è `example.com`, anteporrebbe a tutti i suoi nomi di pacchetti `com.example`. Ogni componente del nome del pacchetto corrisponde a una sottodirectory. Quindi, se l'azienda Example avesse un pacchetto `com.example.graphics` che conteneva un file sorgente `Rectangle.java`, sarebbe contenuto in una serie di sottodirectory come questa:
`....\com\example\graphics\Rectangle.java`

Quando compili un file sorgente, il compilatore crea un file di output diverso per ogni tipo in esso definito. Il nome base del file di output è il nome del tipo e la sua estensione è `.class`. Ad esempio, se il file sorgente è così
```java
//in the Rectangle.java file
package com.example.graphics;
public class Rectangle {
      . . . 
}

class Helper{
      . . . 
}
```
quindi i file compilati saranno posizionati in:
`<path to the parent directory of the output files>\com\example\graphics\Rectangle.class`
`<path to the parent directory of the output files>\com\example\graphics\Helper.class`

In questo modo, puoi dare la directory `classes` ad altri programmatori senza rivelare le tue fonti. Devi anche gestire i file sorgente e di classe in questo modo, in modo che il compilatore e la Java Virtual Machine (JVM) possano trovare tutti i tipi che il tuo programma usa.

Il percorso completo alla directory `classes`, `<path_two>\classes`, è chiamato _class path_ , ed è impostato con la variabile di sistema `CLASSPATH`. Sia il compilatore che la JVM costruiscono il percorso ai tuoi file `.class` aggiungendo il nome del pacchetto al class path. Ad esempio, se

`<path_two>\classes`

è il tuo percorso di classe e il nome del pacchetto è

`com.example.graphics,`

quindi il compilatore e la JVM cercano in `.class files` 

`<path_two>\classes\com\example\graphics.`

Un class path può includere diversi percorsi, separati da un punto e virgola (Windows) o due punti (UNIX). Per impostazione predefinita, il compilatore e la JVM cercano la directory corrente e il file JAR contenente le classi della piattaforma Java in modo che queste directory siano automaticamente nel class path.

### Impostazione della variabile di sistema CLASSPATH

Per visualizzare la variabile `CLASSPATH` corrente, utilizzare questi comandi in Windows e UNIX (Bourne shell):

```
In Windows:   C:\> set CLASSPATH
In UNIX:      % echo $CLASSPATH
```

Per eliminare il contenuto corrente della variabile `CLASSPATH`, utilizzare questi comandi:

```
In Windows: C:\> set CLASSPATH= 
In UNIX: % unset CLASSPATH; export CLASSPATH
```

Per impostare la variabile `CLASSPATH`, utilizzare questi comandi (ad esempio):

```
In Windows: C:\> set CLASSPATH=C:\users\george\java\classes 
In UNIX: % CLASSPATH=/home/george/java/classes; export CLASSPATH
```
