# Intro to REST

## What is REST?

In 2000, Roy Thomas Fielding was frustrated by the hap-hazard different ways web applications were using the HTTP standard. Specifically he was frustrated with how URLs and their corresponding HTTP Verbs were used differently for every single application. So, in his PhD dissertation he came up with REST or REpresentational State Transfer as a standard way web apps should structure their URLs. It also suggested a few other things, but we focus mostly on how it changed URLs. Fielding also noticed the rise in web applications communicating with each other. Using this standard way of forming URLs to access resources, Fielding hoped that inter-application communication would get much easier.

If you have been building applications for a while, there is a good chance that you have already worked with RESTful APIs. Integrating a Facebook login, having something in your application post to Twitter, pulling in a feed of images from Instagram, or even calling a list of locations from Google Maps are all examples of using a RESTful API to communicate between applications.

## Example REST Workflow

For a real world case study let us pretend that you have a newsletter application. The following is a high level view on how REST works in your app:

1. You fill out the form on the 'New Newsletter' page and click submit.

2. Information about you, your newsletter content and any additional information such as media items are all sent to the application server.

3. The server interprets the information, recognizes that the request is for a new newsletter, and generates the new record in the database and performs a myriad of background tasks (updates the newsletter counter, possibly sends notification emails, et cetera).

4. Next the server sends a response back to the client. This does not necessarily mean that the newsletter was posted; the response could be that there was an error posting or something like that. However, in this case we will say that the newsletter post went through properly, so the server sends a success message and tells the browser what page to go to and render.

5. Lastly the browser receives the server information and gives the user feedback. In this case it shows the user a message saying that their newsletter was successfully posted.


## RESTful Conventions in Rails

Rails has RESTful principles built into its core, so whether you are utilizing the built in view rendering system or using the application purely as an API you will have the tools necessary to follow standardized routing procedures.

Let's take a look at a practical example of how this works. If you wanted to build out a Newsletter feature we would need the system to have four key actions: Create, Read, Update, and Destroy – commonly known as CRUD actions. In addition to the CRUD actions, we will also need an `index` page that lists out all of our newsletters – that's five routes. Since our users will need to have a visual interface for creating and updating records (a form for creating and another form for updating), we will need two more routes. Putting all of that together, you will see that we end up with seven different routes. The `GET` routes are all routes that usually render some `erb` content to a web browser. These are the routes that our users will work with day to day. The `POST` and `PUT` are the url in the form `action`, and the `DELETE` is a new type of verb.

Here is a mapping of all of the different route helpers, HTTP verbs, paths, and controller action mappings for our newsletter feature.

```ruby
GET      /newsletters 				    	# Show all newsletters
POST    /newsletters          	 	 # Create a new newsletter
GET    /newsletters/new        # Render the form for creating a new newsletter
GET      /newsletters/:id/edit 	  # Render the form for editing a newsletter
GET    /newsletters/:id      	   # Show a single newsletter
PATCH  /newsletters/:id          # Update a newsletter
DELETE /newsletters/:id          # Delete a newsletter
```

Thankfully, Rails maps these specific things to specific methods or "actions" as they are called in Rails. If we had a controller called `NewsletterController` we would define these seven methods and Rails automatically will call them based on the correct route. Below is a breakdown of each of the controller actions and what they represent, notice the direct correlation between the route mapping above and the controller methods:

```ruby
* index 	# Show all newsletters
* create  	# Create a new newsletter
* new 		# Render the form for creating a new newsletter
* edit 		# Render the form for editing a newsletter
* show 		# Show a single newsletter
* update 	# Update a newsletter
* destroy 	# Delete a newsletter
```

Rails does a great job of integrating RESTful routes into its system. If you can understand routes in Rails you can understand REST in general. Going through the output above you should be able to see that all of the potential CRUD actions are all there, from querying all of the records to deleting a single item from the database, and all of the actions are wired up using RESTful routing nomenclature.

Here is a diagram that shows how how the views, controller actions, routes, and HTTP verbs are all mapped together

![REST Diagram](https://curriculum-content.s3.amazonaws.com/web-development/rails-intro-to-rest/rails_routes.png)

In analyzing the diagram, you can see the flow of data as follows:

1. The HTTP request contains a HTTP verb and hits a specific URL path

2. The router in the application processes the request and 'routes' the request data to the proper controller action

3. The controller action either performs a task, such as creating, updating, or deleting a record in the database, or it runs a database query and renders a view to the client

## Definition of HTTP Verbs

So what do those 'GET', 'POST', et al items represent? Those are HTTP verbs that each give the HTTP request unique behavior, below is an explanation on each verb:

* **GET** - The GET method retrieves whatever information is identified by the Request-URI. This means if you go to `/posts` you will get all of the posts that the application wants your application to have.

* **POST** - The POST method is used to send data enclosed in the request to the server. The server is expected to use this data to create some new resource.

* **PATCH/PUT** - The PUT/PATCH methods both represent the HTTP verbs that are used to update existing resources. So if you sent a `PUT` to `/posts/1` with a new post name, the post with `id` of 1 would be updated.

* **DELETE** - The DELETE method requests that the server delete the resource identified by the Request-URI. This means… it deletes the record; it's nice and explicit.

## A Note on REST and Routing with Reference to Sinatra

If you've worked with [Sinatra](http://www.sinatrarb.com/), you've seen how it's
possible to declare an action's route(s) with the action. Rails eschews this
method of routing in favor of moving routes to a config file and treating them
as RESTful by default. That's not to say that Sinatra applications cannot serve
resources in a RESTful fashion — of course they can! — but Rails goes the
additional step of making it _difficult_ to do anything else.

You can (and should!) read more about Rails routing [here](http://guides.rubyonrails.org/routing.html).

## Summary

Below are a few keys to remember when thinking about REST:

* REST is an architectural design pattern, not a framework or code in itself. Many other web frameworks utilize RESTful design principles in some form or another. By using RESTful principles, Rails apps are able to have a clear and standardized naming structure for routes and actions.

* RESTful routes have a clear mapping between the URL resource and the corresponding controller actions.

* There are seven potential RESTful route options available.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/rails-intro-to-rest'>Intro to Rest</a> on Learn.co and start learning to code for free.</p>
