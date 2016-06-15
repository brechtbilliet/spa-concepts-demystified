# Components demystified

## Table of Contents

  1. [Foreword](#foreword)
  1. [Base concept](#base-concept)
  1. [The hierarchical component-tree](#the-hierarchical-component-tree)
  1. [Smart vs dumb components](#smart-vs-dumb-components)
  1. [Best practices](#best-practices)

## Foreword
These documents are the beginning of a book (or a collection of documents) that will explain SPA-principles in depth. SPA's (single-page-apps) offer us the opportunity to create responsive userfriendly webapplications that have a native look-and-feel. However, with great power comes great responsability! It's not always easy to manage those SPA's when they tend to get big, and most of the time... they will! When applying the principles of 'spa concepts demystified' you should be able to create large-scale applications like it's 'a walk in the park'.

This module will demystify components and explain why certain choices were made.
## Base concept
The concept 'Components' is one of the most commonly used concepts these days in SPA applications. The concept itself exists for a while now, but since React (SPA-framework from Facebook) became popular, most SPA-frameworks are based on this concept.

In essence, a component is a tiny part of a bigger picture, a part of an application for instance. The term 'component' is something that is used quite commonly, but when we talk about components in SPA technologies, a component is something very specific.

**It's the combination of a piece of HTML and a piece of logic, that serve a special purpose together.**
 
A component has a goal, a responsability, and it's very important to think about what kind of responsability that component has. The **separation-of-concerns-principle** is one of the main principles behind this. 
Components are tiny chunks of responsability that will define the presentational layer of our single-page-application.

On a more technical level: **It's a custom DOM tag.**
That custom DOM tag can have some kind of behavior/functionality and a certain look. 
Modern SPA-technologies provide us with a way to create our custom DOM tags.
Just like other native DOM-tags, components can have custom attributes. Those attributes can be used to pass parameters.

**Note: Additionaly components can contain custom stylesheets**


### Example: The native anchor-tag
Let's take a look at the native **anchor-tag** for instance: 

```html
	<a href="http://brecht.io">my link</a>
```

<dl>
  <dt>Functionality</dt>
  <dd>When we click on it, the browser will open the passed url.</dd>

  <dt>Presentation</dt>
  <dd>The content of the anchor tag is highlighted, and will implement native hover functionalities</dd>
</dl>

### Example: A custom rating-tag
```html
<rating value="5"></rating>
``` 

<dl>
  <dt>Functionality</dt>
  <dd>This component will generate 5 stars. Based on the value provided it will select a number of stars. When we click on a star, it will update the value of the passed in parameter</dd>

  <dt>Presentation</dt>
  <dd>When we hover a star it can highlight the star, so the user will know he can click it.</dd>
</dl>

Single page applications will mostly render additional HTML for custom components. The component above might output something like this:

```html
	<rating>
        <i class="fa fa-star rating fa-2x starred"></i>
        <i class="fa fa-star rating fa-2x starred"></i>
        <i class="fa fa-star rating fa-2x starred"></i>
        <i class="fa fa-star rating fa-2x starred"></i>
        <i class="fa fa-star rating fa-2x starred"></i>
	</rating>
```


## The hierarchical component-tree
Most of the modern frameworks these days recommend the use of component-trees. Basically, this means that your entire application is a hierarchical tree of components. 
This means that your pages will become seperate components. This even results in the fact that the application itself will become a component. Yes! **Every presentational chunk of your application becomes a component.** There are no standalone templates nor are there standalone controllers.

A single hierarchical component-tree will give you the following advantages:
<ul>
	<li>It's easy to visualise a component-tree</li>
	<li>Declarative syntax</li>
	<li>Easier debugging in browsers and in code-editors</li>
	<li>It's easier to reason about the application</li>
	<li>Reduces a lot of complexity (when used the right way)</li>
	<li>You don't have to keep track of which controller belongs to which view</li>
	<li>Optimized change detection becomes possible (more on that later)</li>
	<li>Shadow DOM becomes possible</li>
	<li>A strict language to talk about in your team, divide the work properly</li>
</ul> 

## Smart vs dumb components
When structuring components, it's a good idea to separate dumb components from smart components. Dumb components (also called presentational components) are stupid and therefor know nothing about the application. Smart components (also called containers) typically have an interface to the rest of the application. 
When working with a unidirectional dataflow like React or Angular2 this principle can become quite handy to structure your code.

Let's define a set of groundrules shall we?

### Dumb components
<ul>
	<li>They don't know anything about the application</li>
	<li>They will not redirect to other parts of the application</li>
	<li>They will only communicate with their direct parent</li>
	<li>They typically don't have any dependencies injected, but they could</li>
	<li>They can contain other components</li>
	<li>They don't fetch data</li>
	<li>They can contain logic, but only related to the component itself</li>
	<li>They get their state and data passed through attributes</li>
	<li>They do not modify the passed in parameters directly</li>
	<li>They should be reusable</li>
</ul>

A dumb version of the rating component mensioned before would look like this:

```html
<rating value="5" on-set-value="setRating(newRating)"></rating>
``` 

The angular2 code for that could then be:

```html
<rating [value]="5" (setValue)="setRating($event)"></rating>
``` 

Dumb components are very easy to reason about and can mostly be ignored in the thinkproces of your application. Therefore, the main groundrule should be: **Try to use dumb components as much as possible! They make your application less complex and easier to reason about**

### Smart components
<ul>
	<li>They know about the state and data of the application, but should not care how it's managed</li>
	<li>Typically they have an interface that communicates with the rest of the application</li>
	<li>They pass state and data to their child-components</li>
	<li>They also don't modify state theirselves directly</li>
</ul>

## Best practices
### Draw them first, think about the responsabilities first
Since components represent the complete presentationlayer of your application it's important to think about the structure of these components. It's also a good idea to think about what components should dumb and smart before you start writing the application. For that reason I suggest you take a piece of paper or use a whiteboard and start drawing the componenttree for every page. This gives you the ability to start thinking about which state belongs to which component.
### Keep them small
When you keep your components small, you get the following advantages:
<ul>
	<li>Small components are easier to work with. The smaller your code, the easier you get an overview of what the component does</li>
	<li>Easier to maintain</li>
	<li>It makes it easier to work with the "single-responsability-principle" (small components with small responsabilities).</li>
	<li>Because of the "single-responsability-principle" it becomes easier to test</li>
	<li>Easier to debug</li>
	<li>You have more control over the change detection in some frameworks (only rerender what needs to be rerendered)</li>
	<li>Split up into different developer tasks. (developers can work sandboxed on their own set of components)</li>
	<li>Component names in an application create somekind of developer jargon</li>
</ul>
### Don't let components talk directly with the rest of the application
If you have read the rest of this chapter, you should know that this section does not apply to dumb components, since they don't interfere with the rest of the application. They only interfere with there direct parent's and direct children.
Containers (smart components) do know about the application, but that doesn't mean they should have access to everything. 

It's a good idea to **provide some kind of abstraction layer** for your containers. That way the presentation-layer (component-tree) is loosely-coupled from the rest of the application.
If you think about it, the containers should not know how statemanagement is handled, nor should they know how data is being fetched/handled. And in software, the less a component knows, the easier it gets to manage that component.

An option would be to provide some kind of sandbox that only contains the properties of the state that your container needs. The sandbox would also contain the functions your container needs to modify state and or communicate with the backend. You want to keep this abstraction thin, and keep the logic of your container in the container itself. After all, it is its responsability right?
### Strict rules regarding communication
A dumb component should only communicate with its direct parent-component and with its own child-components.
This rule also applies for smart components, however a smart component has somekind of api to communicate with the rest of the application. That's what makes it smart.

The big advantage here is that you don't have to keep track of who notifies who. There is a strict structure here.
### Keep your components dumb where possible
The more dumb components your application has, the easier it gets to maintain that application.
A majority of dumb components has the following advantages:
<ul>
	<li>Less smart components results in less application abstractions (every container needs its own api to the application</li>
	<li>Dumb components are much easier to reason about</li>
	<li>Dumb components makes the application less complex, since dumb components do not modify state/data</li>
	<li>It's easier to give dumb components a clear responsability</li>
	<li>Dumb components are easier to test (less dependencies)</li>
</ul>
### keep your templates inline
Keep the html of the component in the same file of the javascript.
Wait, what?! What about separation of concerns? Actually it is the concern of the component to fulfill its purpose. The component fulfills that purpose by the combination of his html and javascript.
When you put them in the same file there are some advantages:
<ul>
<li>Less context switching when developing the component (don't switch between files)
<li>No absolute paths to templates that are hard to maintain</li>
<li>Less ajax calls to fetch templates, there already there when bootstrapping the application</li>
</ul>
**Note:** This only applies when the component isn't to big, but than again... keep them small remember.
