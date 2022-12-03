# Connect Next Block

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
1. **Connect each component up to state and reducers**
    1. **NextBlock**
        1. **Connect the `next-block` component**
        1. **Implement the `mapStateToProps` function**
        1. **Build out the next block grid to show shapes**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Tetris displays the next block in the upper left corner. This is a component that will display a 4 by 4 grid of square components.

![next-block](assets/next-block.png)

With the default game state defined it's time to connect game state to components.

The goal for this chapter is to display the next block in the NextBlock component. To do this you need to get the _index_ of the next block from game state and _map_ this to an array of squares in the component.

The index of the next block is stored at `game.nextShape` on `state`. Use this to find the array that represents this shape, at the first rotation, and map it to the grid.

The empty grid will be:

`const box = shapes[0][0]`

Remember the first block is empty. The shape would be located at:

`const block = shapes[shape][0]`

The color of the square will match the index of the shape.

To get state from Redux into this Component you'll need to connect the component with React-Redux.

# React-Redux Hooks: useSelector

The useSelector hook give your components access to the redux store. 

Add the following import near the top of `/src/components/NextBlock.js`:

```js
import { useSelector } from 'react-redux'
import { shapes } from '../utils'
```

# Get a piece of state

When using `useSelector` you'll provide a callback that recieves state from Redux and returns the `piece' of state that you're interested in. 

For the NextBlock component you need the `nextShape` piece of state. This is an integer that is the index of a shape in your array of shapes. 

In our case the store looks like this: 

```JS
state = {
  nextShape: 1,
  rotation: 1,
  grid: [..bunch of values...],
  ... more properrties ...
}
```

To get `nextShape` the syntax might look like: `state.nextShape`

Use the `useSelector` hook to get the `nextShape` from state. 

```JavaScript
...
export default function NextBlock() {
	const nextShape = useSelector((state) => state.nextShape)
	...
}
```

**Challenge**

Log `state` to the console in the function argument passed to `useSelector`. Inspect the values. 

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

Here's a solution: 

```JS
const nextShape = useSelector(state => {
  console.log(state)
  return state.nextShape
})
```

The inspector should looks something like: 

```
[Log] Object (bundle.js, line 547)
gameOver: false
grid: [Array, Array, Array, Array, Array, Array, Array, Array, Array, Array, …] (18)
isRunning: true
nextShape: 2
rotation: 0
score: 0
shape: 6
speed: 1000
x: 5
y: -4
Object Prototype
```

When you're done change back to: 

```JS
const nextShape = useSelector(state => state.nextShape)
```

We don't want to have log statements everywhere in our code! 

# Display the next shape

Shapes are stored in an array of arrays of arrays. Seriously, the data is nested pretty deep! At the top level the shape array each index is an array of each shape at each rotation. This means that `shapes[1]` would give be the array of all rotations for shape 1, `shapes[1][0]` would be the two dimensional array representing shape 1's first rotation. 

Add the following to the NextBlock component in `/src/components/NextBlock.js`:

```js
...

export default function NextBlock() {
	const nextShape = useSelector(state => state.nextShape)
	const block = shapes[nextShape][0] // Get the first rotation
  ...
}
```

_Now you can use data mapped to props_. The `shape` key on props now holds the index of the shape to display.

# Product So Far

Refresh the browser to see a different shape/orientation appear in the Next Block area! Our Next Block now **uses Redux/Flux to manage application state!** We also covered working with **systems that manage and merge complex arrays,** and have gotten some more practice with **using functional programming methods like `map`!**

![random-next-block](assets/random-next-block.png)

**Challenge**

The next block always shows as orange, that's color 1. The grey squares are color 0. The block shape array is made up of only 0s and 1s. The variable `nextShape` has the index of the shape and this is also the index of the color for that shape! 

Setting the `color` prop on the `GridSquare` component sets the color of the squares. 

If you do this: 

```JS
<GridSquare key={`${row}${col}`} color={nextShape} />
```

You'll see all of the squares change to the color of the shape. Refresh the page a couple times and you should see color chnage because `nextShape` is random in the intial state! 

The challenge, is to set the color prop to 0 when value of `sqaure` is 0 and set the color prop to `nextShape` when square is 1. 

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
-
-
-
-
-
-
-
-
-

Did you solve the challenge? Compare your solution to mine. There is more than one solution your solution might look different, and that's okay. 

```JS
const grid = block.map((rowArray, row) => {
  return rowArray.map((square, col) => {
    const color = square ? nextShape : 0
    return <GridSquare key={`${row}${col}`} color={color} />
  })
})
```

Here I used the ternary operator `? :` as a sort of inline if else. Read about it here: https://javascript.info/ifelse#conditional-operator

# Now Commit

```bash
$ git add .
$ git commit -m 'Added connection for next block'
$ git push
```
