---
layout: post
title: "Interesting note on the react render"
date: "2015-12-04 17:41:30"
categories: react
---


New to react
Interesting issue:

Error: Invariant Violation: findAllInRenderedTree(...): instance must be a composite component

Import our component

`MyComponent import from 'my/component';`

The variable name starts with an uppercase character.

If however we started the variable with a lowercase character and implement like this:

`myComponent import from my/component;`

`let myComponent = TestUtils.renderIntoDocument(<myComponent />)`

React picks this up as a "normal" html node NOT a React component - so `myComponent` looks like this:

`<mycomponent data-reactid=".0"></mycomponent>`

Instead of a DOMNode object full of all sorts of wonderful things:

`{getDOMNode: function () { ... }, props: Object{}, context: Object{}, refs: Object{}.........`

I want to explore why this happens, discuss the inner-workings of why React does this, why it seemingly needs an uppercase starting character.

It's an intersting problem and an excuse to dig a little deeper into React core.










