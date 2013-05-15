# PLaSM.js surfaces

- - -

## surfaces

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
var domain = PROD1x1([INTERVALS(1)(14),INTERVALS(1)(14)]);
var c1 = CUBIC_HERMITE(S0)([[1,0,0],[0,1,0],[0,3,0],[-3,0,0]]);
var c2 = CUBIC_HERMITE(S0)([[0.5,0,0],[0,0.5,0],[0,1,0],[-1,0,0]]);
var mapping = CUBIC_HERMITE(S1)([c1,c2,[1,1,1],[-1,-1,-1]]);
var surface = MAP(sur3)(domain);
DRAW(surface);
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

