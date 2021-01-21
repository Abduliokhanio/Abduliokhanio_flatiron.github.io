---
layout: post
title:      "CRUD React Redux Final Project"
date:       2021-01-14 16:46:45 -0500
permalink:  redux_faqs_for_beginners
---

Link to Blog:https://abdulkhan-81904.medium.com/crud-react-redux-88c43599c3e8

We’re going to embark on a pretty crazy journey today. We are going to be talking about how to give your single page application CRUD functionality using React Redux.
Just so that were on the same page. Were using rails on our backend: If you want a quick crash course on rails check out the link below.
Rails Crash Course: https://abdulkhan-81904.medium.com/rails-crud-overview-29deb4bd1e5a
And were using react & redux on our front end. Check out the links below.
React JS FAQs: https://abdulkhan-81904.medium.com/react-js-faqs-for-beginners-4a113d5eb7ec
React Lifecycle Methods: https://abdulkhan-81904.medium.com/react-life-cycle-methods-d42e333c12cb
REDUX for beginners: https://abdulkhan-81904.medium.com/redux-faqs-for-beginners-195ed82552cc
I would recommend reading the blogs mentioned above first just to ensure that you can keep up if your a “newb” developer.
Create
Let’s go ahead and create a form in a form.js file. It’s a class component with state parameters set to and empty string (aka “”). To create the form itself I recommend using react-bootstrap. But you can use regular html inside the return as well; its up to you.
We need to give each input area on the form an “Onchange” event listener which allows us to set what we type into state but more importantly it shows us what we are typing.
Then we need a “handle-submit” event listener. The handle submit listener is going to take everything from state and pass it to an action. An action is no different then a function that allows for dispatch commands to be run. In our add action we are send our DB a fetch POST request via the “fetch process.” And then we will send another dispatch command witch will update the state and re-render the index page.
Read
Lets go ahead and talk about the read functionality. We want to be able to display a single item from our data base. Though its not necessary; I recommend following restful routing.
So here’s how we do it:
Lets create another component called “detail”. and well have that component handle the details of the individual objects. In out main book index page we are going to create an event listener called “handleClickRead” and a button that stores the id of the object on the display. And we are going to link that button to our new component; passing the id as a prop.
In our detail component. We are going to “useEffect” & “useState”. Lets “useEffect” on a function called “getObject”. Within the function we are going to go through our fetch method to call upon that particular data from our DB. Once we have that data we are looking for we will use the “useState” function to bring our data into state so that we can display it.
Once we have our data in state go ahead and display it within the return( ) And Voila we have read functionality!
Update
For the update functionality lets start off by creating an edit form. We’re going to use the same functionality as the create form! Honestly you can create a form component if you want to and call it into both the create and edit components; but it’s up to you. Regardless in the handle submit we are going to call the “editObject” action that we are about to create in a minute. But before that we do that in our handle submit function we are going to create a new object with the properties of id and all of the properties that were updated. And we are going to pass that to our new action.
In our action page lets go ahead and create an edit action that takes in our object. Inside we are going to run a fetch with a PATCH method going to the restful route associated with that book. And within the fetch methodology we are going run a dispatch to update our global store.
So that once we go back to the index page we see the changes that have been made.
Delete
The delete button in my opinion is the easiest functionality. For the delete functionality lets start off by creating a delete button in our index component. In the delete button lets give it an onclick function called “handleDelete” which takes the id of the object. And triggers an action we will create called “delete” that will take an id parameter. Now lets go to our action page and create this new action that takes the parameter and sends a fetch with a method of “DELETE” to our restful route based URL. to delete from our db. and then uses dispatch to update the global state with out payload being our id to be further processed on our reducer page to return a new state with out the object of the id that we passed in.
Conclusion
Now that you know how to create, read, update, and delete you are good to go for creating your new application! Happy Coding!
