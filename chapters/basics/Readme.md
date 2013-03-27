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

#### Example

```js
var c = CUBE(3)
```

- - -

## Simple shapes

### draw

#### `DRAW(model)`

Add `model` to the scene.

#### I/O

> **&rArr;** `Model` `model`: the model to draw
>
> **&lArr;** `Model` the model

#### Example

```js
var model = CUBE(3)
DRAW(model)
```

- - -

## Simple shapes

### hide

#### `HIDE(model)`

Hide a model of the scene.

#### I/O

> **&rArr;** `Model` `model`: the model to hide
>
> **&lArr;** `Model` the model

#### Example

```js
var model = CUBE(3)
DRAW(model)
HIDE(model)
```

- - -

## Simple shapes

### show

#### `SHOW(model)`

Show an hidden model of the scene

#### I/O

> **&rArr;** `Model` `model`: the model to show
>
> **&lArr;** `Model` the model

#### Example

```js
var model = CUBE(3)
DRAW(model)
HIDE(model)
SHOW(model)
```

```js
var visible = true
window.setInterval(function () {
  if (visible) {
    HIDE(model)
    visible = false
  } else {
    SHOW(model)
    visible = true
  }
}, 1000);
```

- - -

## Simple shapes

### cuboid

### `CUBOID(dims)`

Create a cuboidal simplicial complex with dimensions `dims`

#### I/O

> **&rArr;** `Array` `dims`: sides length for each dimension of the simplicial complex
>
> - `Number` `dx`: dimension along *x* axis
> - `Number` `dy`: dimension along *y* axis
> - `Number` `dz`: dimension along *z* axis
> - ...
>
> **&lArr;** `plasm.Model`: a cuboidal simplicial complex with dimensions `dims`

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

#### Example

```js
var cylinder = CYLSURFACE([1,3])([32,3]);
DRAW(cylinder);
```

```js
//use default values r=1, h=1, slices=16, stacks=2
var cylinder = CYLSURFACE()();
DRAW(cylinder);
```
