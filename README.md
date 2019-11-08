# zip en javascript
 imitando el comportamiento de la funcion zip de python en javascript

 ```js
 function zip() {
    var args = [].slice.call(arguments);
    var shortest = args.length == 0 ? [] : args.reduce(function(a, b) {
        return a.length < b.length ? a : b
    });

    return shortest.map(function(_, i) {
        return args.map(function(array) {
            return array[i]
        })
    });
}
 ```

 ## Es6 sintaxys

 ```js
 let zip = (...rows) => [...rows[0]].map((_,c) => rows.map(row => row[c]))
 ```

 Esta otra version recibe un solo argumento de listas de listas y  asume que todas las listas tienen la misma longitud:

 ```js
 function zip(arrays) {
    return arrays[0].map(function(_,i){
        return arrays.map(function(array){return array[i]})
    });
}

// Si cree que lo siguiente es un valor de retorno válido:
//   > zip([])
//   []
// entonces puedes hacer un caso especial, o simplemente hacer
//  return arrays.length==0 ? [] : arrays[0].map(...)
 ```

 ## Imitar el comportamiento itertools.zip_longest de Python
 insertando undefined donde las matrices no están definidas:
```js
function zip() {
    var args = [].slice.call(arguments);
    var longest = args.reduce(function(a, b) {
        return a.length > b.length ? a : b
    }, []);

    return longest.map(function(_, i) {
        return args.map(function(array) {
            return array[i]
        })
    });
}

// > zip([1,2],[11,22],[111,222,333])
// [[1,11,111],[2,22,222],[null,null,333]]

// > zip()
// []
```