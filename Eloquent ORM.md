# Eloquent ORM

## Create Model:
```
php artisan make:model Post
```

## Create Model With Migration:
```
php artisan make:model Post -m
```

## Model:
```
namespace App;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    //
}

```

## Define Table Name:
```
namespace App;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    protected $table = 'posts';
    protected $primaryKey = 'flight_id';
    public $incrementing = false;
    public $timestamps = false;
}
 
```

## Run Query:
```
$posts = App\Post::where('active', 1)
               ->orderBy('name', 'desc')
               ->take(10)
               ->get();
 
```

## Retrieving Single Models:
```
$post = App\Post::find(1);

$post = App\Post::where('active', 1)->first();

$post = App\Post::firstWhere('active', 1);

```

## With Not Found Exceptions:
```
$post = App\Post::findOrFail(1);

$post = App\Post::where('legs', '>', 100)->firstOrFail();
 
```

## Retrieving Aggregates:
```
$count = App\Post::where('active', 1)->count();
$max = App\Post::where('active', 1)->max('price');
$min = App\Post::where('active', 1)->min('price');
$sum = App\Post::where('active', 1)->sum('price');
$avg = App\Post::where('active', 1)->avg('price');
```

## Inserts:
```
$post = new Post;
$post->title = 'The title';
$post->save();
```
```
$user = User::create([
    'first_name' => 'Jone',
    'last_name' => 'Done',
    'title' => 'Developer',
]);
 
```
```
$user = User::create([
    'first_name' => 'Jone',
    'last_name' => 'Done',
    'title' => 'Developer',
]);

$user->title = 'Painter';
$user->save();
 
```

## Update:
```
$post = Post::find(1);
$post->title = 'The title';
$post->save();
 
```

## Mass Assignment:
```
namespace App;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = ['title'];
}
```
```
$post = App\Post::create(['name' => 'Flight 10']);
 
```

## Guarding Attributes:

```
namespace App;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    /**
     * The attributes that aren't mass assignable.
     *
     * @var array
     */
    protected $guarded = ['title'];
}

``` 

## firstOrCreate/ firstOrNew:
```
$post = App\Post::firstOrCreate(['title' => 'Flight 10']);

$post = App\Post::firstOrCreate(
    ['title' => 'Flight 10'],
    ['status' => 1]
);

$post = App\Post::firstOrNew(['title' => 'Flight 10']);

$post = App\Post::firstOrNew(
    ['title' => 'Flight 10'],
    ['status' => 1]
);
 
```

## Deleting Models:
```
$post = App\Post::find(1);

$post->delete();

```

```
App\Post::destroy(1);

App\Post::destroy(1, 2, 3);

App\Post::destroy([1, 2, 3]);
```

```
$deletedRows = App\Post::where('status', 0)->delete();
```