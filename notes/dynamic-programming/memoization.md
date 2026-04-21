# Algorithms: Memoization

Memoization is an optimization technique that can be used on _pure functions_. It works by _caching_ the results of computationally expensive calls, so when the same inputs are provided again, the cached result is returned. The cache is typically implemented as a _hash table_ or a _dictionary_, which allows for efficient lookup and insertion of key-value pairs. This is a _space-time trade-off_ where the runtime of the program is reduced at the cost of increased memory usage.

## Implementation

```js
function isPrime(num) {
    /**
     * --- memoization ---
     *
     * This is the memoization logic that creates a cache and
     * returns the cached result if it exists.
     */
    // Create a cache object on the function
    if (!isPrime.answers) isPrime.answers = {};

    // Check for and return previously computed result
    if (isPrime.answers[num] !== undefined) {
        return isPrime.answers[num];
    }

    /**
     * --- computation ---
     *
     * This is the actual function logic implementation that
     * computes the result only if it's not already cached.
     */
    let prime = num !== 1;

    for (let i = 2; i < num; i++) {
        if (num % i === 0) {
            prime = false;
            break;
        }
    }

    return (isPrime.answers[num] = prime);
}
```

## Testing Memoization

Here is a simple function that will take a function and that functions arguments as parameters then log the runtime of the function along with the result.

```js
function checkRuntime(fn, ...args) {
    let startTime = Date.now();
    let result = fn(...args);
    console.log(`Running: ${fn.name}(${args.join(", ")})`);
    console.log(`  -> time: ${Date.now() - startTime} ms`);
    console.log(`  -> result: ${result}`);
}
```

As you can see below the initial run of the `isPrime` function takes a significant amount of time to compute the result. However, the second run of the same function with the same input arguments is almost instantaneous because the result is already cached.

```js
checkRuntime(isPrime, 1000001539); // Running: isPrime(1000000033)
//   -> time: 1343 ms
//   -> result: true

checkRuntime(isPrime, 1000001539); // Running: isPrime(1000000033)
//   -> time: 1 ms
//   -> result: true
```
