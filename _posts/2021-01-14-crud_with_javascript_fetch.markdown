---
layout: post
title:      "CRUD with JavaScript FETCH"
date:       2021-01-14 21:43:37 +0000
permalink:  crud_with_javascript_fetch
---


Today we are going to learn about building a SPA (Single Page Application) Crud application using Fetch. We need to be able to send and receive JSON from the DB. This is what allows the CRUD functionality. Keeping this core principle in mind. You will be able to create any kind of application that you want.
Think of this functionality as the HEART of any SPA crud application that you want to build.
C.R.U.D. = Create | Read | Update | Delete
The way this blog is structured we are going to analyze fetch using the code of a prebuilt SPA CRUD application of mine. We aren’t going to focus on the backend in this blog because fetch is DB-Agnostic. But for those of you who are wondering. I am using Rails as my backend. So this whole project is done using my local host “http://127.0.0.1:3000”. So keep in mind that the variable BaseUrl = “http://127.0.0.1:3000”.
And just so everyone can follow along a little bit easier. My project is base on a favorite childhood passion of mine; Yu-gi-oh cards.

If we look at the structure of a card we can see that the card has a :
Name
Type
Star number
Image
Description
ATK (Attack Points)
DEF (Defense Points)
But for the sake of keeping things simple going forward we are just going to focus on :
Name
Image
Description
MY ORM (Not that you’ll need it)

Now that we got the details you need to keep up with the lesson out the way. Lets start with the Create Functionality.
Create
“Create” allows us to add objects to our database.
We start by building a hash (aka JS Object) that contains all the information that we want our future card to have. As you can see our card has a name (cardName) , a description(cardDesc), an image(cardImgSm) and a cart id(1). These are variable that can be assigned using what ever means necessary. You can use a form with JS event listener or you can pull the information from another API using another fetch request and organizing/assigning the information to their respective variables.
Once you have your have your hash organized. We can start the actual fetch process. You can actually go ahead and make the fetch request and configure your request inside the fetch action but I personally love clean code. And I chose to organize my configurations before hand inside my config object.
If we take a look inside of our config object. well get a better idea oh what's going on with the fetch. As we can see:
We are making a “POST” request.
We have header configurations.
We want our hash to be converted to JSON with the final command.
Once we have our configurations we run the fetch command to actually create our object inside the db.
Read
“Read” allows us to pull information and see what’s in our DB. In the example above I’m pulling card information from my index route which contains information about all the cards. If you’ve implemented restful routing you can also fetch information about a particular card using the Baseurel/${cardId}. I chose to display all the cards in sequence due to the structure and functionality of my application. And this particular request was showing all the cards in my shopping cart. But it’s up to you in regards to what your trying to accomplish.
So we first make the fetch request tour DB using the fetch command. Then we convert the response to JSON using “.json()” and then since I'm getting getting back an array of data; I'm iterating through each element in the array. But if your return value is not an array you; there's no reason for you to iterate through the array; you’re ready to began processing your data. Once your ready to process data you can choose what you want to do with it. Since we are suppose to be “reading” I chose to display the data to an “index.html” file. But feel free to do what ever you want with the data.
Update
“Update” allows us to edit objects in out DB. Generally you have an edit form which you would use to set values to variable then assign those variable to there respective KEY : Value pairs for the hash(JS object) you are trying to build. But you can also hard code those values as well. Looking at my code you can see that in my card hash the only values I’m updating are name & description. This goes to show that you don’t have to edit all the values of an object for this to work. You can pick and choose. Upon creating my object I was ready to launch the fetch request to my db. But I choose to keep my code clean. And wrote my configurations outside the fetch request. If we take a look at my config object we can see that we are making a “PATCH” request. along with sending headers configuration and we are turning our card body into an JSON.
Once our configurations are ready we are ready to launch a fetch request. Since we are updating one card at a time. We have to make sure we are sending the fetch request to the correct URL. In our case our URL is “Baseurl/cards/${cardId}”. So we can edit that one particular card. And honestly you can just stop right there. Your Card in the DB has been updated.
I personally included the 2 “.thens” because I wanted to also display the update instantly using my JS library. Not necessarily something that you have to do though.
Delete
“Delete” our final functionality for our SPA CRUD application. “Delete” is also the simplest CRUD command. To get the delete functionality ready lets start with the fetch. Just kidding. We’re going to start with the configurations for the fetch because we are great engineers and we like to keep our code organized. In our config we can see that we are making a delete method. We also have our headers as well. Now that we are done with our config we are going to make the fetch request(basically where the action happens). Since we are making a delete request we have to be specific with what we are trying to delete. So in my example I am deleting a card with a particular id form the cards db.
Conclusion
In conclusion you can build a single page CRUD application using the javascript fetch(). You now know enough to build what ever type of application you want to build. Happy Coding! : )



