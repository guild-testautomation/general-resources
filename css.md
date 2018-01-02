CSS is a language that is used to describe the style of an HTML document. In order to do so elements in an HTML document need to be classified with selectors in such a way that CSS can target it. It is those classifications that are used in testautomation to find elements and target them. 

In the first part of this guide we are going over some of the basics of CSS to help you understand what it does and in what context you might be able to find it on a webpage. In the second part of this guide we'll describe how to use tools in your browser to find these selectors.


# CSS basics
In its core css is build up of two parts 

1. Selectors 
2. Properties inside those selector 

Whenever you see css the selector is the part before the curly bracket and its most simple form you can directly address html elements. To give you an example, to change something that affects all urls it would look like this 

```css
a {
        property: propertyvalue;
}
```

This is called a type selector, these simply select the different html elements, the  example shown selects all `a` elements which are urls. Used alone these selectors are rarely used in testautomation as they are rarely unique. There are often used in combination with other selectors to make a selection more specific. 
Other elements you will often encounter are: 

- `div`
- `span`
- `input`

[See this page for a complete reference of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

This of course isn't that very useful if you want to change more specific elements. To target specific elements there are a whole host of options available but at its most basic you are looking at two kinds: 

1. IDs 
2. Classes

Then there is allso a third and fourth kind that are a bit more complicated: 

- Attribute selectors
- Pseudo classes

In the rest of this guide we will just focus on the selectors as we are going to use them for testautomation and not css styling. 

## IDs & Classes

IDs are *supposed* to be unique to one element (this is **not** always the case so do not assume they are) and in css always start with #, in html you can also spot them rather easily 

```html
<a id="thisThing">I am an url!</a>
```
So in css you can do something like this 

```css
#thisThing
```

And target that specific element with that ID. Sometimes someone messes up and you end up with two elements with the same ID, but if one is an url and the other is something else (a div for example) you can be more specific with 

```css
a#thisThing
```


Classes are not unique to single elements but can be seen as a category of elements. They too are easy to spot in html

```html
<a class="theseThings">I am an url!</a>
```

And you target them with a dot like this 

```css
.theseThings
```

or once again if you need the specific kind of element 

```css
a.theseThings
```


## Attribute selectors

Sometimes IDs and Classes are not enough to specifically select an element. Which brings us to our third selector. 
Take the following HTML element

```html
<a href="http://www.google.com" target="_blank" title="this goes to google" >I am an url!</a>
```

As you can see it does not have any classes or IDs that will allow you to target it. It does however have a lot of other information available. Whenever you see something like this in an html element `classifier="value"` it is called an attribute. The shown element has three different attributes

- href
- target
- title

Css allows you to select an element based on the selector. Say that you want to select all elements with the value `this goes to google` in their title attribute. We can do that like this

```css
[title="this goes to google"]
```

Or if you want all `a` elements that go to anything with `google` in the url you can use 

```css
[href*="google"]
```

We can also select for just the attribute, so if we want any element with a `title` attribute we can use
```css
[title]
```

[See this page for all the options you can use](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

## Combining selectors 

You might already have spotted it, but you can combine different selectors to make them more specific and likely to target unique elements. For example given the following html 

```html
<a href="http://www.google.com" target="_blank" title="this goes to google" id="google-url" class="outside-link" >I am an url!</a>
```

Combining all selectors we have used so far we could do something like 

```css
a#google-url.outside-link[href*="google"]
```

## Pseudo classes
Technically not really selectors but still very useful. Pseudo classes are added *after* a selector and indicate a state of the selector. For example when hovering over an element on an HTML page you can target this with css with 

```css
a:hover
```

For testautomation purposes there are a few pseudo classess that can help you in better targeting your element. So for example with `:not()` you can exclude some elements from a match. So say that you have the following html. 

```html
<div class="element">text</div>
<span class="element">text</span>
``` 

And you want only to the div element.
You can target this with the methods we used before or you can do 

```css
.element:not(span)
```

There are also pseudo classes to determine if something is visible, checked (for checkboxes), the Xth child element and a whole lot more. 

[See this page for more information](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

## Combinators (parent, child & sibling relations)

In many cases you can select the element you want by using the selectors for that specific element, often that isn't enough though. Consider the following html 

```html
<div id="parent1">
    <span class="child">
        This is the element we want.
    </span>
</div>
<div id="parent2">
    <span class="child">
        This is the element we do not want.
    </span>
</div>
```

With the selectors we previously covered it isn't possible to select just the first `span` element with the `.child` class. 
We can however use the parent as reference and use the following selector 

```css
#parent1 span.child
``` 

This effectively tells us that we want `span.child` only when it is the child element of `#parent1`. This is called a combinator and there are a variety of them that allow you to reference elements in a specific context. Before we continue a little bit about the terms used in here. 

**parent**
An element containing other elements. 

```html
<div class="parent">
    <span>hello world</span>
</div>
```

**child**
An element that is part of a parent element.

```html
<div class="parent">
    <span class="child">hello world</span>
</div>
```

**siblings**
Elements on the same level in HTML 
```html
<div class="parent">
    <span class="child1" id="sibling-of-child2">hello world</span>
    <span class="child2" id="sibling-of-child1">hello world</span>
</div>
```

The main methods to make use of this are listed below.

- `parentElement childElement` - descendant selector -  Any `childElement` that is the decended of `parentElement`
- `parentElement > childElement` - child selector- Any `childElement` that is the a direct child of `parentElement`. Meaning that it will only look one level down.
- `elementA + elementB` - adjacent sibling selector- selects `elementB` only if it immediately follows `elementA` in the same level. 
- `elementA ~ elementB` - general sibling selector- selects `elementB` if it is one of the next siblings following `elementA`.

## additional reading

[More about css selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

# Using your browser tools.
