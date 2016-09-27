<h2> Promisss

<h4>Promiss.join

```
Promise.join(
    Promise<any>|any values...,
    function handler
) -> Promise
```

<h4>Promiss.try

```
Promise.try(function() fn) -> Promise
Promise.attempt(function() fn) -> Promise
```

<h4>Promiss.resolve

`
Promise.resolve(Promise<any>|any value) -> Promise
`

Create a promise that is resolved with the given value. If value is already a trusted Promise, it is returned as is. If value is not a thenable,
a fulfilled Promise is returned with value as its fulfillment value.

<h4>Promiss.reject

`
Promise.reject(any error) -> Promise
`

<h4>Promiss.all

多个异步同时调用(iterated)

<h4>Promiss.props

Like .all but for object properties or Maps* entries instead of iterated values. Returns a promise
that is fulfilled when all the properties of the object or the Map's' values** are fulfilled.(map)

*Only the native ECMAScript 6 Map implementation that is provided by the environment
 as is is supported

<h4>PromissAny

`
Promise.any(Iterable<any>|Promise<Iterable<any>> input) -> Promise
`

Like Promise.some, with 1 as count. However, if the promise fulfills,
the fulfillment value is not an array of 1 but the value directly.

<h4>Promiss.some

```
Promise.some([
    ping("ns1.example.com"),
    ping("ns2.example.com"),
    ping("ns3.example.com"),
    ping("ns4.example.com")
], 2).spread(function(first, second) {
    console.log(first, second);
});
```

<h4>Promiss.map

和.all()类似，但是返回来的是混合的Promise或者value。

```
// Using Promise.map:
Promise.map(fileNames, function(fileName) {
    // Promise.map awaits for returned promises as well.
    return fs.readFileAsync(fileName);
}).then(function() {
    console.log("done");
});
```

<h4>Promiss.reduce()

```
Promise.reduce(
    Iterable<any>|Promise<Iterable<any>> input,
    function(any accumulator, any item, int index, int length) reducer,
    [any initialValue]
) -> Promise
```

Given an Iterable(arrays are Iterable), or a promise of an Iterable,
 which produces promises (or a mix of promises and values),
 iterate over all the values in the Iterable into an array and
reduce the array to a value using the given reducer function.

If the reducer function returns a promise, then the result of the promise is awaited,
before continuing with next iteration. If any promise in the array is rejected or
a promise returned by the reducer function is rejected, the result is rejected as well.


<h4>Promiss.filter

```
Promise.map(valuesToBeFiltered, function(value, index, length) {
    return Promise.all([filterer(value, index, length), value]);
}).then(function(values) {
    return values.filter(function(stuff) {
        return stuff[0] == true
    }).map(function(stuff) {
        return stuff[1];
    });
});
```

Given an Iterable(arrays are Iterable), or a promise of an Iterable,
which produces promises (or a mix of promises and values),
iterate over all the values in the Iterable into an array and filter the array to another
 using the given filterer function.

<strong>It is essentially an efficient shortcut for doing a .map and then Array#filter:</strong>

<h4>Promiss.each

Iterate over an array, or a promise of an array, which contains promises
(or a mix of promises and values) with the given iterator function with the signature
 (value, index, length) where value is the resolved value of a respective promise in the input array.
 Iteration happens serially.
If any promise in the input array is rejected the returned promise is rejected as well.

<h4>Promiss.mapSeries

<h4>Promiss.race

<h4>.reflect

`
.reflect() -> Promise<PromiseInspection>
`

The .reflect method returns a promise that is always successful when this promise is settled.
Its fulfillment value is an object that implements the PromiseInspection interface
and reflects the resolution of this promise.
