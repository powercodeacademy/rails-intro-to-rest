# Intro to REST

## What is REST?

REST stands for REpresentational State Transfer, essentially REST is a standardized design architecture that enables applications to communicate and manage data flow. REST was originally proposed in 2000 by Roy Thomas Fielding in his PhD dissertation as an architectural style for connecting the Internet. At that time the Internet was growing fast, however there was a distinct lack of organization when it came to web applications communicating with each other. RESTful principles helped to bridge the gap between applications and aided in laying the foundation for the Internet ecosystem that exists today.

If you have been building applications for a while, there is a good chance that you have already worked with RESTful APIs. Integrating a Facebook login, having something in your application post to Twitter, pulling in a feed of images from Instagram, or even calling a list of locations from Google Maps are all examples of using a RESTful API to communicate between applications.

## Example REST Workflow

For a real world case study let us pretend that you have a newsletter application, the following is a high level view on how REST works in your app:

1. You fill out the form on the 'New Newsletter' page and click submit.

2. Information about you, your newsletter content and any additional information such as media items are all sent to the application server.

3. The server interprets the information, recognizes that the request is for a new newsletter and it generates the new record in the database and performs a myriad of background tasks (updates the newsletter counter, possibly sends notification emails, et al)

4. Next the server sends a response back to the client, this does not necessarily mean that the newsletter was posted, the response could be that there was an error posting or something like that. However in this case we will say that the newsletter post went through properly, so the server sends a success message and tells the browser what page to go to and render. 

5. Lastly the browser receives the server information and gives the user feedback, in this case it shows you a message saying that your newsletter was successfully posted.


## RESTful Conventions in Rails

Rails has RESTful principles built into its core, so whether you are utilizing the built in view rending system or using the application purely as API you will have the tools necessary to follow standardized routing procedures.

If you were to build out a feature in Rails that entails all of the potential RESTful routes, you would have seven different RESTful URLs, HTTP verbs (more on those later), and actions. As an example, imagine that you have a Newsletter module in your application, if you run ```rake routes``` in the terminal you will receive the following output:

```
newsletters     GET     /newsletters(.:format)          newsletters#index
                POST    /newsletters(.:format)          newsletters#create
new_newsletter  GET     /newsletters/new(.:format)      newsletters#new
edit_newsletter GET     /newsletters/:id/edit(.:format) newsletters#edit
newsletter      GET     /newsletters/:id(.:format)      newsletters#show
                PATCH   /newsletters/:id(.:format)      newsletters#update
                PUT     /newsletters/:id(.:format)      newsletters#update
                DELETE  /newsletters/:id(.:format)      newsletters#destroy
```

Rails does a great job of integrating RESTful routes into their system, if you can understand routes in Rails you can understand REST in general. Going through the output above you should be able to see that all of the potential CRUD actions are all there, from querying all of the records to deleting a single item from the database, and all of the actions are wired up using RESTful routing nomenclature.

Here is a diagram that shows how how the views, controller actions, routes, and HTTP verbs are all mapped together

![REST Diagram](http://reif.io/lib/flatiron/rest_diagram.png)

In analyzing the diagram, you can see the flow of data as follows:

1. The HTTP request contains a HTTP verb and hits a specific URL path

2. The router in the application processes the request and 'routes' the request data to the proper controller action

3. The controller action either performs a task, such as creating, updating, or deleting a record in the database, or it runs a database query and renders a view to the client

## Definition of HTTP Verbs

So what do those 'GET', 'POST', et al items represent? Those are HTTP verbs that each give the HTTP request unique behavior, below is an explanation on each verb:

* **GET** - The GET method means retrieve whatever information (in the form of an entity) is identified by the Request-URI. This means if you go to /posts you will get all of the posts that the application wants your application to have.

* **POST** - The POST method is used to request that the origin server accept the entity enclosed in the request as a new subordinate of the resource identified by the Request-URI in the Request-Line. This means that the server needs to accept the data sent over with the request.

* **PATCH/PUT** - The PUT method requests that the enclosed entity be stored under the supplied Request-URI. If the Request-URI refers to an already existing resource, the enclosed entity SHOULD be considered as a modified version of the one residing on the origin server. This means that the server needs to accept data and that it is understood that the data is going to modify a pre-existing element in the database.

* **DELETE** - The DELETE method requests that the origin server delete the resource identified by the Request-URI. This means… it deletes the record, it's nice and explicit.


## Summary

Below are a few keys to remember when thinking about REST:

* REST is an architectural design pattern, not a framework or code in itself.

* RESTful routes have a clear mapping between the URL resource and the corresponding controller actions.

* There are seven potential RESTful route options available.

* By using RESTful principles, apps are able to have a clear naming structure for routes and actions