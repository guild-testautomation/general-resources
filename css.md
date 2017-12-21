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

This of course isn't that very useful if you want to change more specific elements. To target specific elements there are a whole host of options available but at its most basic you are looking at three kinds: 

1. Types
2. IDs 
3. Classes

Then there is also a fourth kind that is a bit more complicated: 

- Attribute selectors

## Types, IDs & Classes

Type selectors simply select the different html elements, the first example shown is a type selector that select all `a` elements which are urls. Used alone these selectors are rarely used in testautomation as they are rarely unique. There are often used in combination with other selectors to make a selection more specific. 
Other elements you will often encounter are: 

- `div`
- `span`
- `input`

[See this page for a complete reference of elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).



IDs are supposed to be unique to one element and in css always start with #, in html you can also spot them rather easily 

```html
<a id="thisThing">I am an url!</a>
```
So in css you can do something like this 

```css
#thisThing {
        property: propertyvalue;
}
```

And target that specific element with that ID. Sometimes someone messes up and you end up with two elements with the same ID, but if one is an url and the other is something else (a div for example) you can be more specific with 

```css
a#thisThing {
        property: propertyvalue;
}
```


Classes are not unique to single elements but can be seen as a category of elements. They too are easy to spot in html

```html
<a class="theseThings">I am an url!</a>
```

And you target them with a dot like this 

```css
.theseThings {
        property: propertyvalue;
}
```

or once again if you need the specific kind of element 

```css
a.theseThings {
        property: propertyvalue;
}
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
[title="this goes to google"] {
        property: propertyvalue;
}
```

Or if you want all `a` elements that go to anything with `google` in the url you can use 

```css
[href*="google"] {
        property: propertyvalue;
}
```

We can also select for just the attribute, so if we want any element with a `title` attribute we can use
```css
[title] {
        property: propertyvalue;
}
```

[See this page for all the options you can use](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

## Combining selectors 

You might already have spotted it, but you can combine different selectors to make them more specific and likely to target unique elements. For example given the following html 

```html
<a href="http://www.google.com" target="_blank" title="this goes to google" id="google-url" class="outside-link" >I am an url!</a>
```

Combining all selectors we have used so far we could do something like 

```css
a#google-url.outside-link[href*="google"] {
        property: propertyvalue;
}
```


## additional reading

[More about css selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

# Using your browser tools.