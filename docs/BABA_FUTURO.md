# Baba — Idee per il FUTURO (unico elenco)

In questo file c'è **tutto quello che abbiamo pensato per Baba ma che non è ancora fatto**.
Quello che Baba sa già fare sta in **`docs/BABA_OGGI.md`**.

**Come si usa:** apri Baba in Claude Code e di' per esempio *"lavoriamo alla A.1"*.
Lavoriamo un pezzo alla volta: si costruisce, tu lo provi, poi si passa al successivo.
Quando un'idea è finita, **esce da qui** e va in `BABA_OGGI.md`.
"Possiamo fare X?" è una domanda, non un via: Claude risponde (si può fare? come? quanto
costa? a quale voce corrisponde?) e aspetta il tuo "fallo".

*Ultimo aggiornamento: 01/10/2026. Questo file riunisce i vecchi IDEE_FUTURE.md,
FUTURO.md e CAPABILITIES.md.*

---

## ⭐ Ordine consigliato
**Gli ordini originali che avevi deciso:**
- Priorità generale: **A.1** (ricerca approfondita) e **A.2** (memoria per significato).
- Office (A.7.1): PowerPoint passo 1 → Word → Excel → animazioni avanzate.
- Sezione G: **G.1 → G.14 → G.15 → G.8 + G.3 → G.9**.
- Lavoro (F): schede clienti + cose da fare → ore, preventivi, fatture → tasse.

**La mia proposta per unirli (01/10, la decidi tu):**
1. ~~**Z.1 / A.1** Chiudere la ricerca approfondita~~ ✅ FATTO 01/10
2. ~~**Z.2** Collaudi veloci rimasti a metà~~ ✅ FATTO 01/10
3. ~~**A.7.1** PowerPoint passi 1-2~~ ✅ FATTI e provati da Gabriele 01/10
3b. ~~**D.1** Avvio automatico~~ ✅ costruito 01/10 (anticipato su scelta di Gabriele)
4. **A.2** Memoria per significato
5. **G.1 → G.14 → G.15 → G.8 + G.3 → G.9** (nell'ordine originale)

---

## Z. Lavori lasciati a metà (da chiudere prima di aprirne di nuovi)
1. ~~Ricerca approfondita (A.1)~~: FATTA e provata da Gabriele il 01/10 → ora in BABA_OGGI.
2. ~~Collaudi tuoi~~ (calendario in scrittura, market-scout, sfera, voce): FATTI e
   superati il 01/10 ✅.

---

## A. Un cervello più capace
> Nota onesta su "Baba quasi infinito": il cervello è Claude via API, e quella è
> l'intelligenza massima. "Più IA" non vuol dire renderlo più intelligente del modello, ma
> dargli **più strumenti, una memoria migliore e più autonomia** per fare da solo lavori
> a più passi. Così *quello che può fare* diventa quasi illimitato, restando onesto sui
> limiti.

1. ~~Ricerca approfondita~~: FATTA il 01/10, ora è in BABA_OGGI (sezione 6).
2. **Memoria semantica (embeddings)**: oggi la memoria (`memory/rag.py`, ricerca FTS5)
   cerca le **parole uguali**. Con gli embeddings (testo trasformato in numeri che ne
   rappresentano il significato) cercherebbe per **significato**: ricorda anche se lo dici
   in un altro modo. Permetterebbe anche domande come "cosa avevamo deciso su X la
   settimana scorsa?" sulle chat passate, e di costruire nel tempo un tuo profilo
   (progetti, contatti, abitudini). Si può fare con un modello locale (gratis) o via API.
   Ottima per lo studio di finanza e immobiliare e serve per G.11. Nota tecnica: era
   prevista già nella Tappa 3.1 ma non è stata fatta; nel database (`memory/schema.sql`)
   la colonna `embedding` è pronta ma vuota.
3. **Routing dei modelli**: ⚠️ i vecchi file dicevano che c'era già ("Haiku per il
   semplice"), ma il controllo sul codice (01/10) dice di no: Baba risponde **sempre con
   Sonnet**, perché la regola in `core/agent_loop.py` sceglie Haiku solo se non ci sono
   strumenti, e gli strumenti ci sono sempre. Haiku lavora solo per scegliere cosa
   ricordare. Idea: Haiku per le domande semplici (risparmio), Sonnet per il normale,
   Opus per i casi davvero difficili. Più bravo dove serve, economico dove no.
   **Risparmio collegato (idea del 01/10): "prompt caching".** Ogni chiamata a Claude
   rimanda le istruzioni di tutti gli strumenti (~7.000 token, misurato il 01/10). Con il
   caching, dalla seconda chiamata in poi quella parte costa circa un decimo. Utile
   soprattutto ora che briefing e riepilogo mail girano ogni giorno (stima 7-9 €/mese).
4. **Vista (immagini e .jpg)**: mandi una foto (bolletta, grafico, annuncio immobiliare) e
   Baba la legge e la analizza.
5. ~~Documenti~~: FATTO il 01/10/2026, ora è in BABA_OGGI (anydoc).
6. **Sotto-competenze**: comportamenti specializzati (un "analista", un "pianificatore")
   che il cervello richiama quando servono, senza complicare l'architettura di base.
7. **Skill per Baba (competenze caricabili)**: una cartella di skill (file `SKILL.md`
   con metodi da esperto scritti come testo) dentro Baba, più uno strumento che carica
   **solo quella che serve, quando serve**, così costa token solo in quel momento.
   Esempio: con le skill di marketing (marketing-skills, licenza MIT, da citare l'autore)
   Baba prepara campagne, landing page e piani per la consulenza o l'agenzia. Ogni nuova
   skill è una nuova competenza: Baba diventa espandibile un pezzo alla volta.

   **A.7.1 — Baba "fortissimo" in PowerPoint, Word ed Excel** (tua richiesta del
   01/10/2026). Oggi Baba sa solo **aprire** i programmi; deve saper anche **creare e
   compilare** i file da solo ("fammi una presentazione sulla storia della Juventus", "un
   Excel delle spese con grafico", "una lettera o relazione in Word").
   - Metodo: Claude scrive solo i contenuti in forma ordinata, Python costruisce il file
     con un design curato, lo salva in `Documenti\Baba\...` e lo apre.
   - Il codice viene preso o adattato da progetti GitHub con licenza adatta e integrato
     come strumenti **dentro Baba**: non sono skill di Claude Code (è la differenza tra
     muratore e casa).
   - Il Python di Baba è la versione 3.14: va bene per tutte le librerie qui sotto.
   - **PowerPoint**
     - Base: `python-pptx` (MIT).
     - Animazioni (python-pptx da solo non le fa): `BramAlkema/pptx-animation-skill`
       (AGPL-3.0: va bene per uso personale, diventa un vincolo solo se si distribuisce
       Baba). Fa entrate/uscite (16 effetti), enfasi e **percorsi di movimento**, tutti
       verificati in PowerPoint.
     - `hugohe3/ppt-master` (MIT, ~50.000 stelle su GitHub) come riferimento e codice
       per transizioni, **Morph**, grafici, tabelle e narrazione.
     - La skill `morph-ppt` per gli effetti Morph.
     - Interattività: indice con pulsanti cliccabili e "torna all'indice".
     - Passi: 1) slide + design + salva e apri (✅ costruito il 01/10:
       `tools/native/presentation.py`, strumento `create_presentation`; rifatto lo stesso
       giorno perché Gabriele lo trovava "troppo basilare")
       → 2) animazioni e transizioni (✅ in parte il 01/10: transizione Morph + entrata
       "fluttua dentro" degli elementi, scritte in XML Office da noi, senza copiare codice
       AGPL; restano le animazioni avanzate: percorsi di movimento, enfasi)
       → 3) indice cliccabile → 4) immagini da fonti libere (Wikimedia; niente loghi o
       foto protette). Passi 1-2 provati da Gabriele il 01/10 ✅.
   - **Word** ✅ costruito il 05/10 (`tools/native/word.py`, python-docx; provato da Gabriele ✅)
     - Base: `python-docx` (MIT).
     - `python-docx-template` (MIT): modelli con spazi da riempire (lettere, preventivi,
       relazioni).
     - `ruwadgroup/docxengine` (Apache-2.0): pensato per agenti IA, legge e modifica un
       Word senza rovinarlo, gestisce revisioni e commenti, esporta in PDF.
     - Usi: lettere, relazioni, verbali, preventivi da modello.
   - **Excel** ✅ costruito il 05/10 (`tools/native/excel.py`: openpyxl per creare, Excel via COM per modificare i file esistenti senza perdere grafici/pivot; provato da Gabriele ✅)
     - `XlsxWriter` (BSD) per creare file belli: formati, formattazione condizionale,
       **grafici**, filtri, righe e colonne bloccate.
     - `openpyxl` (MIT) per leggere e modificare file esistenti.
     - `knowledgestack/excel-parser` (MIT) per far **capire** a Baba un Excel complesso
       (formule, dipendenze, grafici).
   - ⚠️ NON usare le skill ufficiali Anthropic docx/xlsx/pptx: sono "source-available",
     non open source (vietato copiarle dentro Baba).
   - Ordine: PowerPoint passo 1 → Word → Excel → animazioni avanzate. Ogni pezzo viene
     costruito, provato da te, poi si passa al successivo.
8. **IA di riserva sul PC** (es. Ollama): una seconda IA piccola installata sul PC.
   - Pregi: gratis, offline, illimitata, i dati non escono dal PC. Entra in gioco **solo
     se Claude non risponde** (credito finito, rete assente o guasto di Anthropic), così
     Baba non resta muto.
   - Limiti: molto meno intelligente di Claude, più lenta, dipende dalla scheda video del
     PC, occupa alcuni GB.
   - Regole: Baba dice quando sta rispondendo la riserva. Finanza, immobili e analisi
     restano **solo con Claude**; con la riserva Baba risponde "riprova più tardi".
   - Il tuo PC (dati del 01/10/2026): GTX 1060 6 GB, i5-7400, 8 GB di RAM, ~28 GB
     liberi. Sulla carta regge modelli piccoli che sanno usare strumenti (Qwen3 4B comodo,
     Qwen3 8B al limite). Prima di costruirla: provare davvero che il PC regga un modello
     locale.
   - Non è urgente finché c'è credito API, con ricarica automatica e un tetto mensile.
9. **Più IA dentro Baba (catena di IA con API gratuite)**: oltre a Claude, collegare IA
   online con piano gratuito che si danno il cambio. Se una finisce i messaggi gratis (o
   non risponde), Baba passa alla successiva: token "praticamente infiniti" per uso
   personale.
   - Variante consigliata: **gratis per le cose semplici, Claude per quelle difficili**.
     Risparmia credito senza perdere qualità e si lega ad A.3.
   - Candidati (limiti del 2026, da ricontrollare quando si costruisce):
     - Google Gemini Flash: piano gratuito, senza carta.
     - Groq: 30 richieste al minuto, ~1.000 al giorno sui modelli migliori.
     - OpenRouter: 25+ modelli gratis, 50 richieste al giorno; 1.000 dopo aver caricato
       10 $ di credito una volta sola.
     - Mistral, Cerebras.
     - Molti usano il "formato OpenAI": un solo adattatore ne copre tanti.
   - Regole:
     - **Privacy**: i piani gratuiti possono usare i messaggi per addestrarsi, quindi
       email, calendario, finanze e immobili vanno **solo su Claude** (o su un servizio
       che garantisce di non addestrarsi sui dati). Le cose generiche (web, spiegazioni,
       chiacchiere) possono andare anche sulle IA gratis.
     - Il mentore di finanza resta su Claude.
     - Baba dice quale IA ha risposto.
     - **Un account per servizio**: niente account multipli per aggirare i limiti.
   - Lavoro: un adattatore e un "commutatore" nel cervello (`core/agent_loop.py`),
     qualche sessione.

## B. Rifiniture di quello che c'è
1. **Voce più naturale**: le voci Edge non ti convincono. Da valutare **Google Chirp 3 HD**
   (hai già un progetto Google, 1 milione di caratteri al mese gratis) oppure ElevenLabs
   (spazio per la chiave già previsto in `.env.example`) o Azure.
2. **Sfera HUD**: rifinitura continua di colore, densità e reattività. Modalità **"solo
   voce"** (l'alternativa C dell'HUD): nessun testo a schermo, la sfera pulsa ed espande
   seguendo il ritmo della voce.
3. **Market-scout**: aggiungere la fonte **brevetti** (USPTO/PatentsView, chiave gratuita;
   EPO europeo a chiave, opzionale e in coda) e la fonte **finanziamenti alle startup**
   (TechCrunch RSS gratis; Crunchbase a pagamento, opzionale). Attivare il
   **voto utile/rumore** su ogni segnale per affinare i filtri col tempo (la tabella
   `signal_feedback` è già pronta). Piano originale nel vault: "Finanza/Market-scout
   (piano)".
4. **Google senza riautorizzare Gmail**: oggi l'app Google è in modalità "Test" e il
   permesso Gmail scade circa ogni 7 giorni. "Pubblicare" l'app su Google eviterebbe di
   rifarlo (opzionale).
5. **Robustezza**: errori gestiti meglio, qualche test automatico, log più leggibili.

## C. Nuove capacità
1. **Lista di cose da fare vera** (oggi manca): impegni ("mandare la proposta a Rossi
   entro venerdì") che entrano nel briefing del mattino e arrivano come promemoria. Anche
   "trasforma questa nota in un compito".
2. **Calendario più furbo**: trovare gli orari liberi, promemoria, "preparami per domani"
   (agenda più note collegate).
3. **Indicatori tecnici** per le regole (es. incrocio delle medie mobili), rinviati finché
   non li avrai studiati.
4. **`rent_benchmark(comune)`** (immobiliare, chiesto il 18/09): canone medio €/m² di zona
   preso in automatico dai **dati ufficiali OMI** (Agenzia delle Entrate). NON dai portali
   di annunci: Immobiliare.it e Idealista bloccano i programmi automatici e i loro
   termini d'uso lo vietano. Da costruire insieme alle "fonti esterne" di market-scout.
5. **Fonti di mercato in tempo reale** (a pagamento, con chiave), quando servirà.
6. **Ascolto dal microfono** (Tappa 7.1), se un giorno avrai un microfono. Il 18/09
   avevamo deciso di usare il riconoscimento vocale **del browser** (Web Speech, zero
   installazioni). L'alternativa è Whisper sul PC (le librerie sono già segnate,
   commentate, in `requirements.txt`). Avvio con una parola di attivazione o con un tasto.
7. **Gestione file**: spostare e rinominare, sempre solo dentro le cartelle autorizzate
   (si lega a G.4). Eventualmente lanciare **script autorizzati** (mai comandi liberi).
8. **Musica**: far partire un brano o una playlist su Spotify (oggi apre solo l'app).
9. ~~Stampa di documenti e allegati email~~: FATTA il 05/10 (richiesta di Gabriele, fatta
   subito prima della A.2) → ora in BABA_OGGI. Possibile miglioria: SumatraPDF (gratis)
   per stampare i PDF senza che si apra Acrobat.
10. ~~Trasformare Word/Excel/PowerPoint/immagini in PDF~~: FATTA il 05/10 → BABA_OGGI.

## D. Autonomia e app
1. ~~Avvio automatico all'accensione~~: FATTO il 01/10 (nascosto, con recupero dei lavori
   persi; manca solo la prova di Gabriele al prossimo riavvio del PC) → ora in BABA_OGGI.
   Resta da valutare un'**icona vicino all'orologio** di Windows (nella barra in basso) per
   vedere che Baba è acceso e aprirlo/spegnerlo con un clic.
2. **Un unico file `.exe`** installabile.
3. **Più lavori automatici**: controllo delle scadenze, avvisi personalizzati, controllo
   che Baba stia funzionando bene ("salute del sistema").
4. **Trasloco di Baba su un altro PC**: procedura pronta (tenuta in privato, perché
   elenca i file con chiavi e dati personali).

## F. Baba per il lavoro (idee per una futura attività da consulente)
Non è in costruzione: si riprende quando servirà.

**Cosa fa già oggi Baba per un consulente:**
- Email dei clienti: riassunto della posta alle 12:30 con le cose urgenti, bozze di
  risposta (le invii tu).
- Agenda: fissa e sposta appuntamenti e call; briefing del mattino sulla giornata.
- Documenti: legge e riassume contratti, preventivi ricevuti, bandi, report (PDF, Word,
  Excel). Es. "cosa dice la clausola di recesso?".
- Ricerche: settore del cliente, concorrenti, normative, con le fonti.
- Note per cliente su Obsidian: appunti delle riunioni, decisioni, cose da ricordare.
- I tuoi soldi: mentore per investire i guadagni (insegna, non promette rendimenti).

**Cosa aggiungere (in ordine di utilità):**
1. **Schede clienti** (piccolo gestionale, sul PC): contatti, storico, progetti, prossimi
   passi. Prima di una call, Baba prepara un riassunto mettendo insieme email, agenda e
   note.
2. **Cose da fare**: è la stessa idea di C.1.
3. **Ore e preventivi**: "ho lavorato 3 ore per X" e Baba lo registra; a fine mese sai
   quanto hai lavorato e fatturato per cliente. Preventivi da un tuo modello (usa A.7.1
   Word).
4. **Fatture e incassi**: registro delle fatture emesse, scadenze di pagamento,
   **solleciti in bozza** per chi non ha pagato. La fattura elettronica vera (SdI,
   Agenzia delle Entrate) si potrà collegare più avanti a un servizio tipo Fatture in
   Cloud. Baba **non invia mai niente senza la tua conferma**.
5. **Tasse da accantonare** (es. regime forfettario): stima di quanto mettere da parte
   tra tasse e contributi INPS, controllo della soglia annua di ricavi, **scadenze
   fiscali** in calendario. È solo una **stima**: aliquote e regole vanno verificate ogni
   anno con il commercialista (Baba non lo sostituisce).
6. **Marketing per farti conoscere** (skill A.7): post LinkedIn, proposte commerciali,
   presentazione dei tuoi servizi.
7. **Baba dal telefono (Telegram)**: per scrivergli, non solo per ricevere avvisi. Es. da
   un cliente scrivi "segna 2 ore per Bianchi" o "che appuntamenti ho dopo?". Risponde
   solo a te e non apre porte sul PC. Il file `channels/telegram.py` c'è già come base.
8. **Riassunti delle riunioni** (con la voce, più avanti): registri la call, Baba scrive
   il verbale e una mail di follow-up in bozza.
9. **Modelli da offrire ai clienti** (idea dell'"agenzia" dal piano originale):
   - documenti automatici: legge un documento, ne estrae i dati, riempie un modello e
     produce un Word o un PDF;
   - smistamento email riutilizzabile per ogni cliente;
   - assistente clienti "sui documenti": carichi i documenti di un cliente e Baba risponde
     usando quelli.

Ordine: schede clienti + cose da fare → ore, preventivi e registro fatture → tasse e
scadenze. Con i primi tre è già un vero "assistente da ufficio".

**Regole specifiche per il lavoro:**
- **Dati dei clienti sul PC** (come gli immobili): mai in chat, mai a servizi esterni
  senza motivo e senza il tuo consenso.
- **Niente azioni irreversibili da solo** (inviare email o fatture, pagare): sempre bozza
  più tua conferma.
- **Fisco = stime, non consulenza**: Baba calcola e ricorda, il commercialista decide.
- **Costi bassi**: conti, scadenze e soglie in Python gratis; Claude solo per scrivere e
  ragionare.

## G. Baba super efficiente (idee del 01/10/2026)
**Vita quotidiana**
1. **Sempre a portata di tasto**: una scorciatoia globale (es. Ctrl+Spazio) apre una
   mini-barra sopra qualsiasi finestra. Scrivi "ricordami di pagare l'affitto il 5" e
   torni al lavoro. È l'idea che fa risparmiare più tempo.
2. **Testo selezionato → Baba**: evidenzi un testo ovunque (email, sito, PDF) e premi un
   tasto; Baba lo riassume, traduce, corregge o prepara una risposta.
3. **Scadenziario di vita**: bollo, revisione, assicurazione dell'auto, documenti in
   scadenza, abbonamenti, garanzie; avviso qualche giorno prima.
4. **Archivista automatico**: cartella "Da archiviare". Baba rinomina e sposta bollette,
   ricevute e PDF nella cartella giusta e ne legge importo e scadenza (che finiscono
   nello scadenziario). Sicurezza: spostamenti solo dentro le cartelle autorizzate.
5. **Spese e abbonamenti**: importa l'estratto conto (CSV, sul PC) e ti dice quanto spendi
   e in cosa, quali abbonamenti hai attivi, con un budget. Si lega al mentore: prima
   risparmiare, poi investire.
6. **Riassunto di video e articoli**: dai un link YouTube o un articolo lungo e ottieni 5
   punti chiave, salvabili in Obsidian.
7. **Revisione della sera e della settimana**: la sera, cosa è fatto, cosa resta e cosa
   c'è domani; la domenica, un bilancio della settimana. Completa il briefing del mattino.

**Lavoro**

8. **Follow-up ("in attesa di")**: Baba guarda le email inviate; se qualcuno non risponde
   entro X giorni, te lo ricorda e prepara il sollecito in bozza.
9. **Routine**: sequenze di lavori lanciate con una frase. Es. "fine mese" (riepilogo
   ore, bozze di fatture, solleciti), "lunedì" (agenda della settimana, cose da fare,
   email arretrate). Si creano una volta e si riusano sempre.
10. **Scrive come te**: impara il tuo stile dalle email inviate (sul PC) e prepara bozze
    che sembrano tue.
11. **Ricerca in tutti i tuoi file**: "dove ho messo il contratto di Rossi?", "il
    preventivo con lo sconto del 10%". Cerca anche nei documenti sul PC, non solo nel
    vault (usa A.2).
12. **Giornata a blocchi**: dalle cose da fare e dal calendario propone blocchi di tempo
    ("9-11 proposta Rossi, 14-15 email") da mettere in agenda.
13. **Sorveglia pagine web**: annunci immobiliari in zona sotto X €/m², bandi e
    finanziamenti, il prezzo di un prodotto; avviso quando cambia qualcosa. Il controllo
    lo fa Python gratis, Claude interviene solo per il riassunto.

**Fondamenta (rendono Baba affidabile)**

14. **Backup automatico**: vault Obsidian più dati (immobili, regole, memoria), di notte,
    sul PC o su una chiavetta. Da fare PRIMA di riempire Baba di dati.
15. **Contatore della spesa API**: nel briefing, quanto hai speso ieri e nel mese, con un
    avviso se superi il budget.
16. **Avvisi più intelligenti**: notifiche raggruppate, ore di silenzio (es. 22-7),
    subito solo l'urgente.
17. **Diario delle azioni**: "cosa hai fatto oggi per me?", cioè l'elenco di cosa Baba ha
    letto, creato o modificato. Dà fiducia e aiuta a capire i problemi.

**Ordine originale della sezione G (più resa con meno fatica):** 1 (a portata di tasto)
→ 14 (backup) → 15 (contatore spesa) → 8 + 3 (follow-up e scadenziario) → 9 (routine).

## H. Le tue cose (Tappa 8, opzionale)
1. **Database in sola lettura**: un server dedicato collega Prodactivity (SQL Server) e la
   tua app PostgreSQL. Es. "quanti ticket aperti in Prodactivity?" dà il numero vero.
   Poi report, grafici ed esportazioni dai dati, anche programmati (utile anche per la
   consulenza alle piccole e medie imprese: cruscotti e report automatici). Un numero dal
   database può entrare anche nel briefing del mattino. Il file base
   `mcp_servers/db_server.py` c'è già (con query di esempio). Sicurezza: solo query
   "con nome" scritte prima, mai SQL libero, sola lettura, credenziali in `.env`.
2. **Ponte IoT**: leggere Node-RED/MQTT (es. il sensore HC-SR04 dello scaffale: "qual è la
   distanza dello scaffale ora?"), far partire i flussi Node-RED e avvisare quando un
   valore supera una soglia. Il file da costruire è `mcp_servers/iot_server.py`.
3. **Postazione da sviluppatore**: stato e storico di git, lanciare i test, preparare
   codice, avviare Claude Code per un lavoro di sviluppo.

---

## E. Regole d'oro (valgono per ogni idea)
- **Confine onesto**: Baba calcola, contestualizza e insegna. Non prevede e non garantisce
  guadagni.
- **Privacy**: i dati sensibili (immobili, clienti, finanze) restano sul PC.
- **Costi bassi**: il lavoro "stupido" lo fa Python gratis; Claude interviene solo quando
  serve ragionare o scrivere.
- **Niente azioni irreversibili da solo**: inviare, pagare e cancellare richiedono sempre
  la tua conferma.
- **Un pezzo alla volta**: si costruisce, si prova, poi si va avanti.
