# ☕ 4BINFO 2026/27 — Il Manuale di Java della Classe

Benvenuti nel manuale **ufficiale** di Java della 4ª B Informatica!

Qui trovi tutto quello che abbiamo affrontato in classe, spiegato con metafore, schemi e un sacco di codice da provare. Niente muri di testo: ogni capitolo ha la stessa struttura, così sai sempre dove cercare.

## 🧩 Come è fatto ogni capitolo

| Sezione | Cosa trovi |
|---|---|
| 💡 **La metafora** | Il concetto spiegato con un'analogia della vita reale (o di un videogioco) |
| ⚙️ **Sintassi & Codice** | Esempi commentati riga per riga |
| 🎨 **Schema Visivo** | Il flusso di esecuzione disegnato in ASCII art |
| 🎯 **Esercizio guidato** | Un problema risolto passo dopo passo, col *perché* di ogni scelta |

## 📚 Indice dei capitoli

| # | Capitolo | Di cosa parla |
|---|---|---|
| 1 | [🎤 Parla con il computer: Input / Output](manuale-java/01-input-output.md) | `System.out`, `Scanner`, `printf` |
| 2 | [📦 Le scatole della memoria: Tipi di Dato e Variabili](manuale-java/02-tipi-di-dato-e-variabili.md) | Primitivi, `String`, casting |
| 3 | [🚦 Il bivio del destino: Strutture Condizionali](manuale-java/03-strutture-condizionali.md) | `if`, `else if`, `else`, operatori |
| 4 | [🔁 Ripeti con stile: il Ciclo For](manuale-java/04-ciclo-for.md) | Ripetizione con contatore |
| 5 | [⏳ Finché ne hai, continua: il Ciclo While](manuale-java/05-ciclo-while.md) | Ripetizione condizionale |
| 6 | [🔂 Prima agisci, poi ti chiedo: il Ciclo Do-While](manuale-java/06-ciclo-do-while.md) | Ripetizione post-condizionale |

## 🧭 Quale ciclo uso?

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

## 🛠️ Come usare il manuale

1. **Leggi** la metafora: se capisci quella, il resto viene da sé.
2. **Copia** il codice in un tuo file `.java` e **eseguilo**.
3. **Rompilo** apposta: cambia un valore, togli un `;`, leggi l'errore. Si impara tantissimo così!
4. Prova le **sfide bonus** in fondo a ogni esercizio.

## ✅ Prerequisiti

- JDK installato (`java -version` da terminale per controllare)
- Un editor o IDE a scelta (VS Code, IntelliJ IDEA, Eclipse…)

## 🔜 Prossimamente

Nuovi capitoli man mano che avanziamo con il programma. Tieni d'occhio la repository!

---

*Buon coding! Ricorda: ogni programmatore ha passato ore a cercare un `;` mancante. Tu ora hai solo un vantaggio: lo sai già.* 😄
