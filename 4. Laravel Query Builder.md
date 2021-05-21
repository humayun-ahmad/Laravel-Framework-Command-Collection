# Laravel Query Builder

## Getting all data:
```
DB::table('table_name')->get();
```

## Getting First Row: 
```
DB::table('table_name')->first();
```

## Adding Where Condition:
```
DB::table('table_name')->where('name', 'John')->get();
```

## Find by ID:
```
DB::table('table')->find(3)
```

## Getting the list of a column:
```
DB::table('table')->pluck('column');
```

## Aggregates:
```
DB::table('table')->count();
DB::table('table')->sum();
DB::table('table')->max();
DB::table('table')->min();
DB::table('table')->where('column' 'value')->avg();
``` 

## Selects:
```
DB::table('table')->select('column', 'column as another_name')->get();
DB::table('table')->distinct()->get();
$query = DB::table('table')->select('column');
$results = $query->addSelect('anoter_column')->get();
DB::table('users')
    ->select(DB::raw('count(*) as user_count, status'))
    ->where('status', '<>', 1)
    ->groupBy('status')
    ->get();
```

## Joins:
```
DB::table('users')
            ->join('profile', 'users.id', '=', 'profile.user_id')
            ->select('users.*', 'profile.phone')
            ->get();
 
```

## Left join:
```
DB::table('customers')
            ->leftJoin('invoices', 'customers.id', '=', 'invoices.customer_id')
            ->get();
 
```

## Right Join:
```
DB::table('customers')
            ->rightJoin('invoices', 'customers.id', '=', 'invoices.customer_id')
            ->get();
 
```

## Unions:
```
$first     = DB::table('customers')
                 ->whereNull('first_name');

$customers = DB::table('customers')
                 ->whereNull('last_name')
                 ->union($first)
                 ->get();
 

``` 

## Where Clauses:
```
$customers = DB::table('customers')
                ->where('votes', '>=', 100)
                ->get();

$customers = DB::table('customers')
                ->where('votes', '<>', 100)
                ->get();

$customers = DB::table('customers')
                ->where('name', 'like', 'T%')
                ->get();
 
```

## Multiple where:
```
$customers = DB::table('customers')
				->where('is_active', '=', '1')
				->where('status', '<>', '1')
				->get();
$customers = DB::table('customers')->where([
    ['is_active', '=', '1'],
    ['status', '<>', '1'],
])->get();
 
```

## Or Statements:
```
DB::table('customers')
    ->where('votes', '>', 100)
    ->orWhere('name', 'John')
    ->get();
 
```
## AND statement inside OR statement:
```
DB::table('customers')
    ->where('votes', '>', 100)
    ->orWhere(function($query) {
        $query->where('premium', '1')
              ->where('votes', '>', 50);
    })
    ->get();
 
```
## WHERE BETWEEN:
```
DB::table('customers')
           ->whereBetween('votes', [1, 100])
           ->get();
```

## WHERE NOT BETWEEN:
```
DB::table('customers')
    ->whereNotBetween('votes', [1, 100])
    ->get();
```

## WHERE IN:
```
DB::table('customer')
    ->whereIn('id', [1, 2, 3])
    ->get();
```

## WHERE NOT IN:
```
DB::table('customer')
    ->whereNotIn('id', [1, 2, 3])
    ->get();
```

## WHERE NULL:
```
DB::table('customers')
    ->whereNull('updated_at')
    ->get();
```

## WHERE NOT NULL:
```
DB::table('customers')
    ->whereNotNull('updated_at')
    ->get();
```

## WHERE DATE:
```
DB::table('customers')
    ->whereDate('created_at', '2016-12-31')
    ->get();
```

## WHERE MONTH:
```
DB::table('customers')
    ->whereMonth('created_at', '12')
    ->get();
```

## WHERE DAY:
```
DB::table('customers')
    ->whereDay('created_at', '20')
    ->get();
```
## WHERE YEAR:
```
DB::table('customers')
    ->whereYear('created_at', '2020')
    ->get();
```

## WHERE COLUMN:
```
DB::table('customers')
    ->whereColumn('first_name', 'last_name')
    ->get();
```
```
DB::table('customers')
    ->whereColumn('updated_at', '>', 'created_at')
    ->get();
```
```
DB::table('customers')
    ->whereColumn([
        ['first_name', '=', 'last_name'],
        ['updated_at', '>', 'created_at'],
    ])->get();
```

## Ordering:
```
DB::table('customers')
    ->orderBy('id', 'desc')
    ->get();
```
```
DB::table('customers')
    ->latest()
    ->first();
 
```
## groupBy / having:
```
DB::table('customers')
    ->groupBy('account_id')
    ->having('account_id', '>', 100)
    ->get();
 
```
## skip / take:
```
DB::table('customers')
	->skip(10)
	->take(5)
	->get();
```
```
DB::table('customers')
    ->offset(10)
    ->limit(5)
    ->get();
``` 

## Chunking Results:
```
DB::table('customers')->orderBy('id')->chunk(100, function ($customers) {
    foreach ($customers as $customer) {
        //
    }
});	
 
```

## Inserts:
```
DB::table('customers')->insert(
    ['email' => 'john@example.com', 'votes' => 0]
);
```
```
DB::table('customers')->insert([
    ['email' => 'taylor@example.com', 'votes' => 0],
    ['email' => 'dayle@example.com', 'votes' => 0]
]);
``` 

## Updates:
```
DB::table('customers')
  ->where('id', 1)
  ->update(['votes' => 1]);
```

## Update Or Insert:
```
DB::table('customers')
    ->updateOrInsert(
        ['email' => 'john@example.com', 'name' => 'John'],
        ['votes' => '2']
    );
 
```

## Increment & Decrement:
```
DB::table('customers')->increment('votes');
DB::table('customers')->increment('votes', 5);
DB::table('customers')->decrement('votes');
DB::table('customers')->decrement('votes', 5);
 
```

## Deletes:
```
DB::table('customers')->delete();
DB::table('customers')->where('votes', '>', 100)->delete();
DB::table('customers')->truncate();
``` 

## Debugging:
```
DB::table('customers')->where('votes', '>', 100)->dd();
DB::table('customers')->where('votes', '>', 100)->dump();
```