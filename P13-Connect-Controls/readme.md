# Connect Controls

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
	1. ~~NextBlock~~
	1. ~~GridBoard~~
	1. **Controls**
		1. **Add the actions needed for the controls**
		1. **Implement the `mapStateToProps` function**
		1. **Implement the `mapDispatchToProps` function**
		1. **Connect the `controls` component**
		1. **Call the actions in their appropriate buttons**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Now it's time to issue actions from the buttons. 

Issuing actions will trigger your reducers which will update the state. You'll need to add code to the reducers.

# Dispatch actions from a component with useDispatch

To dispatch actions from a component you need the dispatcher. You can get the dispatcher with `useDipatch` which returns it. 

The controls component will want access to values on state also so it will also import `useSelector`.

At the top of `src/controls.js` import `useDispatch` from `react-redux`:

```JS
...
import { useSelector, useDispatch } from 'react-redux'
...
```

To send an action you'll call the action and pass the value returned as an argument to the dispatcher. 

**Challenge**

Import `moveDown`, `moveLeft`, `moveRight`, `rotate` actions from `src/features/gameSlice.js`.

Check your work against the solution below...

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

Import the `moveDown, moveLeft, moveRight, rotate` actions (as well as `connect`) into `/src/components/Controls.js`

```JS
...
import { moveDown, moveLeft, moveRight, rotate } from '../features/gameSlice'
...
```

The `useDispatch` function returns the dispatcher. Call it at the top of your Controls component and save the dispatcher in a variable. 

**Challenge**

You'll use the `isRunning` from state to disable the buttons when the game is paused. Get the `isRunning` property by calling `useSelector` passing a function as an argument, the argument function should define the state as a parameter and return the state. Get `isRunning` from the state. 

Check your work against the solution below...

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
```js
...

export default function Controls(props) {
	...
	const { isRunning } = useSelector(state => state)
	...
}
```

With this in place, you can get to work making the buttons for their job!

# Call Actions

In the `return` block in `/src/components/controls.js`. Find the "Move Left" button. Edit the "Move Left" button: 

```JS
...
<button 
	disabled={!isRunning}
	className="control-button" 
	onClick={(e) => {
		dispatch(moveLeft())
	}
}>Left</button>
...
```

Notice here you've set the `disabled` prop to `isRunning`. This means the button will be disabled when `isRunning` is true. I put the `!` in front of the `isRunning` boolean to invert it! This way when `isRunning` is `true` then `disabled` will be false!

Next, inside the `onClick` function you called `moveLeft()` and passed its return value to dispatch when you called `dispatch()`. Doing both of these things looks like this: 

```JS
dispatch(moveLeft())
```

You could write this in a longer form like this, and it would do the same thing: 

```JS
const moveLeftAction = moveLeft()
dispatch(moveLeftAction)
```

Either way would work the same! 

**Challenge**

The "Move Right", "rotate", and "moveDown" buttons all need to call their eponymous actions, they should also be disabled when the game is not running. Your job is to complete these buttons!

Check your work against the solution below...

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

Here is the code I had for the whole `Control` component: 

```JS
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { moveDown, moveLeft, moveRight, rotate } from '../features/gameSlice'

export default function Controls(props) {
	const dispatch = useDispatch()
	const { isRunning } = useSelector(state => state)

	return (
		<div className="controls">
      {/* left */}
      <button 
        disabled={!isRunning}
        className="control-button" 
        onClick={(e) => {
          dispatch(moveLeft())
        }
      }>Left</button>

      {/* right */}
      <button 
        disabled={!isRunning}
        className="control-button" 
        onClick={(e) => {
          dispatch(moveRight())
        }
      }>Right</button>

      {/* rotate */}
      <button 
        disabled={!isRunning}
        className="control-button" 
        onClick={(e) => {
          dispatch(rotate())
        }
      }>Rotate</button>

      {/* down */}
      <button 
        disabled={!isRunning}
        className="control-button" 
        onClick={(e) => {
          dispatch(moveDown())
        }
      }>Down</button>

		</div>
	)
}
```

No visual changes yet, we still have a couple more components to connect up. Make sure everything still loads correctly in the browser! Our Controls now **use Redux/Flux to manage application state!**

**Challenge**

Right now the buttons are all enabled (because `isRunning` is true.) Can you think of a way to disable the buttons? 

Check your work against the solution below...

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

Go to `src/utils.js` and set `isRunning` in `defaultState` to `false`. This should disable all of the buttons. Set it back to true when you're done. 

# Now Commit

```bash
$ git add .
$ git commit -m 'Added connection for controls'
$ git push
```
