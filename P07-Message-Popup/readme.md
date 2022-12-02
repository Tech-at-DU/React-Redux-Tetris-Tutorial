# Message Popup

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. **Implement the message popup**
    1. **Build out message popup component**
    1. **Style the controls**
    1. **Add the component to `App.js`**
1. Implement the actions and reducers
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The game will need to display messages about the game state. Messages will be 'Game Over' and 'Paused' for now but can be expanded to showing score, advancing to a new level, and more.

![Modal](assets/Modal.png)

Let's lay out our usual basic requirements:

- The Message Popup will be a component connected to application state.
- This component will appear above the game board in the center of the screen. Like a message popup.
- The HTML element that holds this component needs to display over the rest of the component elements.
- It won't be arranged with Grid and instead will use CSS absolute position. This allows us to place this anywhere on the screen regardless of the other elements.

# Building the message popup

Add a new file: `/src/components/MessagePopup.js` with the following code:

```JS
import React from 'react'

// Displays a message
export default function MessagePopup(props) {
  return (
    <div className='message-popup'>
      <h1>Message Title</h1>
      <p>Message info...</p>
    </div>
  )
}
```

# Give Some Flair to the Message

Use styles to position and display the Message Popup.

Add the following to `/src/index.css`:

Message Popup - These styles apply to the `MessagePopup` container. With `position:absolute` this element can be placed anywhere on the screen, `left, top, transform:translate` perform this function.

```CSS
/* Message Popup Styles */
.message-popup {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: calc(var(--tile-size) * 10);
  height: calc(var(--tile-size) * 10);
  background-color: rgba(255, 255, 255, 0.5);
  text-align: center;
}
```

This style is applied only when the message popup container has both `message-popup` class and the `hidden` class. In this case the Message Popup is not displayed

```CSS
.message-popup.hidden {
  display: none;
}
```

# Add to App.js

Import and add the message popup component to the _bottom_ of App. **It should be the last component in App.**

Add the following to `/src/App.js`

```js
import React from 'react';
import './App.css';

import GridBoard from './components/GridBoard'
import NextBlock from './components/NextBlock'
import ScoreBoard from './components/ScoreBoard'
import Controls from './components/Controls'
import MessagePopup from './components/MessagePopup'

function App() {
  return (
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
  );
}

export default App;
```

# Product So Far

Your browser should now look like the following:

![initial-message](assets/initial-message.png)

Alright, we've got our components in place! Now it's time to make them do something!

# Now Commit

```bash
$ git add .
$ git commit -m 'Added initial message popup'
$ git push
```
