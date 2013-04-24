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

    $ npm install component -g

- - - 

## Introduction

### Installation

#### Install and build

Create your project folder

    $ mkdir project
    $ cd project

Install plasm component

    $ component install cvdlab/plasm
    $ component build

Create a `index.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <title>plasm.js</title>
    <link href="build/build.js">
  </head>
  <div id="plasm"></div>    
  <script src="build/build.js"></script>
  <script>
    var plasm = require('cvdlab-plasm');
    var app = plasm.Viewer('plasm');
  </script>
</html>
```

Open PLaSM.js

    $ open index.html

- - -

## Introduction

### Installation

#### PLaSM.js boilerplate

Clone PLaSM.js boilerplate (a PLaSM.js project scaffold)

    $ git clone git@github.com:cvdlab/plasm-boilerplate.git
    $ cd plasm-boilerplate
    $ component install
    $ component build

Open PLaSM.js

    $ open index.html
    
Open Tools > JavaScript Console

    > DRAW(COLOR([1,0,0])(CUBE(3))
    
If PLaSM works, you should see a red cube
