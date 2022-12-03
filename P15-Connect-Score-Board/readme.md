# Connect the Score Board

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
    1. ~~Controls~~
    1. ~~Message-Popup~~
    1. **ScoreBoard**
        1. **Implement the `useDispatch`**
        1. **Implement the `UseSelector`**
        1. **Connect the `score-board` component and add the actions that it needs**
        1. **Implement the logic for the play/resume buttons**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The score board component shows the current score. It also has a play/pause and restart button. 

The play button should toggle it's text from 'Play' to 'Pause' as the game changes state.

The value displayed for score will come from the score property of your application `state`. 

The buttons will call actions that play/pause and restart the game.

# Update the ScoreBaord

You need to import both `useDispatch` and `useSelecvtor` from `react-redux` at the top of this component. You need these to dispatch messages and access your application state. Sounds like a...

**Challenge**

Edit `src/components/ScoreBaord.js` and a import `useSelector` and `useDispatch`.

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

You should add this at the top: 

```JS
import { useSelector, useDispatch } from 'react-redux'
```

**Challenge**

Next, import the `pause`, `resume`, and `restart` actions from your `gameSlice` at the top. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Add this at the top: 

```JS
import { pause, resume, restart } from '../features/gameSlice'
```

**Challenge**

Get the dispatcher in your `ScoreBoard` function at the top. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Get the dispatcher: 

```JS
export default function ScoreBoard() {
	const dispatch = useDispatch()
	...
```

**Challenge** 

Get `score`, `isRunning`, and `gameOver` from your application state with `useSelectore`. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Add this at the top of the component:

```JS
export default function ScoreBoard() {
	const dispatch = useDispatch()
	const { score, isRunning, gameOver } = useSelector(state => state)

	...
```

**Challenge**

Display the score. There is a div with the text "Score: 0"


-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
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
<div>Score:{ score }</div>
```

**Challenge**

The restart button should dispatch the restart action when you click it. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
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
<button 
	className="score-board-button" 
	onClick={(e) => {
		dispatch(restart())
	}}>Restart</button>
```

**Challenge**

The Pause/Play button should display "Pause" if the `isRunning` is `true` and "Play" if `isRunning` is false. Try and solve this with the Ternary operator if you can! 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
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
<button 
	className="score-board-button" 
	onClick={(e) => {
		
	}}>{isRunning ? 'Pause' : 'Play'}</button>
```

**Challenge**

Clicking the Play/Pause button should do something different depending on the state of the game. 

- If the game is over it should do nothing
- if the game is running the button should issue the pause action (through the dispatch)
- If the game not running it should issue the resume action. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
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
<button className="score-board-button" onClick={(e) => {
	if (gameOver) { return }
	if (isRunning) {
		dispatch(pause())
	} else {
		dispatch(resume())
	}
}}>{isRunning ? 'Pause' : 'Play'}</button>
```

So far clicking the buttons is not going to change applicatio state, to make that work you need to handle the actions with your reducers. You'll do that soon! 

For now it would be good if you could think of a way to test your work...

**Challenge** 

Test the behavior of these buttons. While you are at it test the score variable. You can test these by mocking them up or by setting the values in your default state. 

When: 
- score = 23000
- isRunning = true
- gameOver = false

The score is 23000 the game is running and not over. The play button should show "Pause". 

When: 
- score = 560000
- isRunning = false
- gameOver = false

The score is 560000, the game is not running, and the not over. The play button show "Play".

When: 
- score = 420
- isRunning = false
- gameOver = true

The game is over, the score is 420, and the play button should be disabled. 

Note! If you mock up the variables in the component the Message Popup will not display. If you set the values in the default state it will. 

In the last few chapters you will get the game working. In these chapters you've built all of the pieces that make up the game. 

# Now Commit

```bash
$ git add .
$ git commit -m 'Added connection for score board'
$ git push
```
