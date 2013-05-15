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

### `RULED_SURFACE(profiles)`

Create a ruled surface S mapping between two profile curves A and B (in `profiles`).
The curves can either be a known profile function, like `BEZIER`, or a custom one (see examples).

#### I/O

> **&rArr;** `Array` `functions`: mapping `Function` of the two curves.
>
> **&lArr;** `Function`: mapping of the profile ruled surface

#### Example

```js
// Hyperbolic paraboloid
var dom2D = T([0,1])([-1,-1])( PROD1x1([INTERVALS(2)(10),INTERVALS(2)(10)]) );
var funAlfa = function(pt) { return [ pt[0], pt[0], 0 ]; };
var funBeta = function(pt) { return [ 1, -1, pt[0] ]; };
var out = MAP(RULED_SURFACE([funAlfa,funBeta]))(dom2D);
DRAW(out);
```

```js
// Linear interpolation of curves: surface connecting a Bézier curve and a portion of a circle
var dom2D = PROD1x1([INTERVALS(1)(50),INTERVALS(1)(50)]);
var funAlfa = BEZIER(S0)([[1,1,0],[-1,1,0],[1,-1,0],[-1,-1,0]]);
var funBeta = function(curveFun) {
  return function(pt) {
    var pAlfa = curveFun(pt);
    return [ 
      COS( PI * (3/2) * pt[0] ) - pAlfa[0], 
      SIN( PI * (3/2) * pt[0] ) - pAlfa[1], 
      1 - pAlfa[2] 
    ];
  };
};
var mapping = RULED_SURFACE([funAlfa,funBeta(funAlfa)]);
var out = MAP(mapping)(dom2D);
DRAW(out);
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

### `ROTATIONAL_SURFACE(profile)`

Create a rotational surface mapping given the mapping of the profile to rotate.

#### I/O

> **&rArr;** `Function` `profile`: mapping of the profile to rotate.
>
> **&lArr;** `Function`: mapping of the rotational surface

#### Example

```js
var domain = DOMAIN([[0,1],[0,2*PI]])([20,20]);
var profile = BEZIER(S0)([[0,0,0],[3,0,3],[3,0,5],[0,0,7]]);
var mapping = ROTATIONAL_SURFACE(profile);
var surface = MAP(mapping)(domain);
```

- - -

### `PROFILEPROD_SURFACE(profiles)`

Create a surface S mapping as profile product between two plane curves A and B (in `profiles`)

#### I/O

> **&rArr;** `Array` `profiles`: mapping `Function` of the two plane curves profile to product.
>
> **&lArr;** `Function`: mapping of the profile product surface

#### Example

```js
var domain_1 = INTERVALS(1)(32);
var domain_2 = PROD1x1([INTERVALS(1)(16),INTERVALS(1)(16)]); // DOMAIN([[0,1],[0,1]])([20,20]);

var controls_a = [[0,0,0],[2,0,0],[0,0,4],[1,0,5]];
var mapping_a = BEZIER(S0)(controls_a);
var curve_a = MAP(mapping_a)(domain1);
DRAW(COLOR([1,0,1])(curve0));

var controls_b = [[0,0,0],[3,-0.5,0],[3,3.5,0],[0,3,0]];
var mapping_b = BEZIER(S1)(controls_b);
var curve_b = MAP(mapping_b)(domain_1);
DRAW(COLOR([1,1,0])(curve_b));

var mapping_b0 = BEZIER(S0)(controls_b);
var curve_b0 = MAP(mapping_b0)(domain_1);
DRAW(COLOR([1,1,0])(curve_b));

var mapping_c = PROFILEPROD_SURFACE([mapping_a,mapping_b]);
var surface = MAP(mapping_c)(domain_2);
DRAW(surface);
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

- - -

### `TRIANGLE_DOMAIN(n, points)`

Create a triangle domain using three points as vertices. Every edge is subdivided in n parts.

#### I/O

> **&rArr;** `Number` `n`: number of subdivisions for every edge
> **&rArr;** `Array` `points`: an array of points, represented as arrays of coordinates.
>
> **&lArr;** `plasm.Model`: a triangle domain.

#### Example

```js
var domTRI = TRIANGLE_DOMAIN(32, [[1,0,0],[0,1,0],[0,0,1]]);
DRAW(domTRI);
DRAW(SKELETON(1)(domTRI));
```

- - -

### `TRIANGULAR_COONS_PATCH(controlcurves)`

Create a triangular Coons patch interpolating three control curves

#### I/O

> **&rArr;** `Array` `curves`: an array of three curves
>
> **&lArr;** instance of `plasm.Model`: a triangular Coons patch.

#### Example

```js
var dom1D = INTERVALS(1)(32);
var dom2D = TRIANGLE_DOMAIN(32, [[1,0,0],[0,1,0],[0,0,1]]);
var Cab0 = BEZIER(S0)([[10,0,0],[6,0,3],[3,0,3],[0,0,0]]);
DRAW(MAP(Cab0)(dom1D));
var Cbc0 = BEZIER(S0)([[10,0,0],[10,2,4],[8,8,-4],[2,10,4],[0,10,0]]);
var Cbc1 = BEZIER(S1)([[10,0,0],[10,2,4],[8,8,-4],[2,10,4],[0,10,0]]);
DRAW(MAP(Cbc0)(dom1D));
var Cca0 = BEZIER(S0)([[0,10,0],[0,6,-5],[0,3,5],[0,0,0]]);
DRAW(MAP(Cca0)(dom1D));
var out = MAP(TRIANGULAR_COONS_PATCH([Cab0,Cbc1,Cca0]))(dom2D);
DRAW(out);
DRAW(SKELETON(1)(out));
```

```js
var dom1D = INTERVALS(1)(32);
var dom2D = TRIANGLE_DOMAIN(32, [[1,0,0],[0,1,0],[0,0,1]]);
var Cab0 = BEZIER(S0)([[0,2,0],[-2,2,0],[-2,0,0],[-2,-2,0],[0,-2,0]]);
DRAW(MAP(Cab0)(dom1D));

var Cbc0 = BEZIER(S0)([[0,2,0],[-1,2,0],[-1,1,1],[-1,0,2],[0,0,2]]);
var Cbc1 = BEZIER(S1)([[0,2,0],[-1,2,0],[-1,1,1],[-1,0,2],[0,0,2]]);
DRAW(MAP(Cbc0)(dom1D));

var Cca0 = BEZIER(S0)([[0,0,2],[-1,0,2],[-1,-1,1],[-1,-2,0],[0,-2,0]]);
DRAW(MAP(Cca0)(dom1D));

var out1 = MAP(TRIANGULAR_COONS_PATCH([Cab0,Cbc1,Cca0]))(dom2D);
DRAW(out1);
DRAW(SKELETON(1)(out1));

var Cab0 = BEZIER(S0)([[0,-2,0],[2,-2,0],[2,0,0],[2,2,0],[0,2,0]]);
DRAW(MAP(Cab0)(dom1D));

var Cbc0 = BEZIER(S0)([[0,-2,0],[1,-2,0],[1,-1,1],[1,0,2],[0,0,2]]);
var Cbc1 = BEZIER(S1)([[0,-2,0],[1,-2,0],[1,-1,1],[1,0,2],[0,0,2]]);
DRAW(MAP(Cbc0)(dom1D));

var Cca0 = BEZIER(S0)([[0,0,2],[1,0,2],[1,1,1],[1,2,0],[0,2,0]]);
DRAW(MAP(Cca0)(dom1D));

var out2 = MAP(TRIANGULAR_COONS_PATCH([Cab0,Cbc1,Cca0]))(dom2D);
DRAW(out2);
DRAW(SKELETON(1)(out2));
```
