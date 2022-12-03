# Moving Blocks

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. ~~Implement state and shapes~~
1. ~~Connect each component up to state and reducers~~
1. ~~Implement block rotation~~
1. **Implement moving blocks**
    1. **Build out the MOVE_LEFT case in the `game-reducer`**
    1. **Build out the MOVE_RIGHT case in the `game-reducer`**
    1. **Implement a method that adds a given block to the game grid for a given x, y, position and rotation**
    1. **Implement a method that looks at the grid and determines if any rows are filled.**
    1. **Build out the MOVE_DOWN case in the `game-reducer`**
1. Building a timer system
1. Implementing Game Over and Restart

Make sure you can move the blocks left and right. Down is going to involve a bit more complexity, so you'll do that in the next chapter. Now that you have your `canMoveTo` function, this will be a _lot_ easier!

# Left button

In `src/features/gameSlice.js` find the `moveLeft` action and it's reducer. Should look like this: 

```JS
...
moveLeft: () => {},
...
```

Edit this to look like this: 

```JS
moveLeft: (state) => {
  const { shape, grid, x, y, rotation } = state
  if (canMoveTo(shape, grid, x - 1, y, rotation)) {
    state.x = x - 1
  }
  return state
},
```

Again, got state in a parameter variable then deconstructed to get the properties that you needed. You used the `conMoveTo` function to see if you can move to this new position. 

Note: subtracting 1 from x moves the block to the left. So this is the value that you test here. 

If you can move to the left you modify state.

Last you returned state. 

**Challenge**

Test your work!

# Right button

The move right action does the same thing as the move left function with the exception that it will add 1 to x instead of subtracting. 

Sounds like a...

**Challenge**

Find the move right action, and write the reducer yourself! 

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

```JS
moveRight: (state) => {
  const { shape, grid, x, y, rotation } = state
  if (canMoveTo(shape, grid, x + 1, y, rotation)) {
    state.x = x + 1
}
  return state
},
```

**Challenge**

Test your work! 

# Now Commit

```bash
$ git add .
$ git commit -m 'move left and right'
$ git push
```

# Overview of Moving Down

Moving blocks down serves a few purposes:

1. It moves them down (surprising, right?)
1. It serves as the point where blocks are placed at the bottom of the grid and a new block is added and starts from the top
1. It serves as the point where a block hits an already placed block, and a new block is added and starts from the top
1. If you can't move down without blocks extending off of the top of the grid, it can signal a game over

This is a lot more to think about than with left and right! Let's break down some of the mechanics:

- If a block can't move down it should be added to the grid board array. - This will happen by writing the shape number into grid array at the position of the block.
- If a grid square is empty, the value is 0.
- After placing new squares on the grid we can score points.

We will need a function that checks for complete rows on the grid, remove them, and moves all the rows above down by one.

# Implement an Add block to grid function

This function takes in the `shape` (index), `grid` (array), `rotation`, `x`, and `y`. The values in the new shape should be written into the grid.

It's important that this method create a _copy_ of grid before making any changes!

> [action]
>
> In `/src/utils/index.js`, write the `addBlocktoGrid` function as described above:
>
```JavaScript
// Adds current shape to grid
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
    // Get the block array
    const block = shapes[shape][rotation];
    // Copy the grid
    const newGrid = [...grid];            
    // Map the Block onto the grid                                                           
    for (let row = 0; row < block.length; row++) {
        for (let col = 0; col < block[row].length; col++) {
            if (block[row][col]) {
                newGrid[row + y][col + x] = shape;
            }
        }
    }
    return newGrid;
}
```

# Scoring points

Teris awards points when a row is completely filled with squares. The number is greater if multiple rows are filled.

Once a block is placed, it's possible that one or more rows will be filled.

> [action]
>
> In `/src/utils/index.js`, implement a method that looks at the grid and
determines if any rows are filled.
>
```JavaScript
// Checks for completed rows and scores points
export const checkRows = (grid) => {
  // Points increase for each row completed
  // i.e. 40 points for completing one row, 100 points for two rows
  const points = [0, 40, 100, 300, 1200]
  let completedRows = 0
  for (let row = 0; row < grid.length; row++) {
    // No empty cells means it can't find a 0, so the row must be complete!
    if (grid[row].indexOf(0) === -1) {
      completedRows += 1
      // Remove the row and add a new empty one at the top
      grid.splice(row, 1)
      grid.unshift(Array(10).fill(0))
    }
  }
  return points[completedRows]
}
```

# Implement MOVE_DOWN in game reducer

The `MOVE_DOWN` action is likely the most complicated
block of code in the game, a lot happens here. Here is
the logic we need to implement.

- Check if we can move the block down
  - if so we're done
- If block can't move down we need to place it by doing the following.
  - make a new copy of grid
  - add the block to the grid (`addBlockToGrid`)
  - Properties to start a new block
    - set `shape` to `nextShape`
    - set `nextShape` to a new random shape
  - Check if the next shape can be displayed
    - If not, then game over
  - Call `checkRows` to score some points
  and remove completed rows

> [action]
>
> In `/src/reducers/game-reducer.js`, implement the case for `MOVE_DOWN` based on the above logic. Remember to also import your necessary functions from `utils`, and update what props you're extracting from `state`:
>
```JavaScript
...
import {
  defaultState,
  nextRotation,
  canMoveTo,
  addBlockToGrid,
  checkRows,
  randomShape
} from '../utils'
>
...
>
const gameReducer = (state = defaultState(), action) => {
  const { shape, grid, x, y, rotation, nextShape, score, isRunning } = state
>
...
>
case MOVE_DOWN:
  // Get the next potential Y position
  const maybeY = y + 1
  // Check if the current block can move here
  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
      // If so move the block
      return { ...state, y: maybeY }
  }
  // If not place the block
  const newGrid = addBlockToGrid(shape, grid, x, y, rotation)
  // reset some things to start a new shape/block
  const newState = defaultState()
  newState.grid = newGrid
  newState.shape = nextShape
  newState.nextShape = randomShape()
  newState.score = score
  newState.isRunning = isRunning
>
  if (!canMoveTo(nextShape, newGrid, 0, 4, 0)) {
    // Game Over
    console.log("Game Should be over...")
    newState.shape = 0
    return { ...state, gameOver: true }
  }
  // Update the score based on if rows were completed or not
  newState.score = score + checkRows(newGrid)
>
  return newState
>
...
>
}
```

# Product So Far

Now we can move blocks down in the game, and when they get placed, we can move the next block down as well!

![down-block](assets/down-block.png)

This is great! But we have to manually move the blocks down by clicking the down button. We need the blocks to be able to move down on their own, so let's make that now! We also further covered working with **systems that manage and merge complex arrays!**

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'move down'
$ git push
```
