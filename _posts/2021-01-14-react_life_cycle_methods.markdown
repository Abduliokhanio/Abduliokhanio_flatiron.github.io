---
layout: post
title:      "React Life Cycle Methods"
date:       2021-01-14 21:45:58 +0000
permalink:  react_life_cycle_methods
---


What are Life Cycles?
React has 3 main phases Mounting, Updating, and Unmounting. Lets start with Mounting
Mounting
Mounting means putting elements into the DOM. React has 4 built in components methods that get called when mounting a component.
Image for post
The Render method will always be called. The others are optional.
The Constructor method is called before anything else. it’s used to set up the initial state and other initial values. You can pass in props as arguments. But make sure you pass it to the super() inside as well so that you can use the props with the proper context.
The getDerivedStateFromProps() method sets the passed props into the state of the component you are in
The render() method is required and it’s the method that actually allows us to render HTML the DOM.
The componentDidMount() is called after the component is rendered.
Updating
Image for post
getDerivedStateFromProps() gets called again but in another phase. This time its’s called as soon as a component get updated.
shouldComponentUpdate() returns a Boolean Value that specifies weather or not React should render. The default value is true but it can be used to return false.
render() Rendered gets called again after the update is complete.
getSnapShotBeforeUpdate() Grants you access to the state and props before the update so that you can check and compare your previous values to your current values to see if there were any updates. If you using this to prevent errors you have to inclued the componentDidMount() method.
componentDidUpdate()is called after the DOM is updated.
Unmounting
Image for post
componentWillUnmount() is called after the component has been removed from the DOM.
Conclusion
In conclusion you have a general understanding of what lifecycle phases and what the methods are including what they do. Happy Coding!
