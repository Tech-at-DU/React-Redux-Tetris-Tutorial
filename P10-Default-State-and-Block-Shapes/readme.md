# Default State and block shapes

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. **Implement state and shapes**
    1. **Provide a definition for the default state of the game**
    1. **Build out a nested array to access all shapes in their array representation**
    1. **Write a function to grab a random shape**
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The game will work by managing it's state in a series of arrays managed by the Redux store. Manipulating and comparing these arrays will determine what the game shows and how the game plays.

Nested arrays represent a two dimensional data structure. This reflects the two dimensional grid the game is played on.

# Representation via Array

The game board is an 18 x 10 grid:

![Two-Dimension-grid-with-Arrays](assets/Two-Dimension-grid-with-Arrays.png)

Each shape will be stored as a 4 x 4 grid. These arrays are stored as arrays of rows where the value represents a column. The values are either **0 (empty)** or **1 (draw a block)**. For example the "T" shaped block could be visualized like this:

![Shape-Array-T](assets/Shape-Array-T.png)

Shapes can be rotated so there will be a 4 x 4 grid representing each rotation. The array of shapes and their rotations could be visualized like this:

![Shapes-Array](assets/Shapes-Array.png)

To access the array containing the shape data, you'll use the _index of the shape followed by the index of the rotation_, e.g.

`shapes[shapeIndex][rotationIndex]`

This would return the 4 x 4 two dimensional array containing the 0s and 1s describing one of the shapes e.g. `shapes[2][0]` would give the "T" shape in the above diagram.

# Game State

Game state is an object stored in Redux. This object will have all of the properties that manage the game. Here is a list of all properties with a short description.

- **grid** : (Array) nested array describing the game board
- **shape** : (Int) **index** of current shape block controlled by player
- **rotation** : (Int) rotation **index** of the current shape block
- **x** : (Int) horizontal position of the current shape block on the game board
- **y** : (Int) vertical position of the current shape block
- **nextShape** : (Int) **index** of the next shape to play
- **isRunning** : (Bool) true when game is running, false when paused
- **score** : (Int) number of points scored
- **speed** : (Int) speed of falling blocks
- **gameOver** : (Bool) true when game is over

# Game Board

The game board will be defined as a set of nested Arrays representing rows and columns. There will be 18 rows of 10 columns.

Each grid square will be represented by an integer:

- 0 is an empty square
- 1-7 represent a color.

All of the color values have a corresponding CSS class name in the stylesheet.

An example game board array might look like this:

```JavaScript
[[0,0,0,0,0,0,0,0,0,0],
  [0,0,0,2,2,2,0,0,0,0],
  [0,0,0,0,2,0,0,0,0,0],
 ... 13 more rows ...
  [0,0,0,0,0,1,1,3,0,0]
  [3,3,0,3,4,1,1,3,3,3]
]
```

**Challenge** In the code snippet above answer these questions:

- Spot the T shaped block in color 2? 
- Find the 2 by 2 square block in color 1. 
- Where would be the best place to place the T shaped block? 

# Empty Array

You need a function that will generate a default empty array. This function needs to return an array containing 18 arrays, each of the nested arrays should contain ten 0s. This represents an empty game board.

**Challenge**

Write a function in `/src/utils/index.js`. Try filling in this function on your own, and then check the solution when you're done:

```JS
...
// Returns the default grid
export const gridDefault = () => {
  const rows = 18
  const cols = 10
  const array = []

  // Fill array with 18 arrays each containing
  // 10 zeros (0)

  return array
}
```

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
-
- 
- 
- 
- 
- 
- 
- 
- 

<!-- -->

Solution!

```js
for (let row = 0; row < rows; row++) {
    array.push([])
    for (let col = 0; col < cols; col++) {
      array[row].push(0)
    }
}
```

# Shapes

Shapes will be mapped onto the board. There are 7 shapes. Let's represent them here as letters. The letters approximate the outline of the shape:

- I (has two rotations)
- T (has four rotations)
- L (has four rotations)
- J (has four rotations)
- Z (has two rotations)
- S (has two rotations)
- O (has one rotation)

Some requirements for the shapes:

- Each shape will be mapped to a two dimensional array with a 1 where the shape should draw and 0 everywhere else.
- Each shape can be rotated and it's rotations will be grouped together into an array.
- All of the rotation arrays will be grouped into a master shape array.
- There will be an extra empty shape at the 0 index.
- The color of each shape corresponds to it's _index_ in the top level of the shape Array.
    - For example, given the order above, the "T" shape is color 2, and the I shape is color 1.

Add the following to `/src/utils/index.js`:

```JavaScript
// Define block shapes and their rotations as arrays.
export const shapes = [
  // none
  [[[0,0,0,0],
    [0,0,0,0],
    [0,0,0,0],
    [0,0,0,0]]],

  // I
  [[[0,0,0,0],
    [1,1,1,1],
    [0,0,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [0,1,0,0],
    [0,1,0,0],
    [0,1,0,0]]],

  // T
  [[[0,0,0,0],
    [1,1,1,0],
    [0,1,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [1,1,0,0],
    [0,1,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [1,1,1,0],
    [0,0,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [0,1,1,0],
    [0,1,0,0],
    [0,0,0,0]]],

  // L
  [[[0,0,0,0],
    [1,1,1,0],
    [1,0,0,0],
    [0,0,0,0]],

   [[1,1,0,0],
    [0,1,0,0],
    [0,1,0,0],
    [0,0,0,0]],

   [[0,0,1,0],
    [1,1,1,0],
    [0,0,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [0,1,0,0],
    [0,1,1,0],
    [0,0,0,0]]],

  // J
  [[[1,0,0,0],
    [1,1,1,0],
    [0,0,0,0],
    [0,0,0,0]],

   [[0,1,1,0],
    [0,1,0,0],
    [0,1,0,0],
    [0,0,0,0]],

   [[0,0,0,0],
    [1,1,1,0],
    [0,0,1,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [0,1,0,0],
    [1,1,0,0],
    [0,0,0,0]]],

  // Z
  [[[0,0,0,0],
    [1,1,0,0],
    [0,1,1,0],
    [0,0,0,0]],

   [[0,0,1,0],
    [0,1,1,0],
    [0,1,0,0],
    [0,0,0,0]]],

  // S
  [[[0,0,0,0],
    [0,1,1,0],
    [1,1,0,0],
    [0,0,0,0]],

   [[0,1,0,0],
    [0,1,1,0],
    [0,0,1,0],
    [0,0,0,0]]],

  // O
  [[[0,1,1,0],
    [0,1,1,0],
    [0,0,0,0],
    [0,0,0,0]]]
]
```

**Challenge**

Identify each of the shapes above. The can be identified by their letter shape: I, T, L, J, Z, S, and O. 

These letter shapes are abstractions of the actual shapes for example O shape is a 2x2 square. 

**Challenge** 

Each of the letter shapes can be rotated. Different shapes may have a different number of rotations! 

For example, the O shape is same at each rotation! So it has only one rotation array!

In your head imagine each of the "letter" shapes rotated and find each shape and it's rotations. 

**Challenge**

Which element in the array is the empty shape? How many rotations does it have? 

# Generate Random Shapes

The game needs to generate a random shape from the shape array. Add a function to handle this.

**Challenge**

Return the index of a random shape from 1 to the number of items in `shapes`. You don't want the first item, which is the empty shape

Add this to `src/utils.js` and export it.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
-
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
-
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
-
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
-

Does your solution look simialar to this? Notice I used the random function written earlier. 

```JavaScript
// Random Shape
export const randomShape = () => {
  return random(1, shapes.length - 1)
}
```

The game will use the returned index to get the shape.

# Game State

We need a function that will return the default object that redux uses with all of the properties reflecting a default game state.

Write a function in `/src/utils/index.js` that generates the default state of the game.

```JavaScript
// Return the default state for the game
export const defaultState = () => {
  return {
    // Create an empty grid
    grid: gridDefault(),
    // Get a new random shape
    shape: randomShape(),
    // set rotation of the shape to 0
    rotation: 0,
    // set the 'x' position of the shape to 5 and y to -4, which puts the shape in the center of the grid, above the top
    x: 5,
    y: -4,
    // set the index of the next shape to a new random shape
    nextShape: randomShape(),
    // Tell the game that it's currently running
    isRunning: true,
    // Set the score to 0
    score: 0,
    // Set the default speed
    speed: 1000,
    // Game isn't over yet
    gameOver: false
  }
}
```

**Challenge** 

Find the following properties in the default state:

- `grid` - Notice you called the `gridDefault()` function here to get the value for this property. 
- `shape` - Notice you called the `randomShape()` to get the value for this property
- `rotation` - 0 starting rotation is 0. By default all shapes will show the shape at the first rotation in the array. 
- `x` and `y` - Notice the starting location for the shape will be 5 and -4. The negative y value will place the shape off the top edge of the grid board. 
- `nextShape` - What is the value here? 
- `speed` - sets the speed of the game in milliseconds
- `gameOver` - The value of `false` means the game is not over when it begins. 

You now have a default state for our game, and we **used Redux to manage the application state!** We also covered the beginnings of **building systems that manage and merge complex arrays!**

Notice you exported this `defaultState` function so you can use it else where in your code. 

## Set the initial state

Edit `src/features/gameSlice.js`. Import the `defaultState` function and use it to define the default state in your store. 

```JS
import { createSlice } from '@reduxjs/toolkit'
import { defaultState } from '../utils'

export const gameSlice = createSlice({
  name: 'game',
  initialState: defaultState(),
  reducers: {
    pause: () => {},
		resume: () => {},
		moveLeft: () => {},
		moveRight: () => {},
		moveDown: () => {},
		rotate: () => {},
		gameOver: () => {},
		restart: () => {}
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = gameSlice.actions

export default gameSlice.reducer
```

Notice you set `initialState` by calling the `defaultState` function. The value of `initialState` is value returned from `defaultState`.

In the next couple steps you'll be updating this file and adding code to each of the action/reducer functions. 

# Now Commit

```bash
$ git add .
$ git commit -m 'Added state utils'
$ git push
```
