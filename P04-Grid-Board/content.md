---
title: "React Redux Tetris - Grid Board"
slug: react-redux-tetris-
---

This section takes the grid square created in the last 
section and displays them as a 10 x 18 grid.

# Introduction 

The game is made of a 10 by 18 grid. Where each square 
on the grid is a single 20px by 20px square rendered 
from a grid square component. 

The main game logic has not been implmented yet so you 
will hard code the grid squares. 

## Challenges

Make a new file: 'src/components/grid-board.js'. 

```jsx
import React, { Component } from 'react'
import GridSquare from './grid-square'

// Represents a 10 x 18 grid of grid squares

class GridBoard extends Component {

  makeGrid() {
    const grid = []
    for (let row = 0; row < 18; row ++) {
      grid.push([])
      for (let col = 0; col < 10; col ++) {
        grid[row].push(<GridSquare key={`${col}${row}`} color="1" />)
      }
    }

    return grid
  }

  render () {
    return (
      <div classname='grid-board'>
        {this.makeGrid()}
      </div>
    )
  }
}

export default GridBoard
```

The `makeGrid` method generates an array of 18 rows, 
each containg 10 `GridSquares`. 

Test this in 'App.js'.

The grid squares should all end up stacked vertically. 

Use CSS Grid to arrange them into a grid. 

Add the following your stylesheet. 

```css
* {
  box-sizing: border-box;
}

/* Grid Board */
.grid-board {
  display: grid;
  grid-template-columns: repeat(var(--cols), var(--tile-size));
  grid-gap: 0;
  align-self: flex-start;
}
```

The first rule defines the `box-sizing` method to `border-box`
This has the effect of telling the browser to calculate the 
size boxes to inlcude the border width rather than adding
the border, which is the default. 

The second rule defines the `grid-board` to display as `grid`.
This cause the children of this element to arrange on a grid. 
The number of columns is set by `--cols` var and the width 
of each column is set by `--tile-size`. These two CSS custom 
properties are defined in `:root` which allow them to be easily 
changed. 

## conclusion 



## Resources

- 