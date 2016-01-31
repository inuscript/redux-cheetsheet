# Redux cheet sheet

## main.js
- createStore
- bindAction
- bindRedux

```js
import React, { Component } from "react"
import ReactDom from "react-dom"
import App from "./Component/App.js"
import reducer from "./reducer"
import { createStore, bindActionCreators, applyMiddleware } from "redux"
import * as actions from "./actions"
import { connect, Provider } from "react-redux"
import thunk from "redux-thunk"

function mapStateToProps(state){
  return state
}

function mapDispatchToProps (dispatch) {
  return bindActionCreators(actions, dispatch)
}

function setupStore(){
  const initialState = {
  }
  const middleware = applyMiddleware(thunk)
  return createStore(reducer, initialState, middleware)
}

function connectedApp(){
  let store = setupStore()
  let Connected = connect(mapStateToProps, mapDispatchToProps)(App)
  return (
    <Provider store={store}>
      <Connected  />
    </Provider>
  )
}

function render(){
  let containerEl = document.querySelector("#container")
  ReactDom.render(connectedApp(), containerEl)
}

render()
```

## reducer
```js
import { combineReducers } from 'redux'
import * as types from "./types"

const todos = (state = null, action) => {
  switch(action.type){
    case types.SET_TODO:
      return action.payload
    default:
      return state
  }
}

const rootReducer = combineReducers({
  todos
})

export default rootReducer
```

## actions

```js
import { createAction } from "redux-actions"
import * as types from "./types"

export const setTodo = createAction(types.SET_TODO, (todo) => todo)
```