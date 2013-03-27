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
- - -

## simple shape

### symplex grid

#### `SIMPLEX_GRID`

Create a grid of simplexes

#### I/O

> **&rArr;** `Array` `quotes`: an array of array of quotes for each dimension of the grid  
> >  quotes start from from dimension `0`  
> >  quotes may be both positive and negative  
> >  - positive quotes are filled
> >  - negative quotes aren't filled  
> 
> **&lArr;** `Model` the simplex grid

#### Example

```js
var grid1 = SIMPLEX_GRID([[1,-1,2]])
DRAW(grid1)
```

```js
var grid2 = SIMPLEX_GRID([[1,-1,2],[2,-1,2]])
DRAW(grid2)
```

```js
var grid3 = SIMPLEX_GRID([[1,-1,2],[2,-1,2],[1,-1,0.5]])
DRAW(grid3)
```

- - -

## simple shape

### polyline

#### `POLYLINE(points)`

Create a polyline made by `points`

#### I/O

> **&rArr;** `Array` `points`: an array of points ([p0, p1, ...])
> > `Array` `points[i]` `i`-th point: an array of coordinates
> > > `Number` `point[k]` `k`-th coord
> 
> **&lArra;** `Model` a polyline made by `points`

#### Example

```js
var points = [[0,0], [1,1], [2,0]];
var polyline = POLYLINE(points);
DRAW(polyline);
```
