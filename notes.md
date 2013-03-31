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