# PLaSM.js domain mapping

- - -

## Domain mapping

### Map

#### `DOMAIN(dims)(divs)`

Create a domain.

#### I/O

> **&rArr;** `Array` `dims`: dimensions `[dx, dy, dz, ...]`.
>
> > `Array` `dx`: intervals `[start_x, end_x]`
> > > `Number` `start_x`: *x* min
> > > `Number` `end_x`: *x* max
> >
> > `Array` `dy`: intervals `[start_y, end_y]`
> > > `Number` `start_y`: *y* min
> > > `Number` `end_y`: *y* max
> >
> > `Array` `dz`: intervals `[start_z, end_z]`
> > > `Number` `start_z`: *z* min
> > > `Number` `end_z`: *z* max
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `divs`: divisions `[nx, ny, nz, ...]`.
> >
> > > `Number` `nx`: division along x axes.
> > > `Number` `ny`: division along y axes.
> > > `Number` `nz`: division along z axes.
> >
> > **&lArr;** `plasm.Model`: a domain.

#### Example

```js
var domain1 = DOMAIN([[0,PI])([32]);
DRAW(domain1);
```

```js
var domain2 = DOMAIN([[0,PI], [0,1]])([32, 2]);
DRAW(domain2);
```

```js
var domain3 = DOMAIN([[0,PI], [0,1], [0,0.5]])([32, 2, 5]);
DRAW(domain3);
```

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
