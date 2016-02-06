{{#template name="tutorials.socially.angular1.step_04.md"}}
{{> downloadPreviousStep stepName="step_03"}}

Now that we have full data binding from server to client, let's interact with the data and see the updates in action.

In this chapter you will add the ability to insert a new party and delete an existing one from the UI.

First, let's create a simple form with a button that will add a new party, we will add it above the list, inside the `partiesList` Component view:

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.1"}}

Now we need to make this form functional.

## ng-model

First things first, let's bind the value of the inputs into a new party variable.

To do that we'll use the simple and powerful [ng-model](https://docs.angularjs.org/api/ng/directive/ngModel) Angular 1 directive.

Add `ng-model` to the form like this:

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.2"}}

Now each time the user types inside these inputs, the value of the newParty component variable will be automatically updated.  Conversely, if `partiesList.newParty` is changed outside of the HTML, the input values will be updated accordingly.

## ng-model and ng-if for real-time preview 

Now that we have bound the inputs to these variables, we can show the user what their new entry will look like *as they type it*.  This is an awesome feature of ng-model that meteor allow so easily.  By using an `ng-if`, the code will only appear if the user has infact typed anything.

````html
<ul ng-if="partiesList.newParty.name || partiesList.newParty.description">
	<h2><i>Incoming party!</i></h2>
	<b>-- Live preview --</b>
	<li>
		{{partiesList.newParty.name}}
		<p>{{partiesList.newParty.description}}</p>
	</li>
</ul>
````
This will still not save automatically however, which is good because we don't want to save partially entered parties.  But the immediate feedback available through `ng-model` paired with `ng-if` is a cool feature of Angular1.x.x.  To save it to our `partiesList`, we need to add a click event. 

## ng-click

Now let's bind a click event to the add button with Angular 1's [ng-click](https://docs.angularjs.org/api/ng/directive/ngClick) directive.

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.3"}}

`ng-click` binds the click event to an expression - we just call a method that we will implement soon on the `partiesList`!

Now let's implement the logic on the controller of the Component:

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.4"}}

> Parties is a Mongo.Collection object, and the [insert method](http://docs.meteor.com/#/full/insert) inserts a new object to the collection and assign an id for the new object.

> Meteor support Javascript ES2015 as default so we can take advantage of that and define our `addParty` function as an [Arrow Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Open a different browser, click the button and see how the party is added on both clients. So simple!

Now, let's add the ability to delete parties.

Let's add an X button to each party:

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.5"}}

This time we are binding `ng-click` to a controller function that gets the current party as a parameter.

Let's go into the controller and add that function.

Add the function inside the `partiesList` component in `app.js`:

{{> DiffBox tutorialName="meteor-angular1-socially" step="4.6"}}


Now try to delete a few parties and also watch them being removed from other browser clients.

# Summary

So now you've seen how easy it is to manipulate the data using Angular 1's powerful directives and sync that data with Meteor's powerful Mongo.Collection API.

{{/template}}
