
## _Definizione di Oggetto_

Qualsiasi entità che abbia stato e comportamento è nota come oggetto. Ad esempio, una sedia, una penna, un tavolo, una tastiera, una bicicletta, ecc. Può essere fisica o logica. 
Un Object può essere definito come un'istanza di una classe. 
Un object contiene un indirizzo e occupa un po' di spazio in memoria. 
Gli Object possono comunicare senza conoscere i dettagli dei dati o del codice degli altri. L'unica cosa necessaria è il tipo di messaggio accettato e il tipo di risposta restituita dagli object. 


## _Definizione di Classe_

_La raccolta di oggetti_ è chiamata classe. È un'entità logica.

Una classe può anche essere definita come un blueprint da cui puoi creare un singolo oggetto. La classe non consuma spazio.


## _Definizione di Ereditarietà_

_Quando un oggetto acquisisce tutte le proprietà e i comportamenti di un oggetto padre_ , si parla di ereditarietà. Fornisce riutilizzabilità del codice. Viene utilizzato per ottenere il polimorfismo runtime.

## _Definizione di Polimorfismo_

Se _un compito viene eseguito in modi diversi_ , si parla di polimorfismo. Ad esempio: convincere il cliente in modo diverso, disegnare qualcosa, ad esempio una forma, un triangolo, un rettangolo, ecc.

In Java utilizziamo il sovraccarico e l'override dei metodi per ottenere il polimorfismo.


## _Definizione di Astrazione_

_Nascondere i dettagli interni e mostrare la funzionalità_ è noto come astrazione. Ad esempio, telefonata, non conosciamo l'elaborazione interna.
In Java utilizziamo classi e interfacce astratte per ottenere l'astrazione.


### Che cos'è una classe in Java

Una classe è un gruppo di oggetti che hanno proprietà comuni. È un modello o un progetto da cui vengono creati gli oggetti. È un'entità logica. Non può essere fisica.

Una classe in Java può contenere:
- **Campi**
- **Metodi**
- **Costruttori**
- **Blocchi**
- **Classe e interfaccia nidificate**

#### Metodo in Java

In Java, un metodo è come una funzione utilizzata per esporre il comportamento di un oggetto.

 Vantaggio del metodo:
- Riutilizzabilità del codice
- Ottimizzazione del codice

La parola chiave **new** viene utilizzata per allocare memoria in fase di esecuzione. Tutti gli oggetti ottengono memoria nell'area di memoria Heap.

Esempio di oggetto e classe all'interno della classe:
```Java
1. //Java Program to illustrate how to define a class and fields  
2. //Defining a Student class.  
3. class Student{  
4.  //defining fields  
5.  int id;//field or data member or instance variable  
6.  String name;  
7.  //creating main method inside the Student class  
8.  public static void main(String args[]){  
9.   //Creating an object or instance  
10.   Student s1 = new Student();//creating an object of Student  
11.   //Printing values of the object  
12.   System.out.println(s1.id);//accessing member through reference variable  
13.   System.out.println(s1.name);  
14.  }  
15. }
```

Esempio di oggetto e classe all'esterno della classe:
```java
1. //Java Program to demonstrate having the main method in   
2. //another class  
3. //Creating Student class.  
4. class Student{  
5.  int id;  
6.  String name;  
7. }  
8. //Creating another class TestStudent1 which contains the main method  
9. class TestStudent1{  
10.  public static void main(String args[]){  
11.   Student s1 = new Student();  
12.   System.out.println(s1.id);  
13.   System.out.println(s1.name);  
14.  }  
15. }
```

### 3 modi per inizializzare un oggetto

Inizializzare un oggetto significa memorizzare dati nell'oggetto.

Esistono 3 modi per inizializzare un oggetto in Java.

1. Per variabile di riferimento, esempio di oggetto e classe, inizializzato tramite variabile di riferimento:
```Java
1. class Student{  
2.  int id;  
3.  String name;  
4. }  
5. 
6. class TestStudent2{  
7.  public static void main(String args[]){  
8.   Student s1 = new Student();  
9.   s1.id = 101;  
10.  s1.name = "Mario";  
11. System.out.println(s1.id+" "+s1.name);//printing members with a white space  
12.  }  
13. }

// Produzione: 101 Mario
```

Si possono creare anche più oggetti e memorizzare informazioni in essi tramite variabili di riferimento:
```java
1. class Student{  
2.  int id;  
3.  String name;  
4. }  
5. 
6. class TestStudent3{  
7.  public static void main(String args[]){  
8.   //Creating objects  
9.   Student s1 = new Student();  
10.   Student s2 = new Student();  
11.   //Initializing objects  
12.   s1.id = 101;  
13.   s1.name = "Mario";  
14.   s2.id = 102;  
15.   s2.name = "Andrea";  
16.   //Printing data  
17.   System.out.println(s1.id+" "+s1.name);  
18.   System.out.println(s2.id+" "+s2.name);  
19.  }  
20. }

//Output: 101 Mario 102 Andrea
```

2. Per metodo, esempio di oggetto e classe, inizializzato tramite metodo:
```java
1. class Student{  
2.  int rollno;  
3.  String name;  
4.  void insertRecord(int r, String n){  
5.   rollno = r;  
6.   name = n;  
7.  }  
8.  void displayInformation(){System.out.println(rollno+" "+name);}  
9. }  
10. 
11. class TestStudent4{  
12.  public static void main(String args[]){  
13.   Student s1 = new Student();  
14.   Student s2 = new Student();  
15.   s1.insertRecord(111,"Karan");  
16.   s2.insertRecord(222,"Aryan");  
17.   s1.displayInformation();  
18.   s2.displayInformation();  
19.  }  
20. }
```
   
3. Per costruttore, esempi odi oggetto e classe, inizializzato tramite costruttore:
```java
1. class Employee{  
2.     int id;  
3.     String name;  
4.     float salary;  
5.     void insert(int i, String n, float s) {  
6.         id = i;  
7.         name = n;  
8.         salary = s;  
9.     }  
10.     void display(){System.out.println(id+" "+name+" "+salary);}  
11. }  
12. 
13. public class TestEmployee {  
14.  public static void main(String[] args) {  
15.     Employee e1 = new Employee();  
16.     Employee e2 = new Employee();  
17.     Employee e3 = new Employee();  
18.     e1.insert(101,"ajeet",45000);  
19.     e2.insert(102,"irfan",25000);  
20.     e3.insert(103,"nakul",55000);  
21.     e1.display();  
22.     e2.display();  
23.     e3.display();  
24. }  
25. }
```

### Usare la parola chiave THIS

 In Java, this è una **variabile di riferimento** che si riferisce all'oggetto corrente.
 Ci sono 6 utilizzi della parola chiave this in Java.

1. può essere utilizzato per fare riferimento alla variabile istanza della classe corrente. Se c'è ambiguità tra le variabili istanza e i parametri, questa parola chiave risolve il problema di ambiguità.
2. questo può essere utilizzato per richiamare il metodo della classe corrente (implicitamente). Se non usi la parola chiave this, il compilatore aggiunge automaticamente la parola chiave this durante l'invocazione del metodo.
3. this() può essere utilizzato per richiamare il costruttore della classe corrente. È usata per riutilizzare il costruttore. In altre parole, è usata per il concatenamento del costruttore.
4. questo può essere passato come argomento nella chiamata al metodo.
5. questo può essere passato come argomento nella chiamata del costruttore.
6. può essere utilizzato per restituire l'istanza della classe corrente dal metodo.