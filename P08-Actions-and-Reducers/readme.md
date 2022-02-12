1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. **Implement the actions and reducers**
    1. **Build out the actions needed to run the game, including movement, rotation, and game state**
    1. **For each action, build out action creators**
    1. **Create a stub reducer for the game to be filled in later**
    1. **Call `combineReducers` to define state**
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The game will use Redux to store the state of the application. The game board, the next block, whether the game is playing or paused, and the game score are all part of the application state.

The game will respond to a range of actions that you need to define. Actions will be handled by various components, but this won't effect how you define actions since React-Redux will connect actions to any component.

# Overview of Game Actions

## Game Meta
These actions handle running the game.

- **Pause** : Pauses the game
- **Resume** : Resumes the game
- **Restart** : Restarts the game

## Game Play
These actions work with the player controls to move the block.

- **Move Left** : Moves the current block left
- **Move Right** : Moves the current block right
- **Move Down** : Moves the current block down
- **Rotate** : Rotates the current block

## Game Automation
These actions are issued by the game periodically as play
progresses.

**Note:** "Move Down" can be issued by the player or
the game.

- **Move Down** : Moves a block down
- **Set Next** : Get a random block, this will be the next block
- **Game Over** : The game just ended

# Actions

> [action]
>
> Make a new file: `/src/actions/index.js` and put the following code in it:

```JavaScript
export const PAUSE      = "PAUSE"       // Pause the game
export const RESUME     = "RESUME"      // Resume a paused game
export const MOVE_LEFT  = "MOVE_LEFT"   // Move piece left
export const MOVE_RIGHT = "MOVE_RIGHT"  // Move piece right
export const ROTATE     = "ROTATE"      // Rotate piece
export const MOVE_DOWN  = "MOVE_DOWN"   // Move piece down
export const GAME_OVER  = "GAME_OVER"   // The game is over
export const RESTART    = "RESTART"     // Restart Game
```

# Action Creators

> [action]
>
> In the same `/src/actions/index.js` file, define an action creator for each action:

```JavaScript
export const moveRight = () => {
  return { type: MOVE_RIGHT }
}

export const moveLeft = () => {
  return { type: MOVE_LEFT }
}

export const rotate = () => {
  return { type: ROTATE }
}

export const moveDown = () => {
  return { type: MOVE_DOWN }
}

export const pause = () => {
  return { type: PAUSE }
}

export const resume = () => {
  return { type: RESUME }
}

export const restart = () => {
  return { type: RESTART }
}
```

Ok you've got your actions and action creators. Next you need to add a reducer to handle changes to application state.

# Reducer

The reducer takes in **state and an action**. It looks at the `action.type` and compares it to the action strings with a switch statement.

> [action]
>
> Make a new file `/src/reducers/game-reducer.js` and put the following stub code in it:

```JavaScript
import {
  MOVE_RIGHT, MOVE_LEFT, MOVE_DOWN, ROTATE,
  PAUSE, RESUME, RESTART, GAME_OVER
} from '../actions'

const gameReducer = (state = {}, action) => {
  switch(action.type) {
    case ROTATE:
      return state
    case MOVE_RIGHT:
      return state
    case MOVE_LEFT:
      return state
    case MOVE_DOWN:
      return state
    case RESUME:
      return state
    case PAUSE:
      return state
    case GAME_OVER:
      return state
    case RESTART:
      return state
    default:
      return state
  }
}

export default gameReducer
```

This is a stub for the final implementation. So far it imports the actions and defines and exports the
`gameReducer` method.

There is a lot of work to do here. Currently all cases return `state` unchanged. The entire game state will be handled by a single Object which will pass through this reducer and each case will be responsible for making changes to `state` and returning a **copy** of state.

Reducers are responsible for defining the initial value for state. Currently the stub method sets the default value of state to an empty object `{}`.

# Combine Reducers

There is only one reducer but, we still need to call
`combineReducers` to define state.

> [action]
>
> Add a new file `/src/reducers/index.js` with the following code in it:

```JavaScript
import { combineReducers } from 'redux'
import gameReducer from './game-reducer'

// The state handled by `gameReducer` will be stored with the property name `game` on the Redux store.
const reducers = combineReducers({
  game: gameReducer
})

export default reducers
```

# Now Commit

>[action]

```bash
$ git add .
$ git commit -m 'Added initial actions and reducer'
$ git push
```
