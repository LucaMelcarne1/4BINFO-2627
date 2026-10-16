# 📦 Le scatole della memoria: Tipi di Dato e Variabili

> *"Una variabile è una scatola con un'etichetta. Il tipo di dato decide cosa ci puoi mettere dentro: non puoi infilare una pizza in una busta da lettere."*

---

## 💡 La metafora del mondo reale

Pensa all'**inventario di Minecraft**: ogni slot ha un nome (l'oggetto) e un contenuto (la quantità). Ma immagina che esistano scatole di forme diverse:

- La scatola per le **uova** contiene solo numeri interi (3 uova, mai 3,5 uova!).
- La scatola per la **benzina** accetta anche i decimali (42,37 litri).
- Il **cartello** all'ingresso contiene testo.
- L'**interruttore della luce** ha solo due stati: acceso o spento.

Java è **fortemente tipizzato**: quando crei una scatola devi dichiarare *prima* che cosa ci andrà dentro, e poi non puoi cambiare idea.

---

## ⚙️ Sintassi & Codice

### Dichiarare una variabile

```
tipo nomeVariabile = valore;
```

```java
int vite = 3;               // intero: "dichiaro una scatola di tipo int chiamata vite, dentro ci metto 3"
vite = 2;                   // ho perso una vita: sovrascrivo il contenuto (NON riscrivo "int")
final int VITE_MAX = 5;     // final = costante: dopo l'assegnazione non cambia più
```

### I tipi primitivi

| Tipo | Cosa contiene | Esempio | Note |
|---|---|---|---|
| `byte` | interi piccolissimi (-128…127) | `byte b = 100;` | Risparmia memoria |
| `short` | interi piccoli | `short s = 20000;` | Raro nella pratica |
| `int` | **interi** (circa ±2 miliardi) | `int punti = 1500;` | ⭐ Il default per i numeri interi |
| `long` | interi enormi | `long pop = 8000000000L;` | Serve la `L` finale |
| `float` | decimali (precisione bassa) | `float f = 3.14f;` | Serve la `f` finale |
| `double` | **decimali** (precisione alta) | `double pi = 3.14159;` | ⭐ Il default per i decimali |
| `char` | **un solo** carattere | `char voto = 'A';` | Apici **singoli** |
| `boolean` | `true` o `false` | `boolean vivo = true;` | Base di tutte le decisioni |

### Le stringhe: `String`

`String` **non** è un tipo primitivo: è una *classe* (per questo la S è maiuscola). Contiene testo tra apici **doppi**.

```java
String nome = "Gandalf";                       // testo tra "doppi apici"
String saluto = "Ciao, " + nome + "!";         // + concatena (incolla) le stringhe
int lunghezza = nome.length();                 // 7 → numero di caratteri
String urlo = nome.toUpperCase();              // "GANDALF"
char iniziale = nome.charAt(0);                // 'G' → il primo carattere (si parte da 0!)
```

### Regole per i nomi delle variabili

- Iniziano con una lettera (o `_`), mai con un numero: `1vita` ❌ → `vita1` ✅
- Niente spazi né simboli strani: `punti totali` ❌ → `puntiTotali` ✅
- Convenzione **camelCase**: `puntiVitaMassimi`
- Nomi parlanti! `x` ❌ → `danno` ✅
- Java distingue maiuscole e minuscole: `Punti` ≠ `punti`

### Il casting (conversione tra tipi)

**Casting implicito (allargamento)** — da scatola piccola a scatola grande: Java lo fa da solo, nessun rischio.

```java
int punti = 10;
double puntiDecimali = punti;   // ✅ 10 diventa 10.0 automaticamente
```

**Casting esplicito (restringimento)** — da scatola grande a piccola: devi dirlo tu con `(tipo)`, e **perdi informazione**.

```java
double prezzo = 9.99;
int prezzoIntero = (int) prezzo;   // ⚠️ diventa 9: i decimali vengono TAGLIATI, non arrotondati!
```

```
byte → short → int → long → float → double
 ──────── automatico (implicito) ────────▶
 ◀─────── serve il (cast) esplicito ───────
```

### 🪤 Trappola classica: la divisione tra interi

```java
int a = 7, b = 2;
System.out.println(a / b);            // 3    😱 (int / int = int, niente decimali!)
System.out.println((double) a / b);   // 3.5  ✅ (basta rendere double UNO dei due)
System.out.println(a % b);            // 1    → il resto della divisione (modulo)
```

---

## 🎨 Schema Visivo

```
 MEMORIA DEL COMPUTER (RAM)
 ┌───────────────┬───────────────┬───────────────┬───────────────┐
 │  int          │  double       │  boolean      │  String       │
 │  ┌─────────┐  │  ┌─────────┐  │  ┌─────────┐  │  ┌─────────┐  │
 │  │   150   │  │  │  36.6   │  │  │  true   │  │  │"Gandalf"│  │
 │  └─────────┘  │  └─────────┘  │  └─────────┘  │  └─────────┘  │
 │  etichetta:   │  etichetta:   │  etichetta:   │  etichetta:   │
 │   "monete"    │ "temperatura" │   "vivo"      │   "nome"      │
 └───────────────┴───────────────┴───────────────┴───────────────┘
        ▲
        └── il TIPO decide la forma della scatola,
            il NOME è l'etichetta, il VALORE è il contenuto
```

---

## 🎯 Esercizio di Spiegazione Guidata: "L'Inventario dell'RPG"

**Consegna:** il tuo eroe ha 120 monete d'oro. Ogni pozione costa 17,50 monete. Calcola quante pozioni può comprare e quanto oro gli resta. Poi stampa il tutto.

### Passo 1 — Ragioniamo sui dati

| Dato | Valore | Che tipo di scatola? | Perché? |
|---|---|---|---|
| Nome eroe | "Aria" | `String` | È testo |
| Monete | 120 | `int` | Le monete si contano intere |
| Prezzo pozione | 17.5 | `double` | Ha la virgola |
| Pozioni comprabili | ? | `int` | Non puoi comprare mezza pozione! |
| Oro rimasto | ? | `double` | Il prezzo è decimale, quindi anche il resto |

### Passo 2 — Il codice

```java
public class InventarioRPG {
    public static void main(String[] args) {
        String nome = "Aria";                  // testo → String
        int monete = 120;                      // intero → int
        final double PREZZO_POZIONE = 17.5;    // prezzo fisso → costante

        // Quante pozioni? 120 / 17.5 = 6.857...
        // Mi serve un intero: il cast (int) TAGLIA i decimali → 6
        int pozioni = (int) (monete / PREZZO_POZIONE);

        // Quanto spendo e quanto resta?
        double speso = pozioni * PREZZO_POZIONE;   // int * double → double (cast implicito!)
        double resto = monete - speso;

        boolean puoComprareAltro = resto >= PREZZO_POZIONE;   // boolean: una domanda con risposta sì/no

        System.out.println(nome + " compra " + pozioni + " pozioni");
        System.out.println("Spesa totale: " + speso + " monete");
        System.out.println("Oro rimasto:  " + resto + " monete");
        System.out.println("Può comprarne un'altra? " + puoComprareAltro);
    }
}
```

**Output:**

```
Aria compra 6 pozioni
Spesa totale: 105.0 monete
Oro rimasto:  15.0 monete
Può comprarne un'altra? false
```

### Passo 3 — Il ragionamento dietro ogni scelta

1. **Perché `PREZZO_POZIONE` è `final`?** Il prezzo non deve cambiare per sbaglio durante il programma. Il nome in MAIUSCOLO è la convenzione per le costanti.
2. **Perché il cast `(int)`?** `monete / PREZZO_POZIONE` dà `6.857`. Noi vogliamo le pozioni *intere*: il cast taglia la parte decimale. Qui il "difetto" del cast è proprio ciò che ci serve!
3. **Perché `pozioni * PREZZO_POZIONE` funziona?** `int` per `double`: Java allarga da solo l'`int` a `double` (cast implicito) e il risultato è `double`.
4. **Perché un `boolean` alla fine?** Perché la risposta a "ne posso comprare un'altra?" è sì/no. Tra due capitoli useremo proprio questi `boolean` per far prendere decisioni al programma.

> 🧠 **Sfida bonus:** cosa succede se scrivi `int pozioni = monete / PREZZO_POZIONE;` senza il cast? Provalo e leggi l'errore del compilatore: è un ottimo allenamento.

---

## ✅ Ricorda

- Il **tipo** decide cosa puoi mettere nella scatola, il **nome** è l'etichetta.
- `int` per gli interi, `double` per i decimali, `boolean` per vero/falso, `char` per un carattere, `String` per il testo.
- Da piccolo a grande: casting automatico. Da grande a piccolo: `(tipo)` e perdi dati.
- `int / int` = `int`. Occhio alle divisioni!
