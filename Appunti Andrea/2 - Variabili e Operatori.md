
Una variabile è un contenitore che contiene il valore mentre il programma Java viene eseguito. 

Ci sono tre tipi di variabili: _local_, istance e _static_.
Che possono essere sia primitivi (includono boolean, char, byte, short, int, long, float e double) che non primitivi (che includono classi, Interfacce e Array). 

Una variabile è allocata in memoria, è un nome della posizione di memoria. 

- **Variabile Locale**: Una variabile dichiarata all'interno del corpo del metodo è chiamata variabile locale. Puoi usare questa variabile solo all'interno di quel metodo e gli altri metodi nella classe non sono nemmeno a conoscenza dell'esistenza della variabile.
  Una variabile locale non può essere definita con la parola chiave "static".

- **Variabile di istanza**: Una variabile dichiarata all'interno della classe ma all'esterno del corpo del metodo, è chiamata variabile istanza. Non è dichiarata come _static_.
  Viene chiamata variabile istanza perché il suo valore è specifico dell'istanza e non è condiviso tra le istanze.

- **Variabile statica**: Una variabile dichiarata come static è detta variabile static. Non può essere locale. Puoi creare una singola copia della variabile static e condividerla tra tutte le istanze della classe. L'allocazione di memoria per le variabili statiche avviene solo una volta quando la classe viene caricata nella memoria.

Esempi:
```Java
1. public class A  
2. {  
3.     static int m=100;//static variable  
4.     void method()  
5.     {    
6.         int n=90;//local variable    
7.     }  
8.     public static void main(String args[])  
9.     {  
10.         int data=50;//instance variable    
11.     }  
12. }//end of class
```