# MEAN-STACK



###  [What is Mean Stack]
MEAN stack is a collection of JavaScript technologies used to develop web applications. It stands for MongoDB, Express.js, AngularJS (or Angular), and Node.js. MongoDB is a NoSQL database, Express.js is a web application framework, AngularJS is a JavaScript framework for building web applications, and Node.js is a JavaScript runtime. Together, these technologies provide an end-to-end framework for developing web applications using only JavaScript.


###  MEAN STACK is comprised of four different technologies:
*   **M**ongoDB (Document database): Stores and retrieve data.
    
*   **E**xpress JS (Back-end application framework): Makes requests to Database and returns a response
    
*   **A**ngularJS (Front-end application framework): Handles Client and Server Requests
    
*   **N**ode.js (JavaScript runtime environment): Accept requests and display results to end user
    

The MEAN stack has variants like MERN (replacing Angular.js with React.js) and MEVN (using Vue.js). One of the most popular technological concepts for creating web apps is the MEAN stack.


###  How Does the MEAN Stack Work?
*   The MEAN stack works by using each of the technologies in the stack to handle specific parts of the web development process.
    

*   MongoDB is used to store and manage the application's data. It uses a document-oriented data model, which makes it easy to work with JSON data.
    
*   Express.js is a web application framework built on top of Node.js. It is used to handle routing, middleware, and other back-end tasks. It allows the exposure of APIs and handles requests and responses from the client.
    
*   AngularJS (or Angular) is a JavaScript framework for building dynamic, single-page web applications. It provides a powerful set of tools for building the front end of the application, including data binding, directives, and dependency injection.
    

Node.js is a JavaScript runtime that allows developers to run JavaScript on the server side. It provides an environment for running Express.js and handles server-side logic and database interactions.

The MEAN stack allows developers to use a single language, JavaScript, throughout the entire web development process, from the front end to the back end, making it a popular choice for building modern web applications.


###  
While the MEAN stack isn’t perfect for every application, there are many uses where it excels. It’s a strong choice for developing cloud-native applications because of its scalability and its ability to manage concurrent users. 
The AngularJS frontend framework also makes it ideal for developing single-page applications that serve all information and functionality on a single page. Here are a few examples of using MEAN:**

*   Calendars
    
*   Expense tracking
    
*   News aggregation sites
    
*   Mapping and location finding


### 1. Task- Implement a simple Book Register web form using MEAN stack.


### Step1: Install NodeJs

Provision Ubuntu 20.4 instance in AWS
Once in the terminal, update Ubuntu using this command:
```
 sudo apt update -y
```
Next, upgrade Ubuntu with
```
 sudo apt upgrade
```


  Add certificates:
```
 curl -sL https://deb.nodesource.com/setup_19.x | sudo -E bash -

```

Next, we install nodejs with this: 

```
 sudo apt install -y nodejs
```


###  Step 2: Install MongoDB

First, we add our MongoDB key server with: 

```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```


 Add repository: 
```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```
Install MongoDB with the following command:
```
 sudo apt install -y mongodb
```

 Verify that the service is up and running

```
  sudo systemctl status MongoDB
```

You can further verify that the database is operational by connecting to the database server and executing a diagnostic command. The following command will connect to the database and output its current version, server address, and port. It will also return the result of MongoDB’s internal connectionStatus command:
```
    mongo --eval 'db.runCommand({ connectionStatus: 1 })'
```

```
Output

MongoDB shell version v4.4.25
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("141f3094-1c9e-4917-a064-83599b093c5d") }
MongoDB server version: 4.4.25
{
	"authInfo" : {
		"authenticatedUsers" : [ ],
		"authenticatedUserRoles" : [ ]
	},
	"ok" : 1
}

```

 Install npm – Node package manager: 

```
  sudo apt install -y npm
```
Next, we install body-parser package to help with processing JSON files passed in requests to the server. Use the following command:

```
   sudo npm install body-parser
```


 Next, we create the Books directory and navigate into it with the following command:
```
 mkdir Books && cd Books
```

 Inside the Books directory initialize npm project and add a file to it with the following command: 
```
npm init
```

 Then add sever.js file with:
```
 vi server.js
```
In the server.js file, paste the following code:
var express = require('express');

```
var bodyParser = require('body-parser');

var app = express();

app.use(express.static(\_\_dirname + '/public'));

app.use(bodyParser.json());

require('./apps/routes')(app);

app.set('port', 3300);

app.listen(app.get('port'), function() {

console.log('Server up: [http://localhost](http://localhost):' + app.get('port'));

});
```

### Step 3: Install Express and set up routes to the server


Express will be used to pass book information to and from our MongoDB database and Mongoose will be used to establish a schema for the database to store data of our book register. To begin the installation, type:

\`\`\`

`sudo npm install express mongoose`

\`\`\`

and enter.


 while in Books folder, create a directory named apps and navigate into it with: 
```
mkdir apps && cd apps
```


 Inside apps, create a file named routes.js with: 
```
vi routes.js
```
Copy and paste the code below into routes.js

```
module.exports = function(app) {

app.get('/book', function(req, res) {

Book.find({}, function(err, result) {

if ( err ) throw err;

res.json(result);

});

});

[app.post](http://app.post)('/book', function(req, res) {

var book = new Book( {

name:[req.body.name](http://req.body.name),

isbn:req.body.isbn,

author:[req.body.author](http://req.body.author),

pages:req.body.pages

});

[book.save](http://book.save)(function(err, result) {

if ( err ) throw err;

res.json( {

message:"Successfully added book",

book:result

});

});

});

app.delete("/book/:isbn", function(req, res) {

Book.findOneAndRemove(req.query, function(err, result) {

if ( err ) throw err;

res.json( {

message: "Successfully deleted the book",

book: result

});

});

});

var path = require('path');

app.get('\*', function(req, res) {

res.sendfile(path.join(\_\_dirname + '/public', 'index.html'));

});

};
```

![Step 19 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/2c03faf5-c1a1-42ef-b1b0-659b1465c3af/26980222-7334-4d71-b81d-aa008ac42fa9.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Also, create a folder named models in the apps folder, then navigate into it:
```
 mkdir models && cd models
```
![Step 20 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/68ad81ee-5b51-4c40-82b4-f657cc2cfd41/cef35d69-5efa-416b-9dc1-8910459a57a4.png?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Inside models, create a file named book.js with: 
```
vi book.js
```
Copy and paste the code below into ‘book.js’

```
var mongoose = require('mongoose');

var dbHost = 'mongodb://[localhost:27017/test](http://localhost:27017/test)';

mongoose.connect(dbHost);

mongoose.connection;

mongoose.set('debug', true);

var bookSchema = mongoose.Schema( {

name: String,

isbn: {type: String, index: true},

author: String,

pages: Number

});

var Book = mongoose.model('Book', bookSchema);

module.exports = mongoose.model('Book', bookSchema);
```

![Step 21 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/87d79c29-fddc-4c0a-a2c4-b983c50cb437/273cae98-eb9c-4d9f-9775-cc6ca3880ecb.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Access the routes with AngularJS

The final step would be using AngularJS to connect our web page with Express and perform actions on our book register.



 Navigate back to Books directory using:
```
  cd ../..
```

Now create a folder named public and move into it:
```
mkdir public && cd public
```
![Step 23 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/7c10bbce-1623-4978-8330-118d4d21b8fa/e3318a71-8de8-4dd1-b092-badeef8f199a.png?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Add a file named script.js:
```
 vi script.js
```
And copy and paste the following code:

```
var app = angular.module('myApp', \[\]);

app.controller('myCtrl', function($scope, $http) {

$http( {

method: 'GET',

url: '/book'

}).then(function successCallback(response) {

$scope.books = [response.data](http://response.data);

}, function errorCallback(response) {

console.log('Error: ' + response);

});

$scope.del\_book = function(book) {

$http( {

method: 'DELETE',

url: '/book/:isbn',

params: {'isbn': book.isbn}

}).then(function successCallback(response) {

console.log(response);

}, function errorCallback(response) {

console.log('Error: ' + response);

});

};

$scope.add\_book = function() {

var body = '{ "name": "' + $[scope.Name](http://scope.Name) +

'", "isbn": "' + $scope.Isbn +

'", "author": "' + $[scope.Author](http://scope.Author) +

'", "pages": "' + $scope.Pages + '" }';

$http({

method: 'POST',

url: '/book',

data: body

}).then(function successCallback(response) {

console.log(response);

}, function errorCallback(response) {

console.log('Error: ' + response);

});

};

});
```

![Step 24 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/a636d75a-e06b-45dd-9264-2dd1c8380e8a/ebb7fbbd-0fd6-4736-a749-c12283046366.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Also in the public folder, create a file named index.html: 
```
vi index.html
```
And paste the following html code below into it:

```
<!doctype html>

<html ng-app="myApp" ng-controller="myCtrl">

<head>

<script src="[https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>](https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>)

<script src="script.js"></script>

</head>

<body>

<div>

<table>

<tr>

<td>Name:</td>

<td><input type="text" ng-model="Name"></td>

</tr>

<tr>

<td>Isbn:</td>

<td><input type="text" ng-model="Isbn"></td>

</tr>

<tr>

<td>Author:</td>

<td><input type="text" ng-model="Author"></td>

</tr>

<tr>

<td>Pages:</td>

<td><input type="number" ng-model="Pages"></td>

</tr>

</table>

<button ng-click="add\_book()">Add</button>

</div>

<hr>

<div>

<table>

<tr>

<th>Name</th>

<th>Isbn</th>

<th>Author</th>

<th>Pages</th>

</tr>

<tr ng-repeat="book in books">

<td>{{[book.name](http://book.name)}}</td>

<td>{{book.isbn}}</td>

<td>{{[book.author](http://book.author)}}</td>

<td>{{book.pages}}</td>

<td><input type="button" value="Delete" data-ng-click="del\_book(book)"></td>

</tr>

</table>

</div>

</body>

</html>
```



 Then change the directory back up to Books using: 
```
cd ..
```

 Now, start the server by running this command: node server.js If all goes well server should be up and running and we can connect to it on port 3300.

![Step 27 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/413ffacb-ae3d-4c25-8dbd-12ec0b7a2d9b/b43b8509-8dda-46cf-a1aa-e6545529da68.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)


 Next, I accessed the HTML page over the internet via port 3300 using the public IP: http://34.200.223.160:3300/
![Step 28 screenshot](https://images.tango.us/workflows/859463ac-1a43-44cc-8768-eedf6002be0e/steps/097e6b22-3a69-410c-a81a-ebab11c6bfd0/d9278074-34a1-4161-a94b-1401605facdd.jpeg?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.5000&w=1200&blend-align=bottom&blend-mode=normal&blend-x=800&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmsucG5n)
