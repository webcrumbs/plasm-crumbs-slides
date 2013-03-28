# PLaSM.js domain mapping

- - -

## Domain mapping

### Map

#### MAP(mapping)(domain)

Map a domain by a mapping function.

#### I/O

> **&rArr;** `Function` or `Array<Function>` mapping: the mapping function or an array of mapping functions
> 
> > **&rArr;** `Array` `v`: point of the domain to map
> > 
> > **&lArr;** `Array`: the mapped point.
> 
> **&lArr;** `Function`: an anonymous function.
> 
> > **&rArr;** `plasm.Model` `domain`: the domain to map.
> >
> > **&rArr;** `plasm.Model`: the mapped domain.

#### Example

```js
var mapping = function (v) { return [v[0] + 1, v[1], v[2]]; }
var model = TORUS_SURFACE()()
var mapped = MAP(mapping)(model)
DRAW(mapped)
````

```js
var domain = DOMAIN([[0,1]],[0,2*PI])
var mapping = function (v) { return [SIN(v[0]), COS(v[1])]; })
var model = MAP(mapping)(domain)
DRAW(model)
```

```js
var domain = DOMAIN([[0,1]],[0,2*PI])
var mapping = [
  function (v) { return SIN(v[0]); },
  function (v) { return COS(v[1]); }
]
var model = MAP(mapping)(domain)
DRAW(model)
```
