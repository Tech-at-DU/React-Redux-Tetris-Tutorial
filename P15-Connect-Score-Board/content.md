---
title: "Connect Score Board"
slug: connect-score-board
---

Our last component to connect: the score board.

The score board component shows the current score. It also has a play/pause and restart button. The play button should toggle it's text from 'Play' to 'Pause' as the game changes state.

The value displayed for score will come from the game's `state`.
The buttons will call actions that play/pause and restart the game.

# Import Connect, Actions, mapStateToProps, mapDispatchToProps

We know the drill by now. Make sure to do the following, and then check against the solution:

- Import `connect` from 'react-redux'.
- Import the `pause`, `resume`, `restart` actions.
- Map the `score`, `isRunning`, `gameOver` from state to props.
- Map the `pause`, `resume`, and `restart` actions to the dispatcher.

> [action]
>
> Updated `/src/components/score-board.js`:
>
```js
import React, { Component } from 'react'
import { connect } from 'react-redux'
>
import { pause, resume, restart } from '../actions'
>
class ScoreBoard extends Component {
>
    render() {
        return (
            <div className="score-board">
                <div>Score:{this.props.score}</div>
                <div>Level: 1</div>
>
                <button className="score-board-button" onClick={(e) => {
>
                }}>Play</button>
>
                <button className="score-board-button" onClick={(e) => {
>
                }}>Restart</button>
>
            </div>
        )
    }
}
>
const mapStateToProps = (state) => {
  return {
    score: state.game.score,
    isRunning: state.game.isRunning,
    gameOver: state.game.gameOver
  }
}
>
const mapDispatchToProps = () => {
  return {
    pause,
    resume,
    restart
  }
}
>
export default connect(mapStateToProps, mapDispatchToProps())(ScoreBoard)
```

# Pause/Play button

Now we need to get our Play/Pause button working. Let's use the following logic to handle the text of the button:

- If `isRunning` is `true` the button text should show
'Pause'.
- If `isRunning` is `false` the button text should show
'Play'.

Use the following logic to handle clicks on the button.

- If `gameOver` is `false`, exit without any action
- Otherwise if `isRunning` is `true`, call the `pause` action
otherwise call the `resume` action.

Let's implement this:

> [action]
>
> Update the `render` method in `/src/components/score-board.js` to the following:
>
```js
render() {
    const { isRunning, score, resume, pause, restart, gameOver } = this.props
>
    return (
      <div className="score-board">
        <div>Score:{ score }</div>
        <div>Level: 1</div>
>
        <button className="score-board-button" onClick={(e) => {
          if (gameOver) { return }
          isRunning ? pause() : resume()
        }}>{isRunning ? "Pause" : "Resume"}</button>
>
        <button className="score-board-button" onClick={(e) => {
>          
        }}>Restart</button>
>
      </div>
    )
  }
```

# Restart Button

One more small addition to get the restart button working:

> [action]
>
> Update the Restart button within the `render` in `/src/components/score-board.js` to the following:
>
```js
<button className="score-board-button" onClick={(e) => {
    restart()
}}>Restart</button>
```

You may have noticed that the past few chapters we've been wiring buttons up, but they aren't doing anything. That's because our game reducers are just returning `state` still!

In the next few chapters, we're going to update those to actually change the state.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added connection for score board'
$ git push
```