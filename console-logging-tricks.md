## log formatting 
```
console.log('%c STUFF', 'color: orange;'); // css in console
console.log({ foo, bar, baz }); // this puts variable names with objects
console.table([foo, bar, baz]) // displays a table since objects shares common properties
```

## loop times 
```
console.time('looper'); 

for (let i = 0; i < 1000000; i++) { // stuff }
console.timeEnd('looper');
```

## stack trace
gives stacktrack and tells you what line it's called
```
const stuff = () => console.trace('infostuff');
```
