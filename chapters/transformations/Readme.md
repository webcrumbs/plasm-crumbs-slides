# PLaSM.js transformations

- - - 

## Transformations

### Translate

```js
c = CUBE(3)
DRAW(c)
```

```js
c1 = T([1,2])([10,15])(c)
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

