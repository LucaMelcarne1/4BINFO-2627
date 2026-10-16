# 🔂 Prima agisci, poi ti chiedo: il Ciclo Do-While

> *"Il `while` è un buttafuori: controlla prima di farti entrare. Il `do-while` è un buffet: mangi per primo, e solo dopo ti chiedono se ne vuoi ancora."*

---

## 💡 La metafora del mondo reale

Hai mai usato un **distributore automatico** o un **menu di gioco**?

1. Il menu si mostra **sempre almeno una volta** (non avrebbe senso controllare prima se vuoi vederlo!).
2. Scegli un'opzione.
3. Il menu si ripresenta **finché non scegli "Esci"**.

Oppure la **password dimenticata**: ti chiedono di inserirla *almeno una volta*, e se sbagli te la richiedono.

Il `do-while` è il ciclo per quando **devi eseguire il corpo almeno una volta**, e solo *dopo* decidi se ripeterlo.

---

## ⚙️ Sintassi & Codice

### La struttura del `do-while`

```
do {
    // corpo: eseguito ALMENO UNA VOLTA
} while (condizione);     // ⚠️ qui serve il PUNTO E VIRGOLA!
```

La condizione viene controllata **DOPO** ogni giro. Se è `true` si ripete, se è `false` si esce.

```java
int tentativi = 0;

do {
    tentativi++;
    System.out.println("Provo ad aprire la porta... tentativo " + tentativi);
} while (tentativi < 3);                   // ⚠️ ; obbligatorio

System.out.println("Porta bloccata, mi arrendo.");
```

**Output:**
```
Provo ad aprire la porta... tentativo 1
Provo ad aprire la porta... tentativo 2
Provo ad aprire la porta... tentativo 3
Porta bloccata, mi arrendo.
```

### 🆚 La differenza chiave con il `while`

```java
int x = 100;

while (x < 10) {                           // controlla PRIMA: x < 10 è false → il corpo NON gira mai
    System.out.println("while");
}

do {
    System.out.println("do-while");        // gira UNA volta, poi controlla: x < 10 è false → esce
} while (x < 10);
```

Output: stampa **solo** `do-while`.

| | `while` | `do-while` |
|---|---|---|
| Controllo della condizione | **prima** del corpo | **dopo** il corpo |
| Esecuzioni minime | **0** | **1** |
| Punto e virgola finale | no | **sì** |
| Uso tipico | "finché c'è qualcosa da fare" | menu, validazione input |

### Pattern classico: la validazione dell'input

"Chiedi un numero tra 1 e 10 e **richiedilo finché non è valido**."

```java
Scanner tastiera = new Scanner(System.in);
int voto;                                  // dichiarata FUORI: deve essere visibile anche nella condizione del while

do {
    System.out.print("Inserisci un voto da 1 a 10: ");
    voto = tastiera.nextInt();
    if (voto < 1 || voto > 10) {
        System.out.println("❌ Valore non valido, riprova!");
    }
} while (voto < 1 || voto > 10);           // ripeti SE il voto è fuori range

System.out.println("Voto accettato: " + voto);
```

> ⚠️ **Attenzione allo scope:** la variabile `voto` va dichiarata **prima** del `do`. Se la dichiarassi dentro le graffe, la condizione del `while` (che sta fuori dalle graffe) non potrebbe vederla.

---

## 🎨 Schema Visivo

```
  do { menu(); scelta = leggi(); } while (scelta != 0);

          ┌────────────────────────┐
          │  INIZIO                │
          └───────────┬────────────┘
                      ▼
          ┌────────────────────────┐ ◀───────────────┐
          │  CORPO                 │                 │
          │  (mostra menu, leggi)  │                 │
          └───────────┬────────────┘                 │
                      ▼                              │
              ◇ scelta != 0 ? ◇                      │
              │                │                     │
             NO               SÌ ────────────────────┘
              │          (ripeti il corpo)
              ▼
         FINE ciclo 🚪

  ➜ Il corpo gira SEMPRE almeno una volta: il controllo sta in FONDO.

  Confronto visivo:

    while:                         do-while:
    ┌──────────┐                   ┌──────────┐
    │ controlla│◀──┐               │  corpo   │◀──┐
    └────┬─────┘   │               └────┬─────┘   │
         ▼         │                    ▼         │
    ┌──────────┐   │               ┌──────────┐   │
    │  corpo   │───┘               │ controlla│───┘
    └──────────┘                   └────┬─────┘
                                        ▼
```

---

## 🎯 Esercizio di Spiegazione Guidata: "Il Distributore di Pozioni"

**Consegna:** crea un menu per un negozio di pozioni:

```
1) Pozione di cura   (10 monete)
2) Pozione di mana   (15 monete)
3) Vedi le monete
0) Esci
```

Parti con **50 monete**. Il menu si ripresenta finché l'utente non sceglie `0`. Se non hai abbastanza monete, il negozio ti avvisa.

### Passo 1 — Perché proprio `do-while`?

Il menu va **mostrato almeno una volta**, a prescindere da tutto: non possiamo sapere cosa sceglierà l'utente senza averglielo chiesto. Poi si ripete finché `scelta != 0`. → "Prima agisci, poi controlli": **`do-while`**!

### Passo 2 — Le scelte progettuali

- La variabile `scelta` va dichiarata **fuori** dal ciclo (altrimenti la condizione finale non la vedrebbe).
- Le monete devono **sopravvivere** tra un giro e l'altro → anche `monete` fuori dal ciclo.
- Per gestire le varie scelte usiamo la catena `if / else if / else` del Capitolo 3.

### Passo 3 — Il codice

```java
import java.util.Scanner;

public class DistributorePozioni {
    public static void main(String[] args) {
        Scanner tastiera = new Scanner(System.in);

        int monete = 50;        // stato del gioco: vive FUORI dal ciclo
        int scelta;             // dichiarata fuori, assegnata dentro

        do {
            // 1) Mostro il menu (SEMPRE almeno una volta)
            System.out.println("\n🧪 === NEGOZIO DI POZIONI ===");
            System.out.println("1) Pozione di cura  (10 monete)");
            System.out.println("2) Pozione di mana  (15 monete)");
            System.out.println("3) Vedi le monete");
            System.out.println("0) Esci");
            System.out.print("Scelta: ");
            scelta = tastiera.nextInt();

            // 2) Reagisco alla scelta
            if (scelta == 1) {
                if (monete >= 10) {
                    monete -= 10;
                    System.out.println("❤️ Hai comprato una pozione di cura!");
                } else {
                    System.out.println("💸 Monete insufficienti.");
                }
            } else if (scelta == 2) {
                if (monete >= 15) {
                    monete -= 15;
                    System.out.println("🔷 Hai comprato una pozione di mana!");
                } else {
                    System.out.println("💸 Monete insufficienti.");
                }
            } else if (scelta == 3) {
                System.out.println("👛 Hai " + monete + " monete.");
            } else if (scelta != 0) {                 // 0 è l'uscita: tutti gli altri valori sono errori
                System.out.println("❓ Opzione non valida.");
            }

        } while (scelta != 0);                        // ripeti finché NON sceglie di uscire

        System.out.println("\n👋 Alla prossima, avventuriero! Monete finali: " + monete);
        tastiera.close();
    }
}
```

### Passo 4 — Il ragionamento dietro ogni scelta

1. **Perché `int scelta;` senza valore iniziale?** Perché sarà sempre assegnata dentro il `do` *prima* di essere letta dalla condizione. Nel `do-while` questa garanzia c'è, grazie al primo giro obbligatorio. Con un `while` dovremmo inventarci un valore finto per farlo partire.
2. **Perché `monete` è fuori dal ciclo?** Se la dichiarassimo dentro, si resetterebbe a 50 a ogni visualizzazione del menu: il tuo shopping non lascerebbe tracce.
3. **Perché `else if (scelta != 0)` per l'errore?** Se mettessimo un semplice `else`, anche lo `0` (uscita) stamperebbe "Opzione non valida" prima di chiudere. Escludiamo esplicitamente lo 0.
4. **Perché l'`if` annidato per le monete?** Sono due decisioni distinte: *quale* pozione vuole (scelta) e *se può permettersela* (monete). Annidare le separa in modo chiaro.
5. **Perché il `;` dopo `while (scelta != 0)`?** Sintassi: nel `do-while` la riga di condizione è un'istruzione a sé e va chiusa con `;`. Dimenticarlo è l'errore più comune.

> 🧠 **Sfida bonus:** aggiungi una validazione: se l'utente scrive una lettera invece di un numero, il programma va in crash con `InputMismatchException`. Come potresti evitarlo? (Suggerimento: guarda il metodo `hasNextInt()` dello `Scanner`!)

---

## ✅ Ricorda

- `do-while` = **prima** esegui, **poi** controlli → il corpo gira **almeno una volta**.
- Punto e virgola finale **obbligatorio**: `} while (condizione);`
- Perfetto per **menu** e per la **validazione dell'input**.
- Dichiara fuori dal ciclo le variabili che usi nella condizione.

---

## 🧭 Riepilogo finale: quale ciclo scelgo?

```
        Devo ripetere qualcosa?
                 │
     So QUANTE volte? ──── SÌ ──▶ for
                 │
                NO
                 │
   Il corpo deve girare ──── SÌ ──▶ do-while   (menu, validazione input)
   ALMENO una volta?
                 │
                NO
                 │
                 ▼
               while   (ripeti finché la condizione è vera)
```
