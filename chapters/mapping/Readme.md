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
var domain1 = DOMAIN([[0, PI])([32]);
DRAW(domain1);
```

```js
var domain2 = DOMAIN([[0, PI], [0,1]])([32, 2]);
DRAW(domain2);
```

```js
var domain3 = DOMAIN([[0, PI], [0,1], [0, 0.5]])([32, 2, 5]);
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
var domain = DOMAIN([[0, 2*PI]])([32]);
var mapping = function (v) { return [SIN(v[0]), COS(v[1])]; });
var model = MAP(mapping)(domain);
DRAW(model);
```

```js
var domain = DOMAIN([[0, 2*PI]])([32]);
var mapping = [
  function (v) { return [SIN(v[0])]; },
  function (v) { return [COS(v[1])]; }
];
var model = MAP(mapping)(domain);
DRAW(model);
```

- - - 

## Domain mapping

### Mappings

#### Bisector

```js
var domain = DOMAIN([[0, 5]])([10]);
var mapping = function (v) { return [v[0], v[0]] };
var model = MAP(mapping)(domain);
DRAW(model);
```

```js
var domain = DOMAIN([[0, 5]])([10]);
var fx = function (v) { return [v[0]]; };
var fy = function (v) { return [v[0]]; };
mappings = [fx, fy];
var model = MAP(mappings)(domain);
DRAW(model);
```

- - -

## Domain mapping

### Mappings

#### sin

```js
var domain = DOMAIN([[0, 2*PI]])([36]);
var mapping = function (v) { return [v[0], SIN(V[0])]; };
var model = MAP(mapping)(domain);
DRAW(model1);
```

```js
var fx = function (v) { return [v[0]]; };
var fy = function (v) { return [SIN(V[0])]; };
var mappings = [fx, fy];
var model = MAP(mappings)(domain);
DRAW(model);
```

#### cos

```js
var domain = DOMAIN([[0, 2*PI]])([36]);
var mapping = function (v) { return [v[0], COS(V[0])]; };
var model = MAP(mapping)(domain);
DRAW(model1);
```

```js
var fx = function (v) { return [v[0]]; };
var fy = function (v) { return [COS(V[0])]; };
var mappings = [fx, fy];
var model = MAP(mappings)(domain);
DRAW(model);
```

- - -

## Domain mapping

### Mappings

#### Circle

```js
var domain = DOMAIN([[0, 2*PI]])([36]);
var mapping = function (v) { return [COS(V[0]), SIN(V[0])]; };
var model = MAP(mapping)(domain);
DRAW(model);
```

```js
var domain = DOMAIN([[0, 2*PI]])([36]);
var circle = function (r) {
  return  function (v) {
    return [r * COS(V[0]), r * SIN(V[0])];
  };
};
var mapping = circle(3);
var model = MAP(mapping)(domain);
DRAW(model);
```

- - -

## Domain mapping

### Mappings

#### Sphere

```js
var domain = DOMAIN([[0, PI], [0, 2*PI]])([24,36]);
var mapping = function (v) {
  var a = v[0];
  var b = v[1];
  return [SIN(a)*COS(b), SIN(a)*SIN(b), COS(a)];
};
var model = MAP(mapping)(domain);
DRAW(model);
```

```js
var domain = DOMAIN([[0, PI], [0, 2*PI]])([24,36]);
var sphere = function (r) {
  return function (v) {
    var a = v[0];
    var b = v[1];
    return [r*SIN(a)*COS(b), r*SIN(a)*SIN(b), r*COS(a)];
  };
};
var mapping = sphere(2);
var model = MAP(mapping)(domain);
DRAW(model);
```

- - -

## Domain mapping

### Mappings

#### Torus

```js
var domain = DOMAIN([[0, 2*PI],[0, 2*PI]])([36,72]);
var torus = function (R, r) {
  return function (v) {
    var a = v[0];
    var b = v[1];

    var u = (r * COS(a) + R) * COS(b);
    var v = (r * COS(a) + R) * SIN(b);
    var w = (r * SIN(a));

    return [u,v,w];
  };
};
var mapping = torus(3,1);
var model = MAP(mapping)(domain);
DRAW(model);
```
