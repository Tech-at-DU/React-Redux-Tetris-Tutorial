# Next Block

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. **Implement the "next block" area**
    1. **Build the next block component**
    1. **Add style to the component**
    1. **Add the component to `App.js`**
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

Tetris shows you the next block that will appear to
the side of the game grid. This section makes a component for that purpose.

The **next block** will be displayed in a component that will draw itself as a 4 by 4 grid of grid squares. You will reuse the grid square component here.

You might visualize the array that describes the next block like this:

![Next-Block-Array](assets/Next-Block-Array.png)

It's just like the Grid Board array only smaller with 4 rows and 4 columns!

# Make the Next Block Component

Make a new component `/src/components/NextBlock.js` and add the following code to it:

```js
import React from 'react'
import GridSquare from './GridSquare'

// Draws the "next" block view showing the next block to drop
export default function NextBlock(props) {

	const box = [[0,0,0,0], [0,0,0,0], [0,0,0,0], [0,0,0,0]]
	// Map the block to the grid
	const grid = box.map((rowArray, row) => {
		return rowArray.map((square, col) => {
			return <GridSquare key={`${row}${col}`} color={square} />
		})
	})
 
	return (
		<div className="next-block">
			{grid}
		</div>
	)
}
```

You won't see this component until it is added to another component that displays it. Which you will do in an upcoming step. 

# Add styles for the Next Block

Add some styles to arrange these into a grid.

Add the following to `/src/index.css`:

```css
/* Next Block */
.next-block {
  display: grid;
  grid-template-columns: repeat(4, var(--tile-size));
  align-self: flex-start;
}
```

At this point the page is lacking arrangement but the tiles themselves in each component are arranged in a grid.

Also notice the GridSquares are using the default color 0 in the `Next Block` component. We will get the block shape as an array later and use this to set the color of the blocks.

# Add to App.js

Let's see what we have so far:

Update `/src/App.js` by importing `NextBlock` and displaying it:

```js
import React from 'react';
import './App.css';

import GridBoard from './components/GridBoard'
import NextBlock from './components/NextBlock'

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1 className="App-title">Tetris Redux</h1>
      </header>
      <GridBoard />
      <NextBlock />
    </div>
  );
}

export default App;
```

# Product So Far

You should see the following in your browser:

![initial-next-block](assets/initial-next-block.png)

Doesn't look amazing right now, but we'll spruce it up in future chapters. For now, we've gotten some practice with **using functional programming methods like `map`!**

# Now Commit

```bash
$ git add .
$ git commit -m 'Added initial next block'
$ git push
```
