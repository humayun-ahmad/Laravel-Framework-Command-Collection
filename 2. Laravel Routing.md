# Laravel Routing

## Create Route with a Closure:
```
Route::get('hello', function () {
    return 'Hello World';
});
```

## Create Route with controller:
```
Route::get('/user', 'UserController@index');
 ```

## Router Methods:
```
Route::get('uri', 'ControllerName@method');
Route::post('uri', 'ControllerName@method');
Route::put('uri', 'ControllerName@method');
Route::patch('uri', 'ControllerName@method');
Route::delete('uri', 'ControllerName@method');
Route::options('uri', 'ControllerName@method');
 ```

## Using match or any:
```
Route::match(['get', 'post'], '/', function () {
    //
});

Route::any('/', function () {
    //
});

```

## Redirect Routes with 302 status code:
```
Route::redirect('/from', '/to');
```
## Redirect Routes with 301 status code: 
```
Route::redirect('/from', '/to', 301);
Route::permanentRedirect('/from', '/to');
```

## View Routes:
```
Route::view('/test', 'test');

Route::view('/test', 'test', ['name' => 'Mamun']);
``` 

## Route Parameters:
```
Route::get('user/{id}', function ($id) {
    return 'User id is: ' . $id;
});
```
## Multiple Parameters:
```
Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) {
    //
});
```

## Optional Parameters:
```
Route::get('user/{id?}', function ($id = 1) {
    return $id;
});
```

 

## Regular Expression Constraints:
```
Route::get('posts/{slug}', function ($slug) {
    //
})->where('slug', '[A-Za-z]+');

Route::get('posts/{id}', function ($id) {
    //
})->where('id', '[0-9]+');

Route::get('posts/{id}/{slug}', function ($id, $slug) {
    //
})->where(['id' => '[0-9]+', 'slug' => '[a-z]+']);
```

## Named Routes:

```
Route::get('user', 'UserProfileController@show')->name('user');

```
## Generating URL:
```
// Generating URLs...
$url = route('user');
```

```
// Generating Redirects...
return redirect()->route('user');
```

```
Route::get('user/{id}', function ($id) {
    //
})->name('user');

$url = route('user', ['id' => 1]);
```

 

## Route Groups:
```
Route::middleware(['web'])->group(function () {
    Route::get('test', function () {
        
    });

    Route::get('user/{id}', function ($id) {
        
    });
});
```
```
Route::namespace('Admin')->group(function () {
    // Controllers Within The "App\Http\Controllers\Admin" Namespace
});
```

## Prefix:
```
Route::prefix('dashboard')->group(function () {
    Route::get('users/{id}', function ($id) {
        // Matches The "/dashboard/users/1" URL
    });
});
```

## Form Method Spoofing:
```
<form action="/action-path" method="POST">
    <input type="hidden" name="_method" value="PUT">
    <input type="hidden" name="_token" value="{{ csrf_token() }}">
</form>
```

```
<form action="/foo/bar" method="POST">
    @method('PUT')
    @csrf
</form>
```