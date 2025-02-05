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


  --------------------------------------------------------------------------------------------------------------------------------------------
      GESTIONE MIGRAZIONI ERRATE O DA AGGIORNARE

Se ci accorgiamo che durante una migrazione già eseguita abbiamo sbagliato qualcosa esistono dei comandi utili per rimediare:

-php artisan migrate:rollback
Questo comando ci permette di annullare l'ultimo GRUPPO di migrazioni eseguite e ci riporta le tabelle(in caso di creazione con quella stessa migrazione vengono cancellate nel DB) allo stato antecedente all'ultima migrazione.
possiamo pure elimire più migrazioni eseguite ad esempio se vogliamo cancellare le ultime due fatte e tornare a due stadi prima ci basta eseguire questo comando:
-php artisan migrate:rollback --step=2 (in questo caso il 2 perché voglio tornare indietro di 2 stadi).

-php artisan migrate:reset
Questo comando esegue il rest completo di tutte le migrazioni fatte nel DB.

Quindi si può eseguire il rollback della migrazione da modificare, apportare le dovute modifiche e rieseguire di nuovo la migrazione con il solito comando php artisan migrate

-php artisan migrate:refresh 
Questo comando come quell osopra elimina tutte le tabelle migrate nel database e le riesegue creandole nuovamente.
possiamo pure fare php artisan migrate:refresh -seed
così possiamo resettare->ricrearle->e definire i seeder fatti con il Seeder apposta.

Se si vuole eseguire delle modifiche alla struttura di una tabella esistente bisogna creare una nuova migrazione che specifichi le modifiche da apportare perché laravel non permette di modificare una migrazione SE già eseguita quindi presente nel DB.
si crea una nuova migrazione per l'aggiornamento eseguendo il comando:

-php artisan make:migration update_tablename --table=nome_tabella
quindi collegandoci come prima alla tabella user 
php artisan make:migration update_user --table=utenti
Questo farà in modo che laravel andrà a prendere la tabella utenti perché lo specifichiamo qua --table=utenti e cosa vogliamo fare qua update_user,
quindi se vogliamo aggiungere una colonna magari il numero telefonico degli utenti ma prima non c'era possiamo eseguire un update così:
php artisan make:migration add_phone_number_to_utenti --table=utenti.
quindi all'interno della nostra migrazione in database/migrations troveremo la nostra nuova migrazione all'interno del codice up() e down() mettiamo la nuova colonnapublic function up()
{
    Schema::table('utenti', function (Blueprint $table) {
        $table->string('phone_number')->nullable(); // Aggiunge la colonna phone_number
    });
}

public function down()
{
    Schema::table('utenti', function (Blueprint $table) {
        $table->dropColumn('phone_number'); // Rimuove la colonna phone_number
    });
}

fatte le dovute modifiche eseguiamo sempre il solito comando php artisan migrate e se tutto è andato a buon fine comparirà la nuova colonna all'interno della tabella nel nostro DB.


Se per un motivo o per un altro possiamo sempre eseguire php artisan make:migration rollback per tornare indietro e annullare l'ultima migrazione.


 --------------------------------------------------------------------------------------------------------------------------------------------
                                CREAZIONE DI DATI FITTIZI PER ESEGUIRE DEI TEST

Per eseguire dei test di verifica senza dover inizializzare dati veri possiamo far riscorso al seeder e ai faker di laravel, questi ci permetteranno di popolare le nostre tabelle all'interno del DB  il comando da eseguire per creare un seeder è:
 -php artisan make:seeder NomeSeeder ->sostituire il nome con il nome della tabella che vogliamo popolare esempio ->php artisan make:seeder UsersTableSeeder
creerà il seeder per la tabella 'users'.
Questo comando crea un file dentro database/seeders/UsersTableSeeder.php, dove si può definire i dati da inserire.

all'interno del seeder ci sarà questa funzione 
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class UsersTableSeeder extends Seeder
{
    public function run()
    {
        DB::table('users')->insert([
            'name' => 'Mario Rossi',
            'email' => 'mario.rossi@example.com',
            'password' => bcrypt('password'),
        ]);
    }
}
Quindi questo creerà all'interno del Database e della tabella 'users' le colonne 'name', 'email' e 'password' con i loro rispettivi valori
per eseguire questo codice si usa questo comando:
-php artisan db:seed --class=UsersTableSeeder
OPPURE si può eseguire TUTTI i seeder dentro DatabaseSeeder.php:
-php artisan db:seed

mentre invece se vogliamo generare dei dati casuali e non definiti da noi possiamo usare i FAKER, torniamo all'interno del nostro seeder

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;
use Faker\Factory as Faker;

class UsersTableSeeder extends Seeder
{
    public function run()
    {
        $faker = Faker::create();

        for ($i = 0; $i < 10; $i++) {
            DB::table('users')->insert([
                'name' => $faker->name,
                'email' => $faker->unique()->safeEmail,
                'password' => bcrypt('password'), // Puoi usare sempre la stessa password crittografata
            ]);
        }
    }
}

use Faker\Factory as Faker; 
richiamiamo il faker di laravel così possiamo utilizzarlo all'interno del nostro seeder
Poi sempre dentro la funzione run() eseguiamo questo codice 
$faker = Faker::create();
sotto grazie al ciclo for andrà a creare randomicamente 10 utenti diversi tra loro con i relativi valori sempre generati casualmente.
(il bcrypt('password') renderà la password criptata).

infine per eseguire questa modifica basterà scrivere lo stesso codice di prima:
-php artisan db:seed --class=UsersTableSeeder
eseguirà il seeder CON il faker che appunto genererà i nostri dati fittizi oppure se vogliamo eseguirli tutti
-php artisan db:seed







                                                      