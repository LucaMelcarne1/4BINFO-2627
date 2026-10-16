# 🔁 Ripeti con stile: il Ciclo For

> *"Il bravo programmatore è pigro nel modo giusto: non scrive 100 volte la stessa riga, scrive un ciclo."*

---

## 💡 La metafora del mondo reale

Il tuo prof ti punisce: *"Scrivi 10 volte: non userò più il telefono in classe."*

Puoi scrivere la frase a mano 10 volte (da principiante)... oppure puoi dire a un robot:

> *"Parti da 1, fermati dopo il 10, e ogni volta aumenta di 1 il tuo conteggio. A ogni giro scrivi la frase."*

Quello è un **ciclo `for`**: usalo quando **sai già quante volte** devi ripetere. Come i **push-up in palestra**: *"3 serie da 10"*. Sai in anticipo quanti giri farai.

---

## ⚙️ Sintassi & Codice

### La struttura del `for`

```
for (inizializzazione; condizione; aggiornamento) {
    // corpo: le istruzioni che si ripetono
}
```

Le tre parti dentro le parentesi:

| Parte | Quando viene eseguita | Cosa fa |
|---|---|---|
| **Inizializzazione** | **una sola volta**, all'inizio | Crea il contatore: `int i = 0` |
| **Condizione** | **prima di ogni giro** | Se `true` → entra, se `false` → il ciclo finisce |
| **Aggiornamento** | **alla fine di ogni giro** | Cambia il contatore: `i++` |

```java
for (int i = 1; i <= 5; i++) {                     // parte da 1, finché i <= 5, i aumenta di 1
    System.out.println("Giro numero " + i);        // viene eseguito 5 volte
}
// Dopo il for, la variabile i NON ESISTE più (vive solo dentro il ciclo)
```

**Output:**
```
Giro numero 1
Giro numero 2
Giro numero 3
Giro numero 4
Giro numero 5
```

### Le varianti più usate

```java
for (int i = 0; i < 5; i++)    { ... }   // da 0 a 4: 5 giri (lo standard dei programmatori!)
for (int i = 10; i > 0; i--)   { ... }   // conto alla rovescia: 10, 9, 8 ... 1
for (int i = 0; i <= 100; i += 10) { ... } // salti di 10: 0, 10, 20 ... 100
```

> 💡 `i++` è la scorciatoia di `i = i + 1`; `i--` di `i = i - 1`; `i += 10` di `i = i + 10`.

### Ciclo con accumulatore: la somma dei numeri

```java
int somma = 0;                          // l'ACCUMULATORE: parte da zero (elemento neutro della somma)
for (int i = 1; i <= 10; i++) {
    somma += i;                         // a ogni giro aggiungo il valore corrente di i
}
System.out.println("1+2+...+10 = " + somma);   // 55
```

### Cicli annidati (un ciclo dentro un altro)

```java
for (int riga = 1; riga <= 4; riga++) {          // ciclo ESTERNO: decide quante righe
    for (int col = 1; col <= riga; col++) {      // ciclo INTERNO: decide quante stelle nella riga
        System.out.print("⭐");
    }
    System.out.println();                         // a capo a fine riga
}
```

```
⭐
⭐⭐
⭐⭐⭐
⭐⭐⭐⭐
```

Per ogni giro dell'esterno, l'interno fa **tutti** i suoi giri (come le lancette: i minuti fanno un giro completo per ogni ora).

### Gli errori classici

| Errore | Effetto |
|---|---|
| `i <= 5` invece di `i < 5` partendo da 0 | Un giro **in più** (errore *off-by-one*) |
| Dimenticare l'aggiornamento (`i++`) | **Ciclo infinito** 🔥 |
| Mettere `;` dopo le parentesi: `for (...);` | Il corpo non fa parte del ciclo! |

---

## 🎨 Schema Visivo

```
for (int i = 1; i <= 3; i++) { stampa(i); }

          ┌─────────────────┐
          │ 1. int i = 1    │  ← INIZIALIZZAZIONE (una volta sola)
          └────────┬────────┘
                   ▼
          ┌─────────────────┐   NO
    ┌────▶│ 2. i <= 3 ?     │────────────▶ ESCI dal ciclo 🚪
    │     └────────┬────────┘
    │              │ SÌ
    │              ▼
    │     ┌─────────────────┐
    │     │ 3. CORPO:       │
    │     │    stampa(i)    │
    │     └────────┬────────┘
    │              ▼
    │     ┌─────────────────┐
    └─────│ 4. i++          │  ← AGGIORNAMENTO
          └─────────────────┘

  Traccia di esecuzione:
  ┌───────┬───────────┬──────────┬────────────┐
  │ Giro  │ i prima   │ i <= 3 ? │ Stampa     │
  ├───────┼───────────┼──────────┼────────────┤
  │   1   │    1      │   SÌ     │    1       │
  │   2   │    2      │   SÌ     │    2       │
  │   3   │    3      │   SÌ     │    3       │
  │  (4)  │    4      │   NO ❌  │  (esce)    │
  └───────┴───────────┴──────────┴────────────┘
```

---

## 🎯 Esercizio di Spiegazione Guidata: "L'Allenamento del Guerriero"

**Consegna:** il tuo eroe fa un allenamento di 5 giorni. Il giorno *n* fa un attacco con danno `n × 10`. Stampa il danno di ogni giorno e il **danno totale** accumulato. Poi disegna una "scalinata" di spade che cresce ogni giorno.

### Passo 1 — Capiamo cosa si ripete e cosa cambia

- **Quante volte?** 5 giorni, lo sappiamo in anticipo → **`for`** è la scelta naturale.
- **Cosa cambia a ogni giro?** Il giorno (1, 2, 3, 4, 5) → sarà il nostro contatore `giorno`.
- **Cosa si accumula?** Il danno totale → serve una variabile `totale` **fuori dal ciclo**, partendo da 0.

### Passo 2 — Il codice

```java
public class AllenamentoGuerriero {
    public static void main(String[] args) {
        int totale = 0;                              // accumulatore fuori dal ciclo, altrimenti si azzererebbe a ogni giro!

        for (int giorno = 1; giorno <= 5; giorno++) {
            int danno = giorno * 10;                 // il danno dipende dal contatore
            totale += danno;                         // aggiungo al totale

            System.out.print("Giorno " + giorno + " | Danno " + danno + " | ");

            // ciclo annidato: disegna tante spade quanto il numero del giorno
            for (int s = 1; s <= giorno; s++) {
                System.out.print("🗡️");
            }
            System.out.println();                    // a capo a fine giornata
        }

        System.out.println("💥 Danno totale: " + totale);
    }
}
```

**Output:**

```
Giorno 1 | Danno 10 | 🗡️
Giorno 2 | Danno 20 | 🗡️🗡️
Giorno 3 | Danno 30 | 🗡️🗡️🗡️
Giorno 4 | Danno 40 | 🗡️🗡️🗡️🗡️
Giorno 5 | Danno 50 | 🗡️🗡️🗡️🗡️🗡️
💥 Danno totale: 150
```

### Passo 3 — Il ragionamento dietro ogni scelta

1. **Perché `giorno` parte da 1 e non da 0?** Perché noi umani contiamo i giorni da 1 e vogliamo che il danno del primo giorno sia 10, non 0. Il contatore dovrebbe riflettere il **problema**, non l'abitudine.
2. **Perché `totale` è dichiarato *fuori* dal `for`?** Se lo dichiarassimo dentro, ricomincerebbe da 0 a ogni giro e perderebbe tutto ciò che ha accumulato. Inoltre, una variabile dichiarata dentro il ciclo **non esiste più dopo**, quindi non potremmo stamparla alla fine.
3. **Perché il ciclo interno usa `s` e non `giorno`?** Sono due contatori diversi: il primo conta i giorni, il secondo le spade. Usare lo stesso nome creerebbe un errore di compilazione.
4. **Perché `System.out.println()` a vuoto?** Mandare a capo dopo aver finito di disegnare le spade, altrimenti il giorno 2 inizierebbe sulla stessa riga del giorno 1.

> 🧠 **Sfida bonus:** modifica il programma per far inserire all'utente da tastiera il **numero di giorni** (usa `Scanner`!). Cosa cambia nel `for`?

---

## ✅ Ricorda

- `for` = so **quante volte** devo ripetere.
- Tre parti: **inizio; condizione; aggiornamento**.
- Gli accumulatori (`somma`, `totale`) si dichiarano **fuori** dal ciclo.
- Attenzione a `<` vs `<=` (errore off-by-one) e a non creare cicli infiniti.
