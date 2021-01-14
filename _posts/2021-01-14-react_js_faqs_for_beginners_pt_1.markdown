---
layout: post
title:      "React JS FAQs for Beginners Pt.1"
date:       2021-01-14 21:44:56 +0000
permalink:  react_js_faqs_for_beginners_pt_1
---


Link to Blog: https://abdulkhan-81904.medium.com/react-js-faqs-for-beginners-4a113d5eb7ec

How to create a react app
To create a react app you first start off with npx create-react-app nameofyourap This will create your entire front end of you. Once youa re ready go ahead and type in npm start or yarn start. React comes with yarn. Yarn is nothing more then a package management tool for JS. Upon completion you will have an app that looks like this.
What are components?
In react; components are pieces of reusable code. The are two types of components container and presentational. The difference between them is that the container component use state and the presentation components don’t use state. We’ll go into detail about state next. But the only thing that presentational components deal with is the layout. (i.e. where buttons/forms go ect.)
What is State?
React components come with a built in state object. The state object is where you store the properties that belong to that component. You can access and update state at will. When it comes to updating its a little harder because you need to use hooks but it is possible. The way that react is set up; everything that is being passed from you DB will have to go through state before you are able to display that information to the user.
What are Hooks?
Image for post
Photo by Mael BALLAND on Unsplash
Hooks are a fairly new addition to React. They allow you to use state and other react features without writing class components. Hooks are optional. You don't have to use functional components if you don't want to. You can have a fully functional app with just class components. Hooks are backwards compatible. So if you wanted to update your current code you can with out worrying about breaking things.
There’s lots of different hooks you can use I personally have found useEffect() and useState() to be the most useful.
useEffect() allows you to use a function/ preform an action immediately once a component is rendered
useState() allows you put your return value into state. So that you can youse it in your component.
Here’s a list of some of the most commonly used hooks:
https://blog.bitsrc.io/10-react-custom-hooks-you-should-have-in-your-toolbox-aa27d3f5564d
Conclusion
There were a lot of things covered here. But there are even more things that were not covered. Such as Routes, Links, Switches, component lifecycle methods, parent-child relationships ect. For the sake of brevity im going to be talking about these subjects in another blog. Hope you enjoyed reading! Have fun playing with react.

