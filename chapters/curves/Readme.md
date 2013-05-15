# PLaSM.js curves

- - -

## curves

### Bezier

### `BEZIER(sel)(controlpoints)`
Transfinite mapping function of genric degree Bezier curve.

#### I/O

> **&rArr;** `Function` `selector`: domain coordinate selector function.
>
> > **&rArr;** `Array` `v`: point of the `domain`.
> >
> > **&lArr;** `Number`: the selected coordinate.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `controlpoints`: an array of points and curve mapping functions describing curve control points.
> >
> > **&lArr;** `Function`: an anonymous mapping function.

#### Example

```js
var domain = INTERVALS(1)(32);
var controls = [[-0,0],[1,0],[1,1],[2,1],[3,1]];
var mapping = BEZIER(S0)(controls);
var curve = MAP(mapping)(domain);
DRAW(curve);
```

```js
var domain = PROD1x1([INTERVALS(1)(16),INTERVALS(1)(16)]);
var c0 = BEZIER(S0)([[0,0,0],[10,0,0]]);
var c1 = BEZIER(S0)([[0,2,0],[8,3,0],[9,2,0]]);
var c2 = BEZIER(S0)([[0,4,1],[7,5,-1],[8,5,1],[12,4,0]]);
var c3 = BEZIER(S0)([[0,6,0],[9,6,3],[10,6,-1]]);
var surface = MAP(BEZIER(S1)([c0,c1,c2,c3]))(domain);
DRAW(surface);
```

- - - 

### `CUBIC_HERMITE(selector)(controlpoints)`

Transfinite mapping function of cubic Hermite curve.

#### I/O

> **&rArr;** `Function` `selector`: domain coordinate selector function.
>
> > **&rArr;** `Array` `v`: point of the `domain`.
> >
> > **&lArr;** `Number`: the selected coordinate.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `controlpoints`: an array of points and curve mapping functions describing curve control points.
> >
> > **&lArr;** `Function`: an anonymous mapping function.

#### Example

```js
var domain = INTERVALS(1)(20);
var controls = [[1,0],[1,1],[ -1, 1],[ 1,0]];
var mapping = CUBIC_HERMITE(S0)(controls);
var curve = MAP(mapping)(domain);
DRAW(curve);
```

```js
var domain = PROD1x1([INTERVALS(1)(14),INTERVALS(1)(14)]);
var c1 = CUBIC_HERMITE(S0)([[1,0,0],[0,1,0],[0,3,0],[-3,0,0]]);
var c2 = CUBIC_HERMITE(S0)([[0.5,0,0],[0,0.5,0],[0,1,0],[-1,0,0]]);
var mapping = CUBIC_HERMITE(S1)([c1,c2,[1,1,1],[-1,-1,-1]]);
var surface = MAP(sur3)(domain);
DRAW(surface);
```

- - - 

### `NUBSLINE(degree)(knots)(controls)`

Non-uniform B-Spline.

#### I/O

> **&rArr;** `Number` `degree`: spline degree.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `knots`: Array of integer describing spline's knots.
> >
> > **&lArr;** `Function`: an anonymous function.
> >
> > > **&rArr;** `Array` `controls`: Array of integer describing spline's control points.
> > >
> > > **&lArr;** `plasm.Model`: non uniform spline.

#### Example

```js
var controls = [[0,0],[-1,2],[1,4],[2,3],[1,1],[1,2],[2.5,1],[2.5,3],[4,4],[5,0]];
var knots = [0,0,0,0,1,2,3,4,5,6,7,7,7,7];
var nubspline = NUBSPLINE(3)(knots)(controls);
DRAW(nubspline);
```

- - - 

### `NUBS(sel)(degree)(knots)(controls)`

Transfinite Non-uniform B-Spline.

#### I/O

> **&rArr;** `Function` `sel`: selctor function.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Number` `degree`: spline degree.
> >
> > **&lArr;** `Function`: an anonymous function.
> >
> > > **&rArr;** `Array` `knots`: Array of integer describing spline's knots.
> > >
> > > **&lArr;** `Function`: an anonymous function.
> > >
> > > > **&rArr;** `Array` `controls`: Array of integer describing spline's control points.
> > > >
> > > > **&lArr;** `plasm.Model`: non uniform spline.

#### Example

```js
var domain = INTERVALS(1)(20);
var controls = [[0,0],[-1,2],[1,4],[2,3],[1,1],[1,2],[2.5,1],[2.5,3],[4,4],[5,0]];
var nubs = NUBS(S0)(3)([0,0,0,0,1,2,3,4,5,6,7,7,7,7])(controls);
var model = MAP(nubs)(domain);
DRAW(model);
```

```js
var domain = DOMAIN([[0,1],[0,1]])([30,30]);
var b0 = BEZIER(S0)([[0,0,0],[5,-10,0],[10,0,0]]);
var b1 = BEZIER(S0)([[0,2,0],[8,3,0],[9,2,0]]);
var b2 = BEZIER(S0)([[0,4,1],[7,5,-1],[8,5,1],[12,4,0]]);
var b3 = BEZIER(S0)([[0,6,0],[9,6,3],[10,6,-1]]);
var controls = [b0,b1,b2,b3];
var nubs = NUBS(S1)(3)([0,0,0,0,7,7,7,7])(controls);
var model = MAP(nubs)(domain);
DRAW(model);
```

- - - 


### `NURBSLINE(degree)(knots)(controls)`

Non-uniform Rational B-Spline.

#### I/O

> **&rArr;**  `Number` `degree`: spline degree.
>
> **&lArr;**  `Function`: an anonymous function.
>
> > **&rArr;**  `Array` `knots`: Array of integer describing spline's knots.
> >
> > **&lArr;**  `Function`: an anonymous function.
> >
> > > **&rArr;**  `Array` `controls`: Array of integer describing spline's control points.
> > >
> > > **&lArr;**  `plasm.Model`: non uniform rational spline.

#### Example

```js
var p = SQRT(2)/2.0;
var controls = [[-1,0,1], [-p,p,p], [0,1,1], [p,p,p], [1,0,1], [p,-p,p], [0,-1,1], [-p,-p,p], [-1,0,1]];
var knots = [0,0,0,1,1,2,2,3,3,4,4,4];
var nurbs = NURBSPLINE(2)(knots)(controls);
DRAW(nurbs);
```

- - - 

### `SPLINE(curve)(controlpoints)`

Create spline curve.

#### I/O

> **&rArr;** `Function` `curve`: spline curve generator function, such as the result of application of `CUBIC_UBSPLINE` or `CUBIC_CARDINAL` to a domain.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `controlpoints`: an array of points and curve mapping functions describing curve control points.
> >
> > **&lArr;** `plasm.Struct`: the spline.

#### Example

```js
var domain = INTERVALS(1)(20);
var controlpoints = [[-3,6],[-4,2],[-3,-1],[-1,1],[1.5,1.5],[3,4],[5,5],[7,2],[6,-2],[2,-3]];
var splineCardinal = COLOR([1,0,0])(SPLINE(CUBIC_CARDINAL(domain))(controlpoints));
var splineCubic = COLOR([0,1,0])(SPLINE(CUBIC_UBSPLINE(domain))(controlpoints));
var points = SIMPLICIAL_COMPLEX(controlpoints)([[0],[1],[2],[3],[4],[5],[6],[7],[8],[9]]);
var out = STRUCT([splineCardinal,splineCubic,points]);
DRAW(out);
```

- - -

### `CUBIC_CARDINAL(domain)`

Tranfinite Cubic cardinal splines curve generator function on `domain`.

#### I/O

> **&rArr;** `plasm.Model` `domain`: domain of the generator function.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `controlpoints`: an array of points and curve mapping functions describing curve control points.
> >
> > **&lArr;** `plasm.Model`: a spline segment.

#### Example

```js
var domain = INTERVALS(1)(20);
var controls = [[-3,6],[-4,2],[-3,-1],[-1,1],[1.5,1.5],[3,4],[5,5],[7,2],[6,-2],[2,-3]];
var spline = SPLINE(CUBIC_CARDINAL(domain))(controlpoints);
DRAW(spline);
```

- - -

### `CUBIC_UBSPLINE(domain)`

Tranfinite cubic uniform B-splines curve generator function on `domain`.

#### I/O

> **&rArr;** `plasm.Model` `domain`: domain of the generator function.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `controlpoints`: an array of points and curve mapping functions describing curve control points.
> >
> > **&lArr;** `plasm.Model`: a spline segment.

#### Example

```js
var domain = INTERVALS(1)(20);
var controls = [[-3,6],[-4,2],[-3,-1],[-1,1],[1.5,1.5],[3,4],[5,5],[7,2],[6,-2],[2,-3]];
var spline = SPLINE(CUBIC_UBSPLINE(domain))(controlpoints);
DRAW(spline);
```

