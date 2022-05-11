# Come organizzare un repository GIT


Oggi vi voglio parlare su come organizzare un repository git per i vostri progetti, spiegandovi la mia metodologia. I miei progetti sono quasi esclusivamente applicazioni mobile, ma questa struttura si può estendere a qualsiasi tipo di applicativo.

## Il mio metodo

![git_flow.png](git_flow.png)

Flusso riassuntivo della struttura di un mio repository GIT.

### Master

Questo è il branch principale di produzione. Ne esiste solo un per progetto. In questo branch i commit rappresentano le versioni dell’applicativo pubblicate in produzione. In aggiunta aggiungo anche un tag che identifica la versione, per una rilettura comoda e rapida.
Se sono presenti delle anomalie nelle versioni in produzione che hanno bisogno di essere corrette nel più breve tempo possibile, creo un branch dal commit del master come “Hotfix”.

### Release

Quando decido di portare tutti gli avanzamenti del develop in produzione, creo un branch denominato “release_x.y.z” (dove x.y.z è la prossima versione dell’applicativo). Qui vengono eseguite delle modifiche leggere che riguardano l’aggiornamento della versione. Di solito è il cambio della versione e del build number. Una volta pronti per andare in produzione, unisco questo ramo sia nel “master”(taggando il numero di versione) che nel “develop”, in modo tale da avere un punto sincronizzato trai i rami.

### Develop

Questo è il ramo dello sviluppo, il campo di battaglia! Ne esiste solo di uno per progetto. Da qui vengono creati i rami per le nuove funzionalità e sviluppi. Io tendo, quando possibile, a creare un branch per ogni funzionalità che voglio implementare (partendo da develop). Ci possono essere dei commit che non prevedono la creazione di un ramo, ma sono modifiche molto lievi, quali pulizia del codice, aggiunta di qualche commento e similari.

### Feature

Una volta pianificato e progettato lo sviluppo di una nuova funzionalità, creo un ramo, partendo da develop con il nome “feature_IDENTIFICATIVO-FEATURE”, dove IDENTIFICATIVO-FEATURE è, per l’appunto, l’identificativo della funzionalità. In caso di applicazione progettate e coordinate su JIRA, per esempio, è l’identificativo della storia relativa allo sviluppo (vi consiglio di integrare GIT sul progetto JIRA, la quale permette la creazione, direttamente dalla dashboard, del branch relativo alla storia stessa).

### Hotfix

Questi rami vengono creati quando qualcosa va irrimediabilmente storto. Se sono presenti dei bug in produzione sfuggiti ai test, al quale bisogna porre rimedio subito (interrompendo qualsiasi sviluppo in corso), occorre creare un ramo “hotfix_IDENTIFICATIVO-HOTFIX” (come in develop, identificativo della storia in caso di JIRA od un altro che sia leggibile al volo). Essendo una “toppa” da mettere all’applicazione in produzione, bisogna implementare solo gli sviluppi necessari alla risoluzione, senza incorporare niente del ramo develop che potrebbe essere ancora in sviluppo od in test. Questo ramo, quindi, verrà creato dal master ed, una volta terminato e pubblicato, esso sarà unito sia al ramo master che a quello di develop. Questo è l’unico caso che creo un ramo partendo dalla produzione.
