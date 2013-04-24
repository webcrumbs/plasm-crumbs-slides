# PLaSM.js introduction

- - -

## Introduction

### What is PLaSM.js?

Programming Language for Solid Modeling in JavaScript

- - -

## Introduction

### Web environment

[http://cvdlab.github.com/plasm.js/](http://cvdlab.github.com/plasm.js/)

- - - 

## Introduction

### Web environment

#### Commands

mouse drag-and-drop to rotate the scene

mouse scroll to zoom-in/zoom-out

key `c` point the camera to the centroid of the scene

key `x`, `y`, `z` to align the camera along azix x, y or z

key **&larr;**, **&uarr;**, **&rarr;**, **&darr;** to move the camera on the left, up, right or down direction

- - - 

## Introduction

### Installation

#### Prerequisite

Install [NodeJS](http://nodejs.org/)

Install [component module](https://npmjs.org/package/component)

in console

    npm install component -g

- - - 

## Introduction

### Installation

#### Install and build

Create your project folder

in console

    mkdir project
    cd project

Install and build PLaSM component

in a file `component.js`

```json
{
  "dependencies": {
    "cvdlab/plasm-fun": "*"
  }
}
```

in a file `index.html`

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>PLaSM</title>
  <link rel="stylesheet" href="build/build.css">
</head>
<body>
  <section>
    <div id="plasm"></div>
  </section>
  <script src="build/build.js"></script>
  <script>
    var PLASM = require('cvdlab-plasm-fun');
    PLASM('plasm').globalize();
  </script>
</body>
</html>
```

in console

    component install -d
    component build -d

- - -

## Introduction

### Installation (quick) alternative

#### PLaSM.js boilerplate

Clone [PLaSM.js boilerplate](https://github.com/cvdlab/plasm-boilerplate) (a PLaSM.js project scaffold)

in console

    git clone git@github.com:cvdlab/plasm-boilerplate.git
    cd plasm-boilerplate
    component install -d
    component build -d

- - - 

## Introduction

### Test

#### Hello Cube

Open PLaSM.js

in console

    open index.html

in JavaScript Console

    DRAW(COLOR([1,0,0])(CUBE(3))

if PLaSM works, you should see a red cube
