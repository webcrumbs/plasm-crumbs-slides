# PLaSM.js basics

- - -

## Simple shapes

### cube

#### `CUBE(dim)`

Create a `dim`-dimensional cube.

#### I/O

> **&rArr;** `Number` `dim`: dimension of the cube.
>
> **&lArr;** `plasm.Model`: a cube with `dim` dimension.

- - -

## Simple shapes

### cube

#### `CUBE(dim)`

Create a `dim`-dimensional cube.

#### Example

```js
var c = CUBE(3)
DRAW(c)
```

- - -

## Simple shapes

### cuboid

### `CUBOID(dims)`

Create a cuboidal simplicial complex with dimensions `[dx, dy, dz, ...]`

#### I/O

> **&rArr;** `Array` `dims`: sides length for each dimension of the simplicial complex
>
> - `Number` `dx`: dimension along x axe
> - `Number` `dy`: dimension along y axe
> - `Number` `dz`: dimension along z axe
> - ...
>
> **&lArr;** `plasm.Model`: a cuboidal simplicial complex with dimensions `dims`

- - -

## Simple shapes

### cuboid

### `CUBOID(dims)`

Create a cuboidal simplicial complex with dimensions `[dx, dy, dz, ...]`

#### Example

```js
var dx = 1;
var dy = 2;
var dz = 3;

var cuboid1 = CUBOID([dx]);
DRAW(cuboid1);
```

```js
var cuboid2 = CUBOID([dx, dy]);
DRAW(cuboid2);
```

```js
var cuboid3 = CUBOID([dx, dy, dz]);
DRAW(cuboid3);
```
