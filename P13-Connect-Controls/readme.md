
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

Now you'll connect the controls to actions so that you can play the game! Tapping the left, right, and down buttons move the block. Tapping the rotate button changes the rotation of the block.

Controls need to issue actions to control the game. You'll need to connect this component to `state` so it can issue actions that move the block.

This works by sending actions that change `state`, updating the `x`, `y`, and `rotation` values. _Changing these updates the components that use these values as props!_

You can also use `isRunning` to control the display of the buttons. Imagine the case where the game is paused. In this case you might want the buttons to display as disabled. It might be a good idea to map `isRunning` to props on this component.

# Dispatch actions from a component with useDispatch

To dispatch actions from a component use `useDipatch`. The controls component will want access to values on state also so it will also import `useSelector`.

`useDispatch` sends actions from your action creator functions. You'll need to import these also.

> [action]
>
> Import the `moveDown, moveLeft, moveRight, rotate` actions (as well as `connect`) into `/src/components/Controls.js`

```js
...
...
import { useSelector, useDispatch } from 'react-redux'
import { moveDown, moveLeft, moveRight, rotate } from '../actions'

export default function Controls(props) {
	const dispatch = useDispatch()
	const isRunning = useSelector((state) => state.isRunning)
...
}
```

Your controls need to know if the game is running or not. You don't want the buttons function if the game is paused right?

# Call Actions

Currently the buttons in this component just call actions from props with no params. Let's set that up properly now:

> [action]
>
> Edit the `render` method in `/src/components/controls.js` to actually call actions. Remember that actions should only be sent if the `isRunning` is true:

```JS
...
export default function Controls(props) {
	...
	return (
		<div className="controls">
			{/* left */}
			<button className="control-button" onClick={(e) => {
				dispatch(moveLeft())
			}}>Left</button>

			{/* right */}
			<button className="control-button" onClick={(e) => {
				dispatch(moveRight())
			}}>Right</button>

			{/* rotate */}
			<button className="control-button" onClick={(e) => {
				dispatch(rotate())
			}}>Rotate</button>

			{/* down */}
			<button className="control-button" onClick={(e) => {
				dispatch(moveDown())
			}}>Down</button>

		</div>
	)
}
```

Still no visual changes yet, we still have a couple more components to connect up. Make sure everything still loads correctly in the browser! Our Controls now **uses Redux/Flux to manage application state!**

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added connection for controls'
$ git push
```
