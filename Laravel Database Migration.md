# Laravel Database Migration

## Artisan command for creating migration:
```
php artisan make:migration create_customers_table
```

## Define the table name for creating:
```
php artisan make:migration create_customers_table --create=customers
```
## Define the table name for updating:
```
php artisan make:migration add_votes_to_customers_table --table=customers
```

## Table Structure:
```
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateFlightsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('customers', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('address');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('customers');
    }
}

``` 

## Run migration:
```
php artisan migrate
```
## Run with force:
```
php artisan migrate --force
```
## Rolling Back:
```
php artisan migrate:rollback
```
## Rolling Back With Step:
```
php artisan migrate:rollback --step=3
```
## Rolling Back all migration:
```
php artisan migrate:reset
```
## Rolling Back and Migration:
```
php artisan migrate:refresh
```
## Drop All Tables & Migrate:
```
php artisan migrate:fresh
php artisan migrate:fresh --seed
```

# Creating Columns: 
## Command	Description
```
$table->id();	Alias of $table->bigIncrements('id').
$table->foreignId('user_id');	Alias of $table->unsignedBigInteger('user_id').
$table->bigIncrements('id');	Auto-incrementing UNSIGNED BIGINT (primary key)
$table->bigInteger('votes');	BIGINT column.
$table->boolean('confirmed');	BOOLEAN column.
$table->char('name', 100);	CHAR column and length.
$table->date('created_at');	DATE column.
$table->dateTime('created_at', 0);	DATETIME 
$table->double('amount', 8, 2);	DOUBLE with precision
$table->enum('level', ['easy', 'hard']);	ENUM column.
$table->float('amount', 8, 2);	FLOAT column
$table->increments('id');	Auto-incrementing UNSIGNED INTEGER (primary key) column.
$table->integer('votes');	INTEGER column.
$table->json('options');	JSON column.
$table->longText('description');	LONGTEXT column.
$table->morphs('owner');	Adds owner_id UNSIGNED BIGINT and owner_type VARCHAR columns.
$table->rememberToken();	Adds a nullable remember_token VARCHAR(100) column.
$table->string('name', 100);	VARCHAR column with a length.
$table->text('description');	TEXT column.
$table->time('sunrise', 0);	TIME column 
$table->timestamp('added_on', 0);	TIMESTAMP column
$table->timestamps();	Adds nullable created_at and updated_at TIMESTAMP
$table->tinyInteger('votes');	TINYINT column.
$table->unsignedBigInteger('votes');	UNSIGNED BIGINT column.
$table->unsignedInteger('votes');	UNSIGNED INTEGER column.
$table->uuid('id');	UUID column.
$table->year('birth_year');	YEAR column.
 
```
 
## Column Modifiers:
```
->after('column')
->comment('my comment')
->default($value)
->nullable()
```

## Modifying Columns:
```
composer require doctrine/dbal
```

```
Schema::table('users', function (Blueprint $table) {
    $table->string('name', 50)->change();
});

```

## Rename Column:
```
Schema::table('users', function (Blueprint $table) {
    $table->renameColumn('from_name', 'to_name');
});
``` 

## Droping Column:
```
Schema::table('users', function (Blueprint $table) {
    $table->dropColumn(['one', 'two', 'three']);
});
```
```
Schema::table('table_name', function (Blueprint $table) {
    $table->dropColumn('column');
});
```

## Creating Indexes:
```
$table->string('email')->unique();
 

$table->unique('email');
 

$table->index(['account_id', 'created_at']);
 

$table->unique('email', 'unique_email');
```

## Command	Description
```
$table->primary('id');	 primary key.
$table->primary(['id', 'parent_id']);	Composite keys.
$table->unique('email');	Unique index.
$table->index('state');	Plain index.
```

## Dropping Indexes:
```
$table->dropPrimary('users_id_primary');
$table->dropUnique('users_email_unique');
$table->dropIndex('geo_state_index');
 
```
 

## Foreign Key Constraints:
```
Schema::table('posts', function (Blueprint $table) {
    $table->unsignedBigInteger('user_id');

    $table->foreign('user_id')->references('id')->on('users');
});

```