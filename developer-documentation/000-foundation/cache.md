# Cache

## Memoize

Memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.(Source (Wikpedia)[http://en.wikipedia.org/wiki/Memoization]

ID: `sulu_core.cache.memoize`
Example usage:

```php
function add($a, $b){
  return $memoize->memoize(function ($a, $b) { return $a+$b; });
}
```

In the first call for `add(1,2)` the closure function will be called with the parameter, the return value will be cached and returned
The second call returns only the value from the cache and the closure will not be called.

The `memoize` method uses `debug_backtrace` to determine calling function. It uses the class, function name and the parameters
to generate a unique cache key to cache the return value.

The `memoizeById` method uses the passed id and the passed parameter to generate the unique cache ID.
