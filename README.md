# Redux Course

#### [Redux course by Anurag singh procodrr](https://www.youtube.com/playlist?list=PLfEr2kn3s-br2OoBNSR7S5eJ-kcEeUQcG)

## [Redux Fundamentals in Hindi ](https://github.com/iamtango/redux-course/blob/main/01_redux-intro-and-reducer-pattern/script.js)

- Why we need Redux?
  - It is state management library which is help to effeciently `manage the state`of the application and `Avoid Prop drilling`.
- What is different between ContextAPI and Redux
  - Behind the scene Redux using ContextAPI but in the ContextAPI it requires creating multiple context providers for independent state pieces, potentially leading to nested providers when managing multiple contexts.
  - Redux simplifies state management by providing a single provider `<Provider>` for the entire application, ensuring predictable state updates and facilitating global access to state with minimal setup.

```js
// Example of Context API with multiple context provider and pass the children inside the context Provider
<Context1.Provider value={value1}>
  <Context2.Provider value={value2}>
    <Context3.Provider value={value3}>...</Context3.Provider>
  </Context2.Provider>
</Context1.Provider>

// Example of Redux with multiple Redux provider and pass the children inside the Provider
<Provider store={value}>
<Provider>
```

### Redux Components

- [Redux has 4 components namely, `Store` `Reducer` `Action` and `Middleware`.](https://blog.logrocket.com/understanding-redux-tutorial-examples/)

#### What is a `Store`?

- The store is a `container` that holds the application state, and the only way the state can change is through actions dispatched to the store. Redux allows individual components to connect to the store.
- It is highly recommended to keep` only one store` in any Redux application

#### What is a `Reducer`?

- A reducer is a pure function, which returns the state of the application based on the action dispatched by the store.

#### What is an `Action`?

- It is a payload of information that transmits data from an application to a store. They are the sole source of information for the store. One can send them to the store using store. dispatch() .
- Actions are plain JavaScript objects that must have:

  - A `type` property to indicate the type of action to be carried out
  - A `payload` object that contains the information that should be used to change the state

- Actions are created via an action creator, which is a function that returns an action. Actions are executed using the `dispatch()` method, which sends the action to the store

#### What is a` Middleware`?

- Redux allows developers to intercept all actions dispatched from components before they are passed to the reducer function. This interception is done via middleware, which are functions that call the next method received in an argument after processing the current action.

### `createStore`

- in createStore we need to pass the reducer function
- it has 3 method `getState`, `dispatch` & `subscribe`

#### `getState()`

- Returns the `current state` tree of your application. It is equal to the last value returned by the store's reducer.

#### `dispatch()`

- It is use to call the reducer funtion.
- Dispatches an action. This is the only way to trigger a state change by passing th action.
- The store's reducer function will be called with the current getState() result and the given action synchronously.

#### `subscribe()`

- Adds a change listener. It will be called any time an action is dispatched, and some part of the state tree may potentially have changed. You may then call getState() to read the current state tree inside the callback.

## [Manage Complex State using Redux](https://github.com/iamtango/redux-course/blob/main/04_manage-complex-state-using-redux/script.js)

## [Creating Multiple Reducers | combineReducers in Redux ](https://github.com/iamtango/redux-course/blob/main/05_creating-multiple-reducers)

### combineReducers

- It is use to combine multiple reducers
- The combineReducers helper function turns an object whose values are different `slice reducer` functions into a single combined reducer function.

## [Action Creators in Redux](https://github.com/iamtango/redux-course/tree/main/07_action-creators-in-redux)

#### Action Types

- Action is just an object which goal is to describe your actual intention with a type field and maybe by adding some additional data.

#### Action creators

- Action creators are functions that create and return action objects.
- Action creators help organize and centralize the logic for creating these action objects

### Ducks Pattern

- In the same file we write `actions`, `action Creators` , `reducer`.

## [Connect Redux with React](https://github.com/iamtango/redux-course/blob/main/08_connect-redux-with-react/App.js)

### `useSelector`

- It is hook which help us to subscribe to the redux store it take one call back
  function and comes from react-redux
- useSelector() will also subscribe to the Redux store, and run your selector whenever an action is dispatched
- When an action is dispatched, useSelector() will do a reference comparison of the previous selector result value and the current result value.
- If they are different, the component will be forced to re-render. If they are the same, the component will not re-render.
- useSelector() uses strict === reference equality checks by default, not shallow equality

  ```js
  const productsList = useSelector((state) => state.products);
  ```

## [Make Shopping Cart using React and Redux](https://github.com/iamtango/redux-course/tree/main/09_make-shopping-cart/final-code)

### `useDispatch`

- This hook returns a reference to the dispatch function from the Redux store. You may use it to dispatch actions as needed and comes from react-redux.

  ```js
  const dispatch = useDispatch();
  dispatch(action());
  ```

## [What are Slices in Redux?](https://github.com/iamtango/redux-course/tree/main/11_what-are-slices-in-redux/store/slices)

## [Immer in Redux](https://github.com/iamtango/redux-course/blob/main/12_immerJS-in-redux/store/slices/cartSlice.js)

### produce method

- If we want to change/modify the reducer by functional programming then we use the produce method from the immer library
- first argument is the array of object and then callback function, in that call back function the first argument we get is the copy/proxy object of given array of objects
- [produce takes a base state, and a recipe that can be used to perform all the desired mutations on the draft that is passed in. The interesting thing about Immer is that the baseState will be untouched, but the nextState will reflect all changes made to draftState.](https://immerjs.github.io/immer/produce/#:~:text=produce%20takes%20a%20base%20state,all%20changes%20made%20to%20draftState%20.)
- Produce method return new array

## [Redux Toolkit in Hindi](https://github.com/iamtango/redux-course/blob/main/13_redux-toolkit/store/slices/cartSlice.js)

### createSlice

- it return actions and reducer
- A function that accepts an initial state, an object of reducer functions, and a "slice name", and automatically generates action creators and action types that correspond to the reducers and state.

#### initialState

- The initial state value for this slice of state.

#### name

- A string name for this slice of state. Generated action type constants will use this as a prefix.

#### reducers

- An object containing Redux "case reducer" functions (functions intended to handle a specific action type, equivalent to a single case statement in a switch).

```js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: 0,
  reducers: {
    increment: (state) => state + 1,
  },
});
export const { ncrement } = counterSlice.actions;
export default counterSlice.reducer;
```

### configureStore

- Combining the slice reducers into the root reducer
- Creating the middleware enhancer, usually with the thunk middleware or other side effects middleware, as well as middleware that might be used for development checks
- Adding the Redux DevTools enhancer, and composing the enhancers together
- Calling createStore

## [Middleware in Redux](https://github.com/iamtango/redux-course/blob/main/15_middlewares-in-redux/store/middleware/logger.js)

### middleware

- It is the curring funtion
  - it has 3 params `store`, `next` and `action`
    - `store` has 2 params `getState` and `dispatch`
- By default middleware stop the execution but we can avoid using `next(action)`
- we can create the middleware using the middleware key in configureStore object
- we can Provide multiple middlewares by passing the middlewares in the array

## [Making API Call in Redux](https://github.com/iamtango/redux-course/tree/main/16_making-api-calls-in-redux)

### Fetching the data we have 4 methods to fetch the data

#### Custom API Middleware

#### Thunk

#### Redux Toolkit Query

#### Redux Saga

<hr>
We cannot directly update the whole store  by assigning the action.payload to whole application intead we can return the action.payload to update the whole store.
<br>
if u want to update the whole state in redux then instead of assigning it state= action.payload ❌ just return it.

return action.payload ✅

- Incorrect Approach: state = action.payload ❌

  - This approach mutates the state variable directly. In Redux, you should never mutate the state directly. Instead, you should return a new state object.

- Correct Approach: return action.payload ✅

  - This approach returns a new state object which is a clean and straightforward way to replace the entire state. This ensures that the state remains immutable and adheres to the principles of Redux.

## [Selectors in Redux](https://github.com/iamtango/redux-course/tree/main/17_selectors-in-redux/store/slices)

### What is Selector

- A callback function which is use to pass inside the useSelector hook is calle selector
- A good convention is to write the selector inside the where slice has been define

```js
// slice file
export const getAllProducts = (state) => state.products.list;

// file where useselector hook is used
const productsList = useSelector(getAllProducts);
```

- `createSelector` is a function which is use to memoize the selector by passing the selector as first argument and in the second argument we can pass the callback function

```js
createSelector(getCartItems, (cartItems) => cartItems);
```

## [Custom API Middleware in Redux](https://github.com/iamtango/redux-course/blob/main/18_custom-api-middleware/components/Header.js)

### [API Action Creator](https://github.com/iamtango/redux-course/blob/main/18_custom-api-middleware/store/middleware/api.js)

- It is normal function which has

```js
export const fetchData = (payload) => ({ type: "api/makeCall", payload });
```

## [Fetch Data using Redux Thunk](https://github.com/iamtango/redux-course/blob/main/19_redux-thunk/components/Header.js)

### [Middleware type function](https://github.com/iamtango/redux-course/blob/main/19_redux-thunk/store/middleware/func.js)

- Redux Thunk is a middleware that allows dispatching functions and executing delayed tasks.
- by default the thunk middleware comes with RTK an If we donot write any middlware then the thunk middleware will be activated
- Thunk is something a piece of code that does some delayed work

```js
export const func =
  ({ dispatch, getState }) =>
  (next) =>
  (action) => {
    if (typeof action === "function") {
      action(dispatch, getState);
    } else {
      next(action);
    }
  };
```

- If we want to use custom middleware along with the thunk middleware then we ca use by using following syntax
  ```js
    middleware: (getDefaultMiddleware) => [...getDefaultMiddleware(), logger],
  ```

#### Redux Thunk middleware allows dispatching of functions in the Redux store for data fetching and handling.

## [createAsyncThunk](https://github.com/iamtango/redux-course/blob/main/20_createAsyncThunk/store/slices/cartSlice.js)

- We need to pass the action type as first argument and callback function as second argument
- It will automatically create action creators and they are `fulfilled`, `pending` and `rejected` are the three action creators

```js
export const fetchCartItemsData = createAsyncThunk(
  "cart/fetchCartItems",
  async () => {
    try {
      const response = await fetch(`https://fakestoreapi.com/carts/5`);
      return response.json();
    } catch (err) {
      throw err;
    }
  }
);
```

### extraReducers

- <b>extraReducers allows createSlice to respond and update its own state in response to other action types besides the types it has generated.</b>
- However, unlike the reducers field, each individual case reducer inside of extraReducers will not generate a new action type or action creator.

- If two fields from reducers and extraReducers happen to end up with the same action type string, the function from reducers will be used to handle that action type.
- the extraReducers field uses a "builder callback" notation to define handlers for specific action types, matching against a range of actions, or handling a default case.

```js
  extraReducers: (builder) => {
    builder
      .addCase(fetchCartItemsData.pending, (state) => {
        state.loading = true
      })
      .addCase(fetchCartItemsData.fulfilled, (state, action) => {
        state.loading = false
        state.list = action.payload.products
      })
      .addCase(fetchCartItemsData.rejected, (state, action) => {
        state.loading = false
        state.error = action.payload || 'Something went wrong!'
      })
  },
```

## [RTK Query Complete Guide](https://github.com/iamtango/redux-course/blob/main/19_redux-thunk/components/Header.js)

- RTK Query is a powerful data fetching and caching tool.
- It is designed to simplify common cases for loading data in a web application, <b>`eliminating the need to hand-write data fetching & caching logic yourself`.</b>
- RTK Query is `an optional addon included in the Redux Toolkit package`, and its functionality is built on top of the other APIs in Redux Toolkit.

### [Optimastic Updates](https://medium.com/@stojanovic.nemanja71/optimistic-updates-in-tanstack-query-v5-dfbcbb124113)

- Optimistic update is a technique used in web development to enhance the user experience. Sometimes, in order to make our application feel faster to users, we can assume that certain operations will succeed and update the UI immediately, without waiting for confirmation from the server.

#### [createApi](https://github.com/iamtango/redux-course/blob/main/21_rtk-query/final-code/src/apiSlice.js)

- createApi is the core of RTK Query's functionality.
- It allows you to define a set of "endpoints" that describe how to retrieve data from backend APIs and other async sources, including the configuration of how to fetch and transform that data.
- It generates an "API slice" structure that contains Redux logic (and optionally React hooks) that encapsulate the data fetching and caching process for you.
- It Also Provide the chaching functionality
- It take Object as argument where it contains

```js
export const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: "http://localhost:3000" }),
  tagTypes: [""], // it help to refetch data after a successful completion of the request
  endpoints: (builder) => ({}),
});
```

- If we want to get the data then we need to use the `builder.query` method to get the data

```js
 getTasks: builder.query({
      query: () => "/tasks",
      transformResponse: (tasks) => tasks.reverse(), // it help to get the data in reverse order
      providesTags: ["Tasks"], // it help to call the function after thesuccessful completion of the request
    }),

```

- But for Post,Update or delete then we have to use the `builder.mutation` method

```js
 addTask: builder.mutation({
      query: (task) => ({
        url: "/tasks",
        method: "POST",
        body: task,
      }),
      invalidatesTags: ["Tasks"], //this will call the getTasks()  after post call made
    }),
```

- <b> After Using the createApi if we wanted to use in the app then we must need to Wrap our component with the < ApiProvider> < /ApiProvider>Component</b>

```js
<ApiProvider api={api}>
  <App />
</ApiProvider>
```

#### [Want to use redux store with the createApi then instead of wraping the app with < ApiProvider> we can wrap simply by < Provider> and we have to pass the createApi into the store and also we have to provide the middlware into it](https://github.com/iamtango/redux-course/blob/main/21_rtk-query/final-code/src/store.js)

<h3>Commonly asked Redux questions to help you ace your interview! 💻</h3>

<details>
   <summary> What is Redux, and why is it used in React applications?</summary>
  <p><i> Redux is a predictable state management library commonly used with JS applications. It provides a centralized store to manage the state of the entire application, which helps in maintaining consistency, predictability, and traceability of the application's state. Redux is particularly useful for managing complex state interactions, avoiding prop drilling, and facilitating easier debugging and testing.</i></p>
  <b>Why Redux is used in React applications:</b>
  <pre><b>Centralized State Management</b>: Redux provides a single source of truth for the application's state, making it easier to manage and maintain.
  <b>Predictability</b>: Redux enforces strict rules for how the state can be updated, ensuring that the state changes in a predictable manner.
  <b>Debugging</b>: Redux's single state tree and clear flow of actions and reducers make it easier to debug and understand how the state changes over time.
  <b>Testing</b>: Redux's pure functions (reducers) and clear state transitions simplify unit testing.
  <b>Middleware</b>: Redux allows the use of middleware to handle side effects, asynchronous actions, logging, and more, making it a flexible solution for various needs.
  <b>Time-Travel Debugging</b>: With Redux DevTools, developers can rewind and replay state changes, aiding in identifying issues and understanding the application's behavior.
  <b>Scalability</b>: Redux is designed to handle applications of any size, making it suitable for both small and large applications.</pre>
</details>

<br>

<details>
   <summary>  Explain the core principles of Redux (Actions, Reducers, Store).</summary>
  <p><i>Redux is built on three core principles: Actions, Reducers, and Store. These principles work together to manage and update the state of an application in a predictable and organized manner.</i></p>
  <b>Actions:</b>  Actions are plain JavaScript objects that represent an intention to change the state.
  <br> An action must have a type property, which indicates the type of action being performed. Optionally, it can have a payload property that carries additional data needed for the state transition.
   <br>
   <pre><code> 
    const incrementAction = {
     type: 'INCREMENT',
    payload: 1
    };
    </code></pre>
  <b>Reducers:</b>  Reducers are pure functions that take the current state and an action as arguments, and return a new state.
  <br> Reducers specify how the application's state changes in response to actions sent to the store.
   <br>
   Reducers must be pure functions, meaning they should not have side effects and should return the same output given the same input.
   <pre><code> 
   const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + action.payload;
    case 'DECREMENT':
      return state - action.payload;
    default:
      return state;
  }
};
    </code></pre>
  <b>Store:</b>  The store is a central repository that holds the entire state of the application. or we can say  Store holds the application's state and provides methods to access, dispatch actions, and listen for state changes.
  <br> 
  getState(): Returns the current state of the application.
  <br>
   dispatch(action): Dispatches an action to the store to change the state.
   <br>
   subscribe(listener): Adds a change listener that is called whenever anaction is dispatched, and the state might have changed.
   <br>
   Reducers must be pure functions, meaning they should not have side effects and should return the same output given the same input.
   <pre><code> 
    const incrementAction = {
     type: 'INCREMENT',
    payload: 1
    };
    </code></pre>
</details>

<br>

<details>
  <summary>Describe the flow of data in a Redux application.</summary>
  <p>
  <b>Action Creation:</b>
    An action is an object that describes a change or event in the application. It has a type and, optionally, a payload.
    <br>
    <b>Dispatching an Action:</b>
    An action is dispatched using the dispatch function. This sends the action to the Redux store.
    <br>
    <b>Reducers:</b>
    Reducers are pure functions that take the current state and the dispatched action as arguments. They return a new state based on the action's type and payload.
    <br>
    <b>Store Update:</b>
    The Redux store updates its state based on the new state returned by the reducers.
    <br>
    <b>State Access:</b>
    Components access the updated state using useSelector (in React) or by subscribing to the store.
    <br>
    <b>UI Re-render:</b>
    Components that depend on the updated state re-render to reflect the changes.</p>
  <p><b><h1>Work Flow<h21> </b><h2>1. Action Creation → 2. Dispatching an Action → 3. Reducers → 4. Store Update → 5. State Access → 6. UI Re-render</h2></p>
</details>

<br>

<details>
   <summary> Why is immutability important in Redux, and how is it achieved?</summary>
  <p><i> Immutability ensures that state changes are predictable and traceable. Each action results in a new state, making it easier to debug and understand the flow of data.</i></p>
  <i>Immutability enables shallow comparison checks, improving performance. React components can quickly determine if they need to re-render by comparing previous and current state objects.</i>
  <i>Immutability prevents unintended side-effects by ensuring that state objects are not modified directly. This leads to more reliable and maintainable code.</i>
  <br>
  <b>How is Immutability Achieved in Redux?</b>
  <p>
  <i>♦ Reducers are designed as pure functions that take the current state and an action as arguments and return a new state without modifying the original state.</i>
  <br>
  <i>♦ The spread operator (...) is used to create shallow copies of objects or arrays, ensuring that the original state remains unchanged.</i>
  <br>
  <i>♦ Methods like map, filter, and concat create new arrays without mutating the original array.</i>    
  <br>
  <i>♦ Libraries like Immer can be used to simplify immutable state updates. Immer allows you to write code that appears to mutate state while ensuring immutability.</i>
  </p>
</details>

<br>

<details>
   <summary> What are Action Creators?</summary>
  <p><i> Action creators are functions that create and return action objects. They encapsulate the creation of actions, making the code more modular and reusable.</i>
  <br>
  <i>They help centralize and organize the logic for creating actions, making the codebase cleaner and easier to maintain.</i>
  <br>
<i>They encapsulate the creation logic, making it easier to update or change the way actions are created without affecting other parts of the code.</i></p>
</details>
<br>
<details>
   <summary> Explain the role of Reducers in Redux.</summary>
  <p><i>  Pure functions that take the current state and an action as arguments and return a new state. They specify how the state of the application changes in response to actions sent to the store.</i>
  <br>
  <i>They do not produce side effects and always return the same output for the same input.</i>
  <br>
<i>They encapsulate the creation logic, making it easier to update or change the way actions are created without affecting other parts of the code.They never modify the existing state directly but instead return a new state object.</i>
  <br>
<i> Reducers determine how the state should transition based on the action type and payload.</i>
  <br>
<i> Each reducer handles specific action types and updates the state accordingly.</i></p>
</details>

<br>

<details>
   <summary>What is a Redux Selector? Why and when would you use it?</summary>
  <p><i> <b> A selector in Redux is a function that takes the Redux state as an argument and returns specific data from the state. It allows components to extract and subscribe to only the parts of the Redux state that are relevant to them.</b></i>
  <br>
  <i>Selectors provide a centralized way to extract data from the Redux store.</i>
  <br>
<i>Selectors can be memoized using libraries like Reselect to improve performance by caching results.</i>
  <br>
<i> Reducers determine how the state should transition based on the action type and payload.</i>
  <br>
<i> They promote reusability by encapsulating logic related to retrieving derived state or computed values.</i>
  <br>
<i> When components need to access parts of the state that are deep or nested.
</i>
  <br>
<i> To avoid unnecessary re-renders by ensuring that components only update when relevant parts of the state change.
</i></p>
</details>

<br>

<details>
   <summary>Discuss the difference between Redux Thunk and Redux Saga for handling async actions.</summary>
  <p><i> <b> Redux Thunk:</b></i>
   <i>Selectors provide a centralized way to extract data from the Redux store. Commonly used for simpler async logic or straightforward API calls. Easier to integrate into existing Redux applications due to its simplicity and minimal setup.</i>
   <i> <b> Redux Saga:</b></i>
   <i> Suitable for complex async flows, long-running tasks, and scenarios requiring advanced control over async actions.</i>
</p>
</details>

<br>

<details>
   <summary>What is a Redux Middleware? Provide examples of commonly used middlewares.</summary>
  <p><i> <b>Middleware in Redux intercepts actions dispatched to the store before they reach the reducer. It sits between the action dispatch and the reducer invocation, allowing you to perform additional logic, side effects, or modifications on actions. </b></i>
    <br>
    <i> <b> Commonly Used Redux Middlewares
    </b></i>
    <br>
    <i> ♦ Redux Thunk</i>
    <br>
    <i> ♦ Redux DevTools Extension</i>
    <br>
    <i> ♦ Redux Saga</i>
    <br>
    <i> ♦ Redux Logger</i>
    <br>
    <i> ♦ Redux Persist</i>
</p>
</details>

<br>

<details>
   <summary> How does a middleware handle actions in the Redux flow?</summary>
  <p><i> <b>Redux middleware is software that intercepts and provides a third-party extension point between dispatching an action and the moment it reaches the reducer. It allows you to customize the Redux behavior in various ways, such as logging actions, handling async actions, or modifying actions before they reach the reducer.</b></i>
    <br>
    <i> <b>♦ Middleware is a curried function </b></i>
    <br>
    <i> <b>♦ Interception: </b></i>
Middleware intercepts every action dispatched using store.dispatch(action).
<br>
    <i> <b>♦ Next Function: </b></i>
Middleware functions receive a next function as an argument, which represents the next middleware in the chain or the Redux store's dispatch function if it's the last middleware.
<br>
    <i> <b>♦ Processing: </b></i>
Middleware can inspect the action, perform async operations, modify the action, or dispatch new actions based on conditions.
Passing to Next Middleware: After processing, middleware can either:
<pre> Pass the action to the next middleware (if any) using next(action).
Optionally, modify the action before passing it (next(modifiedAction)).</pre>
<br>
<i> <b>♦ Final Dispatch: </b></i>
If a middleware chooses not to call next(action) (e.g., it handles the action itself), the action flow stops at that middleware, and it doesn't reach the reducer.
<br>
<i> <b>♦ Async Actions: </b></i>Middleware like Redux Thunk or Redux Saga handles async actions by delaying the action dispatch, performing async operations (like API calls), and then dispatching new actions based on the async operation's success or failure.
<br>
<i> <b>♦ Termination: </b></i> Middleware can prevent actions from reaching the reducer altogether or modify the action payload before it reaches the reducer.
</p>
</details>

<br>

<details>
   <summary>What are the main features of Redux Toolkit?</summary>
  <p><i> <b> RTK sets up a default Redux configuration that includes good practices such as using immer for immutability, and providing a simpler way to define reducers and actions.</b></i>
    <br>
    <i> <b> createSlice:  </b>This API allows you to define a slice of your Redux state with a reducer function and automatically generated action creators. It reduces boilerplate code significantly.
   </i>
    <br>
    <i> <b> configureStore:  </b>A utility function that combines reducers, middleware, and other store configuration settings into a Redux store instance. It simplifies store setup, including support for middleware and the Redux DevTools Extension.
   </i>
    <br>
    <i> <b> Immutability and Immer Integration:  </b>RTK encourages immutable updates to state by default, using the immer library under the hood. This makes state updates safer and easier to reason about.
   </i>
    <br>
    <i> <b> Async Logic Simplification: </b> It simplifies handling async logic with the createAsyncThunk API, which generates async action creators for API requests. This removes the need for separate action types and action creators for each async operation
   </i>
    <br>
    <i> <b>Slices and Encapsulation: </b>  Slices allow you to encapsulate related Redux logic, including reducers and actions, into separate modules. This promotes modularity and easier code organization.
</p>
</details>

<br>

<details>
   <summary> Why might someone prefer using RTK over traditional Redux?</summary>
  <p><i> <b> RTK significantly reduces the amount of boilerplate code required to set up a Redux store, define actions, reducers, and action creators. It simplifies the process with utilities like createSlice, createAsyncThunk, and configureStore.</b></i>
    <br>
    <i> ♦ Simplified Code   </i>
    <br>
    <i> ♦ Built-in Middleware  </i>
    <br>
    <i> ♦ Immutable Update Logic  </i>
    <br>
    <i> ♦ Performance Optimizations</i>
</p>
</details>

<br>

<details>
   <summary>Discuss the benefits of using createSlice() in Redux Toolkit.
   </summary>
  <p><i> <b>createSlice() combines the creation of action types, action creators, and reducers into a single, concise function. </b></i>
    <br>
    <i>createSlice() automatically generates action type constants and action creators based on the reducer functions you define. This eliminates the need to manually define these elements, reducing potential errors and making your code more maintainable. </i>
    <br>
    <i>  The reducer functions in createSlice() use Immer under the hood, allowing you to write mutable update logic while ensuring immutability </i>
    <br>
    <i> can define asynchronous actions using createAsyncThunk  </i>
    <br>
    <i>createSlice() allows you to handle actions defined outside of the slice using extraReducers, enabling better integration with other parts of your Redux store and third-party libraries.</i>
</p>
</details>

<br>

<details>
   <summary>Discuss the benefits of using createSlice() in Redux Toolkit.
   </summary>
   <blockquote>
  <p><i> <b>createSlice() combines the creation of action types, action creators, and reducers into a single, concise function. </b></i>
    <br>
    <i>createSlice() automatically generates action type constants and action creators based on the reducer functions you define. This eliminates the need to manually define these elements, reducing potential errors and making your code more maintainable. </i>
    <br>
    <i>  The reducer functions in createSlice() use Immer under the hood, allowing you to write mutable update logic while ensuring immutability </i>
    <br>
    <i> can define asynchronous actions using createAsyncThunk  </i>
    <br>
    <i>createSlice() allows you to handle actions defined outside of the slice using extraReducers, enabling better integration with other parts of your Redux store and third-party libraries.</i>
</p>
   <blockquote>

</details>

<br>

<details>
   <summary>How does memoization play a role in Redux selectors for performance optimization?</summary>
  <p><i> <b>Memoization is a technique used to improve performance by caching the results of expensive function calls and returning the cached result when the same inputs occur again. In Redux, memoization is crucial for optimizing selectors, which are functions used to retrieve specific pieces of state from the store. </b></i>
    <br>
    <i>The reselect library provides the createSelector function to create memoized selectors. createSelector takes one or more input selectors and an output selector. It recomputes the output only if one of the input selectors' results has changed.</i>
</p>
</details>
<br>
