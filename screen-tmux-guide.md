Multiplexer per terminali - parte 1 - screen

di alessioantonielli · 22 marzo, 2016

terminal_multiplexer screen
Nella vita universitaria a maggior ragione, ma anche per alcune attività lavorative, è molto probabile che vi ritroverete a dover eseguire lunghi programmi da far girare per ore su un server che vi è stato fornito. Mettendo per adesso da parte la questione "occupazione delle risorse" e ragionando del tipo "il server è mio!", la prima cosa che vi potreste chiedere è come fare in modo che uno script o un programma lanciato via ssh continui a girare sul server anche dopo la vostra disconnessione, e come potete riagganciarvi a tale processo nelle successive connessioni.

Esistono appositi programmi che vi consentono la "virtualizzazione" di più terminali separati chiamati "terminal multiplexer". In questo breve articolo vi presentiamo screen, uno dei più semplici terminal multiplexer per Linux, mentre in un futuro articolo passeremo in rassegna le caratteristiche del più raffinato tmux.

Per l'installazione sul server (o sul vostro pc) procedete con un semplice:
sudo apt-get install screen

Finita l'installazione, supponiamo per esempio che abbiate uno script in Python chiamato script_python.py che dovete lasciare ad eseguire per un tempo prolungato. Vi basterà utilizzare il comando screen per creare una sessione virtualizzata dove far girare lo script:
screen python script_python.py

Sul terminale aperto vedrete il vostro programma girare normalmente, ma utilizzando la combinazione di tasti concatenata a CTRL + A potrete eseguire le seguenti operazioni:

    CTRL + A CTRL + D: uscite dal terminale virtualizzato corrente.
    CTRL + A CTRL + C: create un nuovo terminale virtualizzato.
    CTRL + A CTRL + N: navigate verso il terminale successivo.
    CTRL + A CTRL + P: navigate verso il terminale precedente.

E' possibile infatti creare nuovi terminali virtualizzati all'interno di terminali virtualizzati, così come è possibile lanciare più programmi con screen ed in seguito accedervi separatamente.

Per riaccedere ad un terminale virtualizzato dopo che siete usciti, dovete conoscere l'id che viene dato ai terminali virtualizzati che sono stati creati.

Per avere una lista di tutti i processi avviati con screen, vi basterà digitare
screen -ls

e vi sarà fornito un elenco con codice del processo screen e data/ora in cui è stato avviato.
Si specifica che per codice del processo possono bastare le cifre che precedono il punto ed il nome della macchina sulla quale è stato lanciato il terminale virtualizzato.

Una volta trovato il processo di interesse nella lista, utilizzate il comando
screen -r ID_PROCESSO

per riagganciarvi al terminale virtualizzato e vedere il processo in esecuzione. Se avete un solo terminale virtualizzato, vi basterà digitare screen -r senza dover specificare l'id.

Infine, per uscire da un terminale potete:

    digitare exit se siete dentro il prompt del terminale virtualizzato
    utilizzare la combinazione di tasti CTRL + A CTRL + K sempre dal terminale virtualizzato
    dall'esterno, ricercare l'id del terminale virtualizzato da chiudere e digitare
    screen -X -S ID_PROCESSO quit

Come sempre vi invitiamo ad aggiungere nei commenti funzionalità non trattate, domande o annotazioni. Nel prossimo articolo della serie vedremo invece come utilizzare tmux.
