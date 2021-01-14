---
layout: post
title:      "RAILS |CRUD|Overview"
date:       2021-01-14 16:41:00 -0500
permalink:  rails_crud_overview
---

Link to Medium Blog: https://abdulkhan-81904.medium.com/rails-crud-overview-29deb4bd1e5a
GOAL:
Our goal here is to build a content management system (CRUD application) using rails.
Disclaimers:
I’m using windows. If you use mac the only thing that will be different will be the terminal commands. But their substitutes are easily “google-able”. Also I personally use VS code so I’ll be writing from that perspective. Aldo there are enough steps to actually write a book. So for the sake of brevity I’ll be focusing on just the main steps.
Step 0 ) Draw out the relationships
It’s important that you draw out the relationships to truly understand what is going on. Otherwise the object relationships get really, really, really confusing and you’ll spend hours of sifting through your code trying to figure out what went wrong.
I recommend using DRAW.IO online. It’s a free tool that has a lot of cool features to help you build the perfect diagrams.
Here’s my diagram:
Step 1) Rails new application
Alright the moment we’ve been waiting for. Lets go ahead and hop into your favorite terminal.
Once we make sure we have ruby (“ruby -v”) & rails(“rails -v”) installed. And once we have decided where we want to generate this project (I recommend saving it to the desktop for easy deletion once you are done and have uploaded your code to github/ your heroku server).
Let’s go ahead and type “rails new crud_app -t”
Go grab a coffee because this could take a while.
This is going to build your application and generate all the files necessary to run your application on your local web server.
Once its done loading go ahead and hop into your favorite IDE and navigate to the file location via ide terminal (Once again I’m using VS code so I’ll be writing from that perspective.).
Now let’s make sure rails is working properly.
In the terminal run “rails s”
If it provides you a local host URL congratulations! You have your 1st rails application up and running. But for most of you that wont be the case. Most likely you (And including me on multiple occasions ) will be asked to “install yarn”
So go ahead and download yarn: https://classic.yarnpkg.com/en/docs/install/#windows-stable
Try running “rails s” again and follow the instructions rails will provide you in your terminal to help get your app running. Rails want you to be successful & it’ll provide hints to what the problem is.
And Voila! You have your 1st rails application running!
Step 2) Rails Generate Models + DB
It’s now time for us to generate our models & data base. The cool thing about rails is that it does both. WITH A SINGLE COMMAND. We’re going to generate 3 models. Post, User, & Genre. Along with whatever attributes we want our modal to have in the database.
Lets type “rails g model Genre genre_name:string” press enter
Lets type “rails g model Post user_id:integer genre_id:integer title:string description:text url:string” press enter
Lets type “rails g model User username:string password_digest:string image:string website:string location:string bio:string” press enter
What you’ll notice now is that your models are built! Don’t believe me? Look in the app/models directory. Our database is also built and ready to migrate. Take a look at the db/migrate directory.
Make sure there are no typos in your db/migrate directory for all the migrations. you ‘ll notice that all your migrations come with “.datetime ” this is a default feature provided by rails. Isn’t it cool???
Whenever your ready lets go ahead and run “rails db:migrate”
Note : We won’t be “crud-ing” for Genres so lets go ahead and hop into “db/seeds.rb” and make some seed data.
Use the following syntax “Genre.create(genre_name: ‘sad’)” and create 4–5 other genre’s
Then run “rails db:seed”
Step 3) Rails Generate Controllers + views
Just like with the models. When you generate the controllers you are able to generate the views as well. In our terminal…
Lets go ahead and type “rails g controller posts new index edit show” press enter
Lets go ahead and type “rails g controller users new edit” press enter
Note we don’t need anything for the genre controller yet. We’ll add scope methods later on.
Our views have been generated in our “/app/views” directory. And if we take a peek inside our Posts and User Controllers well see that our “routes” have been added there as well. WOW!
But we still need to hop into “config/routes.rb” to get the application working.
Step 4) Associations
Before we hop into “config/routes.rb” to get the application working. We need to set up our associations in our models. We want our associations to reflect our Entity(or Object) Relational Diagram (aka ERD). Feel free to use the syntax below. So in our case…
Genre
has_many :posts
has_many :users, through :posts
— — — — — — — — — — — — — — — — — — — — —
Post #(our join table; it joins users and genres )
belongs_to :user
belongs_to :genre
— — — — — — — — — — — — — — — — — — — — —
User
has_many :posts
has_many :genres, through :posts
These relationships are pretty much english but just in case you are still having trouble understanding.
Genre has many posts and has many users through posts
Post belongs to user and genres because its our join table
User has many posts and genres through posts
And boom we have our associations!
Step 5) Routes
Now it’s time to hop into our routes. This is where things get tricky. Initially rails will have provided some routes for you. These routes were created when we built our views. But the issue is. We want nested routes. Because 1) they are more organized & 2) they look really professional. So here’s how we’re going to do it. We’re going to put all our post routes into our user routes block. It’ll look like this
resources :users, only: [:new, :create, :edit, :update] do
resources :posts
end
resources :posts, only: [:index, :create, :update]
Lets go head and delete all our post routes and our user routes and replace them with the code above.
Note: When you use “resources” you call on all the routes that have been built for the controller.
Note: When you use “resources” with an “only” you call on all the routes that have been built for the controller that are within the “only” parentheses.
Step 6) CRUD
We’re using crud in 2 different places in the Post and User objects. So let’s start with the Post, get that working then let’s hop into the User.
Lets go ahead and set up our forms in the post views route.
In “app/views/posts/new.html.erb”
&
In “app/views/posts/edit.html.erb”
<%= form_for(@post) do |f| %>
<%= f.label :url %><br>
<%= f.text_field :url %><br>
<%= f.label :title %><br>
<%= f.text_field :title %><br>
<%= f.label :description %><br>
<%= f.text_field :description %><br><br>
<%= f.label :genre %><br>
<%= f.collection_select :genre_id, Genre.all, :id, :genre_name %><br><br>
<%= f.submit “Submit” %>
<% end %>
For now we are going to put the same code in 2 different views but we will refractor(clean up) towards the end of the project.
Posts
Index:
def index
get_all_posts
end
Create:
def new
@post = Post.new
end
def create
@post = Post.new(post_params)
@post.user_id = session[:user_id]
if @post.save
redirect_to posts_path
else
render :new
end
End
Once a form is submitted it’ll be processed through the create action and redirected to the index page.
Read:
def show
render :layout => ‘logged_in_show’
end
We are also able to look at each post individually.
Update:
def edit
if !check_users_post?
redirect_to posts_path
end
end
def update
if @post.update(post_params)
redirect_to posts_path
else
render :edit
end
end
We can update our post through this action and upon a successful update we are redirected towards the index page.
Delete
def destroy
if check_users_post?
@post.destroy
redirect_to posts_path
end
end
We can delete a post here.
Users
Create:
def new
@user = User.new
render :layout => ‘signup_login’
end
def create
@user = User.new(user_params)
no_image_user
if @user.save
session[:user_id] = @user.id
redirect_to login_path
else
render :new, :layout => ‘signup_login’
end
end
Once a form is submitted it’ll be processed through the create action and redirected to the login page. But this time it will create a User.
Update:
def edit
current_user
render :layout => ‘logged_in’
end
def update
current_user
if @user.update(user_params)
redirect_to posts_path
else
render :edit, :layout => ‘logged_in’
end
end
You can Edit and Update a user profile.
Notice how we intentionally left out the other controller actions.
Step 7) helpers
We need to build out helpers to clean up our code. In the code you see above the helpers are pre- built for us at this point we just need to define them. In a normal work flow. I’d probably build the helpers as I go.
Let’s hop into the application_controller.rb and set our helpers there so that they’ll be available in all the other controllers.
def current_user
@user = User.find_by(id: session[:user_id])
end
def current_post
@post = Post.find(params[:id])
end
def get_all_posts
@posts = Post.all
end
def logged_in?
!current_user.nil?
end
def authorized
redirect_to ‘/login’ unless logged_in?
end
def check_users_post?
current_post.user_id == current_user.id
end
def no_image_user
if @user.image == nil
@user.image = “https://ombud.alaska.gov/wp-content/uploads/2018/01/no-user.jpg"
end
end
Step 8) views
Now lets go ahead and set up our views. Everyone’s views are going to differ and since this is not a html/css tutorial im going to keep this part short. Just have fun with the view’s. Really make the project your own.
Couple of things to remember.
Your html files are technically erb files. So you can actually use ruby code within them.
Don’t forget the difference between “<%%>” & “<%=%>”
The <%%> only allows you to process ruby code.
The <%=%> only allows you to display the output of ruby code
Step 9) partials
Now that our views are built let’s go ahead and clean up the repetitive code that we mentioned earlier. We’re going to clean up our code using partials. Partials are partial layouts and they really come in handy for keeping your code clean and not error prone. So a good place to start would be the create and edit forms in the post’s view.
Right now they look like this:
<%= form_for(@post) do |f| %>
<%= f.label :url %><br>
<%= f.text_field :url %><br>
<%= f.label :title %><br>
<%= f.text_field :title %><br>
<%= f.label :description %><br>
<%= f.text_field :description %><br><br>
<%= f.label :genre %><br>
<%= f.collection_select :genre_id, Genre.all, :id, :genre_name %><br><br>
<%= f.submit “Submit” %>
And we can actually clean up the code into this:
<%= render ‘form’ %>
The first thing that we have to do is to create a file called “_form.html.erb”. Rails knows this is a partial because of the underscore “_” in front of the title.
Next well “cut” (ctrl + x) our code out of the “new.html.erb” view and put it into the “_form.html.erb”
Once completed. Lets go ahead and paste “<%= render ‘form’%>” into the “new.html.erb” to display the form. And BOOM! If you run rails you’ll see that it works completely fine & your code is looking clean!
Conclusion:
The main steps of our rails application are completed and working properly. If you followed this guide. You will have a pretty decent understanding of what’s going on in rails enough to build your own CRUD application. Though your application & code may not look completely like mine. Don’t worry and just have fun with it.



