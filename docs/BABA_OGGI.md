# Baba — Cosa sa fare OGGI

Questo file descrive **solo quello che Baba fa davvero adesso**: è costruito e funziona.
Le idee per il futuro stanno in un file a parte: **`docs/BABA_FUTURO.md`**.

**Regola:** ogni volta che aggiungiamo una funzione a Baba, Claude aggiorna questo file:
la sezione giusta più una riga nel **Registro novità** in fondo.

*Ultimo aggiornamento: 01/10/2026. Controllato direttamente sul codice.*

**Legenda:** ✅ funziona ed è stato provato da te · 🔶 costruito e provato da Claude, ma
manca ancora una tua prova. Se una cosa con 🔶 l'hai già provata e va, dimmelo e la
segno ✅.

---

## Come si usa
- **Baba vive in sottofondo** (01/10): sfera che si chiude da sola, Spegni/Riavvia ✅
  provati da te; partenza da sola all'accensione 🔶 (da verificare alla prossima
  accensione: deve arrivare il briefing). All'accensione del PC parte da solo, nascosto
  (motore + scheduler), dopo ~45 secondi, così briefing e avvisi partono davvero.
  Collegamento "Baba (avvio automatico)" nella cartella Esecuzione automatica di Windows.
- **Sfera:** doppio clic su `Baba.vbs`. Chiudendo la finestra si chiude **solo la sfera**,
  Baba resta acceso in sottofondo. ✅ (la sfera)
- **`Spegni Baba.vbs`**: spegne tutto. **`Riavvia Baba.vbs`**: spegne e riapre.
- **Si aggiorna da solo** 🔶 (05/10): se dopo un aggiornamento del codice apri `Baba.vbs`,
  si accorge che il codice è cambiato e riavvia il motore da solo.
- Togliere l'avvio automatico: `.\.venv\Scripts\python.exe launch.py --autostart off`
  (oppure cancellare il collegamento dalla cartella Esecuzione automatica).
- **Telefono:** le notifiche automatiche arrivano sull'iPhone tramite l'app **ntfy**.
  Dal telefono le ricevi soltanto, non puoi ancora scrivere a Baba. ✅
- **Alternativa da terminale:** `.\scripts\run_engine.ps1` + `.\scripts\run_cli.ps1`
  (è il metodo che usiamo per i collaudi). ✅

---

## 1. Parlare e ragionare ✅
- Risponde in italiano (o nella lingua in cui gli scrivi), in modo conciso, mantenendo il
  suo personaggio.
- Spiega, pianifica, scrive testi, traduce, riassume.
- Usa più strumenti nella stessa richiesta. Esempio: "riassumi le mail e metti in agenda
  quelle importanti". Al massimo 8 giri di strumenti per richiesta (protezione contro i
  giri infiniti).
- **Modello usato:** per rispondere usa **sempre Sonnet** (il modello "bravo"). Haiku (più
  economico) lavora solo dietro le quinte, per scegliere cosa ricordare (vedi sezione 7).
  Scegliere Haiku per le domande semplici, così da risparmiare, è un'idea futura (A.3).

## 2. Email (Gmail) ✅
- Legge, cerca e riassume le mail ("riassumi le ultime mail", "cerca la mail di X").
- Prepara **bozze** di risposta. **Non invia mai** nulla da solo: le bozze le invii tu.
- **Allegati** 🔶 (05/10): quando legge una mail ti dice che allegati ha; li salva in
  `Documenti\BABA\Allegati` (mai sovrascrivendo), così può leggerli o stamparli. Trova le
  mail con PDF ("cerca le mail con un PDF allegato"). Nessuna nuova autorizzazione Google.
- ⚠️ L'accesso Google è in modalità "Test", quindi l'autorizzazione scade circa ogni
  7 giorni. Per rinnovarla basta lanciare `.\scripts\gmail_auth.ps1`.

## 3. Calendario (Google Calendar)
- Legge l'agenda ("che impegni ho domani?") ✅
- Crea, sposta e cancella eventi ✅ (provato da te il 01/10). Lo fa tramite un account
  "robot" che non scade più.
- Limite: non può invitare altre persone agli eventi.

## 4. File sul PC
- Cerca, legge e apre file, **solo** nelle cartelle Documenti e Desktop (per sicurezza) ✅
- **Trova i file anche col nome approssimativo** 🔶 (05/10): maiuscole, accenti, trattini e
  estensione non contano, le parole possono essere in qualsiasi ordine, tollera piccoli
  errori ("prva baba" → "Prova Baba.docx"); "il pdf della fattura" cerca un PDF. Cerca
  anche nelle sottocartelle. Se più file sono ugualmente simili ti chiede quale. Veloce
  (~40 millesimi di secondo invece di 3-5 secondi).
- Legge anche **PDF, Word, Excel, PowerPoint**, OpenDocument, RTF, EPUB e CSV 🔶 (provato
  da Claude su file di prova). Tutto viene elaborato sul PC: niente viene caricato su
  internet.
- **Stampa** ✅ (05/10, provata da te, `print_file`): PDF, Word, Excel, PowerPoint, testo e immagini sulla
  stampante predefinita (la Brother). **Chiede sempre conferma prima** (file, pagine,
  copie, stampante e se è accesa): questa regola è nel codice, non si può saltare. Dopo
  l'invio guarda la coda di stampa e ti dice se il foglio è partito o se è bloccato (es.
  carta finita). "Offline" da solo non lo blocca: la Brother in risparmio energetico
  risulta offline a Windows ma si risveglia da sola (scoperto il 05/10). I PDF
  li stampa tramite Acrobat Reader (che può restare aperto in sottofondo), gli Office con
  Office stesso, invisibile.
- **Trasforma in PDF** ✅ (05/10, provata da te, `convert_to_pdf`): Word, Excel, PowerPoint, testo/RTF/ODT
  e immagini, con l'Office del tuo PC. Il PDF va accanto all'originale con lo stesso nome,
  mai sovrascritto. Provato da Claude su tutti e quattro i tipi.
- Limiti: non sposta, rinomina o cancella file (l'unica cosa che scrive sono i PDF nuovi e
  gli allegati salvati). Non legge i PDF scansionati (quelli fatti solo di immagini):
  servirebbe l'OCR (il riconoscimento del testo nelle immagini), che di proposito non
  mandiamo a servizi esterni, per privacy.

## 5. App e siti ✅
- Apre: Blocco note, Calcolatrice, Esplora file, Paint, Gestione attività (Task Manager),
  Chrome, Edge, VS Code, Spotify, Obsidian (direttamente sul Baba Vault), Word, Excel,
  PowerPoint.
- Apre un sito web nel browser.
- **Crea presentazioni PowerPoint moderne** ✅ (provate da te il 01/10; `create_presentation`, rifatte
  dopo il tuo giudizio "troppo basilari"): Baba scrive i contenuti, il codice impagina.
  - Copertina, capitoli e numeri su sfondo scuro sfumato con anelli luminosi; indice
    automatico; numero del capitolo "a contorno".
  - 9 tipi di slide: schede (con numero o emoji), numeri giganti, linea del tempo, fasi
    a frecce, punti numerati, confronto a due schede, citazione, capitolo, chiusura.
  - **Transizione Morph** (gli anelli scivolano da una slide all'altra) ed **elementi che
    entrano uno dopo l'altro** dal basso, da soli, senza clic.
  - 5 temi (blu, scuro, verde, bordeaux, grafite); il testo si adatta allo spazio e, se
    proprio non entra, viene accorciato e quello completo va nelle note per chi parla.
  - Salva in `Documenti\Baba\Presentazioni`, non sovrascrive mai, e la apre da solo.
  - Provato da Claude in PowerPoint (13 slide × 5 temi + prova di stress) e da te dall'app.
- **Scrive dentro Word** ✅ (05/10, provato da te, `word_document`): crea documenti nuovi (titolo,
  titoletti, paragrafi, elenchi puntati e numerati, tabelle, grassetto/corsivo, citazioni,
  salti pagina) in `Documenti\BABA\Word`; **aggiunge** testo in fondo a un tuo documento;
  **sostituisce** parole o frasi ovunque (anche in tabelle, intestazioni e piè di pagina).
- **Scrive dentro Excel** ✅ (05/10, provato da te, `excel_workbook`): crea fogli nuovi già formattati
  (intestazione colorata, filtri, riga bloccata, larghezze, euro/numeri/date, formule,
  grafico a barre/linee/torta) in `Documenti\BABA\Excel`; **scrive** in celle precise,
  **aggiunge righe** in fondo, **legge** le celle con i loro indirizzi. Sui tuoi file usa
  Excel stesso, così grafici, tabelle pivot e macro restano intatti.
- **Sicurezza:** prima di modificare un tuo file fa sempre una **copia di sicurezza** in
  `Documenti\BABA\Copie di sicurezza`; i vecchi .doc/.xls li converte in una copia nuova
  (l'originale resta com'è); se il file è aperto te lo dice invece di rovinarlo; non fa
  mai partire le macro; non chiude né nasconde mai il tuo Word/Excel aperto.
- Limiti: le presentazioni per ora non hanno indice cliccabile né immagini; in Word non
  inserisce testo "a metà" del documento (aggiunge in fondo o sostituisce).

## 6. Internet
- Cerca sul web (DuckDuckGo, gratis) e legge una pagina ✅ (provati da te dentro la
  ricerca approfondita, 01/10). Legge solo il **testo principale** (via menu, banner dei
  cookie, barre laterali) e legge anche i **PDF online** (sul PC, con anydoc).
- **Ricerca approfondita** (`deep_research`) ✅ (provata da te il 01/10): fa una ricerca per la domanda più fino a 3
  "sottodomande" (altri punti di vista), apre fino a 8 pagine insieme, scarta video e
  social, al massimo 2 pagine per sito, e per ogni fonte tiene i **passaggi più pertinenti**.
  Alla fine dice se il materiale è scarso, così Baba cerca ancora prima di rispondere.
  Provato da Claude su temi veri (ETF, cedolare secca): fonti pulite in 12-20 secondi.
- Meteo (Open-Meteo, gratis) ✅ (lo usa il briefing del mattino).

## 7. Memoria e Obsidian ✅
- Ricorda fatti e preferenze tra una sessione e l'altra ("preferisco risposte brevi").
- **Sceglie da solo cosa ricordare:** dopo ogni risposta, Haiku legge lo scambio e salva i
  fatti che durano nel tempo. **Non** salva il contenuto di email e file letti, i dati di
  mercato o i compiti del momento.
- Legge, scrive ed elenca le note del **Baba Vault** (Obsidian).
- Usa anche i tuoi appunti del vault come fonte quando risponde.
- Limite: la memoria cerca per **parole uguali**, non per significato (migliorabile, A.2).

## 8. Mentore e analista di finanza ✅
- **Mentore:** percorso di studio a livelli nel vault (`Finanza/Percorso di studio.md`).
  Baba aggiorna da solo `Finanza/Progressi.md`. I livelli:
  - 0: mentalità e fondamenta;
  - 1: classi di attività, cioè azioni, cripto e materie prime (oro, argento, petrolio,
    gas, rame, agricole), e come esporsi con ETF/ETC/futures, inclusa la trappola del
    *rollover*;
  - 2: leggere il mercato;
  - 3: valutare un asset;
  - 4: rischio e portafoglio;
  - 5: macro e contesto.
- **Quotazioni** di azioni, cripto, materie prime e indici (Yahoo Finance, gratis, con
  qualche minuto di ritardo).
- **Watchlist:** aggiungi, togli ed elenchi i titoli da seguire, con le notizie relative
  (Google News).
- **Regole tue:** avvisi del tipo "prezzo sopra/sotto X" o "variazione giornaliera ≥ Y%",
  con **prova sul passato** (backtest).
- **Market-scout:** cerca segnali pubblici e verificabili (documenti ufficiali SEC EDGAR +
  notizie di settore) su IoT industriale, robotica, Industry 4.0 e manifattura avanzata.
  Ogni segnale ha la sua fonte. Non ripete i segnali già visti ✅ (provato da te il 01/10,
  notifica arrivata).
- **Confine onesto:** calcola, spiega e insegna. Non fa previsioni e non dice cosa
  comprare o vendere.

## 9. Mentore e analista immobiliare ✅
- **Mentore:** percorso a livelli nel vault (`Immobiliare/Percorso di studio.md`):
  €/m², comparabili, rendimento, cash flow (soldi che entrano meno quelli che escono),
  mutuo, fisco.
- **I tuoi immobili:** registrati **solo sul PC**, mai nella memoria né in chat
  (aggiungi, modifica, rimuovi, elenca).
- **Patrimonio:** valore totale, debito, valore netto, flusso mensile e rendimento.
- **Confronto affitti:** tu gli passi 2-3 annunci simili e lui suggerisce un canone e
  una fascia di prezzo, confrontati col canone attuale. Gli annunci non li prende da solo
  dai portali (Immobiliare.it e Idealista bloccano i programmi automatici e lo vietano):
  la ricerca automatica da dati ufficiali è un'idea futura (C.4).
- **Scenari "e se…":** cosa cambia se variano valore, canone, spese o mesi di sfitto.
  Sono sempre ipotesi, mai previsioni.

## 10. Baba proattivo (fa le cose da solo, a orari fissi)
Funziona solo se Baba è acceso. Ogni avviso viene salvato in `data/` e mandato
sull'iPhone. Se non c'è niente di nuovo, non ti disturba.
⚠️ **Scoperto il 01/10:** dal 18/09 nessun lavoro era mai partito da solo (Baba spento a
questi orari). **Risolto il 01/10 (D.1):** avvio automatico all'accensione + **recupero**:
se accendi il PC dopo l'orario di un lavoro, quello di oggi parte comunque appena Baba è
pronto (briefing fino alle 13, riepilogo mail fino alle 17, market-scout e notizie fino
alle 22; il controllo delle regole a ogni accensione). Ogni lavoro gira al massimo una
volta al giorno. Il risultato vero si vedrà dalle prossime accensioni.
💶 **Costo:** briefing e riepilogo mail usano Claude (Sonnet). Stima: circa 0,25-0,30 $ al
giorno, cioè 7-9 € al mese, se il PC è acceso ogni giorno. Gli altri lavori sono gratis.
| Ora | Cosa | |
|---|---|---|
| 07:45 | Market-scout: nuovi segnali di mercato (gratis, senza Claude) | ✅ |
| 08:30 | Briefing del mattino: meteo (Cordenons), agenda, mail importanti, regole e watchlist | ✅ |
| 12:30 | Riassunto delle email importanti non lette | ✅ |
| 18:00 | Notizie dei titoli in watchlist (gratis, senza Claude) | ✅ |
| ogni 3 ore | Controllo delle tue regole di prezzo (gratis, senza Claude; avvisa solo se ne scatta una) | ✅ |

## 11. Volto e voce (HUD) ✅
Provato da te nell'app vera il 01/10 (chat con la sfera, voce, tendina, mouse).
- **Sfera di particelle** creata dalla tua immagine di Higgsfield, con movimento continuo.
  Mentre Baba risponde si "sfalda" e poi si ricompone. Le particelle vicine al mouse si
  spostano e poi tornano al loro posto.
- **Sfondo pulito:** solo la sfera e un orologio piccolo. La HUD completa (scritte,
  scan-line, ecc.) si può riattivare.
- **Le risposte appaiono parola per parola** e le particelle "atterrano" sul testo.
- **Risposta a voce** (voce Microsoft Edge Remy, multilingue, scelta da te) con il
  pulsante Voce on/off. Se la voce Edge non va, usa quella di Windows. La sfera "respira"
  seguendo la voce.
- **Accento italiano** 🔶 (05/10): il testo viene dichiarato italiano al servizio della
  voce (prima edge-tts lo dichiarava sempre inglese, e a volte Remy parlava con accento
  inglese); il tuo nome è letto come "Gabrièle". Scelto da te a orecchio (prova
  `voci_prova/nome2/5`). Il servizio gratuito non permette di marcare le singole parole
  inglesi né di dettare la pronuncia esatta (provato e rifiutato).
- **Tendina "Trascrizione"** in alto a destra con le ultime domande e risposte.
- Limiti: non c'è **ascolto dal microfono** (non hai un microfono). Le voci Edge ti
  sembrano poco naturali (da migliorare, B.1).

---

## Cosa Baba NON fa (ancora)
Non invia email, non sposta o rinomina file, non guarda immagini o foto, non ha una lista
di cose da fare (to-do), non ascolta dal microfono, non è
collegato ai tuoi database né all'IoT, non sceglie Haiku per le domande semplici.
Tutto questo è in `docs/BABA_FUTURO.md`.

---

## Registro novità (la più recente in alto)
| Data | Novità |
|---|---|
| 05/10/2026 | Voce: testo dichiarato italiano (meno accento inglese, "Gabriele" detto all'italiana) |
| 05/10/2026 | Scrive dentro Word ed Excel (crea, aggiunge, sostituisce, scrive celle, grafici) con copia di sicurezza (A.7.1) |
| 05/10/2026 | Stampa PDF corretta (comando diretto ad Acrobat) e controllo della coda di stampa |
| 05/10/2026 | Ricerca file per nome approssimativo e veloce; Baba.vbs si aggiorna da solo dopo un cambio di codice |
| 05/10/2026 | Stampa con conferma, allegati email salvati, conversione in PDF (C.9, C.10) |
| 01/10/2026 | Avvio automatico all'accensione (nascosto) + recupero dei lavori persi + Spegni/Riavvia Baba (D.1) |
| 01/10/2026 | Presentazioni PowerPoint moderne: 9 tipi di slide, transizione Morph, animazioni d'entrata (A.7.1 passi 1-2) |
| 01/10/2026 | Crea presentazioni PowerPoint con design curato (A.7.1 passo 1, prima versione) |
| 01/10/2026 | Ricerca approfondita rifinita: testo pulito, PDF online, sottodomande, passaggi pertinenti (Z.1) |
| 01/10/2026 | Tendina "Trascrizione" + risposta a voce (edge-tts) con la sfera che segue la voce |
| 01/10/2026 | Nuova sfera dalla tua immagine, sfondo pulito, parole che appaiono, mouse come "sensore", effetto "sfaldamento" |
| 01/10/2026 | Lettura documenti: PDF / Word / Excel / PowerPoint e altri (anydoc, sul PC) |
| 01/10/2026 | Calendario con account "robot": niente più riautorizzazione ogni 7 giorni |
| 21/09/2026 | Ricerca approfondita `deep_research` (da rifinire) |
| 21/09/2026 | Prima sfera di particelle su tua foto di riferimento, scan-line, orologio (poi sostituita il 01/10) |
| 18/09/2026 | Baba diventa un'app: doppio clic su `Baba.vbs`, avvio di tutto in un colpo, finestra nativa |
| 18/09/2026 | Sfera HUD collegata al cervello (Tappa 7.3) |
| 18/09/2026 | Market-scout (SEC EDGAR + notizie → avviso sul telefono) |
| 18/09/2026 | Accesso a internet: ricerca web e lettura pagine |
| 18/09/2026 | Baba proattivo: briefing, avvisi, notifiche sull'iPhone via ntfy (Tappa 6) |
| 18/09/2026 | Immobiliare completo: mentore, immobili, patrimonio, affitti, scenari (Tappa 5) |
| 17/09/2026 | Finanza: watchlist + notizie, regole + backtest (Tappa 4.4-4.5) |
| entro 03/07/2026 | Quotazioni di mercato + modalità mentore di finanza (Tappa 4.1-4.2) |
| entro 03/07/2026 | Cervello, Gmail, Calendario, file, app, memoria, Obsidian (Tappe 0-3) |
