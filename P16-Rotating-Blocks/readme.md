# Rotating Blocks

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
1. **Implement block rotation**
    1. **Implement a util function to provide the next rotation of a shape**
    1. **Implement a util function that tells the game if a shape can move to a certain location**
    1. **Build out the ROTATION case in the `game-reducer`**
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Rotation is handled by setting the `rotation` property on `state`. This integer represents the _index in the shapes array of the shape at a rotation._

Let's do a quick review of the Array that holds the shapes and their rotations. Remember the the shapes array at the top level holds arrays of rotations.

![Shapes-Array](assets/Shapes-Array.png)

At the top level the array holds the shapes.

`[x, I, T, L, J, Z, S, O]`

(Remember `x` is the empty shape)

Each of the letters above represents an Array
of shapes. Each of these shapes is a rotation
of the same shape. For example, in abstract.

`[ [x], [I, –], [T, ...], ... ]`

We see that after the empty shape `x`, the bar array (`I`) is in it hastwo rotations, vertical and horizontal.

Some shapes have a single rotation, such as the `O` shape, which is a square. 

Others have four rotations, for example `J`, and `L`.

From the shapes array, the actual shape is accessed from the shape and rotation index. As we've seen previously:

`shapes[shape][rotation]`

# Make Some New Utils

First off, you're going to be dealing with a lot of moving blocks here. Whether you're rotating, going left, right, or down, you need to know if you can move somewhere. The game needs a function to determine if the current block can move to a new x, y, and rotation. This function will take in the shape, the grid, the x, y, and rotation, and determine if drawing the block with these options would make the block overlap the edges of the board or some placed  blocks. This function will return true if the move is possible, false if not.

Secondly, more specific to the rotation action, you need to be able to easily find the next rotation of a shape, if given the shape and its current rotation.

Both of these functions can be accomplished by making new utilities!

In `/src/utils/index.js`, add the following functions to handle the above scenarios:
>
```js
// Returns the next rotation for a shape
// rotation can't exceed the last index of the the rotations for the given shape.
export const nextRotation = (shape, rotation) => {
    return (rotation + 1) % shapes[shape].length
}

export const canMoveTo = (shape, grid, x, y, rotation) => {
    const currentShape = shapes[shape][rotation]
    // Loop through all rows and cols of the **shape**
    for (let row = 0; row < currentShape.length; row++) {
        for (let col = 0; col < currentShape[row].length; col++) {
            // Look for a 1 here
            if (currentShape[row][col] !== 0) {
                // x offset on grid
                const proposedX = col + x
                // y offset on grid
                const proposedY = row + y
                if (proposedY < 0) {
                    continue
                }
                // Get the row on the grid
                const possibleRow = grid[proposedY]
                // Check row exists
                if (possibleRow) {
                    // Check if this column in the row is undefined, if it's off the edges, 0, and empty
                    if (possibleRow[proposedX] === undefined || possibleRow[proposedX] !== 0) {
                        // undefined or not 0 and it's occupied we can't move here.
                        return false
                    }
                } else {
                    return false
                }
            }
        }
    }
    return true
}
```

# Handle 'ROTATE'

**Challenge**

In `/src/features/gameSlice`, import the new functions `canMoveTo` and `nextRotation` at the top. 

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
import { defaultState, nextRotation, canMoveTo } from '../utils'
```

Let's get our rotation going:

Find the rotate action. It looks like this: 

```JS
...
rotate: () => {},
...
```

Edit this function to the left of the `:`. This is function is a reducer function. It takes in state and an action. It modifies state then returns it. 

In this case you are going to check if the piece can be rotated by getting the next rotation with `nextRotatation` and then checking if it's possible for the block to move to this new position with `canMoveTo`. 

```JS
...
rotate: (state) => {
    const { shape, grid, x, y, rotation } = state
    const newRotation = nextRotation(shape, rotation)
    if (canMoveTo(shape, grid, x, y, newRotation)) {
        state.rotation = newRotation
    }
    return state
},
...
```

Notice that `state` is passed to the to the reducer function and you are getting the properties you need (`x`, `y`, `shape`, `grid`, and `rotation`) from it. 

Notice you are either returning `state` or you are setting `state.rotation` and then returning state. 

A reducer function will always return state. 

Since no blocks are falling on the screen yet, we can't test this out quite yet, but we will soon! We also further covered working with **systems that manage and merge complex arrays!**

**Challenge**

You can test your work by placing the block in the middle of the grid by setting the y property in the default state. 

# Now Commit

```bash
$ git add .
$ git commit -m 'rotate reducer'
$ git push
```
