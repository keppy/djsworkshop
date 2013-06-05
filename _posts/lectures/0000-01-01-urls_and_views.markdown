---
layout: lecture
title: Django Urls and Views
category: lectures
---
 
## Django Urls and Views

### Request and Response Cycle

A lot of server-side web development can be understood through the basic request and 
response cycle. Client applications ( like a web browser ) make requests to a
server. Code on the server handles that request, manipulates it and responds 
with something -- a CSS file, HTML, or JSON.

The code running on the server in our case is Python code and it lives
inside a larger toolset called Django. A simple example of
the request and response cycle in Django would be navigating to a URL in the
web browser. Hitting this URL triggers a request to the server for a web page to be 
displayed and the server -- specifically Django -- responds with that rendered web
page. [[1](https://docs.djangoproject.com/en/dev/ref/request-response/)]


Here's that workflow broken down into slightly more technical terms:

    1. Navigate to a specific URL -- http://www.myblog./about/

    2. An HTTP GET request is sent to server

    3. Django handles the request and creates a HttpRequest object 
    ( it contians details about the request )

    4. Django maps the requested URL pattern to a view and loads that view

    5. Since the HttpRequest object is passed into the view when it is loaded
    we can use it decide how we are going to handle any number of business logic
    things

    6. When each view is done doing its specific processing it **must** return
    a response of type HttpResponse

Understanding this cycle is the key.

### Urls and View Relationship

Open the `urls.py` file for our project located below:

    https://github.com/thebigspoon/djsworkshop/blob/master/project/djsblog/urls.py

Looking at our `urls.py` file we get can an idea about what endpoints or pages our
site will expose. For example, the line below tells us that we have an admin 
page:

    url( r'^admin/', include( admin.site.urls ) ),

URLs are nothing more than addresses for specific resources on the web. In this specific
case it tells us that we can will have a page available here:

    # http://<domain-name>/<path>/
    http://djsworkshop.dev.osgeohacks.com/admin/

Navigate to the url above and see the result

### View Workflow

Now let's examine one view from the final project to understand the request and response
workflow in detail:

    blah blah

