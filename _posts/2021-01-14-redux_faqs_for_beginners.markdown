---
layout: post
title:      "REDUX FAQs For Beginners"
date:       2021-01-14 16:46:45 -0500
permalink:  redux_faqs_for_beginners
---

Link to Blog: https://abdulkhan-81904.medium.com/redux-faqs-for-beginners-195ed82552cc

What is Redux?
Redux according to the official doc’s “is a pattern and library for managing nd updating application state, using events called “actions”” It helps you manage global state. So that you can call &/or update information through out your application.
Redux can be integrated with any front end but is most commonly used with react. With redux since we have a global location where information is stored we don’t have to worry about lifting state up to parent components.
Redux is immutable in nature. any updates to state and object have to be made to the copy of the state or object.
What are actions?
An action is a plain JS object. Actions usually define something thats happening in your application. Actions contain a types and payloads. The types help describe what’s happening and the payload is the actual data being passed.
An action creator is a function that returns an action object.
What are reducers?
A reducer is a function that receives the current state and action and decides hot to update the state if necessary then returns a new state. The reducer listens and based on what action (event) it receives; it will react accordingly.
Reducer are often written as conditionals or switches.
Store — the store is created by creating a reducer and comes with a default value of getState() that returns the current state value.
Dispatch — The redux store comes with a method called .dispatch() which is the only way to update the state and pass in an action object.
Reducers act like event listeners. once something happens that they are interested in that update the state accordingly.
Redux Data Flow:
Image for post
Initial
A redux store is created using a root reducer function
The store calls the root reducer and saves the return value into initial state.
UI components asses the current state of the redux store and decide what to render.
Updates
Something happens in the app.(a button is clicked)
the app dispatch's an action to the Redux store
The store runs the action and return a copy of the passes state along with any updates as a new state.
The store notifies all the subscribed UI
Each component check to see if there any updates
UI re-renders to reflect any changes.
Conclusion
In conclusion You now know what redux is and have a general idea of how to use redux with your full stack application. Happy Coding!
