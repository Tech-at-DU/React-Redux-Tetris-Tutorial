
1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. **Do some code organizing and cleanup**
    1. **Create utils to cover ancillary functions**
    1. **Add a store and provider for reducers and state**
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Keeping files organized is important. Rather than clutter components with more code, it's a good idea to move code to other modules and import it where needed.

# Overview of the code

Let's get a sense of the structure of our game:

- The game will manage the game board as an array.
- Each of the blocks will also be defined as an array
- Each shape will be defined as one or more arrays representing the rotation of a block.

This is a lot of arrays that need to be defined.

Rather than clutter a component or reducer with all of these the goal will be to make _another file_ that contains functions and variables that are used by components.

# Utils

The game needs to generate random numbers. The `Math.random()` works but we will need to get integers in a range. It will be good to define a function that is easier to work with.

> [action]
>
> Add a new file `/src/utils/index.js` with the following function in it:

```JavaScript
export const random = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min
}
```

As the project progresses any time we need more general purpose code we can add it to this file, export, and import as needed.

# Now Commit

>[action]

```bash
$ git add .
$ git commit -m 'Added utils'
$ git push
```

# Add Store and Provider

We need to define the Redux store and wrap child components in a provider component to share the store. We're going to need this if we want to work with state and reducers for our app.

Define the store in App and Create a Provider component that wraps the components rendered by App.

> [action]
>
> Update `/src/App.js` to include the following:

```js
import React from 'react';
import { createStore } from 'redux'
import { Provider } from 'react-redux'
import reducers from './reducers'

import './App.css';

import GridBoard from './components/GridBoard'
import NextBlock from './components/NextBlock'
import ScoreBoard from './components/ScoreBoard'
import Controls from './components/Controls'
import MessagePopup from './components/MessagePopup'

const store = createStore(reducers)

function App() {
  return (
    <Provider store={store}>
      <div className="App">
        <header className="App-header">
          <h1 className="App-title">Tetris Redux</h1>
        </header>
        <GridBoard />
        <NextBlock />
        <ScoreBoard />
        <Controls />
        <MessagePopup />
      </div>
    </Provider>
  );
}

export default App;
```

We're now beginning to **Use Redux/Flux to manage application state**, we'll build more on that going forward.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added store and provider'
$ git push
```
