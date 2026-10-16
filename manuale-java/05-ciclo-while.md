# ⏳ Finché ne hai, continua: il Ciclo While

> *"Il `for` dice: ripeti 10 volte. Il `while` dice: ripeti finché non succede qualcosa. Il boss non muore dopo 10 colpi: muore quando finisce la sua vita."*

---

## 💡 La metafora del mondo reale

Sei a un **boss fight**. Non sai quanti colpi serviranno: dipende dalla fortuna, dal danno, dalle schivate. L'unica regola è:

> *"FINCHÉ il boss ha punti vita, continua ad attaccare."*

Oppure pensa a **scrollare TikTok**: *"finché non ho sonno, continuo a scrollare"*. Non c'è un numero di giri prefissato, c'è una **condizione** da controllare prima di ogni ripetizione.

**Regola d'oro:** quando **non sai in anticipo** quante volte ripetere → `while`.

---

## ⚙️ Sintassi & Codice

### La struttura del `while`

```
while (condizione) {
    // corpo: si ripete FINCHÉ la condizione è true
}
```

La condizione viene controllata **PRIMA** di ogni giro. Se è `false` già dall'inizio, il corpo **non viene eseguito nemmeno una volta**.

```java
int energia = 3;                                   // 1) preparo la variabile da controllare

while (energia > 0) {                              // 2) controllo: finché ho energia...
    System.out.println("Corro! Energia: " + energia);
    energia--;                                     // 3) ⚠️ AGGIORNO la variabile, altrimenti il ciclo non finisce mai
}
System.out.println("Sono esausto 😮‍💨");
```

**Output:**
```
Corro! Energia: 3
Corro! Energia: 2
Corro! Energia: 1
Sono esausto 😮‍💨
```

### Le tre regole per un `while` sano

1. **Inizializza** la variabile usata nella condizione *prima* del ciclo.
2. Scrivi una **condizione** chiara.
3. **Modifica** nel corpo qualcosa che prima o poi renda la condizione falsa. Se dimentichi il punto 3: **ciclo infinito** 💥 (nel terminale si ferma con `Ctrl + C`).

### `for` o `while`?

| Situazione | Scelta |
|---|---|
| So già il numero di ripetizioni (es. "10 volte") | `for` |
| Dipende da una condizione imprevedibile (es. "finché l'utente non scrive 0") | `while` |
| Devo leggere dati finché non ne arriva uno "speciale" | `while` |

> In realtà ogni `for` si può scrivere come `while` e viceversa: la scelta è una questione di **leggibilità**.

### Pattern classico: il valore sentinella

La **sentinella** è un valore speciale che significa "basta, ho finito".

```java
Scanner tastiera = new Scanner(System.in);
int somma = 0;

System.out.print("Inserisci un numero (0 per terminare): ");
int numero = tastiera.nextInt();               // 1) PRIMA lettura, fuori dal ciclo

while (numero != 0) {                          // 2) finché non arriva la sentinella
    somma += numero;                           // 3) elaboro il numero
    System.out.print("Prossimo numero (0 per terminare): ");
    numero = tastiera.nextInt();               // 4) NUOVA lettura: aggiorna la condizione
}

System.out.println("Somma totale: " + somma);
```

### Controlli di flusso extra: `break` e `continue`

```java
while (true) {                  // ciclo "infinito" volutamente...
    // ...
    if (condizioneDiUscita) {
        break;                  // ...da cui usciamo subito con break
    }
}
// continue → salta il resto del giro e passa al prossimo controllo della condizione
```

---

## 🎨 Schema Visivo

```
  int vitaBoss = 40;
  while (vitaBoss > 0) { vitaBoss -= 15; }

              ┌───────────────────┐
         ┌───▶│  vitaBoss > 0 ?   │──── NO ───▶ FINE ciclo 🏆
         │    └─────────┬─────────┘
         │              │ SÌ
         │              ▼
         │    ┌───────────────────┐
         │    │  vitaBoss -= 15   │   ← il corpo DEVE avvicinarci
         │    └─────────┬─────────┘     alla condizione falsa
         │              │
         └──────────────┘

  Traccia:
  ┌───────┬────────────────┬─────────────┬──────────────┐
  │ Giro  │ vitaBoss prima │ Condizione  │ vitaBoss dopo│
  ├───────┼────────────────┼─────────────┼──────────────┤
  │   1   │      40        │  40>0  SÌ   │     25       │
  │   2   │      25        │  25>0  SÌ   │     10       │
  │   3   │      10        │  10>0  SÌ   │     -5       │
  │  (4)  │      -5        │  -5>0  NO ❌│   (esce)     │
  └───────┴────────────────┴─────────────┴──────────────┘
```

---

## 🎯 Esercizio di Spiegazione Guidata: "Il Boss Fight"

**Consegna:** il boss "Drago Lagghoso" ha 100 punti vita. A ogni turno il tuo eroe infligge un danno casuale tra 5 e 25. Simula il combattimento, stampa ogni turno e dì in quanti turni hai vinto.

### Passo 1 — Perché proprio `while`?

Non sappiamo in quanti turni il drago cadrà: dipende dal caso. L'unica certezza è la condizione: **finché `vitaBoss > 0` si combatte**. Se ci chiediamo "so quante volte?" e la risposta è "no" → `while`.

### Passo 2 — Gli ingredienti

| Cosa serve | Variabile |
|---|---|
| Vita del boss | `int vitaBoss = 100;` |
| Contatore dei turni | `int turno = 0;` |
| Danno casuale | `Random` con `nextInt(21) + 5` |

💡 `rand.nextInt(21)` produce un numero da **0 a 20**; sommando 5 otteniamo da **5 a 25**.

### Passo 3 — Il codice

```java
import java.util.Random;

public class BossFight {
    public static void main(String[] args) {
        Random dado = new Random();           // il nostro generatore di numeri casuali
        int vitaBoss = 100;                   // INIZIALIZZO la variabile della condizione
        int turno = 0;                        // contatore: quanti turni ci vorranno?

        System.out.println("🐉 Il Drago Lagghoso appare! (100 HP)");

        while (vitaBoss > 0) {                // condizione: il boss è ancora vivo?
            turno++;                          // nuovo turno
            int danno = dado.nextInt(21) + 5; // danno casuale da 5 a 25
            vitaBoss -= danno;                // AGGIORNO la variabile: avviciniamo la fine!

            if (vitaBoss < 0) {               // evitiamo "vita negativa", brutta da leggere
                vitaBoss = 0;
            }

            System.out.println("Turno " + turno + ": colpisci per " + danno
                               + " → HP boss: " + vitaBoss);
        }

        System.out.println("🏆 Boss sconfitto in " + turno + " turni!");
    }
}
```

**Esempio di output (varia a ogni esecuzione!):**

```
🐉 Il Drago Lagghoso appare! (100 HP)
Turno 1: colpisci per 18 → HP boss: 82
Turno 2: colpisci per 7 → HP boss: 75
Turno 3: colpisci per 24 → HP boss: 51
Turno 4: colpisci per 15 → HP boss: 36
Turno 5: colpisci per 22 → HP boss: 14
Turno 6: colpisci per 19 → HP boss: 0
🏆 Boss sconfitto in 6 turni!
```

### Passo 4 — Il ragionamento dietro ogni scelta

1. **Perché `vitaBoss = 100` prima del ciclo?** La condizione `vitaBoss > 0` deve poter essere valutata fin dal primo controllo: se la variabile non esistesse o valesse 0, il ciclo non partirebbe.
2. **Perché `vitaBoss -= danno` dentro il ciclo?** È la riga "salvavita": è ciò che rende prima o poi falsa la condizione. Senza di lei, il Drago sarebbe immortale e il programma girerebbe per sempre.
3. **Perché `turno++` e non un `for`?** Il numero di turni non è deciso in partenza: lo **scopriamo** alla fine. Il contatore qui è un *risultato*, non una guida del ciclo.
4. **Perché l'`if (vitaBoss < 0)` dentro il ciclo?** Perché un colpo finale da 24 su 14 HP darebbe -10. Stampare "HP boss: -10" è brutto: ritocchiamo il dato prima di mostrarlo.

> 🧠 **Sfida bonus:** aggiungi un contrattacco: anche l'eroe ha 60 HP e il drago colpisce per 3-12 danni a turno. Come cambia la condizione del `while`? (Suggerimento: `vitaBoss > 0 && vitaEroe > 0`.) Chi vince?

---

## ✅ Ricorda

- `while` = ripeti **finché** la condizione è vera (non so quante volte).
- La condizione si controlla **prima** di ogni giro: può darsi che il corpo non giri mai.
- Inizializza → controlla → **aggiorna**. Se dimentichi l'aggiornamento: ciclo infinito.
- Valore sentinella: un dato "speciale" che dice di fermarsi.
