# Action and Reducers

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. **Implement the actions and reducers**
  1. **Build out the actions needed to run the game, including movement, rotation, and game state**
  1. **Create a stub reducer for the game to be filled in later**
  1. **Add a store and provider for reducers and state**
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The game will use Redux and Redux Toolkit to store the state of the application. The game board, the next block, whether the game is playing or paused, and the game score are all part of the application state.

The game will respond to a range of actions that you need to define. Actions will be issued by various components to do things like play and pause the game and move and rotate blocks. 

Reducers handle the actions to update the application state.

The application state determines what is displayed. When the application is updated all of the components will redraw themselves.

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
These actions are issued by the game periodically as the play
progresses.

**Note:** "Move Down" can be issued by the player or
the game.

- **Move Down** : Moves a block down
- **Set Next** : Get a random block, this will be the next block
- **Game Over** : The game just ended

## Install Redux Toolkit

Import the Redux Toolkit library: 

```bash
npm install @reduxjs/toolkit
```

Import react-Redux. This is the glue that connects Redux with React. 

```bash
npm install react-redux
```

Redux is a state management library and can be used with any package React-redux provides the utility to get React and Redux working together. Redux Toolkit makes it easier to use Redux.

## Create the Store

The store is where all of your application state is stored. 

Make a new folder: `src/app`. 

Then add a new file: `src/app/store.js`:

Add the following code to this new file: 

```JS
import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})
```

You'll be coming back here to add some code in the future. At the moment you are just setting up the "plumbing" that will make the whole thing work. 

Notice that you created the store with `configureStore()` and exported the store to share it with other parts of your app. 

## Set up the Provider

The provider is a component that passes the application state to its child components. You'll wrap your whole App in the Provider so that the application state can be shared with all the other components in the app! 

Edit `src/index.js`:

```JS
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

import { store } from './app/store'
import { Provider } from 'react-redux'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

Notice, everything is the same as the original file with the additions of: 

- You imported `store`
- You imported `Provider`
- You created a new instance of the `Provider` component and it wraps the `App` component!

Testing your app now it should look the same. If you check the inspector you'll see an error: 

> Store does not have a valid reducer. Make sure the argument passed to combineReducers is an object whose values are reducers.

If you recall in the last step our reducers are empty! It looked like this: 

```JS
export const store = configureStore({
  reducer: {},
})
```

This error will be resolved when you define the reducers in the future! 


## Adding a Slice

A slice is a piece of application state. In more detail, the code block for the slice determines what this piece of named, and we need the name to access this piece of state. 

The slice also determines what the initial value is for this piece of state. State is a JS object with properties. Something like: 

```JS
{
  isRunning: true, 
  score: 5200, 
  x: 3, 
  y: 10, 
  ...
}
```

The slice defines actions that can trigger changes to this slice of state. Actions are things that can happen in your app that make changes to state. For example, actions might be things like: 

- `play` - sets `isRunning` to `true`
- `pause` - sets `isRunning` to `false`
- `moveLeft` - Adds 1 to `x`
- `moveRight` - subtracts 1 from `x`

And last, the slice defines reducers that are triggered by actions and makes actual changes to state returning the updated state in the process. 

Reducers are functions that receive the state object, make changes to that object and return the updated state. 

Let's implement the ideas above in the code. Create a new folder: `src/features`.

Create a new file: `src/features/gameSlice.js`.

Add the following: 

```JS
import { createSlice } from '@reduxjs/toolkit'

export const gameSlice = createSlice({
 
})

// Action creators are generated for each case reducer function
export const { } = gameSlice.actions

export default gameSlice.reducer
```

Here `createSlice` takes an object and returns a "slice". 

The slice has some actions stored on its `actions` property and a `reducer` stored on its reducer property. This file exports these. 

Give your slice a name: 

```JS
export const gameSlice = createSlice({
  name: 'game'
})
```

Now add the initial state: 

```JS
export const gameSlice = createSlice({
  name: 'game',
  initialState: {}
})
```

Notice that state is an object. You're going to add some starting values in an upcoming step!

Now add your reducers: 

```JS
export const gameSlice = createSlice({
  name: 'game',
  initialState: {},
  reducers: {}
})
```

reducers is also an object. This object will contain the actions and functions that handle state changes. Before we add those here is a list of the actions we need to make the game work: 

- `pause` Pause the game
- `resume` Resume a paused game
- `moveLeft` Move block left
- `moveRight` Move piece right
- `moveDown` Move block down
- `rotate` Rotate block
- `gameOver` Stops the game
- `restart` Starts the game 

Define the actions like this: 

```JS
export const gameSlice = createSlice({
  name: 'game',
  initialState: {},
  reducers: {
  pause: () => {},
  resume: () => {},
  moveLeft: () => {},
  moveRight: () => {},
  moveDown: () => {}
  },
})
```

The actions are the property names to the left of the colon. 

The functions to the right of each action are reducers. 

There is a lot of work to do here. Each of these functions is responsible for handling changes to state and you will be adding code to each of these functions in the coming steps. 

**Challenge**

Add actions and reducer functions for the following actions: 

- `rotate`
- `gameOver`
- `restart`

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

Does your solution look like this: 

```JS
export const gameSlice = createSlice({
  name: 'game',
  initialState: {},
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
```

The last step here is to export your actions. 

At the bottom of the page find: 

```JS
export const { } = gameSlice.actions
```

Add all of your actions here: 

```JS
// Action creators are generated for each case reducer function
export const { 
  moveLeft, 
  moveRight, 
  moveDown, 
  rotate, 
  pause, 
  resume, 
  gameOver, 
  restart } = gameSlice.actions
```

## Connecting the slice to the store

Now you need to connect this slice to your store. Edit `src/app/store.js`: 

```JS
import { configureStore } from '@reduxjs/toolkit'

import gameReducer from '../features/gameSlice'

export const store = configureStore({
  reducer: gameReducer,
})
```

Here you imported the `gameSlice.reducer` which was exported from `src/features/gameSlice.js`. 

Then you named this piece of state `game` and set the value to the `gameReducer`. 

With that in place, your app should run without error.

I know this might seem pretty mysterious, especially if you haven't used Redux before. But stick with it! This is a professional library that is programmed at a high level! With practice, you will start to understand everything that is going on here! 

What you have done in this step is put all of the boilerplate Redux and Redux Toolkit code into place. All that's left is to fill in the reducers! 

# Now Commit

```bash
$ git add .
$ git commit -m 'Added initial actions and reducer'
$ git push
```

