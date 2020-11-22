# Come usare VS Code e Git

Questo appunti sono giusto giusto un minimo di comandi per newbie come me ma possono essere utili a qualcuno che si trova nella stessa situazione.

In questo e nel prossimo paragrafo vedremo i comandi utili per usare git in locale senza bisogno di repository online. Successivamente vedremo come interarire con un repsitory come [GitHub](https://github.com)

## Comandi base

Tutti comandi di seguito riportati possono essere eseguiti su un terminale esterno come as esempio Terminal in Mac OSX o cdm.exe in Windows oppure nel termilae di VS Code selezionando da menu Terminal>New Terminal

1. Entrare nella cartella del progetto: **cd /percorso_progetto**
2. Verificare se git è istallato: **git --version**
3. Inizializzare git da dentro la cartella del progetto: **git init**
   1. Git ti risponderà in questo modo:
   2. _Initialized empty Git repository in /Users/utente/percorso/.git/_
4. Configurare git con il proprio username e la mail (basta la prima volta)
   1. **git config --global user.name "tuonome"**
   2. **git config --global user.email "tuaemail"**
5. Controlliamo lo status del repository locale:
	1. **git status**
	2. Risposta: Git ci risponte dicendoci che siamo nel ramo master (master branch), fa un elenco dei file presenti e ci dice di aggiungere i file con il comando _add_
6. Aggiugiamo i file allo staging area ossia fra i file che possono essere uplodati
	1. **git add** _nomefile_ nel caso vogliamo aggiugere tutti i file: **git add** .
	2. Per rimuovere qualche file: **git rm --cached** nomefile
7. Facciamo il commit: **git commit**.

	Si apre una finestra che dobbiamo editare:
	premendo i sulla tastiere possiamo editare scrivendo o togliendo il cancelletto #.
	Per evitare gi aprire la finesta dei commenti: **git commit -m "commento"**
	
	Per uscire premere _esc_ e scrivere _:wq_
	
8. Per tornare all'ultimo commit (ultima verione del file salvata): **git checkout --nomedelfile**
9. Per uno storico dei commit fatti: **git log**
10. Per tornare indietro ad un particolare commit: **git reset** + numero del commit
11. Per ignorare un file: aggingere nella root del repository il file _.gitignore_ ed inserire l'elenco dei file da ignorare.
	Una buona lista di file riccornti da ignorare la trovi qui: [gitignore list](https://github.com/github/gitignore)

## Lavorare con i branch (rami)
1. Per creare un nuovo ramo del software: **git branch nomedelramo**
2. Per vedere quanti branch ci sono **git branch** con l'asterisco è indicato il branch attivo (**git branch -a** per vedere anche i rami in remoto)
3. Per spostarsi e lavorare su un determinato ramo: **git checkout nomedelramo**
4. Per aggiungere e fare in commit al ramo appena creati vedi paragrafo precendere (add e commit)
5. Per unire i due rami master ed un ramo: **git merge** 
	PS: Per ignorare dei file dirante il merge fare cosi:
	Ad esempio si hanno 2 rami: master e dev
	Avendo creto un file nel ramo dev che si vuole ignorare durante il merge
	
	'
	git config --global merge.ours.driver true
	git checkout master
	echo "path/file_to_ignore merge=ours" >> .gitattributes
	git merge dev
	'
	
	E' possibile ignorare anche tutti i file con la stessa estensione:
	Ad esempio ignorare tutti i file .txt:
	
	'
	echo "*.txt merge=ours" >> .gitattributes	
	'

## Integrazione con GitHub.com

1. Andare a creare un nuovo repository online e configurarlo
2. Dal pulsante verde Code dei files del progetto copiare il link https del repository (ad esempio: https://github.com/antedoro/portabiciauto.it_PROD.git)
3. Collegare il repository locale al remoto:(ad esempio: **git remote add origin <https://github.com/antedoro/portabiciauto.it_PROD.git>**)
4. Per controllare se il collegamnto è avvenuto: **git remote -v**
	Se la risposta è la seguente va tutto bene:
	> 	origin  https://github.com/antedoro/portabiciauto.it_PROD.git (fetch)
	> 	origin  https://github.com/antedoro/portabiciauto.it_PROD.git (push)

5. Carichiamo (push) i file in remoto: **git push -u origin master**
6. Per scaricare i file da Github.com: **git pull**
7. Per clonare un progetto: **git clone** + _url_ del progetto


## Usare un submodulo
Fare il submodule di un repository:
1. **cd /percorsodelsubmodulo**
2. **git init**
3. **git submodule add https://github.com/dillonzq/LoveIt.git** (esempio di link)
4. **git status**

Vedi questa [spiegazione](https://www.atlassian.com/git/tutorials/git-submodule)

## Clonare un progetto e i suoi submoduli

Se vuoi clonare un progetto incluso i suoi submoduli: **git clone --recursive url**

Se invece hai gia clionato un progeto e vuoi scaricare anche i submoduli: **git submodule update --init**

## Come configurare una repositary git sul proprio server

[How to Deploy a Website to a Remote Server Using GIT](https://hackernoon.com/deploy-website-to-remote-server-using-git-da6048805637)

