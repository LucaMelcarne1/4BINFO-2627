# 🎤 Parla con il computer: Input / Output

> *"Un programma che non comunica è come un amico che non risponde ai messaggi: tecnicamente esiste, ma a che serve?"*

---

## 💡 La metafora del mondo reale

Immagina di entrare in un fast food con il chiosco touchscreen:

- Lo **schermo** che ti mostra il menù e il conto è l'**Output** (`System.out`): il programma ti *parla*.
- Il **dito** con cui tocchi "Doppio cheeseburger" è l'**Input** (`Scanner`): tu *parli* al programma.

In Java la console è questo chiosco, un po' spartano: niente immagini, solo testo. Ma è il posto perfetto per imparare a far dialogare uomo e macchina.

---

## ⚙️ Sintassi & Codice

### Output: `System.out`

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Ciao, mondo!");      // stampa e va A CAPO
        System.out.print("Niente ");             // stampa e RESTA sulla stessa riga
        System.out.print("a capo qui\n");        // \n = a capo manuale
        System.out.printf("Hai %d anni e sei alto %.2f m%n", 17, 1.78); // output formattato
    }
}
```

| Comando | Cosa fa |
|---|---|
| `System.out.println(x)` | Stampa `x` e va a capo |
| `System.out.print(x)` | Stampa `x` senza andare a capo |
| `System.out.printf(...)` | Stampa con segnaposto formattati |

**Segnaposto di `printf`:**

| Segnaposto | Significa | Esempio |
|---|---|---|
| `%d` | numero intero | `42` |
| `%f` / `%.2f` | numero decimale (con 2 cifre dopo la virgola) | `3.14` |
| `%s` | stringa | `"Luca"` |
| `%c` | singolo carattere | `'A'` |
| `%n` | a capo (portabile tra sistemi) | |

### Input: `Scanner`

```java
import java.util.Scanner;                         // 1) importiamo lo strumento

public class Main {
    public static void main(String[] args) {
        Scanner tastiera = new Scanner(System.in); // 2) creiamo il "microfono" collegato alla tastiera

        System.out.print("Come ti chiami? ");
        String nome = tastiera.nextLine();         // 3) legge una RIGA intera

        System.out.print("Quanti anni hai? ");
        int eta = tastiera.nextInt();              // 4) legge un numero intero

        System.out.println("Ciao " + nome + ", tra un anno ne avrai " + (eta + 1) + "!");

        tastiera.close();                          // 5) chiudiamo il microfono quando abbiamo finito
    }
}
```

**I metodi di lettura più usati:**

| Metodo | Legge | Tipo restituito |
|---|---|---|
| `nextLine()` | una riga intera (spazi inclusi) | `String` |
| `next()` | una sola parola | `String` |
| `nextInt()` | un intero | `int` |
| `nextDouble()` | un decimale | `double` |
| `nextBoolean()` | `true` / `false` | `boolean` |

### ⚠️ La trappola del `nextLine()` dopo `nextInt()`

Il bug più famoso del primo anno. Guarda questo:

```java
System.out.print("Livello: ");
int livello = tastiera.nextInt();       // l'utente scrive 5 e preme INVIO
System.out.print("Nome: ");
String nome = tastiera.nextLine();      // 😱 legge subito "" (stringa vuota)!
```

**Perché?** `nextInt()` si prende il `5` ma lascia nel buffer l'**INVIO**. Il `nextLine()` successivo trova quell'INVIO, pensa "ah, riga finita!" e restituisce una stringa vuota.

**Soluzione:** "mangia" l'INVIO avanzato con un `nextLine()` a vuoto.

```java
int livello = tastiera.nextInt();
tastiera.nextLine();                    // 🍽️ spazzola l'INVIO rimasto
String nome = tastiera.nextLine();      // ora funziona!
```

---

## 🎨 Schema Visivo

```
   TASTIERA                 PROGRAMMA                  SCHERMO
  ┌────────┐   "Luca⏎"   ┌─────────────┐             ┌──────────────┐
  │ ⌨️ ⌨️ ⌨️ │ ──────────▶ │   Scanner   │             │              │
  └────────┘             │ nextLine()  │             │              │
                         │     │       │             │              │
                         │     ▼       │             │              │
                         │ nome="Luca" │             │              │
                         │     │       │  println()  │              │
                         │     └───────┼───────────▶ │ Ciao Luca!   │
                         └─────────────┘             └──────────────┘
      INPUT (System.in)                                OUTPUT (System.out)
```

---

## 🎯 Esercizio di Spiegazione Guidata: "La Scheda del Tuo Eroe RPG"

**Consegna:** il programma chiede nome, livello e altezza del personaggio e stampa una scheda ordinata.

### Passo 1 — Ragioniamo prima di scrivere

Il programmatore non parte mai dalla tastiera, parte dalla domanda: *"quali dati mi servono e di che tipo sono?"*

- Nome → testo → `String`
- Livello → numero intero → `int`
- Altezza → numero con la virgola → `double`

### Passo 2 — Il codice

```java
import java.util.Scanner;

public class SchedaEroe {
    public static void main(String[] args) {
        Scanner tastiera = new Scanner(System.in);

        // Leggiamo prima i numeri...
        System.out.print("Livello del tuo eroe: ");
        int livello = tastiera.nextInt();

        System.out.print("Altezza in metri (usa la virgola, es. 1,85): ");
        double altezza = tastiera.nextDouble();

        tastiera.nextLine(); // 🍽️ ripuliamo l'INVIO lasciato da nextDouble()

        // ...poi il testo
        System.out.print("Nome dell'eroe: ");
        String nome = tastiera.nextLine();

        // Output formattato
        System.out.println();
        System.out.println("╔══════════════════════════╗");
        System.out.printf ("║ Nome:    %-15s ║%n", nome);
        System.out.printf ("║ Livello: %-15d ║%n", livello);
        System.out.printf ("║ Altezza: %-15.2f ║%n", altezza);
        System.out.println("╚══════════════════════════╝");

        tastiera.close();
    }
}
```

### Passo 3 — Perché l'abbiamo scritto così?

1. **Perché leggiamo prima i numeri e poi il testo?** Per ridurre i guai col buffer. Ma sapendo la trappola, mettiamo comunque `nextLine()` di pulizia: il codice resta corretto anche se qualcuno cambia l'ordine delle domande.
2. **Perché `%-15s`?** Il `-` allinea a sinistra e `15` riserva 15 caratteri: la scheda resta dritta anche con nomi di lunghezze diverse.
3. **Perché `%.2f`?** Per mostrare sempre due decimali: `1.8` diventa `1,80`.
4. **Perché `printf` e non tante `+`?** Con `+` avremmo dovuto incollare pezzi di stringa a mano. Il formato è più leggibile e più facile da modificare.

> 🧠 **Sfida bonus:** aggiungi una riga "Classe" (Guerriero, Mago, Ladro…) e fai in modo che la cornice si adatti da sola. Spoiler: ti servirà un ciclo, che vedremo presto!

---

## ✅ Ricorda

- `System.out.println` → il programma parla.
- `Scanner` → il programma ascolta.
- `nextLine()` dopo un `nextInt()` o `nextDouble()`? **Pulisci il buffer!**
- Chiudi sempre lo `Scanner` con `close()` quando hai finito.
