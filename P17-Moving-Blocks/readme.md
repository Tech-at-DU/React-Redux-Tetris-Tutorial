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
    1. **Build out the moveLeft action and reducer**
    1. **Build out the moveRight action and reducer**
1. Building a timer system
1. Implementing Game Over and Restart

Make sure you can move the blocks left and right. Down is going to involve a bit more complexity, so you'll do that in the next chapter. Now that you have your `canMoveTo` function, this will be a _lot_ easier!

# Left button

In `src/features/gameSlice.js` find the `moveLeft` action and its reducer. Should look like this: 

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

Again, got the state in a parameter variable and then deconstructed it to get the properties that you needed. You used the `conMoveTo` function to see if you can move to this new position. 

Note: subtracting 1 from x moves the block to the left. So this is the value that you test here. 

If you can move to the left you modify the state.

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
