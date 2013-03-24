# PLaSM.js transformations

- - - 

## Transformations

### Translate

### `TRANSLATE(dims)(values)(object)` / `T(dims)(values)(object)`

Clone `model` and translate cloned model by `values` on dimensions `dims`.

#### I/O

> **&rArr;** `Array` `dims`: an array of `Number` specifying which dimensions translate (first dim has index 0).
>
> **&lArr;** `Function`: anonymous function.
>
> > **&rArr;** `Array` `values`: an array of `Number` specifying translation quantity for every dimension in `dims`.
> >
> > **&lArr;** `Function`: anonymous function.
> >
> > > **&rArr;** `plasm.Model` or `plasm.Struct` `object`: the object to translate.
> > >
> > > **&lArr;** `plasm.Model` or `plasm.Struct`: the translated object.

- - - 

### `TRANSLATE(dims)(values)(object)` / `T(dims)(values)(object)`

Clone `model` and translate cloned model by `values` on dimensions `dims`.

#### Example

```js
c = CUBE(3)
DRAW(c)
```

```js
c1 = T([1,2])([2,3])(c)
DRAW(c1)
```

- - -

## Transformations

### Rotate

```js
c = CUBE(3)
DRAW(c)
```

```js
c1 = R([1,2])(PI/4)(c)
DRAW(c1)
```

- - -


## Transformations

### Scale

```js
c = CUBE(3)
DRAW(c)
```

```js
c1 = S([1,2])([10,15])(c)
DRAW(c1)
```

