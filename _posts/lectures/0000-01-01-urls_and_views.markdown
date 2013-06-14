---
layout: lecture
title: Django Urls and Views
category: lectures
---
 
## Django Urls and Views

### Request and Response Cycle

A lot of server-side web development can be understood through the basic request and 
response cycle. Client applications ( like a web browser ) make requests to a
server. Code on the server handles that request and responds 
with something -- a CSS file, HTML, JSON.

The code running on the server in our case is Python code and it lives
inside a larger toolset called Django. A simple example of
the request and response cycle in Django would be navigating to a URL ( such as
`http://www.myblog./about/` ) in the browser's address bar. Hitting this 
URL triggers a request to the server for a web page. Django responds with the rendered web
page. [[1](https://docs.djangoproject.com/en/dev/ref/request-response/)]

Here's that workflow broken down into slightly more technical steps for certain people.

### Request Response Workflow

**1.** Navigate to a specific URL -- `http://djsblog.dev.osgeohacks.com/`

**2.** An HTTP GET request is sent to server. We can visualize this GET request by 
opening Firebug in Firefox or opening the Developer Tools in Chrome.
![alt img name](../../image/base/GET_request.png)

**3.** Django handles the request and creates a HttpRequest object 
( it contains details about the request )

**4.** Django maps the requested URL pattern to a view and loads that view. It does 
this by referring to our `urls.py` file. We will look at this step very soon.

**5.** Since the HttpRequest object is passed into the view when it is loaded
we can use it decide how we are going to handle any number of business logic
things

**6.** When each view is done doing its specific processing it **must** return
a response of type HttpResponse

Read through these steps again. They are slightly abstract but make your 
best effort to try and commit them to memory. Understanding this cycle is the key.
The next two sections will walk through these steps individually.

### Urls and View Relationship
__\*this following section will cover steps 3 and 4 from above\*__

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

Navigate to the url above and see the result. [[2](http://www.cs.cmu.edu/afs/cs/usr/mwm/www/tutorial/url.html)]

### View Workflow
__\*this following section will cover steps 5 and 6 from above\*__

Now let's examine one view from the final project to understand the request and response
workflow in detail.

Let's take a look at some of the code in the `views.py` file located at `/blogengine/views.py`:

    from django.shortcuts import render_to_response
    from blogengine.models import Post, Category

    def getPost(request, postSlug):
        # Get specified post
        post = Post.objects.filter(slug=postSlug)

        # Display specified post
        return render_to_response( 'single.html', { 'posts':post } )


The URL that points to this view ( it will trigger it to run ) can be found by 
looking in setting app's `/djsblog/urls.py` file. Look for this line. This is the
beginning of the request cycle:

    #
    # Blog Posts Detail
    #
    url(r'^\d{4}/\d{1,2}/(?P<postSlug>[-a-zA-Z0-9]+)/?$', 'blogengine.views.getPost'),

This looks complicated, but ignore that for now. All this line is doing is mathcing a URL
to the `getPost` function that we listed above. 

So we don't leave you completely in the dark the weird URL syntax above is just 
mathcing a year, month and post ID in the URL. The most important part of the 
URL above is `(?P<postSlug>[-a-zA-Z0-9]+)` which matches any number of 
lowercase/uppercase alpha values and numbers at the end of the URL and passes it to
the view function. The name `postSlug` is going to be matched
in the view's function definition:


    def getPost(request, postSlug):

Without knowing anthying about what a view is we can piece together some crucial
things about this workflow. The view function is passed a request object. 
The request object contains a pile of information about what is happening. For example, 
it contains informaiton about what type of HTTP method this view was request with ( ex. POST, 
GET ). They also potentially have information about the user and their permissions.
[[3](https://docs.djangoproject.com/en/dev/ref/request-response/#httprequest-objects)]

The view function is also the variable name `postSlug` that we saw in URL. A slug
is another name for an ID. We will use this ID to request information from
the database about a specific post, the one identified by the postSlug variable:

    # Get specified post
    post = Post.objects.filter(slug=postSlug)

Let's ignore the syntax for now, since we are going to talk about Models and the ORM next. The above
code gets a post from the database. It's just an object with attributes that map to the 
database fields. 

The last code statement in the view is the last step in the request/response cycle ( this is not
really true, but for simplicity let's just assume this true ). This line of code
is taking the data we've packaged in the dictionary and passing it to a template to 
be rendered ( more about this later ).

    # Display specified post
    return render_to_response( 'single.html', { 'posts':post } )

