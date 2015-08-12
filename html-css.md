# HTML & CSS notes

A few notes prepared while writing training courses...


## The World-wide web

The internet (as a collection of networked computers) existed for decades before the creation of the world-wide web

The methods of communication between these computers wasn't as simple (for the average person) as it is today

In 1990, Tim Berners-Lee, a British engineer working at CERN (European Organisation for Nuclear Research, in Switzerland) combined several key communication protocols known collectively as the 'World-Wide Web'

> "A web of hypertext documents to be viewed by browsers using a client–server architecture"


### Components of the World-Wide Web

The key components of the 'World-Wide Web'

 - HTML - a markup language used to give structure to information
 - URLs - used to uniquely identify documents
 - Hyperlinks (hypertext) - to move between documents
 - Web browsers - a simple Graphical User Interface (GUI) to view these documents
 - Web servers - a way to provide requested documents

These technologies have revolutionised our consumption of information


### The World-Wide Web Consortium (W3C)

An organisation set up by Tim Berners-Lee in 1994

They are responsible for developing "non-proprietary, interoperable technologies" for the World Wide Web

They attempt to make the web universally accessible, regardless of ability, language, or culture

They do this by creating standards for web technologies, such as HTML, CSS and XML


### Web browsers

Many different options

These days, they're all fairly similar, and compete on adding new features

Most browsers update themselves, quite often

It wasn't always this way - *Internet Explorer 6...*


### Browser technologies

3 main languages:

 - Content - HTML
 - Styling - CSS
 - Interaction - JavaScript


### Why you should learn to write code by hand

 - Gain complete control over your site
 - Stop your site being a 'black box' that just works
 - With a bit of practice, it's the quickest way to make things
 - It's easier to debug if something isn't working
 - Easy to make quick fixes from anywhere


## HTML

Describes the structure of content - used to give structure to information

It is a universal language - provided you have a web browser that is capable of reading HTML, you can use any operating system or device to view it


### Giving structure with code

We "mark up" a document to give it structure, by describing the meaning of its parts

HTML is a type of "markup" language


### How would we mark up a book?

Take the following example of a book:

> "The Pineapple: King of Fruits" by Francesca Beauman. Published by Chatto & Windus in 2005.

Or

> In 2005, Francesca Beauman wrote "The Pineapple: King of Fruits" and published with Chatto & Windus.

Humans can understand this informtion, but to a computer it needs putting into a formal structure:

 - *Title*: The Pineapple: King of Fruits
 - *Author*: Francesca Beauman
 - *Date*: 2005
 - *Publisher*: Chatto & Windus
 - *Description*: This enchanting, juicy history…


In a mock markup language, this becomes:

```
<book>
    <title>Pineapple: King of the fruits</title>
    <author>Francesca Beauman</author>
    <date>2005</date>
    <publisher>Chatto & Windus</publisher>
    <description>This enchanting, juicy history…</description>
</book>
```

### Hyper-Text Markup Language (HTML)

HTML is a collection of simple `<tags>`

You only need to know a few to get started:

 - `<h1>`Headings`</h1>` (there are 6 heading levels, from `<h1>` to `<h6>`)
 - `<p>`Paragraphs`</p>`
 - `<em>`Emphasis`</em>`
 - `<strong>`Strong importance`</strong>`
 - Images: `<img src="cat.jpg" alt="My cat">`
 - `<a href="http://google.com">Links</a>`


### HTML rules

There are a few simple rules:


#### Opening & closing tags

Tags wrap around the content they describe:

```
<tag>content</tag>
```

***WRONG***

```
<p>In Xanadu did Kubla Khan
<p>A stately pleasure-dome decree
```

***WRONG***

```
<p>In Xanadu did Kubla Khan</div>
```

***RIGHT***

```
<p>In Xanadu did Kubla Khan</p>
```

Some tags are 'self-closing', because they don't wrap around content:

```
<img src="filename.jpg" alt="Image description">
```


#### Nesting tags

Tags should be properly nested

***WRONG***

```
<p>In <strong>Xanadu did Kubla Khan</p>
```

***WRONG***

```
<p>In <strong>Xanadu</p> did Kubla Khan</strong>
```

***RIGHT***

```
<p>In <strong>Xanadu</strong> did Kubla Khan</p>
```


#### Case

Tags should match case (just use lower-case)

Note that this isn't a strict rule like the previous two, but should still be adhered to

***WRONG***

```
<STRONG>In Xanadu did Kubla Khan</strong>
```

***WRONG***

```
<STRONG>In Xanadu did Kubla Khan</STRONG>
```

***RIGHT***

```
<strong>In Xanadu did Kubla Khan</strong>
```


### Attributes

Extra information for a tag can be given with attributes in the opening tag

```
<a href="http://google.com">Go to Google</a>
<a href="http://bing.com" title="A search engine">Bing is here</a>
<img src="cat.jpg" alt="My cat">
```


### Classes and IDs

Sometimes you'll want to add styling or interactivity to only certain parts of a page

For example, you might want to make a paragraph look bigger

We can target specific HTML elements through their `id` or `class` attributes

```
<p id="intro">Lorem ipsum dolor sit amet</p>
<p class="example">Lorem ipsum dolor sit amet</p>
```

#### IDs

When do you add an ID?

A type of element that occurs only once on the page

e.g. a page header, footer, navigation and main content area

```
<nav id="site-navigation">
    …
</nav>
```

#### Classes

When do you add a class?

On elements that may be repeated throughout a page

```
<article class="news">
    …
</article>
```


#### Using classes and IDs

When naming classes and IDs, don't use spaces - hyphens and underscores are fine

Any element can have more than one class (separated by spaces)

An element can only have one ID

Each ID should only be used once on each page


### Marking up with HTML

HTML has a limited number of tags, as it was originally designed for long, linear technical documents

It is now used for many things - there aren't enough tags for every possible scenario

How do you decide which HTML tag to use?

Tags are semantic - they have different meanings

There is no right or wrong answer

View the source code for websites you visit


### Example

An example HTML page:

```
<html>
    <head>
        <title>My web page about biscuits</title>
    </head>
    <body>
        <h1>Best Biscuits</h1>
        <p id="intro">This is a list of the best biscuits</p>
        <ul class="biscuits">
            <li>Chocolate Hobnob</li>
            <li class="ginger">Ginger Nut</li>
        </ul>
    </body>
</html>
```

#### `<head>`

Contains metadata about the page

Where you add the page title, description, and any other relevant information

Not rendered into the page itself


#### `<body>`

Contains the page content

Anything you put here will be rendered by the browser


### Validation

#### What is it?

Checking the validity of the code (have you followed the rules?)

Make sure sites adhere to the W3C standards


#### Why bother?

It will eliminate 90% of simple rendering bugs immediately

Accessibility - With compliant code, any browsing device can render it

 - [http://validator.w3.org/](http://validator.w3.org/)


***Further information:***

 - [http://www.htmldog.com/](http://www.htmldog.com/)
 - [https://www.codecademy.com/tracks/web](https://www.codecademy.com/tracks/web)
 - [http://learn.shayhowe.com/html-css/](http://learn.shayhowe.com/html-css/)


## CSS

CSS makes pages pretty

 - HTML lets us add content - text, images and video
 - CSS adds style - layout, colours, fonts

All aspects of design and layout are covered by CSS

 - Layout
 - Colour
 - Typography
 - Background images
 - Borders
 - Shadows
 - Animation


### Adding CSS

Assuming we want to style the following HTML page:

```
<html>
    <head>
        <title>My web page about biscuits</title>
    </head>
    <body>
        <h1>Best Biscuits</h1>
        <p id="intro">This is a list of the best biscuits</p>
        <ul class="biscuits">
            <li>Chocolate Hobnob</li>
            <li class="ginger">Ginger Nut</li>
        </ul>
    </body>
</html>
```

#### Styling by tag name

```
h1 {
    color: red;
}
```


#### Styling by ID

```
#intro {
    font-weight: bold;
}
```


#### Styling by Class

```
.ginger {
    color: orange;
}
```


#### Styling multiple elements

```
li {
    font-size: 200%;
}
```


#### Styling things inside of other things

```
.biscuits li {
    background: green;
}
```


#### Grouping styles

Instead of separate styles for everything:

```
p {
    color: red;
}
h1 {
    color: red;
}
```

You can combine styles:

```
p, h1 {
    color: red;
}
```

(This will apply to all `<p>` and `<h1>` elements)


### Applying CSS

#### CSS inline (in an HTML Page)

```
<html>
    <head>
        <title>My Page</title>
        <style>
            h1 {
                background-color: purple;
                color: white;
            }
        </style>
    </head>
    <body>
        <h1>Hello World</h1>
    </body>
</html>
```


#### CSS in a separate file

index.html

```
<html>
    <head>
        <title>My Page</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>Hello World</h1>
    </body>
</html>
```

style.css

```
h1 {
    background-color: purple;
}
```

***Further information:***

 - [http://www.htmldog.com/](http://www.htmldog.com/)
 - [https://www.codecademy.com/tracks/web](https://www.codecademy.com/tracks/web)
 - [http://learn.shayhowe.com/html-css/](http://learn.shayhowe.com/html-css/)


## Page layout with CSS

### Block and Inline Elements

It's important to know the difference between the two


### Block Elements:

`<h1>`-`<h6>`, `<p>`, `<ul>`, `<ol>`, `<li>`, `<div>`, `<table>`, `<form>`, etc

 - sit on their own line
 - fill 100% of page width


### Inline elements

`<a>`, `<em>`, `<strong>`, `<span>`, etc

 - Will sit next to one another on the same line
 - Don't always automatically receive all CSS styles (padding/margin/width/height etc) - this can be confusing!
 - Putting block-level elements within an inline element (such as a link) can lead to unexpected results

Easy to alter with CSS - `display: block` or `display: inline`

See:

 - [http://www.quirksmode.org/css/display.html](http://www.quirksmode.org/css/display.html)
 - [http://learnlayout.com/inline-block.html](http://learnlayout.com/inline-block.html)


### Layout

The main CSS properties we use for layout are `display`, `float` and `position`

A great tutorial:

 - [http://learnlayout.com/](http://learnlayout.com/)


### Positioning

By default, all HTML elements have a CSS position attribute of `static`

```
<div id="main">...</div>
<div id="sidebar">...</div>
<div id="footer">...</div>
```

```
#main,
#sidebar,
#footer {
  position: static; /* this is the default value */
}
```

These block HTML elements will be on their own line

Changing the CSS position attribute allows you to set top/bottom/left/right values - relative to the `<body>`, or a parent container that has `position: relative` applied:

```
#main {
  position: absolute;
  left: 10px;
  width: 75%;
  background: #eee;
}

#sidebar {
  position: absolute;
  right: 10px;
  width: 20%;
  background: #ffd;
}
```

A page laid out using `position: absolute` has its limits

 - 'fixed' heights of content
 - layout doesn't adapt to the content

`position` is useful, but not for main page layout


### Floats

HTML elements can have a float set with CSS - `float: left;` or `float: right;`

```
#main {
  background: #eee;
  float: left;
  width: 80%;
}

#sidebar {
  background: #ffd;
  float: right;
  width: 15%;
}
```

A floated element is shifted to the left or right of its container element as far as possible

If we float another element in the same direction, it will be shifted until its edge reaches the edge of the first floating element

Unfloated content flows and wraps around floated elements

Floats are better that positioning for layout - unlike absolutely positioned elements, floated elements remain in the document flow, so can expand with content

You should (almost) always set widths on floated elements, although elements with inherent widths (e.g. images) don't need a width set


#### Controlling floats

If we want to control how many floated elements appear on a line, we can wrap a div element around the floated content, and set a width:

```
<div id="block-container">
  <div class="block">block 1</div>
  ...
  <div class="block">block 10</div>
</div>
```

```
#block-container {
  width: 500px;
}
.block {
  float: left;
  width: 100px;
  margin-right: 20px;
}
```

#### Two main uses for floats:

 - page layout
 - layout of elements within a block


#### float: centre?

You can't float an element to the centre - there are other techniques for that

```
body {
  width: 600px;
  margin: 0 auto;
}
```


## Responsive websites

We can no longer assume that most people primarily use a desktop or laptop computer to browse the internet

People use a variety of internet browsers and operating systems

Nowadays most people have at least one other device that they use to browse the internet

These devices are increasingly being used in place of 'traditional' browsers

We should ensure that our websites work across all commonly used desktop browsers

We should take non-desktop browsers/devices into consideration when building a website

These devices have different display resolutions (or browser dimensions)

These devices also have different methods of interaction


### Media queries

You can specify CSS for different browser resolutions (or dimensions) using CSS `@media` queries.

For a typical website you might create three sets of styles:

 - one set of generic page styles, used on every device/browser
 - another set of styles just for low-resolution (mobile) browsers
 - a third set just for higher-resolution (desktop/tablet) browsers

The point at which the design 'snaps' from one layout to the next is commonly known as the 'break point'

These media queries can appear inline in the CSS:

```
@media (max-width: 480px) {
  #main-content,
  #aside {
    width: 100%;
    float: none;
  }
}
```

Styles put within the `@media` query will only be used if the specified conditions are true.

Using `@media` queries to create different layouts for different resolutions (or browser dimensions) is generally known as responsive web design

Content layout should adapt to fit different browser sizes


### Meta viewport

You can control how a page renders in a (modern) mobile browser using a `<meta>` viewport declaration:

```
<meta name="viewport" content="width=device-width, initial-scale=1" />
```


### Mobile first

It is possible to make an existing site more responsive by adding additional styles (within an `@media` query) for mobile devices

Bandwidth issues for desktop browsers are less relevant nowadays with broadband, but is still a concern for mobile browsers

Using `@media` queries means a mobile must download an entire desktop site, and then extra styles

It may make more sense to first create a basic design for mobile, and then add extra layout styles for desktop browsers

This approach has become known as mobile-first

This approach is device-inclusive

The default set of styles sent to every browser/device should be for the most basic page layout

In this capacity, a lack of `@media` query support should be seen as your first `@media` query

i.e. old browsers or devices don't support `@media` queries, so these devices receive the default mobile version


***Further information:***

 - [http://blog.cloudfour.com/responsive-design-for-apps-part-1/](http://blog.cloudfour.com/responsive-design-for-apps-part-1/)
 - [http://www.webdesignerdepot.com/2011/09/the-ultimate-responsive-web-design-roundup/](http://www.webdesignerdepot.com/2011/09/the-ultimate-responsive-web-design-roundup/)
 - [http://www.designbyfront.com/demo/goldilocks-approach/](http://www.designbyfront.com/demo/goldilocks-approach/)
 - [http://coding.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/](http://coding.smashingmagazine.com/2010/07/19/how-to-use-css3-media-queries-to-create-a-mobile-version-of-your-website/)
 - [http://marcdrummond.com/web-standards/2011/06/20/hell-bad-devices-responsive-web-design-and-web-standards](http://marcdrummond.com/web-standards/2011/06/20/hell-bad-devices-responsive-web-design-and-web-standards)
 - [http://stefangirard.com/2012/01/responsive-design-is-bad/](http://stefangirard.com/2012/01/responsive-design-is-bad/)
 - [http://www.webdesignshock.com/responsive-design-problems/](http://www.webdesignshock.com/responsive-design-problems/)



## Web Standards

### What are web standards?

An 'agreed' specification for HTML, CSS and JavaScript

 - How we should write code
 - How web browsers should read and render code

Web standards allow web developers to focus on their code

If the code is valid, the page should render in a web browser as expected

A good example comes from the history of the `<img>` element:

 - [A long digression into how standards are made](http://diveintohtml5.info/past.html#history-of-the-img-element)


#### A short summary of web standards

 - Use valid, semantic HTML for content
 - Use CSS for layout
 - Use JavaScript for behaviour


### Web standards and accessibility

Web standards define rules for accessibility

> "The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect."
>
> — [W3C Web Content Accessibility Guidelines](http://www.w3.org/TR/WCAG20/)


### Why are web standards important?

Tim Berners-Lee created HTML as a language to help represent information in a consistent manner

If everyone can agree on a shared vocabulary, then a web browser should be able to interpret what I have created and display it to you in a predictable way

This was overseen by the W3C, who defined standards that should be followed by all

This was a good plan in theory - until the web became more popular than anyone could have imagined

In the early days of the web, competing web browsers were created, and in an attempt to win market share, numerous new features were introduced that weren't available in rival browsers. New elements, new ways to lay out and interact with web pages

On the one hand, this led to a great deal of innovation. Which, in theory, is a good thing. But in practice... it led to fragmentation in how browsers rendered HTML

This fragmentation caused a great deal of problems for developers, and web users alike

To create a website that worked everywhere often meant creating the same thing twice, in two different ways. Or, more commonly, building a website and optimising it just for a single browser

Browser manufacturers wanted to implement new functionality, web developers wanted to be able to do that weren't possible in a browser, because of a lack of agreement for how to implement them

Groups of developers formed collectives such as the Web Standards Project (WaSP) to convince rival browser manufacturers to embrace the common standards set out by the W3C, for the benefit of all

It took a number of years for their message to be heard, but eventually the major browser manufacturers realised the approach would benefit them too


### Web standards today

Web standards are still relevant today - we have a range of desktop and mobile browsers

To ensure these browsers operate in a consistent manner they must continue to follow a mutually agreed set of design principles and rules

To get anything built efficiently, developers need consensus. We need to know that what we build will work

The difference today is, with web standards, we have some reassurance that this is indeed the case

The browser manufacturers themselves are now actively involved in the process of defining the new standards for HTML, CSS and JavaScript

They (mostly) follow agreed standards and conventions when creating these innovations, meaning innovative features can be reliably implemented to create an experience that works in any browser
