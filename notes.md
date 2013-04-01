The "el" property
  Every Backbone View has an el property
  el is the element that binds to the DOM element
  
render()
  Render will load the template into the views' el property using jQuery
  
Tip: Place template files separately and serve them via TCDN so that your application is cached.

Listening for events
  We use events attribute of Backbone.View
    Event listeners can only be attached to child elements of the "el" property
    i.e. click listen to a button
    
Using Template variables

<%= %> use this thing to access template variables

What is a Model
  Models are the heart of any JavaScript application, containing the interactive data as well as a large part of the logic surrounding it: conversions, validati
  ons, compute red properties, and access control.
  
  
  initialize() is triggered whenver a new instance of a model is created. 
  
  
  Passing javascript objects to constructors is the same as calling model.set().
  
  Retreiving models
  
  model.get()
  
  opposed to model.set()
  
  How to set model defaults
    default goes before the initialize
    just make an object with default and the keys assignment
    
  Not just get and set 
  Learn to manipulate!
    simply create a method that sets to 'this' so that it looks for the variable being set.
    
    Examples for another item
    
    given:
    
    adopt: function( newChildName ){
      this.set({ child: newChildsName });
    }
    
    Another may be
    
    getOld: function( newAge ){
      this.set({ age: newAge });
    }
  
  Next is listening for changes.
    models can have listeners bound to them to detect changes to their values
    
  SQL table of Users with columns id, name, email would be able tyo access via a RESTful URL /user
  model would look like
  
  var UserModel = Backbone.Model.extend({
    urlRoot: '/user',
    defaults: {
      name: '',
      email: ''
    }
  });
  var user = new Usermodel();
  // Notice that we haven't set an 'id'
  var userDetails = {
    name: 'Lenny',
    email: 'lkbgift@gmail.com'  
  };
  // Because we have not set a 'id' the server will call
  // POST /user with a payload of {name:'Lenny', email:'lkbgift@gmail.com'}
  //The server should save the data and return a response containing the new 'id'
  
  user.save(userDetails, {
    success: function (user){
      alert(user.toJSON());
    }
  })
  
  
  Getting models
  
  use FETCH
  
  // Here we have set the 'id' of the model
  var user = new Usermodel({id: 1});
  user.fetch({
    success: function (user) {
      alert(user.toJSON());
    }
  })
  
  Updating the model
  
  use SAVE
  
  // Here we have set the 'id' of the model
  var user = new Usermodel ({
    id: 1,
    name: 'Lenny',
    email: 'lkbgift@gmail.com'
  });
    
  // Let's change the name and update the server
  // Because there is 'id' present, Backbone.js will fire
  // PUT /user/1 with a payload of {name: 'Kiyoshi', email: 'lkbgift@gmail.com'}  
  user.save({name: 'Kiyoshi'}, {
    success: function (model) {
      alert(user.toJSON());
    }
  });
  
  Deleting a model
  
  Use DESTROY
  
  // Here we have set the 'id' of the model
  var user = new Usermodel ({
    id: 1,
    name: 'Lenny',
    email: 'lkbgift@gmail.com'
  });
  
  //Because there is 'id' present, Backbone.js will fire
  // DELETE /user/1
  user.destroy({
    success: function () {
      alert('Destroyed');
    }
  });
  
Tips and tricks

Get all the current attributes

.attributes

var person = new Person({ name: "Lenny", age: 23});
var attributes = person.toJSON(); // { name: "Lenny", age: 67}

/* This simply returns a copy of the current atributes */

var attributes = person.attributes;

/* The line above gives a driect reference to the attributes and you should be careful when playing with it. Best practise would suggest that you use .set() to edit attributes of a model to take advantage of backbone listeners. */

Validate data before you set or save it

Person = Backbone.Model.extend({
  // If you return a string from the validate function,
  // Backbone will throw an error
  validate: function( attributes ){
    if( attributes.age < 0 && attributes.name != "Dr Manhatten" ){
      return "You can't be negative years old";
    }
  },
  intialize: function(){ 
    alert("Welcome to this world");
    this.bind("error", function(model, error) {
      // We have received an error, log it, alert or forget it
      alert( error );
    });
  }
});
var person = new Person;
person.set({ name: "Mary Poppins", age: -1 });
// Will trigger an alert outputting the error

var person = new Person;
person.set({ name: "Dr. Manhatten", age: -1 });
