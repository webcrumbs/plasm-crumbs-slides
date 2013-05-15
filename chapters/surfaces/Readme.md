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

### `CYLINDRICAL_SURFACE(profile)(vector)`

Create a specific ruled surface where  
`vector` is the direction of the lines  
`profile` is the non-complanar section curve  
that can be a known profile function (e.g. `BEZIER`, ...)

#### I/O

> **&rArr;** `Function` `profile`: mapping `Function` of the profile curve.
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Array` `vector`: an array of vector costant components.
> >
> > **&lArr;** `Function`: mapping of the profile of the cylindrical surface.


#### Example

```js
var domain = PROD1x1([INTERVALS(1)(20),INTERVALS(1)(6)]);
var ncpVector = [0,0,1];
var funProfile = BEZIER(S0)([[1,1,0],[-1,1,0],[1,-1,0],[-1,-1,0]]);
var out = MAP(CYLINDRICAL_SURFACE(funProfile)(ncpVector))(domain);
DRAW(out);
```

- - -

### `CONICAL_SURFACE(apex)(profile)`

Create a conical surface between a vertex (`apex`) and a `profile` curve.  
The curve can be a known profile function, like `BEZIER`, or a custom one.

#### I/O

> **&rArr;** `Array` `apex`: the cone's vertex (an array of coordinates).
>
> **&lArr;** `Function`: an anonymous function.
>
> > **&rArr;** `Function` `profile`: mapping `Function` of the profile curve.
> >
> > **&lArr;** `Function`: mapping of the profile of the conical surface.


#### Example

```js
var domain = PROD1x1([INTERVALS(1)(20),INTERVALS(1)(6)]);
var apex = [0,0,1];
var funProfile = BEZIER(S0)([[1,1,0],[-1,1,0],[1,-1,0],[-1,-1,0]]);
var out = MAP(CONICAL_SURFACE(apex)(funProfile))(domain);
DRAW(out);
```

- - -

### `COONS_PATCH(controlpoints)`

Mapping function of a Coons Patch.

#### I/O

> **&rArr;** `Array` `controlcurves`: an array of curves mapping functions describing surface's boundaries
>
> **&lArr;** `Function`: an anonymous mapping function.

#### Example

```js
var dom1D = INTERVALS(1)(32);
var dom2D = PROD1x1([INTERVALS(1)(16),INTERVALS(1)(16)]);
var Su0 = BEZIER(S0)([[0,0,0],[10,0,0]]);
var curve0 = MAP(Su0)(dom1D);
DRAW(curve0);

var Su1 = BEZIER(S0)([[0,10,0],[2.5,10,3],[5,10,-3],[7.5,10,3],[10,10,0]]);
var curve1 = MAP(Su1)(dom1D);
DRAW(curve1);

var control2 = [[0,0,0],[0,0,3],[0,10,3],[0,10,0]];
var Sv0 = BEZIER(S1)(control2);
var curve2 = MAP(BEZIER(S0)(control2))(dom1D);
DRAW(curve2);

var control3 = [[10,0,0],[10,5,3],[10,10,0]];
var Sv1 = BEZIER(S1)(control3);
var curve3 = MAP( BEZIER(S0)(control3))(dom1D);
DRAW(curve3);

var out = MAP(COONS_PATCH([Su0,Su1,Sv0,Sv1]))(dom2D);
DRAW(out);
```
