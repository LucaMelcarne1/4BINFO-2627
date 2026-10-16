# 🚦 Il bivio del destino: le Strutture Condizionali

> *"Un programma senza decisioni è una playlist: parte, va avanti, finisce. Con gli `if` diventa un videogioco: dipende da come giochi."*

---

## 💡 La metafora del mondo reale

Sei davanti a una **porta di un dungeon** con un buttafuori troll:

- *SE* hai la chiave → entri.
- *ALTRIMENTI SE* hai abbastanza monete → paghi e entri.
- *ALTRIMENTI* → il troll ti lancia lontano.

Il troll controlla le condizioni **dall'alto verso il basso** e si ferma alla **prima** che è vera. Questo è esattamente un `if / else if / else`.

---

## ⚙️ Sintassi & Codice

### La struttura base

```java
if (condizione) {
    // eseguito SOLO se la condizione è true
} else if (altraCondizione) {
    // eseguito se la prima era false e questa è true
} else {
    // eseguito se TUTTE le condizioni precedenti erano false
}
```

- La condizione è sempre un'espressione che produce un **`boolean`** (`true`/`false`).
- `else if` ed `else` sono **opzionali**; puoi avere un `if` da solo.
- Puoi concatenare quanti `else if` vuoi, ma `else` è uno solo ed è sempre l'ultimo.

```java
int vita = 25;

if (vita <= 0) {                           // 1) controlla la condizione più "grave" per prima
    System.out.println("Game Over 💀");
} else if (vita < 30) {                    // 2) solo se la 1 è falsa
    System.out.println("Attenzione, vita bassa! ❤️‍🩹");
} else {                                   // 3) in tutti gli altri casi
    System.out.println("Stai benone 💪");
}
```

### Operatori relazionali (confronti → restituiscono `boolean`)

| Operatore | Significa | Esempio | Risultato |
|---|---|---|---|
| `==` | uguale a | `5 == 5` | `true` |
| `!=` | diverso da | `5 != 3` | `true` |
| `>` | maggiore | `3 > 5` | `false` |
| `<` | minore | `3 < 5` | `true` |
| `>=` | maggiore o uguale | `5 >= 5` | `true` |
| `<=` | minore o uguale | `6 <= 5` | `false` |

> ⚠️ **`=` assegna, `==` confronta!** `if (vita = 0)` è un errore. Leggi `=` come "diventa" e `==` come "è uguale a?".

### Operatori logici (combinano più condizioni)

| Operatore | Nome | Vero quando… | Esempio |
|---|---|---|---|
| `&&` | AND | **entrambe** sono vere | `eta >= 18 && haBiglietto` |
| `\|\|` | OR | **almeno una** è vera | `haChiave \|\| haScasso` |
| `!` | NOT | inverte il valore | `!haPagato` |

**Tabelle di verità:**

```
  A      B    │  A && B  │  A || B       A   │  !A
 ─────────────┼──────────┼─────────     ─────┼──────
 true  true   │   true   │   true       true │ false
 true  false  │   false  │   true       false│ true
 false true   │   false  │   true
 false false  │   false  │   false
```

### 🪤 Confrontare le stringhe: MAI con `==`

```java
String password = tastiera.nextLine();

if (password == "magia")        { /* ❌ SBAGLIATO: confronta "dove sta" la stringa in memoria */ }
if (password.equals("magia"))   { /* ✅ GIUSTO: confronta il CONTENUTO */ }
if (password.equalsIgnoreCase("MAGIA")) { /* ✅ ignora maiuscole/minuscole */ }
```

### Condizioni annidate

```java
if (haChiave) {
    if (livello >= 5) {
        System.out.println("Il portone si apre!");
    } else {
        System.out.println("Hai la chiave ma sei troppo debole.");
    }
}
```

Meglio, quando possibile, **semplificare con `&&`**: `if (haChiave && livello >= 5)`.

---

## 🎨 Schema Visivo

```
                    ┌──────────────────┐
                    │  INIZIO controllo│
                    └────────┬─────────┘
                             ▼
                   ◇ vita <= 0 ? ◇
                   │              │
                  SÌ             NO
                   │              ▼
                   │        ◇ vita < 30 ? ◇
                   │        │              │
                   │       SÌ             NO
                   ▼        ▼              ▼
              "Game Over" "Vita bassa!" "Stai benone"
                   │        │              │
                   └────────┴──────┬───────┘
                                   ▼
                       ┌────────────────────┐
                       │ il programma       │
                       │ continua da qui    │
                       └────────────────────┘

  ➜ Si esegue UN SOLO ramo: il primo la cui condizione è vera.
```

---

## 🎯 Esercizio di Spiegazione Guidata: "Il Buttafuori del Dungeon"

**Consegna:** per entrare nel Dungeon dell'Oscurità servono:
- **livello almeno 10**, oppure
- una **password segreta** ("alohomora"), a prescindere dal livello.

Se hai livello tra 5 e 9 (e non conosci la password) ti dà un consiglio gentile; sotto il 5, ti caccia.

### Passo 1 — Traduciamo le regole in condizioni

| Regola in italiano | Condizione Java |
|---|---|
| "livello almeno 10" | `livello >= 10` |
| "oppure password giusta" | `|| password.equals("alohomora")` |
| "livello tra 5 e 9" | `livello >= 5` (arriviamo qui solo se la prima è falsa!) |
| "altrimenti" | `else` |

💡 **Trucco da programmatore:** l'ordine conta! Siccome `else if` si valuta solo se il precedente è `false`, non serve scrivere `livello >= 5 && livello <= 9`: se siamo arrivati lì, è già sotto il 10.

### Passo 2 — Il codice

```java
import java.util.Scanner;

public class ButtafuoriDungeon {
    public static void main(String[] args) {
        Scanner tastiera = new Scanner(System.in);

        System.out.print("Livello del tuo eroe: ");
        int livello = tastiera.nextInt();
        tastiera.nextLine();                         // pulizia del buffer (ricordi il Cap. 1?)

        System.out.print("Password segreta (premi INVIO se non la sai): ");
        String password = tastiera.nextLine();

        // 1) Il caso "vincente" va per primo
        if (livello >= 10 || password.equalsIgnoreCase("alohomora")) {
            System.out.println("🧌 Il troll si scansa: «Prego, entra, grande eroe!»");
        }
        // 2) Se siamo qui, il livello è < 10 E la password è sbagliata
        else if (livello >= 5) {
            System.out.println("🧌 Il troll sospira: «Torna al livello 10, ragazzo.»");
        }
        // 3) Tutti gli altri
        else {
            System.out.println("🧌 «TU?! Fuori di qui!» *vieni lanciato a 300 metri*");
        }

        tastiera.close();
    }
}
```

### Passo 3 — Il ragionamento dietro ogni scelta

1. **Perché `||` nel primo `if`?** Le regole dicono "livello OPPURE password": basta che *una* delle due sia vera.
2. **Perché `equalsIgnoreCase`?** Per non punire chi scrive "Alohomora" con la maiuscola. Un buon programmatore pensa agli utenti distratti.
3. **Perché il caso "entra" va per primo?** Mettere per prima la condizione più specifica/vincente evita di valutare ramificazioni inutili e rende il codice leggibile come una storia.
4. **Perché nell'`else if` basta `livello >= 5`?** Perché ci arriviamo solo se `livello >= 10` era falso: la condizione implicita "< 10" è già garantita.

> 🧠 **Sfida bonus:** aggiungi un controllo per i livelli negativi ("Livello non valido!") *prima* di tutti gli altri. Dove lo piazzi e perché?

---

## ✅ Ricorda

- `if` decide, `else if` offre alternative, `else` raccoglie tutto il resto.
- `=` assegna, `==` confronta. Le **stringhe** si confrontano con `.equals()`.
- `&&` = e (entrambe), `||` = o (almeno una), `!` = non.
- L'**ordine** delle condizioni è parte della logica: pensa sempre a cosa controlli per primo.
