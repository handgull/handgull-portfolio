---
title: "La mia roadmap"
description: "Quello che farei, e in che ordine lo farei se dimenticassi tutto quello che ho imparato"
publishDate: "28 Aug 2024"
tags: ["roadmap", "general"]
draft: true
---

## Non sono un guru

Parto col dire che non mi ritengo un guru della programmazione, cercherò solamente di dire (argomentando) secondo me cosa un completo neofita che voglia fare il mio stesso percorso (sviluppatore fortemente orientato al frontend web e mobile) dovrebbe studiare.

## Cosa si può saltare

C'è chi dice ai neoprogrammatori di cominciare dal C (un linguaggio di programmazione), io dico che dipende. Se il proprio obbiettivo è sviluppare software per IoT, sistemi operativi, cose appunto dove un linguaggio "di basso livello" che conferisca un controllo al dettaglio ad esempio per la gestione della memoria sia vantaggioso... allora sì, è bene partire dal C. Ma se l'obbiettivo è ad esempio lavorare come sviluppatore frontend si può benissimo evitare. È importante avere delle nozioni generali, ad esempio sapere cos'è un puntatore o come funziona un garbage collector. Ma non è necessario imparare linguaggi che poi non faranno mai parte degli strumenti quotidiani. (a meno che non ci siano da fare grandi computazioni, magari in web assembly).

## Setup iniziale

Installate sul pc il necessario per programmare, se volete sviluppare frontend web servono le seguenti cose:

- chrome (il mio browser preferito per gli strumenti da sviluppatore che fornisce)
- nodejs (un runtime, se non sapete cos'è scopritelo. In realtà all'inizio non vi servirebbe ma potrebbe tornare utile più avanti quando dovrete lavorare con i framework)

Se invece volete essere sviluppatori mobile io consiglio di studiare flutter e installare appunto Flutter, il sito ufficiale ha un ottima guida

Una cosa che hanno in comune entrambi gli ambiti (mobile e web. Ma in realtà praticamente qualsiasi programmatore ne ha bisogno), è l'IDE/editor: il luogo dove il programmatore scrive il codice. Io come editor uso Visual Studio Code. Sia con flutter che con le tecnologie web. (per alcune cose in realtà in flutter sarebbe meglio Android Studio)

## Sporchiamoci le mani

Seconda cosa... va studiata un po di teoria. Come funziona un computer a grandi linee? Cos'è il linguaggio macchina? Il computer come fa a capire il tuo codice sorgente? Cos'è un paradigma di programmazione? Scoprilo e scopri quanti ce ne sono. SPOILER js lo strumento principale di uno sviluppatore frontend abbraccia il paradigma funzionale ma è anche un linguaggio ad oggetti. Se dovessi sceglierne uno da approfondire prima degli altri sceglierei di approfondire il paradigma orientato agli oggetti, la OOP. Parole chiave da sapere PER FORZA sono ad esempio ereditarietà (e magari anche la composizione), l'incapsulamento, il polimorfismo, il significato di SOLID, il significato di LSP, e successivamente guardare i design patterns; ma solo dopo avere molta confidenza con la OOP. e prima di arrivarci bisogna studiare le basi dei linguaggi procedurali come cicli, condizioni... ecc.

Per dirla più facile: studiate js o dart partendo dalle basi dei linguaggi procedurali/imperativi per poi passare alla OOP ed ai design pattern (un concetto di ingegneria del software).

## Cosa è vitale sapere dopo aver imparato le basi

Appena dopo aver imparato a fare piccoli programmini funzionanti è importante imparare come versionare il proprio codice. Git è lo standard de facto. Ho scritto anche un articoletto sulle basi di git. A cosa vi servirà? A collaborare con i colleghi potendo lavorare in parallelo, a tenere traccia delle versioni, a volte aiuta a trovare i bug e molto altro. È VITALE IMPARARE GIT, e magari fatevi un profilo github.

## Altro studio

Ok, ora che abbiamo parlato dell'ABC e del versionamento è il momento di studiare i frameworks (che, se avete studiato in maniera approfondita i design patterns avrete già visto di cosa si tratta). I framework sono usati dagli sviluppatori per fare le cose più in fretta (e spesso anche meglio) di come farebbero se dovessero fare tutto a mano, cioè reinventando la ruota. A me come frameworks piacciono principalmente Angular e Flutter, a volte uso fastify o nestjs per il backend (essendo fortemente frontend uso js anche nel backend). È anche il momento per approfondire argomenti specifici dei linguaggi in questione. Closures, Prototyping, come funziona lo Scope, le Macros...

> NOTA: se volete essere sviluppatori mobile può esservi utile anche una base di come funziona il nativo perchè a volte bisogna toccare files nativi anche usando Flutter.

Ultima cosa utile... le basi del funzionamento del web. Cos'è il protocollo https, verbi http, codici http, SSL, TCP/UDP, Websockets... Il modello ISO/OSI, cos'è un API REST/graphql... la lista è molto lunga.

## Aumentare la produttività

È saggio (e io questo consiglio l'ho ignorato per anni) imparare bene le shotcuts e gli strumenti forniti dal proprio IDE/editor. Questo aumenta notevolmente la produttività. Meno toccate il mouse prima finite. Ci sono spesso anche estensioni che generano snippets di codice (evitano di scrivere cose ripetitive).

## Debug

Il debug è un arte, va imparata. Soprattutto con js si è tentati di printare in console e basta ma sforzatevi di imparare come mettere dei breakpoint e studiate i devtools forniti dal browser o da flutter.

## Non si arriva mai

Bhe siete condannati a studiare per sempre... è solo la punta dell'iceberg. Molte cose neanche le ho mai fatte... tipo non ho mai dovuto usare direttamente cose come la hydration di js, la concorrenza (l'avrò usata un paio di volte e non nel frontend) e molto altro. Si impara al bisogno o magari ci si porta avanti man mano dedicando ogni giorno qualche minuto alla formazione.

## Errori da evitare

Non scrivete codice brutto... ci sono mille modi per non farlo i due più importanti credo siano:

- DRY: Don't repeat yourself. Ovvero non sparpagliare in giro nell'app pezzi di codice uguali che fanno le stesse cose. Se un giorno dovesse cambiare la logica dell'app dovreste cambiarla in n posti.
- Astrazione: questo è un concetto più difficile, è da esperti. In sostanza tramite l'ingegneria del software ci sono accortezze che si possono prendere per rendere il codice facilmente intercambiabile. Se ad esempio si cambiasse database, o se si passasse da una REST API a graphql... o si decidesse di cambiare qualche libreria di terze parti un codice scritto bene permetterebbe queste cose in maniera indolore, in un brutto codice potrebbe rivelarsi un incubo.

## Libri che consiglio

A me piace molto imparare dai libri. Questi in particolare mi hanno reso un programmatore migliore:

- Design Patterns
- Pragmatic programmer (da per scontate alcune cose, non va letto da uno che si sta approcciando)
- Clean architecture (anche questo non da completi novizi)
