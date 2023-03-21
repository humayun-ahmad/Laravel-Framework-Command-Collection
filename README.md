# Laravel-Framework

## Github Editor
[Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

# blade tamplate
```
@extends('')

@section('title', '')

@push('css')

@endpush


@section('content')


@endsection

@push('js')

@endpush

```

### And don't forget run this command:
```
php artisan config:cache
php artisan config:clear
```

### Toastr for Laravel

Toaster link:: https://github.com/brian2694/laravel-toastr

### View Composers
```
View::composer('layouts.frontend.partial.footer', function ($view){
     $categories = App\Category::all();
     $view->with('categories', $categories);
});
``` 
*Reference by programming kit 36 no. video lecture*

### For Search System in laravel:
     1. Algolia (vue.js)

### How can I resolve "Your requirements could not be resolved to an installable set of packages" error? [click here](https://stackoverflow.com/questions/29318709/how-can-i-resolve-your-requirements-could-not-be-resolved-to-an-installable-set)
#### After running below command I got solution
```
sudo apt-get install php-xml
```

### Mysql install in linux [click here](https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04)




### Less secure apps will be turned on if you [click here](https://www.google.com/settings/security/lesssecureapps)

