Faccio un piccolo ripasso di come gestire e creare un DB con PHPMYADMIn e la sua gestione con LARAVEL.

---------------------------------------------------------------------------------------------------------------------------------------------
                                                       PRIMISSIMA FASE

creo una cartella di lavoro dove voglio (possibilimente all'interno di htdocs di MAMP per usare laravel)
 - dopo aver creato la cartella di lavoro avvio il terminale ed eseguo il comando di installzione di composer per laravel, cioè
   composer create-project --prefer-dist laravel/laravel . 
   questo comando creerà il prgetto Laravel all'interno della cartella.

 - non avendo una cartella .git (perchè creato nel mio computer) posso inizializzare un nuovo repository GIT:
  git init (comando da utilizzare all'interno direnttamente da VS o da Cmd)

 - aggiungo poi il mio progetto alla rpository di GitHub con questo comando
   git remote add origin https://github.com/tuo-utente/tuo-repository.git (sostituisco l'URL con quello generato dalla mia repository di GitHub)

 - aggiungo e commito i file ->
   git add . ->
   git commit -m "Aggiunto il progetto Laravel"
 
---------------------------------------------------------------------------------------------------------------------------------------------
                                                        PRIMA FASE

Creo il mio Database da PHPMYADMIN e lo collego poi a laravel dentro il file env nella sezione de BD metto nel nome il nome esatto messo in PHPMYADMIN e nella parte username e password uso root perché il DB è all'interno del mio PC.
-possibile modifica creare una API_URl per gestire i dati del database tramite API -> seguire la doc di laravel per la creazione di API RESTful.

Fatto le dovute modifiche al file .ENV eseguiamo il comando:
- php artisan key:generate
questo comando crea la chiave personale tipo:
base64:5Nqj1Xw4whzHv7TjOZ5v0C2n4c9zROavjIr6RMYh/9M= nella sezione APP_KEY
la chiave viene utilizza per proteggere i dati sensibili come password e token
ogni progetto deve averne una sua e tutte diverse per garantire la sicurezza
è necessaria per la gestione delle sessioni e dei cookie senza non funzionerebbero correttamente.


Una volta eseguiti questi passaggi eseguo il comando:
- php artisan serve questo avvia il server in locale e sono pronto a modificare ed implementare cose all'interno del mio progetto.

--------------------------------------------------------------------------------------------------------------------------------------------
                                                      SECONDA FASE

Fatto ed eseguito correttamente i passaggi sopra che sono obbligatori per far funzionare il progetto eseguo i primi veri comandi

-php artisan make:migration *NOME_DELLA_MIGRAZIONE
Questo comando crea le prime migrazioni delle tabelle che andremo a creare ad esempio:
php artisan make:migration create_utenti_table creerà la tabella denominata utenti all'interno del nostro DB e la migrazione stessa all'interno di database/migrations con un nome simile a 2025_01_27_123456_create_utenti_table.php.

-php artisan migrate -> comando per migrare appunto la tabella e/o le sue modifiche interne al nostro DB.

-php artisan make:controller *NomeController ad esempio prendiamo la tabella utenti quindi:
Questo comando creerà il file UtentiController.php all'interno della cartella app/Http/Controllers, che sarà responsabile per gestire le operazioni relative alla tabella utenti.

-php artisan make:model *NomeModello ad esmpio prendiamo la tabella utenti quindi:
Questo comando creerà il modello Utente.php all'interno della cartella app/Models. Laravel assumerà che la tabella associata al modello Utente sia chiamata utenti (al plurale). si può personalizzare il nome della tabella all'interno del modello se necessario.




                                                      