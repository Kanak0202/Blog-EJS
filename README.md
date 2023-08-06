# Blog-EJS

Express route parameters

Used to route dynamically. 
https://masteringjs.io/tutorials/express/route-parameters

Challenge 16  (306)

In the url after posts, if we enter any route name then it gets console logged in our terminal.

app.get('/posts/:postno', function(req, res){
  console.log(req.params.postno);
});)

Challenge 17 (308)

print "match found" in console if the requested parameter of url matches any of the post's title.

app.get('/posts/:postName', function(req, res){
  let requestedTitle = req.params.postName;
  for(var i=0; i<posts.length;i++){
    if(requestedTitle === posts[i].pTitle){
      console.log("Match Found!");
    }
  }
});

Challenge 18 (310)
Implement lodash by reding the documentation

Websites use ""kebab case"" in their urls. 
Lodash -  A utility library that makes it easy to work with js inside our node apps

install lodash by writing npm i lodash in terminal

require lodash: const _ = require('lodash');       //this underscore is our lodash

app.get('/posts/:postName', function(req, res){
  let requestedTitle = req.params.postName;
  requestedTitle = _.lowerCase(requestedTitle);
  for(var i=0; i<posts.length;i++){
    if(requestedTitle === _.lowerCase(posts[i].pTitle)){
      console.log("Match Found!");
    }
    else{
      console.log("Not a match");
    }
  }
  // console.log(req.params.postName);
});


Challenge 19

Create dynamic pages for every blog we publish

in post.ejs:
<%- include("partials/header") %>
<h1><%= titlePost %></h1>
<p><%= contentPost %></p>
<%- include('partials/footer') %>

in app.js:

app.get('/posts/:postName', function(req, res){
  let requestedTitle = req.params.postName;
  requestedTitle = _.lowerCase(requestedTitle);
  for(var i=0; i<posts.length;i++){
    if(requestedTitle === _.lowerCase(posts[i].pTitle)){
      let postP = posts[i].pTitle;
      let postB = posts[i].pBody;
      res.render('post', {titlePost:postP, contentPost: postB});
    }
  }
});


Challenge 20

Show only a 100 characters of blog post.

in home.ejs:
<p> <%= post.pBody.substring(0, 100) + "..."  %> </p>

Challenge 21

On the home page at the end of each blog post we have to have a link named read more clicking on which takes us to the respective blog page

In home.ejs:
<p> <%= post.pBody.substring(0, 100) + "..."  %> <a href="/posts/<%= post.pTitle %>">Read more</a></p>
