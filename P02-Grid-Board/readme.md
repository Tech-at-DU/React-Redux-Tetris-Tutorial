# Grid Board"

1. ~~Implement the overall grid square~~
1. **Implement the game board**
    1. **Build the game board component using the grid squares**
    1. **Import it into `App.js`**
    1. **Style the board**
1. Implement the "next block" area
1. Implement the score board
1. Arrange the layout of the game
1. Implement the controls
1. Implement the message popup
1. Implement the actions and reducers
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

This section takes the grid square created in the last section and displays a group of them as a 10 x 18 grid. This grid of squares will be a component.

![game-board](assets/game-board.png)

Before you build out this grid, let's establish some initial requirements:

- The the main view of the game is made of a 10 x 18 grid.
- Each square on the grid is a single 20px x 20px square rendered from a grid square component.
- The main game logic has not been implemented yet so we will hard code the grid squares for now.
- The grid is made up of an array containing 18 arrays. Each of these arrays represent one row on the grid.
- Each row is an array containing 10 integers. Each integer represents the color displayed at that row and column.
- This a **two dimensional array**. You might visualize it like this
if all the squares contained color 0.

![Two-Dimension-grid-with-Arrays](assets/Two-Dimension-grid-with-Arrays.png)

# Make the GridBoard Component

Make a new file `src/components/GridBoard.js` and put the following code in it:

```js
import React from 'react'
import GridSquare from './GridSquare'

// Represents a 10 x 18 grid of grid squares

export default function GridBoard(props) {

  // generates an array of 18 rows, each containing 10 GridSquares.

	const grid = []
	for (let row = 0; row < 18; row ++) {
		grid.push([])
		for (let col = 0; col < 10; col ++) {
			grid[row].push(<GridSquare key={`${col}${row}`} color="1" />)
		}
	}

  // The components generated in makeGrid are rendered in div.grid-board

	return (
		<div className='grid-board'>
			{grid}
		</div>
	)
}
```

Notice the nested for loop. The outer loop makes 18 rows, and the inner loop makes arrays containing 10 instances of the GridSqaure component. 

Now you should import `GridBoard` into `/src/App.js`

Change `/src/App.js` to the following:

```js
import React from 'react';
import './App.css';

import GridBoard from './components/GridBoard'

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1 className="App-title">Tetris Redux</h1>
      </header>
      <GridBoard />
    </div>
  );
}

export default App;
```

The grid squares should all end up stacked vertically:

![vertical-stack](assets/vertical-stack.png)

To arrange them in a grid we need some more CSS! 

# Use CSS Grid to arrange the squares

Now you'll use the CSS Grid to arrange the single row of grid squareas into an actual grid (what a concept!)

Add the following to `/src/index.css`:

This tells the browser to calculate the size boxes to include the border width rather than adding the border to the width, which is the default behavior.

```css
* {
  box-sizing: border-box;
}
```

Now the grid squares should be 20px by 20px. before they were 20px plus the 5px border width on all sides which was a total of 30px! 

The `.grid-board` class defines the `grid-board` to display as `grid`. This causes the children of this element to arrange on a grid. The number of columns is set by `--cols` var and the width of each column is set by `--tile-size`. These two CSS custom properties were defined in `:root` which allow them to be easily changed.

```CSS
.grid-board {
  display: grid;
  grid-template-columns: repeat(var(--cols), var(--tile-size));
  grid-gap: 0;
  align-self: flex-start;
}
```

Now the orange squares should all be arranged in a 10 by 18 grid. 

# Product So Far

You should now see a grid in your browser:

![orange-grid](assets/orange-grid.png)

To read more about box-sizing, check out this resource on [CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model).

# Now Commit

```bash
$ git add .
$ git commit -m 'Added grid board'
$ git push
```

## Resources

- https://www.w3schools.com/css/css_grid.asp
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model
