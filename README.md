# How to set up React + Redux

## Install the following NPM packages globally if you haven't already:

```
sudo npm i -g create-react-app
```

Optional - Yarn

```
sudo npm i -g yarn
```

## Run create-react-app and install the following NPM packages for the project:

```
create-react-app *name of react app*

cd *dir of react app*

yarn add axios reactstrap@next bootswatch react-redux redux redux-logger bootstrap
```

## Directory structure

* Create an actions folder in ./src
* Create a reducers folder in ./src
* Create a components folder in ./src
* Create a file named store.js in ./src

### Bootswatch bootstrap css import

* Add from node modules directory either from bootstrap or bootswatch

```javascript
import 'bootstrap/dist/css/bootstrap.css'; 

import 'bootswatch/dist/materia/bootstrap.min.css';
```

## Example actions file

* Create a file in ./src/actions named *component_name*.actions.js

```javascript
export const ADD_ACTION = 'ADD_ACTION'

export const addNewAction = (action) => {
    return {
        type: ADD_ACTION,
        payload: action
    }
}
```

## Example reducers files

* Create a file in ./src/actions named *component_name*.reducer.js

```javascript
import { ADD_ACTION } from '../actions/*component_name*.actions'

let initialState = []

export default ( state = initialState, action ) => {
    switch(action.type) {
        case ADD_ACTION:
            return [ ...state, action.payload ]
        default:
            return state
    }
}
```

* Create a file in ./src/reducers named index.js

This combines all the reducers...

```javascript
import addActionReducer from './*component_name*.reducer.js'
import { combineReducers } from 'redux'

const rootReducer = combineReducers({
    todos: todosReducer
})

export default rootReducer
```

* In the ./src/store.js file

```javascript
import { applyMiddleware, createStore } from 'redux'
import { rootReducers } from './reducers'
import { logger } from 'redux-logger'

export default () => {
    return createStore( {
        rootReducer,
        applyMiddleware(logger)
    } )
}
```