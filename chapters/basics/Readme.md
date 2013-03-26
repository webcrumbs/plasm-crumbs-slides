# PLaSM.js basics

- - -

## Getting started

### draw

#### `DRAW(model)`

Add `model` to the scene.



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

- - - 

## Simple shapes

### cylinder surface

### `CYL_SURFACE(dims)(divs)`

Create a cylindrical surface.

#### I/O

> **&rArr;** `Array` `dims`: dimensions `[r, h]`
> > `Number` `r`: the radius (`1` by default)  
> > `Number` `h`: the height (`1` by default)
>
> **&lArr;** `Function`: an anonymous function
>
> > **&rArr;** `Array` `divs`: divisions `[slices, stacks]`
> > > `Number` `slices`: slices (`16` by default)  
> > > `Number` `stacks`: stacks (`2` by default)
> >
> > **&lArr;** `plasm.Model`: a cylindrical surface with radius `r` and height `h`, divided in `slices` and `stacks`

- - - 

## Simple shapes

### cylinder surface

### `CYL_SURFACE(dims)(divs)`

Create a cylindrical surface.

#### Example

```js
var model = CYLSURFACE()();
DRAW(model);
```
