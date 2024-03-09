---
title: "Le basi di git"
description: "Una carrellata iniziale per imparare git nel migliore dei modi con tanti approfondimenti"
publishDate: "8 Mar 2024"
tags: ["git", "basics", "versioning"]
---

## Introduzione al versioning

Il software attraversa molteplici fasi di sviluppo e versioni, dal momento della modifica del file sorgente fino alla creazione di versioni di test, alpha, beta e finali. Queste versioni vengono create per diverse piattaforme e per diversi rilasci di prodotto.

Il versionamento del codice gestisce e **tiene traccia** di queste diverse versioni, consentendo il **recupero** di versioni precedenti per risolvere eventuali bug introdotti nelle versioni più recenti e la gestione di più versioni in contemporanea.

Questi strumenti agevolano lo **sviluppo collaborativo** e la gestione di documenti e programmi, estendendosi anche a file binari come le immagini. Il versionamento del codice è una pratica comune e utile non solo per il codice sorgente, ma per l'intera base di codice, inclusa la documentazione e i file di configurazione.

### Tipi di sistemi di versionamento

Esistono diversi sistemi per il controllo di versione(version controlsystems-**VCS**):

- **Locali**: mantengono un archivio dei cambiamenti del software sul computer usato per lo sviluppo. Hanno il vantaggio di essere molto **facili** da usare perché non è richiesta nessuna attività al programmatore, ma lo svantaggio di **non consentire la collaborazione** con altri utenti, la mancanza di sicurezza dato che non offrono una funzione di backup e il fatto che la storia della codebase è vista file per file, **senza la possibilità di sapere quali file fossero in quale versione** in un certo momento dello sviluppo.

- **Centralizzati**: sono gli strumenti più "tradizionali", come **CVS** o **Subversion**.
  L'archivio è mantenuto su di un **server centrale**, mentre gli sviluppatori lavorano su una copia locale di uno degli stati del software.
  Si usano delle operazioni di **checkout** per prelevare uno stato del sistema dal server(es.la versione più recente), e con un'operazione di **commit** si inviano le proprie modifiche per aggiornare lo stato sul server.

- **Distribuiti**: sono i sistemi, come **Git** o **Mercurial**, in cui **il sistema locale ha una copia completa** della storia dello sviluppo, per cui si può lavorare con sistema diversionamento anche senza connessione. Dato che sono distribuiti non si ha più un server centrale di riferimento se non per convenzione comune.

## Hello git: workflow di base

Git è un software che permette di **tenere traccia** dei cambiamenti fatti su un progetto nel tempo. Git ricorda ogni modifica, tenendone traccia e dando la possibilità di **accedere ad ogni versione** salvata del progetto.

### I 3 stadi di un progetto git

Possiamo semplificare (di molto) il workflow di git dividendolo in 3 parti:

1. Effettuo delle modifiche al progetto (aggiunta/rimozione/modifica di files).
2. Aggiungo le modifiche alla lista di modifiche pronte per essere "committate" (detta **staging area**).
3. Salvo i cambiamenti in una **commit**, le commit vengono conservate nella **git repository**.

![Git states](./images/01.webp)

> La Working Directory è quindi la directory del progetto nello stato attuale

```sh
# Primo utilizzo di git: configurare i dati relativi all'autore
git config --global user.name "Nome Cognome"
git config --global user.email indirizzo@ema.il

git init # init = initialize, inizializza tutti gli strumenti necessari al versioning (nella cartella .git)
git status # Visualizza lo stato del branch
git add <filename> # Aggiunge le modifiche relative al file/ai file alla staging area sopra citata
git add <filename> <otherFilename> ... # Posso specificare anche più di un file alla volta
git add -A # Aggiunge tutte le modifiche pendenti alla staging area
git commit -m"<comment>" # Salva permanentemente come commit le modifiche
git commit --amend -m"<comment>" # Sovrascrive l'ultima commit effettuata, utile per mantenere la history pulita e chiara in caso di piccole sviste
```

Convenzioni riguardanti i commenti:

- Dovrebbero essere in [Present Tense](https://learnenglish.britishcouncil.org/grammar/english-grammar-reference/present-tense)
- Non dovrebbero superare i 50 caratteri

![Git screenshot 1](./images/02.avif)

> I files in verde sono gli staged files, quelli rossi sono quelli in attesa di essere aggiunti alla staging area

> Al posto dei nomi dei files volendo si possono usare le [wildcards](https://www.tecmint.com/use-wildcards-to-match-filenames-in-linux/) offerte da bash!

### git diff: vedere le modifiche effettute

Git ci permette di vedere le **differenze** tra i files della working directory e la staging area (molti editor/IDE supportano Git e forniscono uno strumento grafico per vedere questo, naturalmente essi si appoggiano al comando fornito da git).

```sh
git diff <filename> # Visualizza la lista dei cambiamenti di un file rispetto alla staging area
```

![Git screenshot 2](./images/03.avif)

### git log & git blame: lo storico

Le commit possono essere viste grazie ad uno **storico** (come vedremo, lo storico può essere sia locale che remoto).<br>
È inoltre possibile per ogni riga di ogni file **sapere chi** (ed in quale commit) ha effettuato l'ultimo cambiamento a quella riga.

```sh
git blame <filename> # Stampa ogni riga del file, con hash autore e data dell'ultima commit che ha avuto a che fare con quella riga
git log # Stampa a video lo storico delle commit
git log --pretty=oneline # Stampa le commit in formato abbreviato, facendo occupare una sola riga per commit
git log --graph # Stampa a terminale le commit con un grafo che fa capire lo stato dei vari branch
```

Screenshot di una sezione dello storico in modalità grafo:

![Git screenshot 3](./images/04.avif)

> In arancione possiamo vedere un codice alfanumerico di 40 caratteri, questo è l'hash o SHA della commit e viene usato come identificativo per riferirsi alla commit.
