# HuntTheWumpus_App
Join backend and frontend projects into one :

- [Frontend Project (Android)](http://github.com/ivochan/WumpusWorldGame)
- [Backend Project (Java)](https://github.com/ivochan/HuntTheWumpusOrNot)



## Introduzione
Questa applicazione Android è ispirata al videogioco conosciuto con il nome di “Hunt the Wumpus”, realizzato nel 1972 da Gregory Yob. 
Si tratta di un gioco di avventura che si svolge in un labirinto, generato in maniera casuale e costituito da una serie di stanze, tra loro comunicanti se adiacenti.
Il giocatore interpreta il ruolo di un cacciatore che, durante l’esplorazione del dungeon, dovrà sopravvivere alle insidie disseminate lungo il percorso e cercare di individuare la tana del mostro, il Wumpus, senza rivelargli la propria presenza e rischiare di farsi uccidere.
Questo sarà possibile sfruttando le tracce disseminate per il labirinto, ovvero il cattivo odore emanato dal mostro, che giunge sino alle celle attigue alla sua tana. Questo indizio, nel gioco originale, veniva fornito mostrando nelle celle adiacenti delle macchie di sangue.
La sola possibilità che si ha di sfuggire al mostro è quella di ucciderlo scoccando una freccia, da una qualsiasi stanza adiacente a quella in cui è nascosto.
Inoltre, bisogna evitare le stanze con i pozzi, in cui si corre il rischio di caderci dentro, attigue alle celle da cui giunge la brezza che, sostituisce, nel gioco originale, la presenza del muschio.
Un ulteriore rischio, nel gioco di Yob, è costituito dai super-pipistrelli, che possono catturare il giocatore e rilasciarlo in una stanza differente, scelta in maniera casuale.
Si è deciso di implementare questo gioco, un esempio ricorrente nell’ambito dell’intelligenza artificiale, proprio per realizzare un agente che fosse in grado di calcolare una soluzione, ovvero un percorso sicuro, in ogni partita, che possa condurre il personaggio giocabile alla vittoria.
Questa funzionalità può essere richiesta dall’utente selezionando la voce corrispondente dal menu di gioco, visualizzando così il percorso che l’agente dotato di intelligenza artificiale è riuscito a calcolare, a partire dalla posizione corrente del personaggio giocabile.

## Specifiche progettuali

La versione del gioco che costituisce il fulcro di questo progetto, differisce, per alcuni aspetti, dal gioco ideato da Yob.
Infatti, mentre il gioco dello statunitense fu sviluppato, in linguaggio BASIC, inizialmente in modalità testuale e soltanto in seguito convertito in modalità grafica, la versione trattata in questo elaborato è stata ideata ed implementata per interezza in Java.
Dopo averla testata e resa giocabile, dall’utente, ricevendo degli input testuali da console, è stata creata una libreria che ne racchiudesse le funzionalità, affinché andasse a costituire il back-end di quella che sarebbe stata l’implementazione dell’applicazione Android vera e propria, dotata di grafica e progettata per dispositivi mobili dotati di questo sistema operativo.
Il nome dell’applicazione è “Wumpus World Game”, o “Il mondo del Wumpus”, in base alla lingua del dispositivo.


### Informazioni sulla versione del gioco
Per quanto riguarda la modalità di gioco, oltre all’assenza dei super-pipistrelli, che verranno integrati in futuro, un’ulteriore differenza con il gioco originale è costituita dalla possibilità, data al giocatore, di decidere che ruolo interpretare nella storia.
Nello specifico, l’utente potrà decidere se impersonare il cacciatore e quindi avere come obiettivo quello di trovare il tesoro nascosto del mostro, oppure se prendere le parti del Wumpus e cercare di sopravvivere a questa caccia spietata, trovando una via di fuga che lo conduca fuori dal labirinto.
Questo vuol dire che, se il cacciatore avrà a sua disposizione una sola freccia per tentare di colpire il Wumpus, nel caso in cui quest’ultimo sia il personaggio giocabile, allora, avrà a disposizione un masso per cercare di uccidere il cacciatore, prima che lo stani.
Qualunque sia il ruolo scelto, la partita termina se il giocatore muore, sia che cada nel pozzo o che venga ucciso dal mostro, nel caso del cacciatore, sia che venga catturato da una trappola o che venga colpito dal cacciatore, nel caso del Wumpus.
Per quanto riguarda lo scenario in cui si può muovere il giocatore, nella versione originale questo era costituito da una serie di caverne misteriose collegate tra loro, mentre, nella versione del progetto trattato in questo elaborato l’ambientazione è rappresentata da una foresta fitta dai percorsi intricati.

### Modalità di gioco
Il mondo del gioco “Hunt the Wumpus” è strutturato come una matrice di dimensione (4 x 4).
Questa mappa andrà costituire il terreno di gioco in cui dovrà muoversi il giocatore, indipendentemente che sia l’utente dell’applicazione Android oppure il giocatore automatico, cioè l’agente basato su conoscenza, cercando di evitare i pericoli, tentando di colpire il nemico se si trova nelle vicinanze e puntando alla vittoria.
Questi sono gli obiettivi che il giocatore dovrà perseguire, a prescindere che si trovi ad impersonare il cacciatore oppure il mostro.
Si precisa, che a seconda della modalità di gioco scelta ad inizio partita, il PG sarà quello che potrà muoversi sulla mappa di gioco, mentre il nemico rappresenterà un NPG, cioè un personaggio non giocabile, che manterrà fissa la sua posizione, per tutta la durata della sessione di gioco corrente.
Oltre alla possibilità di scegliere che ruolo avere nel gioco, l’utente potrà decidere se muovere direttamente il PG oppure affidare la risoluzione della sessione avviata ad un giocatore automatico, costituito da un agente software basato su conoscenza.
Come già detto per l’utente, anche l’agente avrà a disposizione dei suggerimenti, degli indizi sul contenuto delle celle della mappa che sono adiacenti alla sua posizione, in modo tale da acquisire una conoscenza parziale dell’ambiente che lo circonda, trattandosi di un agente basato su conoscenza.
Quindi, sia nella modalità di gioco interattiva, ovvero quella in cui viene coinvolto l’utente del dispositivo su cui gira l’applicazione Android, sia nella modalità di risoluzione automatica, in cui sarà, invece, l’agente a condurre la partita, verranno fornite queste informazioni:
- Le celle adiacenti al nemico, che sarà rappresentato dal Wumpus oppure dal cacciatore, dipendentemente dalla scelta di giocare con l’uno o l’altro come PG (tramite la variabile ENEMY_SENSE);
-Le celle adiacenti ad un pericolo, che può essere un pozzo o una trappola, a seconda del PG che si sta utilizzando, conterranno, rispettivamente, la brezza che giunge sin dalla prossimità del pozzo oppure un mucchio di foglie, volte a coprire la trappola (per mezzo della variabile DANGER_SENSE);

### Desctizione dell'ambiente

L’ambiente è costituito da una griglia, costituita da quattro righe e quattro colonne, per un totale di sedici celle.
Sarà questa matrice, di dimensione prefissata e non modificabile, che andrà a costituire il terreno su cui andranno posizionati tutti gli elementi di gioco.
Nello specifico, il contenuto di ogni cella verrà scelto in maniera casuale, secondo una specifica funzione di probabilità e sarà stabilito nella fase di creazione del terreno di gioco.
Gli elementi che andranno a riempire la mappa saranno:
-	Il personaggio giocabile scelto dall’utente;
-	il nemico del personaggio giocabile;
-	dei sassi o alberi che potrebbero ostruire il passaggio al giocatore;
- il premio che permetterà di ottenere, al giocatore, dei punti in più;
-	dei pericoli, ovvero dei pozzi o delle trappole, in base alla modalità di gioco;
Si precisa che alcune celle potranno essere vuote, cioè non conterranno nessuno degli elementi sopraelencati e pertanto potranno essere considerate come sicure.

### Sensori

Nel gioco del Wumpus, i sensori messi a disposizione all’agente lo aiuteranno a determinare la posizione dei pericoli e del nemico, sul terreno di gioco.
Nel dettaglio, si avrà l’accensione del sensore ENEMY_SENSE, se il nemico si trova in una cella adiacente e/o del sensore DANGER_SENSE, se il personaggio giocabile si trova vicino un pericolo.
Nell’implementazione del gioco trattata in questo elaborato non è stato previsto un sensore che indichi, all’agente, la vicinanza con il premio.
Altre indicazioni che l’agente riceve, durante la sua esplorazione, sono:
- La percezione della fine della mappa, se tenta di spostarsi oltre una qualsiasi delle celle della cornice;
- L’informazione che la cella in cui si trova è sicura, perché nessuna delle celle adiacenti contiene un elemento che è risultato di interesse per i sensori;

Per il problema trattato, ovvero il gioco del Wumpus, la definizione delle prestazioni riguarda la determinazione, da parte dell’agente, di un percorso sicuro ed il più breve possibile, che gli consenta di evitare i pericoli, abbattere il nemico ed ottenere il premio, conseguendo, così, la vittoria della partita.
Infatti, il massimo profitto si ottiene acquisendo il punteggio massimo, che potrà essere raggiunto riuscendo a terminare la partita dopo aver compiuto le seguenti azioni:
-	Evitare tutti i pericoli disseminati sulla mappa;
-	Abbattere il nemico con la freccia;
-	Trovare la cella contenente il premio, che per il cacciatore è rappresentato dal tesoro del Wumpus, mentre, nella modalità in cui è il mostro ad essere il PG scelto dall’utente, è costituito da un passaggio segreto che lo condurrà in salvo;
-	Effettuare il minor numero possibile di mosse, poiché ogni cella in più che viene visitata comporta un punto di penalità;
La valutazione di tutti questi elementi sarà quella che consentirà di effettuare una stima delle prestazioni raggiunte dall’agente razionale in questione.
A questo proposito, si riportano i valori dei punteggi stabiliti:
-	+100, in caso di vittoria del personaggio giocabile, che evidentemente ha trovato il premio;
-	-50 nel caso in cui il giocatore si posizioni in una cella contenente un pericolo;
-	-100, se il personaggio giocabile viene ucciso dal nemico;
-	+50, se il giocatore è riuscito ad individuare ed abbattere il nemico;
-	-1, per ogni cella esplorata, ovvero per ogni mossa effettuata dal personaggio giocabile;

## Struttura del back-end

Per l’implementazione dell’applicazione Android “Wumpus World Game”, dal punto di vista progettuale, si è deciso di scrivere prima il codice che andasse a costituirne il back-end e poi di integralo, dopo averne verificato il corretto funzionamento, con la parte grafica, realizzata con le librerie di Android.

Il back-end, quindi, costituisce un progetto a sé stante, denominato “Hunt the Wumpus or Not”, implementato interamente in Java 8, che realizza una versione del gioco “Hunt the Wumpus” anch’essa testuale.
Infatti, già da questa versione del progetto, si hanno a disposizione tutte le funzionalità che poi verranno utilizzate e richiamate nell’interfaccia utente dell’applicazione Android.
Ad esempio, per quanto riguarda la modalità di gioco, è stata prevista l'introduzione di due tipi differenti di giocatore, ovvero:
-	il giocatore vero e proprio, Human Player, pilotato dall'utente;
-	il giocatore automatico, IA Player, che consiste nell'implementazione di un agente dotato di una semplice intelligenza artificiale;

Quindi, al momento dell'avvio del gioco, l’utente potrà scegliere in che modalità giocare, ovvero se nella versione classica, Hero Side, in cui l'avventuriero deve uccidere il Wumpus oppure nella versione Wumpus Side, in cui dovrà impersonare proprio il mostro del gioco e riuscire a sopravvivere alla battuta di caccia.
Inoltre, l'utente sarà nelle condizioni di poter decidere se vuole essere lui direttamente a controllare le mosse del suo personaggio oppure lasciare che la risoluzione del gioco e, quindi, l'esplorazione del labirinto, sia affidata al giocatore automatico, ovvero un agente provvisto di intelligenza artificiale.


## Casi d'uso

Per casi d’uso si intende la descrizione dell’insieme di interazioni che si possono verificare tra un utente ed un sistema, per consentire all’utilizzatore del software di eseguire delle azioni tramite le funzionalità di cui questo dispone.
Segue la definizione dei casi d’uso principali dell’applicazione mobile descritta in questo elaborato:

1.	L’utente sceglie la modalità in cui avviare la partita, se Avventuriero o Wumpus;
2.	Dopo aver scelto la modalità di gioco, l’utente visualizza la schermata di gioco, in cui potrà muovere il suo PG sulla mappa tramite i tasti direzionali e potrà scagliare una freccia tramite il pulsante centrale;
3.	Al termine della partita l’utente potrà decidere se condividere o meno il punteggio ottenuto, selezionando la sua preferenza nella finestra che verrà visualizzata;

Estensioni dei casi d’uso riportati sopra:

1a.	L’utente può accedere, tramite il menu, a differenti schermate, indicate dalle voci: “Informazioni”, “Tutorial”, “Punteggi” ed “Impostazioni”;
1.	L’utente seleziona la voce “Informazioni” e visualizza una descrizione del gioco;
a.	L’utente ritorna alla schermata precedente tramite il pulsante di navigazione “Indietro”.
2.	L’utente seleziona la voce “Tutorial” e visualizza una descrizione della storia e dei personaggi del gioco;
a.	L’utente seleziona il tasto “Avanti” e visualizza una spiegazione dei comandi generali del gioco;
i.	L’utente seleziona il tasto “Indietro” e ritorna alla schermata in cui è illustrata la storia del gioco;
b.	L’utente ritorna alla schermata precedente tramite il pulsante di navigazione “Indietro”.
3.	L’utente seleziona la voce “Punteggi” e visualizza la classifica dei punteggi che ha ottenuto fino a quel momento.
a.	Cliccando il pulsante di condivisione nella sezione “Record”, l’utente può condividere il suo miglior punteggio;
b.	Cliccando il pulsante di condivisione nella sezione “Ultimo punteggio”, l’utente può condividere il suo ultimo punteggio;
c.	L’utente ritorna alla schermata precedente tramite il pulsante di navigazione “Indietro”.
4.	L’utente seleziona la voce “Impostazioni” ed accede alle impostazioni dell’applicazione.
a.	Nella scheda “Generali” l’utente può:
i.	abilitare oppure disattivare gli effetti sonori dell’applicazione;
ii.	modificare il suo nome da giocatore;
b.	Nella scheda “Dati e Sincronizzazione” l’utente può:
i.	Importare i dati di gioco selezionando dall’archivio del dispositivo un file contenente dei punteggi precedenti,
ii.	Esportare i dati di gioco scegliendo la locazione in cui memorizzare il file contenente i punteggi ottenuti fino a quel momento;
iii.	Eliminare i dati di gioco cancellando il file dei salvataggi;
c.	Nella scheda “About” l’utente può:
i.	Inviare un feedback allo sviluppatore dell’applicazione tramite posta elettronica;
ii.	Visualizzare le informazioni dello sviluppatore ed i crediti dell’applicazioni;
d.	L’utente ritorna alla schermata precedente tramite il pulsante di navigazione “Indietro”.
2a.	L’utente, durante la sessione di gioco, può accedere al menu, costituito dalle voci “Nuova partita”, “Giocatore Automatico” e “Comandi di gioco”.
1.	L’utente seleziona la voce “Nuova Partita” per avviare una nuova sessione di gioco; perciò, la mappa viene generata da capo;
2.	L’utente seleziona la voce “Giocatore Automatico”, avviando la risoluzione automatica della mappa di gioco sfruttando l’agente;
3.	L’utente seleziona la voce “Comandi di gioco”, visualizzando, così, i comandi di gioco specifici per la modalità che ha scelto;


## Struttura del front-end

L’applicazione è stata progettata in maniera tale che fosse semplice ed intuitiva per l’utente, implementando due differenti modalità di gioco e mettendo a disposizione la possibilità di vedere la soluzione di ogni partita avviata, lasciando che sia un agente software a concludere la sessione di gioco corrente.
Per quanto riguarda la struttura del progetto, si è cercato di rispettare quelle che sono le convenzioni adottate nello sviluppo di applicazioni Android, suddividendo nei rispettivi package i componenti dello stesso tipo, come si è fatto, ad esempio, per la definizione dell’aspetto di ogni activity, descritto in un file .xml contenuto in layout o per la memorizzazione delle immagini utilizzate, contenute nella cartella drawable, insieme ai file .xml che realizzano gli sfondi delle attività e dei loro componenti.

## Sviluppi futuri

Per migliorare l’applicazione, oltre ad eventuali ottimizzazioni del codice, si è pensato di inserire alcune funzionalità aggiuntive, come la presenza dei super pipistrelli, così come previsto nella versione originale del gioco. In questo modo, durante la sessione di gioco, l’utente avrà una variabile in più di cui tenere conto, che potrebbe portarlo a dover cambiare strategia, visto che il PG, incontrando questo tipo di elemento sul terreno di gioco, verrebbe trasportato in un punto casuale della mappa.
Inoltre, si cercherà di implementare differenti algoritmi di risoluzione, in modo da dare la possibilità, allo stesso utente, di scegliere il tipo di intelligenza artificiale di cui verrà dotato l’agente software, cioè il giocatore automatico.
Per permettere una maggiore personalizzazione della sessione di gioco, in aggiunta, si vorrebbe definire un insieme di regole da adottare per la creazione e per la configurazione del terreno di gioco, in modo da lasciare che l’utente sia libero di impostare la dimensione della mappa, la difficoltà della partita, che verrà incrementata aumentando il numero di pericoli da posizionare sulla stessa e prevedere, di conseguenza, una serie di livelli, diversi per abilità richiesta e scenario.
Infine, si vorrebbero disegnare, in formato vettoriale, l’icona identificativa dell’applicazione e tutte le immagini rappresentative degli elementi di gioco, in maniera tale che siano originali, al contrario di quelle attualmente in uso che, invece, sono state prese, così come è stato fatto per le clip audio, dal sito https://opengameart.org.

