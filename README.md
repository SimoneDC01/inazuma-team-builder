# 🏆 Draft Squadra - Algoritmo a Torneo (Inazuma Eleven)

Questo progetto è un'applicazione web a pagina singola (HTML/JS/CSS) progettata per permettere agli utenti di creare fino a 10 formazioni ideali selezionando i migliori giocatori da un enorme database (es. 5400+ personaggi) attraverso scontri 1vs1, minimizzando il numero di voti necessari.

## 🇮🇹 Versione Italiana

### ✨ Caratteristiche Principali

* **Ottimizzazione degli Scontri (Tournament Sort Adattato):** Non dovrai far scontrare tutti contro tutti. L'algoritmo crea un albero gerarchico: chi perde contro il vincitore entra in una "piscina di ripescaggio", garantendo di trovare sempre il vero 2°, 3° e 4° miglior giocatore col minimo sforzo.
* **Filtro Moduli Dinamico:** L'app applica regole calcistiche reali. Puoi scegliere giocatori liberamente finché i ruoli selezionati rientrano in uno dei moduli ammessi (4-4-2, 3-5-2, 4-5-1, 3-6-1, 5-4-1). Se hai già preso 4 difensori e l'ultimo modulo disponibile è il 4-4-2, l'algoritmo bloccherà la scelta di ulteriori difensori per i titolari.
* **Gestione Multi-Squadra:** Puoi formare fino a 10 squadre complete (11 titolari + 5 riserve). I giocatori eletti nelle squadre precedenti vengono rimossi dalla selezione per le squadre successive.
* **Strumento di Estrazione (Scraper) Integrato:** Per aggirare i blocchi CORS dei browser, l'app fornisce uno script da copiare e incollare nella console del sito sorgente. Lo script naviga le pagine in background, estrae i dati e li copia negli appunti.
* **Salvataggio Automatico Ottimizzato:** Lo stato del torneo viene salvato nel `localStorage` del browser ad ogni click. Per evitare di saturare i 5MB limite del browser, il motore salva solo gli ID dei giocatori.
* **Rimescolamento Equo:** Utilizza l'algoritmo *Fisher-Yates* per randomizzare le coppie ad ogni nuovo turno, evitando pattern ripetitivi.

### 🚀 Come si usa

1. **Avvio:** Apri il file `index.html` nel tuo browser. L'app ti avviserà che il database è vuoto.
2. **Estrazione Dati:**
* Apri il menu a tendina **"🛠️ Strumento di Estrazione (Scraper)"**.
* Clicca su **"📋 Copia Script Scraper"**.
* Vai sul sito del database ufficiale (es. *zukan.inazuma.jp*).
* Apri i DevTools del browser (premi `F12`), vai sulla tab **Console**, incolla lo script e premi `Invio`.
* Attendi pochi secondi: l'intero database in formato JSON verrà copiato automaticamente nei tuoi appunti.


3. **Importazione:**
* Torna all'applicazione e apri **"⚙️ Gestione Database Giocatori"**.
* Incolla il JSON nel campo di testo e clicca su **"Sincronizza e Aggiungi"**.


4. **Draft:** Inizia a votare! Scegli il tuo preferito in ogni scontro 1vs1. L'algoritmo farà il resto, riempiendo la dashboard in basso mano a mano che i ruoli vengono assegnati.

### 🧠 Logica dell'Algoritmo (Fasi)

* **Fase 1 (Ricerca del Capitano):** Tutto il database viene mischiato e inserito in un tabellone a eliminazione diretta. Il vincitore assoluto diventa il Capitano della Squadra 1. L'algoritmo annota tutti i giocatori che il Capitano ha sconfitto direttamente.
* **Fase 2 (Draft Titolari e Panchina):** I giocatori sconfitti dal Capitano (e SOLO loro) partecipano a un mini-torneo di ripescaggio per eleggere il 2° miglior giocatore, filtrati per i ruoli ancora disponibili nel modulo. Chi vince entra in squadra, e la "piscina" si aggiorna aggiungendo i giocatori che questo nuovo membro aveva sconfitto in precedenza.
* **Fase 3 (Nuova Squadra):** Quando una squadra arriva a 16 giocatori, il processo ricomincia per la squadra successiva pescando dai migliori giocatori rimasti nella piscina.

---

## 🇬🇧 English Version

### ✨ Main Features

* **Matchup Optimization (Adapted Tournament Sort):** You won't have to compare everyone against everyone. The algorithm builds a hierarchical tree: players who lose to the winner enter a "candidates pool", ensuring the true 2nd, 3rd, and 4th best players are found with minimal voting.
* **Dynamic Formation Filter:** The app strictly enforces real football/soccer formations (4-4-2, 3-5-2, 4-5-1, 3-6-1, 5-4-1). If you've picked 4 defenders and the only valid remaining formation is 4-4-2, the algorithm prevents you from seeing or voting for any more defenders for the starting lineup.
* **Multi-Team Management:** Build up to 10 complete teams (11 starters + 5 bench players). Players drafted to earlier teams are excluded from the candidate pool for subsequent teams.
* **Built-in Web Scraper:** To bypass browser CORS restrictions, the app provides a script to copy/paste into the target website's console. It navigates pagination in the background, extracts data, and auto-copies the JSON to your clipboard.
* **Optimized Auto-Save:** The tournament state is saved to the browser's `localStorage` on every click. To prevent hitting the 5MB storage limit when handling 5000+ players, the engine only saves player IDs in the matchup history.
* **Fair Shuffling:** Uses the *Fisher-Yates* algorithm to fully randomize matchups at the start of every new bracket/round, preventing repetitive patterns.

### 🚀 How to Use

1. **Start:** Open the `index.html` file in your browser. The app will notify you that the database is empty.
2. **Data Extraction:**
* Open the **"🛠️ Strumento di Estrazione (Scraper)"** dropdown.
* Click **"📋 Copia Script Scraper"** (Copy Scraper Script).
* Go to the target database website (e.g., *zukan.inazuma.jp*).
* Open Browser DevTools (press `F12`), go to the **Console** tab, paste the script, and hit `Enter`.
* Wait a few seconds: the entire database will be parsed into JSON and automatically copied to your clipboard.


3. **Import:**
* Go back to the app and open **"⚙️ Gestione Database Giocatori"** (Database Management).
* Paste the JSON into the text area and click **"Sincronizza e Aggiungi"** (Sync and Add).


4. **Draft:** Start voting! Pick your favorite in each 1v1 matchup. The algorithm handles the rest, automatically populating the dashboard as roles are filled.

### 🧠 Algorithm Logic (Phases)

* **Phase 1 (Finding the Captain):** The entire database is shuffled and put into a single-elimination bracket. The absolute winner becomes the Captain of Team 1. The algorithm keeps track of every player the Captain defeated directly.
* **Phase 2 (Drafting Starters and Bench):** The players defeated by the Captain (and ONLY them) participate in a mini-bracket to find the 2nd best player, filtered by roles still needed for a valid formation. The winner joins the team, and the "pool" updates by adding the players that this newly drafted member had defeated previously.
* **Phase 3 (Next Team):** Once a team reaches 16 players, the process seamlessly transitions to drafting the next team by drawing from the highest-ranked remaining players in the pool.
