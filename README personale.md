Faccio un piccolo ripasso di come gestire e creare un DB con PHPMYADMIn e la sua gestione con LARAVEL.

---------------------------------------------------------------------------------------------------------------------------------------------
                                                       PRIMISSIMA FASE

creo una cartella di lavoro dove voglio (possibilimente all'interno di htdocs di MAMP per usare laravel)
 - dopo aver creato la cartella di lavoro avvio il terminale ed eseguo il comando di installzione di composer per laravel , cioè

 composer create-project --prefer-dist laravel/laravel .
 questo comando creerà il prgetto Laravel all'interno della cartella.

 - non avendo una cartella .git (perchè creato nel mio computer) posso inizializzare un nuovo repository GIT:
  git init (comando da utilizzare all'interno direnttamente da VS o da Cmd)

 - aggiungo poi il mio progetto alla rpository di GitHub con questo comando
   git remote add origin https://github.com/tuo-utente/tuo-repository.git (sostituisco l'URL con quello generato dalla mia repository di GitHub)

 - aggiungo e commito i file 
   git add .
   git commit -m "Aggiunto il progetto Laravel"
 
                                                 