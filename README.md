# trello-clone

```
npm install
```

cd to /public

```
bower install
```


Have a running mongo instance on the default port (27017)

```
 > mongod
```

then

```
 > nodemon server.js
```

and open in browser: localhost:8000


## Intro / node modules (Day 1)

### Project introduction

####
In this project, you will be building a full-stack app that will be a clone of trello.com. In order to get started, you will need to clone [THIS](https://github.com/DevMountain/trello-clone) repo. You will automatically be on the `master` branch. This branch is the project solution. You may refer to this code if you need to. For each day, you will need to checkout to a new branch. In the new branches we have removed the code that you will be working on that day, but we have left in the rest of the code for the rest of the project. This will give you the ability to test the app after you finish each day's work. After you finish everything for that day, you will be able to fire up your project and see it in your browser. If it pulls up okay, and everything is working, then you know you finished the day's work correctly. If it doesn't work, then you will some more work to do.

Now, at the start of each new day (section), you will need to checkout to the branch that will be associated to that day. So, to start today's work, open your terminal, and navigate (cd) to the root of this project. If you run `ls`, you should see `server.js`. From there, run this command in your terminal: `git checkout day-one`. Now you are ready start today's work. Each day you will run that same command, but with the new branch for that day (ie. `day-two`, `day-three`, etc.).

Finally, instructions for building this project are in the [Project Guide](http://projectguide.devmounta.in/#/trello-clone). In the project files themselves there will be a few comments and instructions to give you a little bit of a guide, but you will want to follow the instructions in the project guide.

If you have any feedback on the project, or instructions, you can make a change in the project, or on the README.md, then submit a pull request to the DevMountain repository, and we will review those changes. (It will happen a lot faster if you message the link to your pull request to your teacher).

Have fun!

### Project Setup

####
You will probably notice that the file structure is different than the last project. This setup organizes files by file type. So, in your angular app, you will see that all of the controllers are in one directory, and then the services are in a seperate directory. In the `views` directory, you will see another directory called `partials`. This directory is used for html templates that are used by the directives in this project.

Project organization is determined by the project itself, and then the developers working on the project. You will see different styles of organization used in the programing world, and will probably quickly come to have your own preference for organization.

### Node Modules

####
To get our node server up and running, install the `express` module with npm, then import `express` into your server.js file.

####
* Open your terminal and navigate (cd) to the root of your project
* Install `express` using npm
* Import `express` into your server.js file with a require

####
##### Using npm to install node modules
Open your terminal, and make sure you have navigated to the root of your project (if you run the `ls` command, you should see `server.js`, `api`, and `public`. When you are there, you can now run the `npm` command to install node modules for your project.

To start out, we want to install `express`. To do that, run `npm install --save express`. This tells npm to install the express library to your project, and save a reference of the express library in your `package.json` file.

##### Import a node module with require
Now that the node module is installed, we need to import it into your server.js file. This will allow us to access and use the library from this file. You can compare this to injecting a service into a controller in Angular. By doing that, the service, and its built-in functions become "available" to the controller. In the same way, if you import a node module into a .js file, it becomes "available" to that file.

Import express into the server.js file like this (it will always go at the top of your file) :

`var express = require('express');`

## Create and run your node server

### Wire up your server

####
Set two variables under your imports called `app` and `port`, and give them the appropriate values needed to be able to start you server. Then, finish setting up your server using the `listen` function on `app`.

####
##### Define app and port
With `var app` we need to use express to create an express app in our node server. With `var port` we will declare a port which our server will run on.

##### Start the listen function
Use the `app.listen` method to finish starting up your server. Remember, this method takes two parameters - a number for which port to use, and a callback function. Inside the callback function you can use a `console.log` to show when your server starts up.

####
Your server.js file at this point should look like this:

```
var express = require('express');

var app = express();
var port = 8000;

app.listen(port, function() {
    console.log("Server started on port " + port);
};
```

(I like to have a little fun at this point, and log something like `console.log("I am watching you... " + port);`

### Start up your server

####
In your terminal, install `nodemon` if you haven't yet already - `npm install -g nodemon`. Remember, the flag `-g` means that nodemon will be available globally on your computer, and you will be abl to use it for any of your node projects. When that is installed, navigate (cd) into your project root folder where server.js is, and run nodemon to spin up your new node server - `nodemon server.js`.

## Create and Test your First Endpoints (Day 2)
### Set up endpoint
####
##### Fundamentals of our node server
Now the magic begins! Our server.js file is a lot like any other javascript file we have written so far in the class. The biggest difference is that it does not live in the browser like our Angular files do. This file will live on a server (ie Amazon Web Services (AWS), or Digital Ocean servers, or a local server inside your computer). Knowing that, we have to understand that whichever server your server.js is living on will receive communication from a browser, or even another server. This will come in the form of an HTTP request.
##### HTTP communication
Remember building $http requests in Angular? With every single request you have made from Angular, you have defined the type of request you are making, and the URL it is supposed to go to. But what happens when we make that request from the browser? The request goes to a server, locates the correct endpoint that correlates with the defined URL, and then invokes a function, and waits for that function to execute and return something. It is really that simple!

##### A basic 'successful' api call - or HTTP request - will happen something like this:
* Request in Angular is defined with the request type, the URL, and also any data we need to send with the request.
* Request is sent from the browser to the server with that specific information and data.
* The request is matched with the corresponding endpoint on the server, and the function associated with that endpoint is invoked.
* The server returns whatever was returned by the function that was called.

The connecting piece in all of this is the URL that is defined in our Angular files, and the endpoints that are defined in our server.js file.

Create an endpoint in your server.js file that will correspond with a 'GET' request made to `http://localhost:8000/api/test`. That endpoint will return a string that will confirm that the test was successful.

####
In the public, or browser file that makes this request (that would be in an Angular service file), the request will look something like this:
```
this.testRequest = function() {
  $http.get(http://localhost:8000/api/test).then(function(res) {
    console.log(res);
    return res;
  }
};
```
We are expecting that console.log to be a string that will confirm the success of our HTTP request. In order to make that happen on the server side - within the server.js file - we need to match up the appropriate pieces, and return some success string:

http://localhost:8000/api/test ---> matches up with our endpoint ---> '/api/test'
_HINT_:
```
app.get('endpoint', cb(req, res) {
    res.send(string);
});
```

Don't forget that there is not a return inside the function. Instead, we are going to use the `res` object (think of it as the 'response' object - the object that the server is going to 'respond' to the request with), which has a method on it called `res.send()` to send back, or 'respond' back with the success string.

####
So, your code will look something like this:

```
app.get('/api/test', function(req, res) {
    res.send("The request was successful!");
});
```

### Test your new endpoint with Postman
####
If you haven't already, download Postman. This is a tool that will help us test api calls, whether to our own server, or some cool third-party api like the Marvel Api!

When that is installed, open it up, and you will see a gray bar at the top that has a dropdown for request types, then a space to enter your URL, and a SEND button. We are going to use this tool to test our new server.

STOP!!! Before you can test your server, you need to start up your server! No communication can be made to a server if it's not running... Right?!? So, in your terminal, navigate to the root of your project and run this command:
`nodemon server.js`.

You should see the message that you console logged in your app.listen function. Now your server is fired up, and ready to receive some requests!

In Postman, make a request to the new endpoint on your server. You will have to choose the right request type and fill in the URL. When you hit SEND, you should get your success string back as the response. Try it now!

### Build an Angular App and test your server
####
##### Angular basic structure
In the file structure, there is a directory called public. This will hold all the files for our Angular app. Inside that directory, build out your angular app. Go ahead and build out the angular structure for all of the files, but for now, we are just going to be working in the authView, authCtrl, and the listService. You will need to build the routes for ui-router as well. We will only need an `auth` state, and a `list` state.

##### Wire up an $http request
In the listService, write a $http request that will hit the test endpoint in your server. Build out the service, controller, and view so that you can display the returned string in your browser. There is still one step that we need to complete before this can be successful, so you won't be able to test things yet.

##### Serving the public files
In your server.js file, have your express app serve the public files (aka "static" files) that are in the public directory. Then, fire up your server, and test your angular app.

####
If you had tried to test your new endpoint from your angular app before you have served the static files from your server, you've probably realized it isn't ready quite yet. If you ran `nodemon server.js` in your terminal to try and test it, you were moving in the right direction, but first, we need to serve the static files that are in the public directory to the browser. Luckily, your express app as a method to do just that.

_HINT:_ In the app.use method, run the express.static() method, defining the path of the public directory that needs to be served.

####
In order to serve the static files that you have in your project, you will need the following code:

```
app.use(express.static(__dirname + '/public'));
```

Now that you have that set up, spin up your server with `nodemon server.js` and test it in your browser.

## Middleware and Frontend (Day 3)

### Set up the middleware
####
Middleware in a server is a function - or a set of functions - that will run with every single request that comes to your server. This is done before a request even makes it to the server's endpoints. Middleware can handle headers, parse JSON, or check for authentication, among other things. You can consider middleware a "gatekeeper" for your server.

##### Setting up cors
Install and import the `cors` node module into your server. This will take care of all of the headers your server will need in order to make your "cross origin" AJAX requests from your user's browser to your server. Now use your express app to run `cors` as a middleware in your server.

##### Setting up bodyParser
Install and import the `bodyParser` node module into your server. This will take care of parsing all of the JSON in the AJAX requests your api will receive. Now use your express app to run `bodyParser` as a middleware in your server.

##### Setting up morgan
Install and import the `morgan` node module into your server. This will log incoming traffic to your server for you. Now use your express app to run `morgan` as a middleware in your server.

####
##### cors
* Install the `cors` library with npm in your terminal - remember that this needs to be done at the root of your project.
* Import `cors` to your server.js file using `require`.
* Set up `cors` as to run middleware using the `.use()` function that is available on your express app.

##### bodyParser
* Install the `bodyParser` library with npm in your terminal.
* Import `bodyParser` to your server.js file using `require`.
* Set up `bodyParser` as to run middleware using the `.use()` function that is available on your express app.

##### morgan
* Install the `morgan` library with npm in your terminal.
* Import `morgan` to your server.js file using `require`.
* Set up `morgan` as to run middleware using the `.use()` function that is available on your express app.

####
##### cors
```
var cors = require('cors');

app.use(cors());
```

##### bodyParser
When you set up `bodyParser` as middleware, you will need to use `.json()` to parse JSON data, and `.urlencoded({extended: false}))` to tell this middleware to only parse urlencoded bodies, and to use the `querystring` library (see https://www.npmjs.com/package/body-parser-json).
```
var bodyParser = require('body-parser');

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended: false}));
```

##### morgan
The `morgan` function takes a string as it's first parameter to determine the logger's format (a list of available options can be found at https://www.npmjs.com/package/morgan). We are going to use `'dev'` as the format for our morgan logger.
```
var morgan = require('morgan');

app.use(morgan('dev'));
```

##### server.js file
```
/************* IMPORTS *************/
var express = require('express');
var bodyParser = require('body-parser');
var cors = require('cors');
var morgan = require('morgan');
var app = express();
var port = 8000;

/********** MIDDLEWARE **********/
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({extended: false}));
app.use(cors());
app.use(morgan('dev'));

/************* API *************/
app.get('/api/test', function(req, res) {
    res.send("The request was successful!");
});

app.listen(port, function() {
	console.log('Server listening on port ' + port);
});
```

### Building out the login page

####
If you don't know what trello is, now is a really good time to go to trello.com, sign up for a fee account, and play around with it. We are building a simplified version of trello, so it will help to be a little familiar with how it works.

For our app though, we just want a login page, and a home page where we will have the trello style boards and lists. So, first let's build a login page. You can style this however you want. The only requirements are for you to have a place for the user to type in their username, and then a button that will log them in. Don't worry about having a password field. We will only require a username. In the login process, run a function in your controller that passes the username to your service, then make a request from the service to your server. In your server, console.log the request that came in and return a string with a success message. Finally, route the user to the lists page.

Finally, try to make this page look really nice. Remember, design really counts when it comes to the job hunt!

####
In order for your user to log in with their username, you will need an `input` element in your html that is bound to the $scope object with the ngModel directive. You can wrap the `input` tag in an html `form` tag to give you the ability to use ng-submit, which will let you user hit enter to login. You will still need to include the button, as some people will click the button to log in as well. Inside your authCtrl, you will need a login function on the $scope object that hits some endpoint on your server, sending the users username. In your server, console.log the reqquest body, and make sure it is going through. Then return some string that says that the login was a success.

####
Your code may look something like this:

##### authView.js
```
<form ng-submit="login()">
    <input type="text" placeholder="Enter username" ng-model="username" autofocus>
    <button>Login</button>
</form>
```

Remember to style this form. The default `<button>` tag is horrific, and definitely needs some help!

##### authCtrl.js
```
$scope.login = function(username) {
    console.log("username: ", username);
    authService.login(username).then(function(res) {
        console.log(res);
        $state.go('list');
    };
};
```

##### authService.js
```
this.login = funciton(username) {
   return $http.post(url, {username: username});
};
```

##### server.js
```
app.post('endpoint', function(req, res) {
    console.log('**** request body', req.body);
    res.send("You have succesfully logged in! Best secure login ever!");
});
```

## MongoDB Intro (Day 4)

### Intro to Databases

####
Now that we have worked on building a Node server, we need to learn how to persist data. We are going to use a database to do that. There are a lot of things that we would want to save in a database. If we look at this project, there are a  few things that we will persist to our database. Username, lists, and cards on each list. We also want to be able to make sure that there is some way to tue cards to their core t list, and lists to the correct user. MongoDB will help us make sure all of those stay correlated correctly, and that our data is stored and ready to be called to the browser.

### CRUD operations

####
Remember the "verbs" that we have learned about with HTTP communication? GET, POST, PUT, and DELETE? Databases use a very similar system of communication to know what to do when they receive requests from a browser. The commands are different though, and you can remember them with the acronym CRUD - Create, Read, Update, and Delete. Hopefully you see the correlation between the different verbs. It's something like this:

CREATE  -->   POST <br/>
READ    -->   GET <br/>
UPDATE  -->   PUT <br/>
DELETE  -->   DELETE <br/>

So... if you are making a 'GET' request from the browser, your server will receive that request, then it will use 'READ' commands to read, (or "get") data on the database in order to complete that request. Or, if your server receives a 'POST' request, it will run 'CREATE' commands to the database to create, or write, new data onto the database. And so on.

## MongoDB in our App (Day 4)

### Start up a mongo instance

####
Now we get to put all of our new knowledge into practice! We are going to build out one of each type of request. So, you should be able to run create, read, update, or delete commands within your database. To start off, we need to install and import mongojs in the server.js file. Then define a database instance. You can name the instance "trello-clone", then create a collection called "lists".

####
Using your terminal (from the root of your project) use npm to install `mongojs`. Then you will require that module in your server.js. Now we need to define a new variable that will start our new instance of MongoDB that we will use for this project. Remember, you will invoke your require variable with the name of the instance as a string, and then a collection that will be in the database, defined as a string in an array.

####
##### Install MongoDB
In your terminal, run `npm install --save mongojs` from the root of your project

##### Require MongoDB in your server.js
You will have a line of code in your server.js like this:

```
var mongoJS = require('mongojs');
```

##### Start an instance of MongoDB
Now, to start up an instance of your database, you will use the variable `mongoJS` that you just defined with your require. As mentioned above, we can invoke `mongoJS` and give it a string, then an array of strings as parameters. The string is the name of the database instance - 'trello-clone'. The array of strings will be different collections you can have within your database. We will just use one right now - 'lists'. See the code below:

```
var db = mongoJS('trello-clone', ['lists']);
```

This new variable, `db`, will be used to run commands to your database from your server. You will see in the next step that we will use this variable within our endpoints to do the necessary interactions between our server and our database, all dependent on what api calls are made from the browser.


### In your endpoints, make requests to your database

####
In your server.js, you will need to create endpoints that will receive all four types of HTTP requests from the browser. Then, within the callback functions of your endpoints, you will use your new variable that has the defined database instance to run commands to your database depending on what api calls come in from the browser. Here is what each call should do:

'GET' --> Should return all data within the "lists" collection<br/>
'POST' --> Should receive an object with a new "lists" name, and write that to the database. <br/>
'PUT' --> Should receive an object with a  "lists" id, and the data you want to change (the "lists" new name).<br/>
'DELETE' --> Should receive the id number for whichever "list" you want to delete, then delete it from the database.

####
We can run commands to our database right inside of our endpoints in the server.js files. That's what we will do today, but in the next class it will change a little bit. For now, create four endpoints like we have done already in our Node server. For example, your 'GET' endpoint will look something like this:

```
app.get('api/getLists, function(req, res) {
  console.log(req.body);
  res.send("it worked!");
};
```

But now we want to add the database commands inside the endpoints callback function. Use the `db` variable we declared earlier:

```
db.lists.find(function(err, response){
  if(err) {
    res.status(500).json(err);
  } else {
    res.json(response);
  }
});
```

You will need to build out the database commands using mongo commands. As shown above, 'GET' requests will use a `.find()` command. Here are the others you will use: 'POST' requests will use a `.save()` command. 'PUT' requests will use a `.findAndModify()` command. Finally, 'DELETE' requests will use a `.remove()` command. Now, look at the mongo docs to find out how to build each database command. 

####
To build your endpoints that will interact with the database, you will need to understand what each command is doing. Let's look at them one at a time:

##### 'GET' and `.find()`
With MongoDB, you will use the `.find()` method to GET data from your database. This type of command is known as a "query", and it is a "read" command. We will query our database for data - more specifically for "lists" that we have saved onto the database. The `.find()` method can simply return everything within a collection, which is what we want for now. So, we use the `db` variable, call the specific collection we want to query - `db.lists` - then add our method to it. Now, with all of these commands, we will pass in a callback function so that we can watch for any errors, or get back a response from the database, so that will be built into the callback function. Here is the endpoint to get all of the data back from the "lists" collection:

```
app.get('api/getLists', function(req, res) {
  db.lists.find(function(err, response){
    if(err) {
      res.status(500).json(err);
    } else {
      res.json(response);
    }
  });
};
```

Make sure you can identify each piece of this endpoint, and know what it is doing.

##### 'POST' and `.save()`
Like the 'GET' endpoint, we are going to run a method that will run a command to the database. This method is the `.save()` method. It has a little more to it than running a query that returns all the data from a collection. Let's think about this from the front end perspective. In order to make a 'POST' request from the browser, you need to send a data object, right? So then, your server will receive that object in `req.body`. From the server, we need to pass that object on to the database. So, in the `.save()` method, we will pass that object in as an argument, before we pass in the callback function. Again, we start by definig the endpoint - `app.post('api/addList', callbackFunction)` - then inside the callback function, run the `.save()` method on the collection - `db.list.save(dataObject, callbackFunction)`. Our `dataObject` is going to be `req.body`, which holds the data object that the browser sent. Let's see it all toghether:

```
app.post('api/addList', function(req, res) {
  db.lists.save(req.body, function(err, response) {
    if(err) {
      res.status(500).json(err);
    } else {
      res.json(response);
    }
  });
};
```

##### 'PUT' and `.findAndModify()`
The `.findAndModify()` method is a lot like the `.save()` - you pass is an object so the database knows what to do. The object you pass in has to have some idenbtifier for what you want to find (eg a specific "list's" id number, or a "list's" name). You will then also need to have the data that you want to change. So, if we have a "list" called 'DevMtn Homework' with and id of '5', and you want to change the name to 'DM Homework', you would tell the database to find the "list" that has the id of '5', then give it an object that would look like this: `{ update: { $set: { name: 'DM Homework' } } }`. `$set` is a new command we haven't seen. If you look into the mongojs, or MongoDB docs, you will see this pattern all over. The object above is telling the database that it is going to change some info on some piece of data that it already has. Once you have queried for that specific piece of data, or in our case, the "list" that has the id number '5', it will "set" the name of that "list" to 'DM Homework'.

There is, however, one part that we are missing. How will the database know to query for that particular "list"? Before we pass the above object in to set the new name, we will use a "query" object that will be pretty similar to the `update` object - `query: { _id: mongoJS.ObjectId(req.query.id) }`. Let's look at this one. `mongoJS.ObjectID()` is a method that takes and id number, and parses it into a MongoDB id. This is necessary, because a MongoDB id is actually a 'number' data type in javascript. ([MDN Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)). It is it's own data type, so we have to parse our number into a "MongoDB id". 

So, here is the data object that we are going to give our `.findAndModify()` method as the first argument:

```
db.lists.findAndModify({
    query: {
      _id: mongoJS.ObjectId(req.query.id) 
    },
    update: {
      $set: req.body
    }, 
  }, callbackFunction);
```

I know that sometimes with the way we lay out objects, it can be harder to tell what is going on. Here is a step by step write out, starting with psudeo-code, that maybe will help with that:

```
db.lists.findAndModify(dataObject, callbackFunction);

// then build dataObject with a query object and an update object:

db.lists.findAndModify({ query: queryObject, update: updateObject }, callbackFunction);

// Now build the queryObject and updateObject with the respective mongoJS commands:

db.lists.findAndModify({ query: { _id: mongoJS.ObjectId(req.query.id) }, update: { $set: { name: 'DM Homework' } } }, callbackFunction);

// Now you have the same code as above, but just in a single line, rather than split into different lines. 
```

With that, we can now build this into our endpoint:

```
app.put('api/updateList', function(req,res) {
  db.lists.findAndModify({
    query: {
      _id: mongoJS.ObjectId(req.query.id) 
    },
    update: {
      $set: req.body
    }, 
  }, function(err, response) {
    if(err) {
      res.status(500).json(err);
    } else {
      res.json(response);
    }
  });
};
```

##### "DELETE" and `.remove()`
And, last but not least, the "DELETE" request. This method will be like the `findAndModify()` method. This time, you will only need to pass in an id number for the database to query by, then the database will delete that particular "list". So, it should look something like `db.lists.remove({ _id: mongoJS.ObjectId(req.query.id) }, callbackFunction);` So, your full endpoint will look like this:

```
app.delete('api/removeList', function(req, res) {
  db.lists.remove({ _id: mongoJS.ObjectId(req.query.id) }, function(err, response){
    if(err) {
      res.status(500).json(err);
    } else {
      res.json(response);
    }
  });
};
```

That's it! Now we need to test these endpoints.

### Run and Test your Database

####
You will want to test all four endpoints after you have created them. To do so, you will need to download RoboMongo - if you haven't already. Start up your mongo database (with launchrocket for mac, or just run `mongod` in your terminal), then open RoboMongo. You will see your database instance in the sidebar menu. If you click on that, you will see a directory called "Collections" which, when you open that in the sidebar you will see a collection called "lists"! So cool! Things are starting to come together! Now we just need to populate the database.

Spin up your server, then with postman run a couple 'POST' requests. You should see these populate inside RoboMongo. You can then run a 'GET' request in postman and you should get back all the lists you have made. Now try a 'PUT' request to change some of the data, and a 'DELETE' to delete one of your lists. It's so cool! Great job!!! 

Now that it is all tested and working, you can comment out your code and uncomment the project code to test the trello app, but you haven't really built any of that code yet, because in the next class, we will change up how we interact with MongoDB by introducing mongoose - a library that will help simplify database commands. So, at this point, you can only test your code in postman (unless you want to be ambitious and build out the front end code for your new found database powers of awesomeness).

## MongoDB with Mongoose (Day 5)

### Intro to Mongoose

####
What is MongooseJS, and why will we want to use it? This blogpost, titled [MongoDB + Mongoose](http://blog.modulus.io/getting-started-with-mongoose) says: "Mongoose is a Node.js library that provides MongoDB object mapping similar to ORM with a familiar interface within Node.js. If you aren't familiar with Object Relational Mapping (ORM) or, Object Data Mapping (ODM) in the case of Mongoose, this means is that Mongoose translates data in the database to JavaScript objects for use in your application." 

Sounds really useful, right? Right! 

And, from [MongooseJS](mongoosejs.com) itself: "Let's face it, writing MongoDB validation, casting and business logic boilerplate is a drag. That's why we wrote Mongoose. Mongoose provides a straight-forward, schema-based solution to model your application data. It includes built-in type casting, validation, query building, business logic hooks and more, out of the box." 

Now you're talking! Let's get started!

### Install and require `mongoose`, and define your MongoDB instance

####
In the terminal, use `npm` to install `mongoose`, import it into your server.js with `require`, and then setup all your database connections through MongooseJS.

####
To set up your database connections using MongooseJS, you will need to use the `mongoose.connect()` method. Now let's set `mongoose.connection` to our `db` variable. Now we can run methods like `db.on()` and `db.once()`. In the `db.once()` method, we will tell mongoose to console.log  a message that tells us that the database is running "once" the database is "open" (_hint hint_).

Then, to get error message logged into the terminal, you can use `db.on()`, and specify that "on" any "error" (_hint hint_) we wan to log that error in the console.

####
After installing MongooseJS by running this command in our terminal, at the root of the project: `npm install --save mongoose`, we need to import the module into our server.js file using this code: `var mongoose = require('mongoose');`.
Now we can use mongoose as an interface between our NodeJS server and our MongoDB database.

The code to start up our database instance using MongooseJS will look like this:

```
var mongoUri = 'mongodb://localhost:27017/betterTodo';
mongoose.connect(mongoUri);

var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error: '));
db.once('open', function() {
    console.log('connected to db at ' + mongoUri)
})
```

### Object Modeling with MongooseJS

#### 
Inside the models files, we are going to build the schemas for our database. So, for your listmodel.js, require `mongoosejs` and make a `Schema` variable. Then build out the `List` Schema. For today, just give each `List` a name. `name` will be required, and will be a 'String'. Then export this new module.

Next, in the usermodel.js, require `mongoosejs` and set your `Schema` variable again. Now build your `User` schema with a username that is required and is a 'String'. Then export this module as well.

Finally, inside your server.js, you will need to import both of those modules using a `require`.

####
To build your modules, you need to set `Mongoose.Schema` to the variable `Schema`. This gives us the ability to create a new "instance" of each model on the database. So, for each new list a user makes, it will create a new instance of the list, or user schemas. 

Next, we will create these instances by using the "new" keyword with `Schema`. For example, in listModel.js:

```
var List = new Schema();
``` 

Then, pass in an object to `Schema` so that you define what each new schema instance should look like in the database. This goes back to the purpose of MongooseJS to provide MongoDB with "object mapping". MongoDB is a very flexible database, in that you don't need to define what documents are supposed to look like before passing data to it like you would with SQL databases and their tables. However, it would be very beneficial to provide some structure to your database, so that when you call the data at a later point, you have an idea of what it will look like. So, enter MongooseJS, and schemas. We can keep the flexibility of MongoDB as a document database, AND have schemas defined and structured to keep our data organized. 

So... back to what we were doing. We are going to give structure to the data going into our database by passing an object into the `Schema` we just defined above. This will tell our database that anything goes in as a `List` should have a name, and that the name should be a "String", and should be required. 

Finally, use `module.exports` to export this module. MongooseJS has a method that will define the module name - `Mongoose.model()`. It takes two arguments: first, a string with the name that you want the module exported as; second, it takes the variable that you created (`List`) that captures the new instances of the list schema. So something like this: `Mongoose.model('List', List);

Follow this pattern with the userModel.js file as well.

####
##### listModel.js
```
var Mongoose = require('mongoose');
var Schema = Mongoose.Schema;

var List = new Schema({
    name: {
        type: String,
        required: true
    }
});

module.exports = Mongoose.model('List', List);
```

##### userModel.js
```
var Mongoose = require('mongoose');
var Schema = Mongoose.Schema;

var User = new Schema({
    username: {
        type: String,
        required: true
    },
    lists: [{
        type: Schema.ObjectId,
        ref: 'List'
    }]
})

module.exports = Mongoose.model('User', User);
```

### Rewrite the server's endpoints

####
So far, we have built all of our logic into our endpoints. Today we are actually going to import new files called "controllers" into our server.js file, invoke functions that live inside those seperate "controller" files from our endpoints, then build our logic inside there. This logic is what houses the database interactions and comand. The "controllers" will import the models we just created so that MongooseJS will know what the schemas look like as the interaction with the database happens.

We already have the models built, so now let's build the endpoints in the server.js file, then we will build the "controllers" as the middle pieces. 

Build three endpoints that will be for the `List` schema. 

##### 'GET'
Build a 'GET' endpoint, and have that invoke a function called `getLists` that will be in the list controller - ie `ListCtrl.getLists`. One interesting thing to note here is that you don't have to have invoking parenthesis. These functions will run without them. That is an "under-the-hood" feature. 

##### 'POST' to add a list
Now build an endpoint for 'POST' requests that will invoke the function `addList` in the controller.

##### 'POST' to delete a list
A 'POST request to delete a list? Yep! This is one way to delete a list. We can pass a data object with a 'POST' request, and therefore have the list id that we need in order to query for the correct list, and then remove it from the database (which will happen in the controller in a minute...). This endpoint will invoke a function called `deleteList` in the controller.

Finally, in order for us to call functions inside the controllers like this: `ListCtrl.getLists` we need to define `ListCtrl`. Import the list controller using a require, and giving it the relative path to that file, then set that to a new variable called `ListCtrl`. Now we have imported that file, and can call the methods there that we need to.

####
To import `ListCtrl` require the file in your server.js like this - `var ListCtrl = require(./api/controllers/ListCtrl.js`

####
Your endpoints should look like this:

```
app.get('/api/getLists', ListCtrl.getLists)

app.post('/api/addList', ListCtrl.addList);

app.post('/api/deleteList', ListCtrl.deleteList);

```

### Building the controllers

####
Now, with your schemas ready, and the enpoints built in your server, you can build the list controller. In the controller you will need to import the `list` module at the top of your file. Now, set up your functions that you are invoking in your endpoints. Remember, these functions are properties of an object. Also, don't forget to export that object, so that you can import it into the server.js and have these functions available to the endpoints.

####
We have the `List` variable now that is importing the `List` Schema. We can query off of this variable and retrieve data to display, or to change, or to delete. We can also instantiate a new instance of the `List` model to create a new list. Let's start with querying for all of the lists.

##### getLists
The get function is going to query the database and return all of the lists in the `Lists` document. To do that, we will use the `.find()` method on the `Lists` model. Then run the `.exec(callbackFunction);` method to catch any errors and return the error to the browser, or, if there are no errors, return the success result to the browser.

##### addList
Now let's look at adding a list. We don't need to query for any lists on the database, just add a new one. To do that, we need to instantiate a new instance of the `List` model using the "new" keyword and passing in the req.body, then set that to a variable (ie `newlist`), and then run the `.save(callbackFunction);`. The callback function is where you will catch errors, and send an error message, or the success result to the browser.

##### deleteList
Finally, let's delete a list from the `Lists` document. We will need to query the database for the particular list you want to remove, then remove it. Luckily, MongooseJS has a method that will do both steps at once - `.findByIdAndRemove(id, callbackFunction);` The id number you want to pass in is a part of the req.body object. You can `console.log(req.body)` to find out how to pass that in. Your callback function will catch errors, and again return an error message, or success result to the browsers.

####
Your controller should have these two parts:

```
var List = require('../models/ListModel.js');
```

and

```
module.exports = {


};
```

Then your functions are set as properties on that object:

```
module.exports = {

  getLists: function(req, res){},

  addList: function(req, res){},

  deleteList: function(req, res){}

};
```

Now the business logic that will run commands to the database will be built inside each function.

##### getLists

```
getLists: function(req, res) {
  List.find()
  .exec(function(err, result) {
     if (err) return res.status(500).send(err);
     else res.send(result);
  });
},
```

Keep in mind that you can pass query parameters into the `.find()` method if you want to do a more specific query to the database, like finding a specific list by id, or name.

##### addList

```
addList: function(req, res) {
  var newList = new List(req.body);
  newList.save(function(err, result {
    if (err) return res.status(500).send(err);
    else res.send(result);
  };
},
```

##### deleteList

```
deleteList: function(req, res) {
  List.findByIdAndRemove(req.body.id, function(err, result){
    if (err) return res.status(500).send(err);
    else res.send(result);
  });
}
```

### Test your new backend system
####
Now you can run `mongod` and `nodemon server.js` to fire up your backend, then use postman and robomongo to test your new backend. We are not quite to a point that we can use this code in the full project, because there is one more crucial part to making the backend work for our project. If you notice, when you create a "card" on a single "list", it only shows up on that list, and not every single list. How does the database know to only show that particular card on that particular list? There is a way to reference a specific card to a specific list, but we won't learn that until the next lesson. So, if you would like to see the project up and working, you will need to comment out your code, and put the project code back in. This would be a great time to look through the models and controllers we have set up for the project and see you can start to get an understanding of what is going on. 


## Data Relationships (Day 6)

### Building the Models

####
Now, as mentioned earlier in the project guide, we want to be able to associate a user and his/her lists, and also a list with all of its cards. This association will make so that when you login to the website, you don't get someone else's lists, and your lists won't have the wrong cards in them. With MongooseJS, there is two ways to create these relationships. Referencing a schema inside another schema, or embedding a schema inside another one.

In our project, we are going to reference the `List` schema inside the `User` Schema. So, create the userModel and give the model object a username that is required and is a String. Then, give it a "lists" property. This property will be of the type "Schema.ObjectId", and will reference 'List'.

Then in the `List` schema, we will just embed an object directly into the schema for the cards. So, on the model object, include a property called "cards" that will be an array. The cards within this array will have a title that will be a String and will be required.

####
So, for the `User` schema, we will reference the user's lists by adding an array on the model object. Inside the array, we are just defining the reference, so there will just be the one object in it. But, when you have a user with multiple lists, you will see in robomongo that the array will be populated with the lists for that user. So, "lists" will be an array with a single object. This object will specify that the reference will be of the type "Schema.ObjecId", and the we are referencing the lists from the `List` document. That part is cool, because it will tell MongoDB to only look in the `List` document for the lists, and won't have to look throught the entire database! Cool, huh?

Then the `List` Schema will have an array of cards for each list. We are just going to embed a "schema-like" object onto a property called "cards" in the model object. "cards" is also going to be an array with the object inside it. Just like the lists array in `User`, "cards" will be populated with each card in each list. The object in the array will have a property called "title". The value of that property will be another object where we can specify the type to be a String, and that we want to require the title for each card.

####
userModel.js:

```
var Mongoose = require('mongoose');
var Schema = Mongoose.Schema;

var User = new Schema({
    username: {
        type: String,
        required: true
    },
    lists: [{
        type: Schema.ObjectId,
        ref: 'List'
    }]
})

module.exports = Mongoose.model('User', User);
```

listModel.js:

```
var Mongoose = require('mongoose');
var Schema = Mongoose.Schema;

var List = new Schema({
    name: {
        type: String,
        required: true
    },
    cards: [{
        title: {
            type: String,
            required: true
        }
    }]
})

module.exports = Mongoose.model('List', List);
```

### Build the Controllers

####
Now that the schemas have been updated, the functions on our controllers have to change as well. Look at the endpoints in the server.js file, all except the login / logout and moveCard endpoints (we will look into those in the next lesson), and build in the corresponding functions inside the controllers. This may be a little tough. This is where all of your JavaScript logic powers of awesomeness will com in play! 

####
Let's look at the functions one at a time. I will give you hints on how to form the logic. 

`getLists` will be simliar to what we had before, but now you will need to add the cards to each lists by using the `.populate()` method.

The `addList` function will need to add the list to the database, query the database for the user that added the list (`User.findById(req.session.user._id)`), then "push" the _id to the to the array of lists in the `User` document for that user. Now, you won't have the _id of the new list until the database saves it, and send it back with a success response. So, after you save the list, inside the callback function, query for the user, reference the "lists" array on that user, then push the _id that was sent back for the new list.

In the `deleteList` function, query the database for the list by its _id and delete it, then query for the user, and delete the reference to that list from the "lists" array on the user object.

`addCard` will query the `List` for the correct list to save the card on, then just push the card to the "cards array on the list object. Finally, save the new list object.

`deleteList` will query the database for the list, remove the card from the "cards" array, and then save the new list object.

####
Your listCtrl should look somewhat like this:

```
// List functions
// save list
// update list name
var _ = require('underscore');
var ObjectID = require('mongodb').ObjectID;
var User = require('../models/UserModel.js')
var List = require('../models/ListModel.js')

module.exports = {

    getLists: function (req, res) {
        var user = req.session.user;
        User.findById(user._id)
            .populate('lists')
            .exec(function (err, foundUser) {
                if (err) {
                    console.log(err);
                    return res.status(500).send(err);
                }
                return res.status(200).json(foundUser.lists)
            })

    },
    addList: function (req, res) {
        var list = req.body;
        var user = req.session.user;
        //create list
        var newList = new List({
            name: list.listName
        });
        newList.save(function (err, savedList) {
            if (err) {
                console.log(err);
                return res.status(500).send(err);
            }
            //add ref to user
            User.findById(user._id)
                .exec(function (err, foundUser) {
                    if (err) {
                        console.log(err);
                        return res.status(500).send(err);
                    }
                    foundUser.lists.push(savedList._id);
                    foundUser.save(function (err, savedUser) {
                        if (err) {
                            console.log(err);
                            return res.status(500).send(err)
                        }
                        return res.status(200).json(savedList);
                    })
                })
        })
    },
    deleteList: function (req, res) {
        var listId = req.body.list._id;
        var userId = req.session.user._id;
        List.findByIdAndRemove(listId)
            .exec(function (err, deletedList) {
                console.log(deletedList);
                if (err) {
                    console.log(err);
                    return res.status(500).send(err);
                }
                User.findById(userId)
                    .exec(function (err, foundUser) {
                        foundUser.lists.splice(foundUser.lists.indexOf(listId), 1);
                        foundUser.save(function (err, savedUser) {
                            if (err) {
                                console.log(err);
                                return res.status(500).send(err);
                            }
                            return res.status(200).json(deletedList)
                        })
                    })
            })
    },
    addCard: function (req, res) {
        var listId = req.body.listId;
        var newCard = req.body.newCard;
        List.findById(listId)
            .exec(function (err, list) {
                if (err) {
                    console.log(err);
                    return res.status(500).send(err);
                }
                list.cards.push(newCard);
                list.save(function (err, result) {
                    if (err) {
                        console.log(err)
                        return res.status(500).send(err);
                    }
                    return res.status(200).json(list.cards);
                })
            })
    },
    deleteCard: function (req, res) {
        // list Id, card
        var listId = req.body.listId;
        var card = req.body.card;
        console.log(card);
        List.findById(listId)
            .exec(function (err, list) {
                if (err) {
                    console.log(err);
                    return res.status(500).send(err);
                }
                for (var i = 0; i < list.cards.length; i++) {
                    if (list.cards[i]._id.toHexString() === card._id) {
                        list.cards.splice(i, 1)
                        i--;
                    }
                }
                list.save(function (err, result) {
                    if (err) {
                        console.log(err);
                        return res.status(500).send(err);
                    }
                    return res.status(200).json(list.cards);
                });
            })
    },
    moveCard: function (req, res) {
        var card = req.body.card;
        var toList = req.body.toList;
        var fromList = req.body.fromList;

        List.findById(toList).exec(function (err, list) {
            if (err) {
                res.status(500).send(err);
            }
            list.cards.push(card);
            list.save(function (err, saved) {
                if (err) {
                    res.status(500).send(err)
                }
                List.findById(fromList).exec(function (err, listfrom) {
                    if (err) {
                        res.status(500).send(err)
                    }
                    for (var i = 0; i < listfrom.cards.length; i++) {
                        if (listfrom.cards[i]._id.toHexString() === card._id) {
                            listfrom.cards.splice(i, 1)
                            i--;
                        }
                    }
                    listfrom.save(function (err) {
                        if (err) {
                            res.status(500).send(err)
                        }
                        res.status(200).send('moved card')
                    })
                })
            })
        })
    }

}

// Card functions
// save card (to list)
// move card between lists
// update card title
```

### Now test it out!

####
Now that you have the models and controllers ready, fire it up and test away! 
