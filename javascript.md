# JavaScript notes

A few notes prepared while writing training courses...

These notes assume a small amount of prior knowledge of programming in general and JavaScript knowledge in particular. At the very least it assumes an understanding of what JavaScript is, why we use it, and how to execute it in a web browser.


## JavaScript fundamentals

### Variables

An analogy often used to describe a variable is *a container that you can put something in*. 

The name that you give a variable is the label you put on the container, so you know how to find it again later. They can be used to store anything - numbers, text or other types of information:

```
var nearestStar = "Alpha Centauri";
var lightYearsAway = 4.3;
var age = 6000000000;
var isHot = true;
```

When you need to reference that information later, refer to it via the variable name:

```
alert(nearestStar); // "Alpha Centauri"
```

Variables can be set using the values from other variables:

```
var planets = 8;
var dwarfPlanets = 5;

var planetCount = 8 + 5; // 13
```

The value of a variable can be changed (that's why it's called a *variable*):

```
var numberOfPlanets = 9;

numberOfPlanets = numberOfPlanets - 1; // bye bye Pluto
```

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar\_and_types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types)


### Arrays

We can store related lists of information in arrays. This allows us to group them together, and later to easily run code for all items in the array.

Creating an array:

```
var planets = [
    "Mercury",
    "Venus",
    "Earth",
    "Mars",
    "Jupiter",
    "Saturn",
    "Uranus",
    "Neptune"
];
```

And to access the array:

```
var len = planets.length; // 8
var planet = planets[2];  // "Earth"
```

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)


### For loops

`for` loops are an easy way to access information stored in an array:

```
for (var counter = 0, planetCount = planets.length; counter < planetCount; counter++) {
    var planet = planets[counter];
    alert("I like the planet " + planet);
}
```

This code uses a variable to cache the array length once, rather than checking it each time we pass through the loop. This is for a (negligible) speed improvement. It's one of a number of small enhancements developers often recommend to speed up JavaScript performance. Others will be discussed where relevant.

Another way to loop through an array is with `forEach`:

```
function enthuse (planet) {
    alert("I like the planet " + planet);
}

planets.forEach(enthuse);
```

For the purposes of looping through the array, either `for` or `forEach` can be used to satisfy our requirements.

This choice of options for how to structure code demonstrates the programming principle of *there's more than one way to do it*.

However, as is often the case, one option may have advantages or disadvantages. In this situation, be aware that `forEach` this isn't as widely supported as a simple `for` loop, at least in older browsers.

***Further reading:***

 - [http://stackoverflow.com/a/9329476](http://stackoverflow.com/a/9329476)
 - [https://coderwall.com/p/kvzbpa/don-t-use-array-foreach-use-for-instead](https://coderwall.com/p/kvzbpa/don-t-use-array-foreach-use-for-instead)
 - [https://css-tricks.com/snippets/javascript/loop-queryselectorall-matches/](https://css-tricks.com/snippets/javascript/loop-queryselectorall-matches/)


### Objects

Objects are useful to group related values together:

```
var mars = {
    radius: 3396,
    distanceFromSun: 227900000
};

var earth = {
    radius: 6371,
    distanceFromSun: 149600000
};
```

These values can be accessed in different ways:

```
earth["radius"] // 6371
earth.radius // 6371
```

We can put arrays and objects inside one another. This can be a useful way to organise complex information:

```
var planets = [
    {
        name: "mars",
        radius: 3396,
        distanceFromSun: 227900000
    },
    {
        name: "earth",
        radius: 6371,
        distanceFromSun: 149600000
    }
];
```

We can then loop through this information and perform functions to extract useful information:

```
function describePlanet (planet) {
    alert(planet.name + " has a radius of " + planet["radius"] + "km");
}

planets.forEach(describePlanet);
```

JavaScript objects are the basis for JSON (*JavaScript Object Notation*). The important rule to remember is that to be valid JSON, all keys must be quoted with double quotes:

```
[
    {
        "name": "mars",
        "radius": 3396,
        "distanceFromSun": 227900000
    },
    {
        "name": "earth",
        "radius": 6371,
        "distanceFromSun": 149600000
    }
];

```

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working\_with_Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
 - [http://www.sitepoint.com/back-to-basics-javascript-object-syntax/](http://www.sitepoint.com/back-to-basics-javascript-object-syntax/)


### Functions

Functions are a set of instructions that can be specified (or *defined*) now but used (or *called*) later on. The main advantage of using a function is that you only need to create it once, and then you can re-use it as often as you need.

Functions can be defined in two ways. There are subtle but important differences.

**Function declarations:**

```
function enthuse (planet) {
    return "I like the planet" + planet;
}
```

**Function expressions:**

```
var enthuse = function (planet) {
    return "I like the planet" + planet;
}
```

Either than can be used, with the same code:

```
var sentence = enthuse("Mercury"); // "I like the planet Mercury"
```

The main difference is that declared functions are *hoisted*, meaning they are moved by the JavaScript interpreter to the top of the block. Therefore they can be referenced before they are declared.

***Further reading:***

 - [http://stackoverflow.com/a/336868](http://stackoverflow.com/a/336868)
 - [http://www.unicodegirl.com/function-statement-versus-function-expression.html](http://www.unicodegirl.com/function-statement-versus-function-expression.html)


### if / else conditionals

if/else conditionals allow us to execute certain functionality only when specific conditions have been met.

Their use requires a condition that will be either true or false, upon which we can base our decision:

```
if (planet === "Earth") {
    asYouWere();
} else if (planetHasOxygen()) {
    breatheDeeply();
    thinkAboutHome();
} else {
    holdYourBreath();
    lookForRocketShip();
}
```

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)


## Developer tools

Most browsers have useful developer tools built in. Here are some notes on the main tools that are useful for JavaScript development. They are specific to panels in the current version of the Chrome developer tools, although equivalents are generally available in other major browsers.


### Console panel

The console panel is the primary place to log messages, spot errors, test code and interact with the current page.


#### Logging messages

It can be useful to use `console.log();` to view the current value of a variable during development. One or more variables can be passed as *parameters* to this function.

```
console.log(planets, stuff, somethingElse);
```

You can apply string formatting and custom styles to different messages, allowing for a differentiation in display of messages logged for different purposes.

```
var message = "%c Planet %s has a radius of %d km";
var styles = "color: orange; background: blue; font-size: 16pt";
var planet = "Earth";
var radius = 6371;

console.log(message, styles, planet, radius);
```

Other useful `console` options are available, such as `console.group()` for collating related messages into a collapsable group, and `console.table()` for displaying repetitive data in a table.

***Further reading***

 - [https://developer.chrome.com/devtools/docs/console-api](https://developer.chrome.com/devtools/docs/console-api)
 - [https://developer.chrome.com/devtools/docs/tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks)


#### Spotting errors

If you make a mistake in your JavaScript code it will be referenced in the console.

This should give a filename, line number and (hopefully) an indication of the nature of the error.

If you click on the error it will take you through to the *sources* panel to help debug it.

***Further reading***

 - [https://developer.chrome.com/devtools/docs/console#errors-and-warnings](https://developer.chrome.com/devtools/docs/console#errors-and-warnings)


#### Testing code

Before writing code it can be helpful to experiment in the console. This can help to see a live preview of your changes, interacting with the current page every time you execute a command. When it's ready, this code can then be copied into an external file.

Every time you refresh the page, this code will be reset. It will still be available in the console's history (just like a terminal window) so pressing up/down on the keyboard will cycle through previous commands.


### Elements panel

The inspector is primarily used for displaying the current HTML and CSS, but it can be useful for JavaScript debugging too.

For example, it can display which elements in the page have *event listeners* attached. These will be discussed later.

Also, on any HTML element you can right-click and select a *'break on...'* option that will allow you to pause and debug JavaScript at the point where the HTML element is manipulated via JavaScript.


### Network panel

The network panel lists all HTTP requests, which can be useful when debugging AJAX requests - for example it allows you to see the parameters that have been sent to the server, and the data returned (or not) from the server.

***Further reading***

 - [https://developer.chrome.com/devtools/docs/network](https://developer.chrome.com/devtools/docs/network)


### Sources panel

The sources panel is where the JavaScript of the current page can be analysed. These debugging tools are powerful and complex.


#### Sources

The *sources tab* lists all text-based sources in the page, for example the HTML, CSS and JavaScript files that make up the current page. Clicking on any of these files will display it in the main panel. Right-clicking on any file will bring up a number of further options.

When viewing a minified file, the 'pretty print' option in the main panel is handy to unminify the code.

If you set up a *workspace*, you can edit files directly in the editor and save your changes to your local files.

***Further reading:***

 - [https://developer.chrome.com/devtools/docs/workspaces](https://developer.chrome.com/devtools/docs/workspaces)


#### Content scripts

The *content scripts* tab lists all scripts that are loaded into the current browser tab from extensions (and other sources) rather than directly from the website itself. For example this is where the scripts injected into the current page by your browser extensions will be displayed.


#### Snippets

The *snippets* tab allows you to create and save your own custom scripts that you can then run manually on a page.

These are handy if you constantly need to run the same piece of code on a page, but don't want to include the code in 'production' Javascript.

Right-click in the panel to create a new snippet. Enter and save your code. Right-click again to run.

An example piece of code to test snippets with:

```
var headings = document.querySelectorAll("h1");
for (var i = 0; i < headings.length; ++i) {
    headings[i].style.color = "#f90";
}
```


#### Debugging

Debugging JavaScript is a complex subject, explained thoroughly elsewhere on the web. The following guides are fairly comprehensive.

The best way to debug issues is to isolate the error and identify how it can be replicated consistently. This will make it easier to eliminate.

***Further reading***

 - [https://developer.chrome.com/devtools/docs/authoring-development-workflow](https://developer.chrome.com/devtools/docs/authoring-development-workflow)
 - [https://remysharp.com/2012/12/21/my-workflow-never-having-to-leave-devtools](https://remysharp.com/2012/12/21/my-workflow-never-having-to-leave-devtools)
 - [https://developer.chrome.com/devtools/docs/javascript-debugging](https://developer.chrome.com/devtools/docs/javascript-debugging)
 - [https://gist.github.com/jedrichards/9942165](https://gist.github.com/jedrichards/9942165)


#### Remote debugging

When working with an iOS device you can remotely debug Mobile Safari by plugging the device in to the USB port of a mac and opening the Safari Developer tools.

When working with an Android device you can remotely debug Mobile Chrome by plugging the device in to the USB port of a computer and following [these instructions](https://developer.chrome.com/devtools/docs/remote-debugging).

Third-party tools like [jsconsole.com](http://jsconsole.com/remote-debugging.html) can also help with remote debugging.


### Other panels

 - The *Timeline* panel is useful for tracking rendering performance: [https://developer.chrome.com/devtools/docs/timeline](https://developer.chrome.com/devtools/docs/timeline)
 - The *Profiles* panel is useful for tracking CPU and memory usage: [https://developer.chrome.com/devtools/docs/profiles](https://developer.chrome.com/devtools/docs/profiles)
 - The *Resources* panel is useful for tracking information stored in cookies and local storage: [https://developer.chrome.com/devtools/docs/resources](https://developer.chrome.com/devtools/docs/resources)
 - The *Audits* panel is useful for testing the performance of a page, and analysing ways to improve it: [https://developer.chrome.com/devtools#audits](https://developer.chrome.com/devtools#audits)


## The DOM

In a web browser, JavaScript has two special *global* variables - `window` and `document` - that allow us to interact with the browser and the web page respectively.

The `window` variable is often used to detect when a page is loaded, when the window is scrolled, and to access its dimensions.

The most common use of `document` is to access HTML elements in a web page by referencing the _Document Object Model_ (DOM), which is the JavaScript representation of the HTML page structure:

**HTML**

```
<html>
    <body>
        <h1>Stuff in space</h1>
        <ul class="planets js-planets">
        </ul>
    </body>
</html>
```

**JS**

Two examples of interacting with this page via JavaScript, using the DOM:

```
var heading = document.querySelector("h1");
heading.textContent = "The Planets";
heading.style.color = "#f90";
heading.setAttribute("class", "heading-main");
```

And another:

```
var planetList = document.querySelector(".js-planets");
var planet = document.createElement("li");
planet.id = "planet-earth";
planet.classList.add("planet");
planet.textContent = "Earth";
planetList.appendChild(planet);
```

We can usually do all the DOM manipulation we need with these native JavaScript commands, without having to resort to using an external library. We don't *require* jQuery just to access and manipulate the DOM. But it does make these interactions (and many others) far easier.

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object_Model/Introduction](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)


## jQuery

Shortly after its creation, jQuery quickly became a popular tool for helping to manage the many inconsistencies in how different browsers had (incorrectly) implemented JavaScript.

This is no longer such a concern, as modern browsers generally implement the same set of standards. But jQuery is still useful, and not just for DOM interactions. It also simplifies *Ajax* calls, handling *events* and object/array manipulation amongst others.

A big advantage is that *most* front-end developers have some familiarity with jQuery, which helps teams work on a shared codebase.

The presence of jQuery in any website of reasonable size and complexity is almost ubiquitous. As such, it's useful to learn not just how to use it, but also its quirks and deficiencies.

This guide assumes a basic knowledge of jQuery - how add it to a web page and use it to select and manipulate DOM elements.


### jQuery tips

#### Don't put everything in *document ready*

The most common use of jQuery is to initialise code to start when the DOM of the page has loaded, using:

```
$(document).ready(function () { ... });
```

*This is sometimes shortened to:*

```
$(function () { ... });
```

This often leads to an entire application's code being stored in a single *global.js* file, all referenced within the *ready* function:

```
$(document).ready(function () {
    ...
    (an entire application's code goes here)
    ...
});
```

This isn't a good idea, for several reasons.

If all the website's JS code is stored in a single place it can quickly become difficult to manage.

Unless you are careful, you might run into trouble with scope, where no two variables can share the same name. This will be discussed in more detail later.

Another issue is that it may slow down the initial rendering of the website, as this code will not be parsed until the page is ready to be rendered. There may be parts of the code that could be executed immediately rather than having to wait for the DOM to finish loading.

A solution to this issue is to keep code modular, and only *initialise* the code within the DOM *ready* function.

```
// set up all tab functionality
function tabs () {
    ...
}

// set up all slideshow functionality
function slideshows () {
    ...
}

// start all functionality
function init () {
    tabs.init();
    slideshows.init();
}

// run on DOM load
$(document).ready(init);
```

Note that this is a simplification of a solution to demonstrate the issue. More detailed solutions will be demonstrated later.

***Further reading:***

 - [https://learn.jquery.com/code-organization/concepts/](https://learn.jquery.com/code-organization/concepts/)
 - [http://www.elijahmanor.com/dont-initialize-all-the-things-in-jquery-ready/](http://www.elijahmanor.com/dont-initialize-all-the-things-in-jquery-ready/)


#### Consider prefixing jQuery objects with *$*

A widely used convention that can help to differentiate a variable that references a jQuery object from other types of variable. It is common to prefix these variable names with a `$`:

```
var $planetsEl = $("#planets .planet");
var planetCount = $planetsEl.length;
```

This helps to show which variables also have access to use jQuery's many functions.

Some developers like this approach, others don't. But it's worth considering and deciding on a convention one way or the other.

***Further reading:***

 - [http://www.bennadel.com/blog/1778-using-variable-in-jquery-code-is-just-hungarian-notation.htm](http://www.bennadel.com/blog/1778-using-variable-in-jquery-code-is-just-hungarian-notation.htm)


#### Cache DOM elements

jQuery makes it very easy to quickly interact with the DOM. However, DOM interaction is slow. As such, for speed purposes it is best to interact with the DOM as little as possible.

When querying the DOM to look for an element, cache the result for future use.

```
var $el = $(".list-item");

$el.addClass("active");

$el.on("click", function (e) {
    $el.toggleClass("active");
});
```

***Further reading:***

 - [http://ttmm.io/tech/selector-caching-jquery/](http://ttmm.io/tech/selector-caching-jquery/)
 - [http://james.padolsey.com/javascript/js-adolescence/](http://james.padolsey.com/javascript/js-adolescence/)


#### Creating DOM elements

Again, DOM interaction is slow.

If you are creating a number of new DOM elements, it is a good approach to generate the new HTML markup and then insert it into the page in a single command:

```
var planets = ["Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune"];

var $planetList = $(".planet-list");
var planetElements = "";

for (var counter = 0, planetCount = planets.length; counter < planetCount; counter++) {
    planetElements += "<li>" + planets[counter] + "</li>";
}

$planetList.append(planetElements);
```

An alternative method is to *detach* the elements from the DOM while they're being manipulated, then reattach them when complete.

***Further reading:***

 - [http://learn.jquery.com/performance/detach-elements-before-work-with-them/](http://learn.jquery.com/performance/detach-elements-before-work-with-them/)
 - [http://24ways.org/2011/your-jquery-now-with-less-suck](http://24ways.org/2011/your-jquery-now-with-less-suck)


#### Cache $(this)

Similar to the point about caching DOM elements, if you are referencing `$(this)` multiple times then consider caching the element for improved performance:

```
$(".el").click(function (e) {
    var $this = $(this);
    $this.addClass("active");
    $this.slideDown();
    var $a = $this.find("a");
});
```


#### Avoid $(this) entirely

Sometimes it isn't necessary to wrap an element in a jQuery object at all.

Consider the following example:

```
$(".el").click(function (e) {
    var $this = $(this);
    var id = $this.attr("id");
});
```

In this instance, if all we're after is the ID of the element then it doesn't need to be wrapped in a jQuery object, as it could easily be accessed directly from the native DOM object:

```
$(".el").click(function (e) {
    var id = this.id;
});
```

Learning native JavaScript methods can be beneficial for knowing when you don't need to use jQuery.


#### Manipulate classes not styles

When wanting to change the style of an element, don't manipulate its styles directly:

```
// Bad
$(".planet").css({
    "background": "#036",
    "border-color": "#f90"
});
```
Instead, define those styles in CSS:

```
.planet {
    background: #036;
    border-color: #f90;
}
```

And then add (or remove) the class with JavaScript:

```
$(".planets li").addClass("planet");
```

This helps maintain the principle of *separation of concerns* - CSS is responsible for styling, JavaScript is used for behaviour.

It also allows for easier testing of styles, as it becomes possible to add or remove the class manually to test layout without having to change any JavaScript.

***Further reading:***

 - [http://www.smashingmagazine.com/2012/11/19/building-relationship-between-css-javascript/](http://www.smashingmagazine.com/2012/11/19/building-relationship-between-css-javascript/)


#### Consider alternative methods of animation

If you are creating a simple transition, consider whether it can be done with CSS:

```
.planet {
    position: absolute;
    top: 0;
    left: 0;
    width: 25%;
    height: 25%;
    transition: all .25s ease-in-out;
}

.planet.is-active {
    top: 25%;
    left: 25%;
    width: 50%;
    height: 50%;
}
```

It may be possible to trigger an animation simply by toggling a class name with JavaScript:

```
$(".planet").on("click", function (e) {
    $(this).toggleClass("is-active");
});
```

It isn't always possible to use CSS for animations. If you are going to use JavaScript, consider trying the [jQuery animate enhanced](https://github.com/benbarnett/jQuery-Animate-Enhanced) plugin (or similar) because it attempts to use hardware-accelerated CSS3 transitions when possible. This will need testing, as it doesn't always work, and can introduce strange rendering issues.

A non-jQuery alternative for animations is the [GSAP](http://greensock.com/gsap) library.

***Further reading:***

 - [http://www.smashingmagazine.com/2014/09/04/animating-without-jquery/](http://www.smashingmagazine.com/2014/09/04/animating-without-jquery/)
 - [https://css-tricks.com/myth-busting-css-animations-vs-javascript/](https://css-tricks.com/myth-busting-css-animations-vs-javascript/)
 - [http://davidwalsh.name/css-js-animation](http://davidwalsh.name/css-js-animation)


#### Don't loop through a collection unnecessarily

If you want to apply an action to a collection of elements, you don't necessarily need to loop through them.

For example, you do not need to manually loop through elements in order to apply a class name:

```
$("li").each(function () {
    $(this).addClass("planet");
});
```

You can just do:

```
$("li").addClass("planet");
```


#### $el.find();

If you have already used jQuery to find an element:

```
var $planetList = $(".planets");
```

If you then want to find another element within it (a *descendent*), jQuery offers a number of different ways to search for them, but general consensus (and tests) suggest that the best approach is to use `.find()` to locate these elements.

```
var $planets = $planetList.find("li");
```

***Further reading:***

 - [http://vaughnroyko.com/the-real-scoop-on-jquery-find-performance/](http://vaughnroyko.com/the-real-scoop-on-jquery-find-performance/)


#### Chain responsibly

Just because you can chain jQuery methods, doesn't mean you always should.

There's no absolute rules here, but consider code legibility when organising logic.

```
$(this)
    .addClass("done")
    .find("span")
        .addClass("done")
    .end()
    .show("slow", function(){
        $(this).removeClass("done");
    });
```

Try to find a way to write logic so it remains succinct but maintains legibility.


### jQuery pros and cons:

jQuery is great. It's easy to use, well documented, and most developers have at least some experience of using it. It handles a number of strange browser quirks and generally makes a developer's life easier.

In addition, there are a lot of plugins available to help implement common functionality requirements without having to write a lot of custom code.

But jQuery is not always the right choice for every situation.

People often learn to use jQuery before (or without) learning JavaScript. As such it can be difficult to know how to modify scripts downloaded from the web.

jQuery UI in particular is a large library, whereas smaller alternatives exist that could potentially do the same job at a fraction of the file size.

When deciding on the best solution, consider alternatives, such as using a collection of small libraries.

***Further reading***

 - [http://lea.verou.me/2015/04/jquery-considered-harmful/](http://lea.verou.me/2015/04/jquery-considered-harmful/)
 - [http://youmightnotneedjquery.com/](http://youmightnotneedjquery.com/)
 - [https://gist.github.com/rwaldron/8720084#file-reasons-md](https://gist.github.com/rwaldron/8720084#file-reasons-md)
 - [https://etherpad.mozilla.org/jquery-browser-bug-analysis](https://etherpad.mozilla.org/jquery-browser-bug-analysis)
 - [http://blog.romanliutikov.com/post/63383858003/how-to-forget-about-jquery-and-start-using-native](http://blog.romanliutikov.com/post/63383858003/how-to-forget-about-jquery-and-start-using-native)
 - [http://microjs.com/](http://microjs.com/)


## JavaScript Tips

Some tips that cover general JavaScript features (and quirks).

### Declaring variables

Always declare variables for the first time using the `var` keyword.

Although it's not consensus, many developers prefer to define their variables at the top of a code block:

```
function flyToMars () {

    var home = "Earth";
    var self = this;
    var pi = 3.14;
    var $rocket, $thing, $stuff; // empty for now but will be used later

    ...
}
```

Stay consistent in the usage of `var`, whether it's using it for every declaration or chaining multiple variables with a single `var` declaration:

```
var home = "Earth";
var self = this;
var pi = 3.14;
```

*or*

```
var home = "Earth",
    self = this,
    pi = 3.14;
```

There are advantages to the first approach as it is easy to accidentally break the second (for example losing a comma or replacing it with a semi-colon).


***Further reading***

 - [http://benalman.com/news/2012/05/multiple-var-statements-javascript/](http://benalman.com/news/2012/05/multiple-var-statements-javascript/)
 - [http://danhough.com/blog/single-var-pattern-rant/](http://danhough.com/blog/single-var-pattern-rant/)
 - [http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html)
 - [http://james.padolsey.com/javascript/js-adolescence/](http://james.padolsey.com/javascript/js-adolescence/)


### Naming conventions

Pick a naming convention for variables and functions, and stick to it.

There are some fairly common naming conventions for JavaScript, such as to use:

 - `camelCase` for functions, variables and objects.
 - `PascalCase` for constructors and classes.

If using this naming convention, don't use underscores in variable names.

Use descriptive names rather than short names where possible - code for future legibility, leave byte-saving to a minifier.

When naming functions, use *verbs* to describe the nature of the function:

```
flyRocketShip();
fireBoosters();
returnToEarth();
eatBiscuit();
```

### "use strict"

At the top of a function, consider adding a `"use strict"` statement:

```
function flyToMars () {

    "use strict";

    ...

}
```

This puts the JavaScript interpreter into a *strict* context for the duration of that function - the current *scope*.

This changes the nature of some JavaScript errors that would otherwise fail silently - instead they now cause exceptions. This is a good thing, you want to find and fix potential errors rather than allowing them to unnoticed.

For example, using strict mode ensures that you have to declare a variable with `var` before you can use it.

It can also (potentially) make code run (marginally) faster than non-strict mode code.

***Further reading:***

 - [http://ejohn.org/blog/ecmascript-5-strict-mode-json-and-more/](http://ejohn.org/blog/ecmascript-5-strict-mode-json-and-more/)
 - [http://www.nczonline.net/blog/2012/03/13/its-time-to-start-using-javascript-strict-mode/](http://www.nczonline.net/blog/2012/03/13/its-time-to-start-using-javascript-strict-mode/)


### Primitive types

Variables can store simple bits of information like text (*strings*) and numbers:

 - Strings: `"hello"`
 - Booleans: `true`
 - Numbers: `3.14`

When creating a variable that is one of these (primitive) types, the new variable is a ***copy*** of the original. Changing the new variable leaves the original unchanged:

```
var myPlanet = "Earth";
var yourPlanet = myPlanet;
yourPlanet = "Venus";

// myPlanet === "Earth", yourPlanet === "Venus"
```


### Object types

Variables can also store more complex information.

**Arrays:**

```
var planets = [
    "Earth",
    "Mars"
]
```

**Objects:**

```
var earth = {
    "weather": "not bad"
}
```

**Functions:**

```
function flyToVenus () {
    ...
}
```

When creating a new variable, if you assign its value to an existing variable that is one of these complex types, it will ***reference*** the original variable, *rather than copying it*. Therefore any changes to the new variable will *also* change the original version:

```
var myPlanet = {
    "name": "Earth",
    "atmosphere": "Air",
    "water": "wet"
};

var yourPlanet = myPlanet;
yourPlanet["atmosphere"] = "Not air";

// myPlanet.atmosphere === "Not air"
```

***Further reading***

 - [http://snook.ca/archives/javascript/javascript_pass](http://snook.ca/archives/javascript/javascript_pass)


#### Use named functions, not anonymous functions

Something common to see in JavaScript is an anonymous function. As the name (ironically) suggests, they are functions without names:

```
function () {
    ...
}
```

They are never used on their own, such as in the code block above. Instead, they are used as part of another function. A common occurrence when using jQuery is to use an anonymous function like this:

```
$("a").click(function () { ... });
$(document).ready(function () { ... });
```

This could easily be rewritten to use a named function:

```
function doSomethingWhenClicked () { ... }
$("a").click(doSomethingWhenClicked);

function init () { ... }
$(document).ready(init);
```

Anonymous functions are often used when wanting to *encapsulate* some commands to be used for a specific purpose, but this piece of code is unlikely to be re-used elsewhere.

Anonymous functions are difficult to debug, and can't be reused. A better approach is to never use them, and instead to always declare and name functions before use.


***Further reading:***

 - [http://toddmotto.com/avoiding-anonymous-javascript-functions/](http://toddmotto.com/avoiding-anonymous-javascript-functions/)
 - [http://learn.jquery.com/code-organization/beware-anonymous-functions/](http://learn.jquery.com/code-organization/beware-anonymous-functions/)


### truthy and falsy

Some conditions will return a value that is a *boolean* `true` or `false`

```
var $firstPlanet = $(".planet").first();
var isMercury = ($el.text() === "Mercury"); // true
```

Others conditions will return a value that is not strictly `true` or `false` but can be treated as *truthy* or *falsy*:

```
var $planets = $(".planets");
if ($planets.length) {
    flyCloser();
} else {
    flyToNextStar();
}
```

In this scenario, `$planets.length` won't be `true` or `false`, instead it will be a numeric value, `0` or more. If its value is `0`, it is *falsy*, whereas if it is a value above `0` it is treated as *truthy*.

Another example, checking whether an input field contains any text:

```
var $name = $("input#name");
if (!$name.val()) {
    alert("Don't forget to add your name!");
}
```

Notice the `!` before `$name.val()` - this reverses the condition (and turns it into a boolean) to check for a negative value rather than a positive one - whether the text field is empty and therefore *falsy*. In this situation it is useful to use `!` because we only want to add functionality if it is empty, and so saves having to write an empty `if` statement and extra `else` block.

You may sometimes see `!!` used before a condition. This turns a 'truthy' or 'falsy' value into a real boolean `true` or `false`, but unlike using a single exclamation mark it doesn't reverse its state.

```
var $name = $("input#name");
if (!!$name.val()) {
    alert("Well done for having a name!");
} else {
    alert("You probably should have a name...");
}
```

The following will all return a *falsy* value:

 - `false`
 - `0`
 - `""`
 - `null`
 - `undefined`
 - `NaN`

Everything else will return a *truthy* value.

However, be aware that truthy and falsy values can lead to errors - for example if you are looping through an array the first index will be 0, which is treated as 'falsy'.

***Further reading:***

 - [http://www.sitepoint.com/javascript-truthy-falsy/](http://www.sitepoint.com/javascript-truthy-falsy/)
 - [http://james.padolsey.com/javascript/truthy-falsey/](http://james.padolsey.com/javascript/truthy-falsey/)


### Strict comparators (===)

Strict comparators check the *type* of a variable along with its value.

If you use `==` (or `!=`) you may see issues testing against `null` values, confusing numbers and strings, and confusing `0` with boolean `false`.

```
"2" != 2;  // false
"1" == 1;  // true
```

Instead you might need to use `===` (or `!==`) to check both value and type:

```
"1" === 1; // false
"2" !== 2  // true
```

In general it is good practice to always use a strict comparator.

Unexpected errors can often occur when testing form inputs against expected values. It may be necessary to convert numbers into strings (or vice versa). An easy way to test is to see what *type* a value is.

```
// assume the user has entered '10' into this text field
var $age = $("input#age");
var age = $age.val();

typeof age // "string"
age == 10  // true
age === 10 // false

age = parseInt(age, 10); // convert to number
typeof age // "number"
age == 10  // true
age === 10 // true
```

***Further reading:***

 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)
 - [http://www.2ality.com/2011/06/javascript-equality.html](http://www.2ality.com/2011/06/javascript-equality.html)


### syntax

#### curly brackets

When writing blocks such as `if` statements and `for` loops, technically it isn't compulsory to add curly brackets, as the following statement can be assumed to be connected:

```
// works as expected
if (isEarth)
    landRocket();
```

However, it is good practice to always use curly brackets. It's easy to add conditions to an `if` statement at a later date but not notice that there were no curly brackets:

```
if (isEarth)
    landRocket();    // controlled by the if statement
    takeOffHelmet(); // not bound to the if statement, will always happen!
```


#### tabs vs spaces

Choose spaces or tabs, don't mix them.


#### quotes

Choose single quotes or double quotes, don't mix them.


#### commas and semi-colons

Decide where to put commas, e.g. at the start or end of a list of items in an array or object.

```
var innerPlanets = [
      "Mercury"
    , "Venus"
    , "Earth"
    , "Mars"
];
```

or

```
var outerPlanets = [
    "Jupiter",
    "Saturn",
    "Uranus",
    "Neptune"
];
```

Don't use an additional comma at the end of an array/object, as it can cause issues with older browsers:

```
// Don't do this
var planets = [
    "Uranus",
    "Neptune",
];
```

Decide whether to use semi-colons at the end of a line.

***Further reading:***

 - [http://benalman.com/news/2013/01/advice-javascript-semicolon-haters/](http://benalman.com/news/2013/01/advice-javascript-semicolon-haters/)
 - [http://www.codecademy.com/blog/78-your-guide-to-semicolons-in-javascript](http://www.codecademy.com/blog/78-your-guide-to-semicolons-in-javascript)


### debug message logging

Rather than leaving `console.log` messages in an application, or leaving them in for development but manually removing them when code is 'complete', you could use (or create) a simple debugging library that you call instead of `console.log`. This would allow you to leave debug messages in your code and switch them on and off globally with a single configuration option.

```
// log messages like so:
debug.log("Log message");
debug.warn("Warning message");

// set the level of messages to display
debug.setLevel(0);
```

Catching client-side errors could be fundamental to ensuring the application works as expected, so consider [capturing errors and logging them to a third-party application](http://jslogger.com/).

***Further reading:***

 - [http://benalman.com/projects/javascript-debug-console-log/](http://benalman.com/projects/javascript-debug-console-log/)
 - [http://jslogger.com/](http://jslogger.com/)


### async and defer

By default, when a browser finds a `<script>` tag in an HTML document, it stops parsing the HTML immediately until the *script* file has been downloaded and parsed.

Because of this, when inserting `<script>` elements into HTML pages, the convention has been to put them at the bottom of the page, just before the closing `</body>` tag, so they are read after the rest of the HTML has already been parsed.

There are ways to change this behaviour, by adding attributes of `async` or `defer` to the script tag.

```
<script src="venus.js"></script>
<script async src="earth.js"></script>
<script defer src="mars.js"></script>
```


#### async

Async scripts will not stop the HTML downloading, and will be executed as soon as they are downloaded. While being executed they pause the parsing of the HTML document. They will be executed in whatever order they finish downloading.


#### defer

Deferred scripts download alongside the HTML document, but execution is delayed until HTML parsing is complete. They will be executed in the order that they appear in the document.

Older versions of Internet Explorer have poor/no support for defer.


***Further reading:***

 - [http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)


### js- classnames for JS hooks

If you have an HTML element that you are going to manipulate via JavaScript, give it a class name (or data attribute) that is prefixed with `js-`. This helps to differentiate classes added for style from those added purely as hooks for JavaScript functionality.

***Further reading:***

 - [http://philipwalton.com/articles/decoupling-html-css-and-javascript/](http://philipwalton.com/articles/decoupling-html-css-and-javascript/)
 - [http://davidwalsh.name/css-do](http://davidwalsh.name/css-do)


### Ternary operators

Ternary operators are quick ways to write an if/else statement that sets a single value:

```
if (planet === "Earth") {
    var dinner = "chips";
} else {
    var dinner = "salad";
}
```

Can be rewritten as:

```
var dinner = (planet === "Earth") ? "chips" : "salad";
```

Consider brevity vs legibility when considering whether to use ternary operators.

***Further reading:***

 - [http://davidwalsh.name/learning-ternary-operators-tips-tricks](http://davidwalsh.name/learning-ternary-operators-tips-tricks)


### 0.1 + 0.2

Beware one of JavaScript's weird quirks:

```
0.1 + 0.2 // ...
0.1 + 0.2 === 0.3 // ...
```

This doesn't occur in the wild often, but it can cause issues.

***Further reading:***

 - [http://stackoverflow.com/a/588014](http://stackoverflow.com/a/588014)


### Passing objects to functions

When creating a function, if you are expecting more than a few arguments, consider passing a single object rather than lots of arguments.

There are a few advantages to this approach:

 1. The order of arguments doesn't matter
 2. The parameters are named, and so easier to reference
 3. If some of the arguments are optional it saves passing `null` into the function

```
// function usage
modelSolarSystem({
    star: "The Sun",
    planets: ["Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune"]
});

// function definition
function modelSolarSystem (data) {
    var star = data.star;
    data.planets.forEach(create);
    ...
}
```

***Further reading:***

 - [http://rmurphey.com/blog/2011/04/25/objects-as-arguments/](http://rmurphey.com/blog/2011/04/25/objects-as-arguments/)


### Enhance with JavaScript, don't rely on it

Rather than having functionality that doesn't appear if JavaScript isn't present, try to ensure that the initially generated page content is useable for people who don't have JavaScript enabled:

```
<p class="js-relative-date">14th June 2015</a>
```

Then with JavaScript, for those people who are using a browser that supports it, you can detect these elements and enhance the functionality:

```
var $relativeDates = $(".js-relative-date");
makeDatesRelative($relativeDates);
```

***Further reading:***

 - [https://www.gov.uk/service-manual/making-software/progressive-enhancement.html](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html)
 - [http://alistapart.com/article/understandingprogressiveenhancement](http://alistapart.com/article/understandingprogressiveenhancement)


## JavaScript style guides

There are many ways to write JavaScript. Sticking to the rules laid out in a _style guide_ (or _coding standards_ document) means you can write code consistently across a team.

The aim shouldn't just be to get the job done, but to write logical maintainable code.

(For reference, there are popular [CSS](http://cssguidelin.es/) and [SASS](http://sass-guidelin.es/) equivalents.)

There's not a great deal of point writing your own coding standards when others have done the hard work for you.

A useful summary of why it's worth using a JavaScript style guide:

 - [http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/](http://addyosmani.com/blog/javascript-style-guides-and-beautifiers/)

Some JavaScript style guides to consider:

 - [https://github.com/rwaldron/idiomatic.js](https://github.com/rwaldron/idiomatic.js)
 - [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
 - [http://seravo.fi/2013/javascript-the-winning-style](http://seravo.fi/2013/javascript-the-winning-style)
 - [http://www.2ality.com/2013/07/meta-style-guide.html](http://www.2ality.com/2013/07/meta-style-guide.html)


## Ajax

Ajax is the term commonly used to describe the technique of performing an _HTTP request_ with JavaScript in order to retrieve content from a server (or other third-party data source) without having to refresh the current page.

Many JavaScript libraries such as jQuery provide the ability to make Ajax requests.

Ajax can use the HTTP methods *get* and *post* to interact with servers. Both *get* and *post* can be used to send and receive data, but they have their differences that make each suited for different scenarios.


### Get requests

An Ajax *get* request would generally be used to retrieve information from a server. To give an example with jQuery:

```
$.get("/api/planets/");
```

This would request the URL *http://[domain]/api/planets/*

It is possible to pass parameters to the server via the request URL:

```
$.get("/api/planets/", { planet: "Earth"});
```

jQuery converts the second parameter into a query string, transforming the requested URL into: *http://[domain]/api/planets/?planet=Earth*

In the two examples above, the data may have been requested from the server but nothing is happening when that data is received. It is necessary to define what we want to do once data has been returned, or if there was an error.

```
$.get("/api/planets/", { planet: "Earth"})
    .done(function () {
        // this function will be called if
        // the request completes successfully
    })
    .fail(function () {
        // this function will be called if
        // there was an error with the request
    })
    .always(function () {
        // this function will always be called
    });
```

As has already been discussed, it is possible (and recommended) to define these functions separately rather than using anonymous functions.

```
function done () { ... }
function fail () { ... }
function always () { ... }

$.get("/api/planets/", { planet: "Earth"})
    .done(done)
    .fail(fail)
    .always(always);
```

***Further reading:***

- [https://developer.mozilla.org/en-US/docs/AJAX/Getting_Started](https://developer.mozilla.org/en-US/docs/AJAX/Getting_Started)
- [https://api.jquery.com/jquery.get/](https://api.jquery.com/jquery.get/)
- [http://visionmedia.github.io/superagent/](http://visionmedia.github.io/superagent/)


### Post requests

When sending information to a server, *post* requests should be used. They don't limit the amount of data that can be sent to the server as with a *get* request, and they can also be used to upload files.

With *post* requests, the information being posted to the server often comes from form inputs.

Using jQuery, *post* requests are made in a similar manner:

```
function done () { ... }
function fail () { ... }
function always () { ... }

$.post("/api/planets/", { planet: "Earth"})
    .done(done)
    .fail(fail)
    .always(always);

```

***Further reading:***

- [https://api.jquery.com/jquery.post/](https://api.jquery.com/jquery.post/)
- [http://www.sitepoint.com/key-differences-post/](http://www.sitepoint.com/key-differences-post/)


### Cross-domain requests

The two examples above assume that the server providing the data is the same server that the website lives on. There are two possible ways to interact with a different web server. This is useful when dealing with APIs provided by other services.


#### CORS

When attempting to access another server via JavaScript, a *security policy* error may be displayed in the console unless the host server has *cross-origin resource sharing* (CORS) enabled. Although not difficult to enable, there are security implications that must be understood and accepted before deciding to enable support for CORS.

***Further reading***

 - [http://enable-cors.org/](http://enable-cors.org/)
 - [http://dev.housetrip.com/2014/04/17/unleash-your-ajax-requests-with-cors/](http://dev.housetrip.com/2014/04/17/unleash-your-ajax-requests-with-cors/)


#### JSONP

An alternative option is to request *JSONP*, again if the host server provides it.

This gets around the *same-origin* security issue by allowing the host server to return the requested data wrapped in a JavaScript object. This is then embedded into the original web page.

As ever, jQuery provides an easy way to use JSONP, potentially allowing easy interaction with third-party APIs.

***Further reading***

 - [http://www.sitepoint.com/jsonp-examples/](http://www.sitepoint.com/jsonp-examples/)
 - [http://json-p.org/](http://json-p.org/)
 - [https://learn.jquery.com/ajax/working-with-jsonp/](https://learn.jquery.com/ajax/working-with-jsonp/)


## Promises

When creating the Ajax requests above, three functions were defined to accompany it:

 - A `done` function to call when the Ajax request has been successful
 - A `fail` function to call when the Ajax request has been unsuccessful
 - An `always` function to call when the Ajax request has been completed, regardless of the result.

An alternative method of triggering a function when the Ajax request completes is to use a *promise*.

Creating a promise is straightforward, with similar syntax to what has already been demonstrated:

```
function done () { ... }
function fail () { ... }
function always () { ... }

var request = $.post("/api/planets/", { planet: "Earth"});

request.done(done);
request.fail(fail);
request.always(always);
```

The difference here is that the ajax POST request has been stored in a variable called `request`, which is then used to define what should happen with the result of the ajax request.

The advantage of using *promises* is the ability to chain a number of functions to occur asynchronously, triggering later functions only if earlier functions complete successfully.

***Further reading:***

 - [https://api.jquery.com/promise/](https://api.jquery.com/promise/)
 - [https://www.promisejs.org/](https://www.promisejs.org/)
 - [http://www.html5rocks.com/en/tutorials/es6/promises/](http://www.html5rocks.com/en/tutorials/es6/promises/)
 - [http://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html](http://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html)


## Callbacks

A number of the examples demonstrated above are possible because JavaScript allows functions to be passed as arguments to other functions.

This is known as a *callback*.

```
function init () {
    // define the callback
}

// run the callback on DOM load
$(document).ready(init);
```

Callbacks take advantage of the *asynchronous* nature of JavaScript, which provides the ability to execute commands at the appropriate time. The example above demonstrates the *init* function being called when the DOM has finished loading.

Further examples of callbacks will be demonstrated in the following sections.

***Further reading***

 - [https://gist.github.com/infovore/b6c4bc71a1bffdfd9846](https://gist.github.com/infovore/b6c4bc71a1bffdfd9846)
 - [http://stackoverflow.com/questions/9596276/how-to-explain-callbacks-in-plain-english-how-are-they-different-from-calling-o](http://stackoverflow.com/questions/9596276/how-to-explain-callbacks-in-plain-english-how-are-they-different-from-calling-o)


## Timeouts

One of the most common uses of a callback is to trigger a function after a set period of time, rather than immediately.

Sometimes you don't want to do something now, you want to do it later.

```
function doSomethingInTheFuture () {
    alert("It is now the future, here's your jet pack");
}

var timeout = setTimeout(doSomethingInTheFuture, 5000); // 5 seconds
```

This timeout will execute once, 5 seconds from when the timeout has been set.

It is also possible to trigger a function repeatedly on a set interval:

```
function doSomethingContinuously () {
    alert("Is this annoying yet?");
}

var interval = setInterval(doSomethingContinuously, 10000); // every 10 seconds
```

A real world use for timeouts and intervals could be to perform an Ajax request to check for new content every few seconds.

Timeouts and intervals can be cancelled:

```
clearTimeout(timeout);
clearInterval(interval);
```

Of the two, there are disadvantages to using intervals, specifically when they're running in an inactive browser tab they can queue up, meaning that the callback function may be called a number of times when the user finally switches back to the active tab. For this reason it is usually recommended to use timeouts rather than callbacks.

***Further reading***

 - [http://ejohn.org/blog/how-javascript-timers-work/](http://ejohn.org/blog/how-javascript-timers-work/)
 - [http://stackoverflow.com/q/6183463](http://stackoverflow.com/q/6183463)


## Events

Another common use of callbacks is with *events*.

An event can be thought of in the following way:

> *When this happens, do that*

The most common use of events is listening for interactions with DOM elements, such as a click on a specific link or the submission of a form.

The following example demonstrates how to use jQuery to add an *event listener* to a DOM element. It triggers a *callback* function when the link is clicked:

```
function linkClicked () {
    alert("The link was clicked!");
}

$(".js-my-link").on("click", linkClicked);
```

It is possible to add event listeners without using jQuery, but certain older browsers use slightly different syntax, and so using a library saves us from having to define the same function in two slightly different ways.

In the example above, the DOM element has a `class` attribute that starts with `js-` - as has been discussed above, this is a useful convention that allows us to differentiate between CSS classes that are used for styling and those that are used for JavaScript.

Although events can be placed on almost any HTML element, for accessibility purposes it is beneficial to put them on `<a>` elements and form input controls, as this allows for easier keyboard navigation.

***Further reading:***

 - [http://eloquentjavascript.net/14_event.html](http://eloquentjavascript.net/14_event.html)
 - [http://www.kirupa.com/html5/javascript_events.htm](http://www.kirupa.com/html5/javascript_events.htm)


### Prevent default events

When adding custom events, sometimes we may want to stop the initial link from carrying out its default action.

For example, we may have a link that we want to trigger a specific piece of functionality, but for users without JavaScript clicking on the same link would refresh the entire page.

By default, when an event has been triggered an `event` object is available to be passed through to the callback function.

The method to prevent this default behaviour is:

```
$(".js-my-link").on("click", function (e) {
    e.preventDefault();
});
```

***Further reading***

 - [https://css-tricks.com/return-false-and-prevent-default/](https://css-tricks.com/return-false-and-prevent-default/)
 - [https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)


## closures

A closure is formed when a *nested* function is made accessible outside of the function in which it was defined, so that it may be executed after the outer function has returned. It maintains access to the local variables, arguments, and inner function declarations of its outer function.

```
var myPlanet = (function () {
    var atmosphere = "Air";

    return function() {
        // We have access to *atmosphere*
        // because it is defined in the same scope as this function
        alert(atmosphere);
    };
})();
```

One common example of a closure is the module pattern, demonstrated below. This returns a simple object containing references to methods that are defined within the parent function.

Closures are a useful method of creating complex functionality while protecting scope.

***Further reading***

 - [https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/)


## Object literals

As has been demonstrated above, objects are a useful method of storing related information together in a single variable.

```
var planet = {
    name: "mars",
    radius: 3396,
    distanceFromSun: 227900000
};
```


### Functions in objects

Objects are useful for more than just collecting data, as they can contain functions too.

```
var planet = {
    name: "mars",
    radius: 3396,
    distanceFromSun: 227900000,
    getName: function () {
        return this.name;
    },
    revolve: function () {
        ...
    }
};
```

Functions within objects are often called ***methods***, and variables within objects are often called ***properties***.

To call an object's method, you first reference the initial variable name, followed by the function name:

```
var planetName = planet.getName(); // "mars"
```

Storing related properties and methods within an object encapsulates these related functions together within a single variable.

There are possible issues with this approach - mainly that it is possible for other scripts to access (and overwrite) internal parts of an object, for example in the `planet` object defined above:

```
planet.name = "earth"; // override previous value
```

Using objects as the basis of storing variables and functions is a key feature of writing maintainable JavaScript. More complex methods exist to help protect data in an object from being overridden (whether accidentally or intentionally). These will be discussed in the following sections.

***Further reading***

 - [http://www.sitepoint.com/back-to-basics-javascript-object-syntax/](http://www.sitepoint.com/back-to-basics-javascript-object-syntax/)
 - [http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code/](http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code/)


### *this* keyword

In JavaScript, the value of the variable `this` is special. Its value changes depending on where and how it is used.

For example, when referencing other properties or methods within an object literal, use `this` to access (or set) other parts of the object.

```
var planet = {
    name: "mars",
    init: function (name) {
        this.setName(name);
        this.rotate();
    },
    getName: function () {
        return this.name;
    },
    setName: function (newName) {
        this.name = newName;
    },
    rotate: function () {
        ...
    }
};
```

The value of `this` can change when used in different contexts, as will be demonstrated later.

***Further reading***

 - [https://gist.github.com/cjohansen/4135065](https://gist.github.com/cjohansen/4135065)
 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)


## Scope

When you create a variable or function, by default it is defined in the *global* scope. This means that it is available anywhere within the code.


### Understanding scope

Variables created in the *global* scope are accessible to functions defined in the same scope:

```
// this variable is defined in the global scope
var planet = "Earth";

function enthuse () {
    // this is now the local scope, but it has access to variables
    // defined in the global scope

    alert("I like the planet " + planet); // "I like the planet Earth"
}
```

Variables defined within functions are *local* to that function, and so are not available outside:

```
function enthuse () {
    var planet = "Earth";
}
alert("I like the planet " + planet); // ERROR: unknown variable *planet*
```


Variables within functions take priority over variables defined outside:

```
var planet = "Earth";

function enthuse () {
    var planet = "Mars";
    alert("I like the planet " + planet); // "I like the planet Mars"
}
enthuse();
alert("I like the planet " + planet); // "I like the planet Earth"
```


Variables passed into functions also become part of the *local* scope, therefore overriding the variable of the same name declared in the global scope:

```
var planet = "Earth";
function enthuse (planet) {
    alert("I like the planet " + planet); // "I like the planet *undefined*"
    planet = "Mars";
    alert("I like the planet " + planet); // "I like the planet Mars"
}
enthuse(); // no planet passed to function
alert("I like the planet " + planet); // "I like the planet Earth"
```

Also:

```
var planet = "Earth";
function enthuse (planet) {
    alert("I like the planet " + planet); // "I like the planet Venus"
    planet = "Mars";
    alert("I like the planet " + planet); // "I like the planet Mars"
}
enthuse("Venus"); // planet passed to function
alert("I like the planet " + planet); // "I like the planet Earth"
```

***Further reading:***

 - [http://stackoverflow.com/a/500459](http://stackoverflow.com/a/500459)
 - [http://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/](http://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/)


### Issues with scope

The flexibility of scope can be handy, but equally it can cause issues, especially when it isn't taken into consideration.

The main issue with working in the global scope is that it is easy to accidentally override a variable by declaring another with the same name. JavaScript (in a web browser) offers no isolation of scope across files, meaning all code shares the same global scope unless efforts are made to isolate pieces of code into separate local scopes.

Many websites use their own JavaScript code along with third party JavaScript, such as that used for tracking or inserting advertising into a website. It is important that this third-party code is handled in isolation so that it doesn't interfere with any other JavaScript.

The best way to avoid issues with scope is to encapsulate all code within individual local scopes, so that few (if any) variables are defined in the global scope, meaning they do not conflict with one another.

Methods to do this will be discussed shortly.


## Modularity

When building a large and complex website, a significant amount of JavaScript may be written to control its various pieces of functionality. Although certain aspects may need to interact with one another, generally these pieces of code can be managed separately.

Without attempts to keep this code organised, it can quickly become difficult to manage and maintain each piece of functionality without accidentally affecting other parts.

By organising code into *modular components*, it means that each part of the code can be kept and maintained separately from all other components.

Using modular components also helps with managing *scope* - each component can be defined within its own scope rather than the global scope, reducing the potential for any one variable to accidentally override another.

Splitting JavaScript into separate files is a good start to identify logical components. By itself this doesn't protect against issues with scope.

There are a number of possible ways to organise JavaScript into modular components, discussed below.


### Namespaces

One method of creating modular components is to break components into separate objects, and to define a *namespace* within which each object can live.

The following two examples demonstrate how separate pieces of code are isolated from one another within a single namespace.

File 1 - *earth.js*:

```
var PLANETS = PLANETS || {};

PLANETS.earth = {
    name: "Earth",
    radius: 6371,
    distanceFromSun: 149600000,
    moons: ["The Moon"],
    init: function () {
        ...
    }
};
```

File 2 - *mars.js*:

```
var PLANETS = PLANETS || {};

PLANETS.mars = {
    name: "Mars",
    radius: 3396,
    distanceFromSun: 227900000,
    moons: ["Phobos", "Deimos"],
    init: function () {
        ...
    }
};
```

The approach above means there is only a single global variable, in this case called `PLANETS`. This is our *namespace*.

These two files could be included in any order. The first line of both reference the global variable `PLANETS`. If it has already been created, it won't be overwritten. If this is the first file to reference it, a new empty object will be created.

Within the two objects above, all variables are safe and won't overwrite each other.

At a later date another script can reference `PLANETS.mars.init();` or `PLANETS.earth.init();`, or any other method or property defined in the namespace.

***Further reading:***

 - [http://elegantcode.com/2011/01/26/basic-javascript-part-8-namespaces/](http://elegantcode.com/2011/01/26/basic-javascript-part-8-namespaces/)


### IIFEs

Another method of avoiding the global scope is to surround code in an anonymous function that is run (or *executed*) immediately.

The syntax for doing this is:

```
(function () {

    // code goes here...

})();
```

This method is known as an *Immediately Invoked Function Expression*. The advantage of using an *IIFE* is that all code is kept within a function, and so creates its own scope rather than putting any variables or functions in the global scope.

The syntax of an IIFE can be understood in two parts:

 1. The first part is the definition of a function, surrounded in parentheses, which allows a local scope to be created.
 2. The second part is the second set of parentheses that immediately follow the first, which calls the function immediately.

IIFEs are useful when you have some code that needs to be run immediately (for example on initial page load), but this code doesn't need to reference anything else in the site, or be referenced once set up. Surrounding this code with an anonymous function protects it from the rest of the codebase, while the immediate function ensures that it is initialised as soon as it has been created.


#### Exposing IIFEs

One way in which IIFEs can make variables available to other scripts is to be passed an external variable, or *context*. In the following example, the context is passed through on the final line, as the keyword `this` (which defaults to referencing the `window` object, the global scope). Within the anonymous function, this parameter is referred to by the argument `context`:

```
(function (context) {

    var planet = "Earth";
    var radius = 6371;

    function setPlanetName () {
        // do something private
    }

    context.myPlanet = {

        radius: radius,

        getPlanetName: function () {
            return planet;
        }
    };

})(this);
```
This method adds `window.myPlanet` to the global scope:

```
window.myPlanet.radius           // 6371
window.myPlanet.getPlanetName()  // "Earth"
```

Using the approach above, anything that hasn't explicitly been set in the `myPlanet` object isn't accessible by an external script.

***Further reading***

 - [http://benalman.com/news/2010/11/immediately-invoked-function-expression/](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
 - [http://esbueno.noahstokes.com/post/77292606977/self-executing-anonymous-functions-or-how-to-write](http://esbueno.noahstokes.com/post/77292606977/self-executing-anonymous-functions-or-how-to-write)


### Module pattern (revealing)

Another method to access functions and variables created in an IIFE is for it to return a value.

A popular approach is to use the _revealing module pattern_ to isolate scope with an IIFE, and then `return` an object of publicly accessible parameters (variables) and methods (functions).

```
var myPlanet = (function () {

    var planet = "Earth";
    var radius = 6371;

    function setPlanetName () {
        // do something private
    }

    function getPlanetName () {
        return planet;
    }

    // publicly available things
    return {
        radius: radius,
        getPlanetName: getPlanetName
    };

})();
```

In this example, a single global variable of `myPlanet` has been defined, whereas all the code within the function has its own local scope.

The result is that `myPlanet` has the following publicly accessible values:

```
myPlanet.radius           // 6371
myPlanet.getPlanetName()  // "Earth"
```

Using the approach above, anything that hasn't explicitly been returned isn't accessible by an external script.

***Further reading***

 - [http://alistapart.com/article/the-design-of-code-organizing-javascript](http://alistapart.com/article/the-design-of-code-organizing-javascript)
 - [http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)


### Combining IIFEs, the module pattern and namespaces

For large codebases, it is a common approach to combine IIFSs, the module pattern and namespaces to help create a logical structure for your code:

```
var MyApp = MyApp || {};

MyApp.Accordions = (function () {

    var foo = "Foo";
    var bar = "Bar";

    function private () {
        // do something
    }

    function public () {
        // do something
    }

    return {
        foo: foo,
        public: public
    };

})();
```

All of the code above is contained within a single *namespace* of `MyApp`, within which each piece of modular code has its own name which returns a set of public parameters and methods.

In the example above, it creates `MyApp.Accordions` within the namespace, so you could call (for example) `MyApp.Accordions.public();`.

This method is used as the basis for many complex codebases.

***Further reading:***

 - [http://addyosmani.com/resources/essentialjsdesignpatterns/book/](http://addyosmani.com/resources/essentialjsdesignpatterns/book/)


## Constructors and the *new* keyword

An alternative way to create modular code is to *construct* new objects that can be used as a *prototype* of other objects.

Consider the following example:

```
function Planet (name, radius) {
    this.name = name;
    this.radius = radius;
}
```

The way to use this object is to create an *instance* of the `Planet` object:

```
var earth = new Planet("Earth", 6371);
var mars = new Planet("Mars", 3396);
```

Note the use of the keyword `new` before the name of the function. This is vital to ensure that we create an *instance* of the `Planet` object rather than creating a variable that referencing it directly.

To add a function to the `Planet` object that can be referenced by any instances of it, you need to add them to the `prototype`:

```
Planet.prototype.revolve = function () {
    ...
};
```

Creating objects in this manner can have its advantages, especially when creating different types of object that can inherit properties and methods from one another.

***Further reading***

 - [http://wildlyinaccurate.com/understanding-javascript-inheritance-and-the-prototype-chain/](http://wildlyinaccurate.com/understanding-javascript-inheritance-and-the-prototype-chain/)
 - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)



## App structure

When first learning to use JavaScript, it can be tempting to create a single JavaScript file containing every piece of functionality needed for a website. As has already been demonstrated, this can lead to issues with scope, and can be difficult to maintain. Instead, the application should be broken down into modules that each deal with a specific piece of functionality.


### global init location

When creating modular components, each one could be made responsible for initialising itself and controlling its own behaviour.

This is an acceptable approach if every module is completely self-contained and no two modules need to communicate with one another.

An alternative approach is to create a global `init` function that is responsible for initialising all other modules:

```
// create namespace
var MyApp = {};

// set up all tab functionality
MyApp.tabs = (function () {
    function init () {
        console.log("tabs init");
    }
    return {
        init: init
    };
})();

// set up all slideshow functionality
MyApp.slideshows = (function () {
    function init () {
        console.log("slideshows init");
    }
    return {
        init: init
    };
})();

// start all functionality
MyApp.init = function () {
    var tabs = MyApp.tabs.init();
    var slideshows = MyApp.slideshows.init();
};

// run on DOM load
$(document).ready(MyApp.init);
```

The advantage of using a single location to initialise everything is that you can create a *mediator* that knows about the various components of the application and can handle interaction and communication between them, if necessary.

***Further reading***

 - [https://css-tricks.com/how-do-you-structure-javascript-the-module-pattern-edition/](https://css-tricks.com/how-do-you-structure-javascript-the-module-pattern-edition/)


### Communication between modules

Communication between modules is possible by directly referencing their public methods from another function.

Consider the following simplified example of two modules:

```
MyApp.tabs = function () {
    $(".tab").on("click", MyApp.slideshows.init);
}

MyApp.slideshows = function () {
    function init (selectedTab) {
        // do something with the selected tab
    }
}
```

Two modules communicating directly is known as *tight coupling*, and is not a good idea. In principle, modules should never know about one another or directly call each other. Instead we can use an alternative method to enable this communication - *publishing* and *subscribing* to events. This is often shortened to *pub/sub*.

Native events were covered earlier, with an example of detecting when a user clicking on a link (or any other HTML element) and triggering a JavaScript function. Custom events can also be created and triggered in a similar manner.

When something important happens within a module, it can *publish* an event to announce this.

```
// a new row has been added, announce this
MyApp.pubSub.publish("repeating-row-added");
```

Other scripts can *subscribe* to specific events, running specific functions when they occur.

```
// listen for new repeating rows being added,
// and init show/hide on them
MyApp.pubSub.addSubscriber("repeating-row-added", initShowHide);
```

There are a number of different *pub/sub* JavaScript libraries that enable this form of communication between modules.

***Further reading***

 - [http://tech.pro/blog/1402/five-patterns-to-help-you-tame-asynchronous-javascript](http://tech.pro/blog/1402/five-patterns-to-help-you-tame-asynchronous-javascript)
 - [https://github.com/postaljs/postal.js](https://github.com/postaljs/postal.js)


## Plugins and libraries

Many years ago, it was fairly common to have a file full of useful reusable functions that would be copied from project to project. This *library* file could provide some handy shortcuts, saving time recreating the same behaviour across multiple projects.

Open-source libraries such as jQuery have reduced the need for bespoke complex libraries to be maintained privately by individuals.


### jQuery plugins

jQuery offers a range of useful features, but by itself it doesn't cater for every possible requirement.

jQuery *plugins* offers to extend its core functionality to add features such as slideshows, tabs, accordions, and many other features.


### Standalone libraries

Other libraries exist that offer similar benefits of useful functionality, without a dependency on jQuery to function.

For example, the [moment](http://momentjs.com) JavaScript library is useful when dealing with dates. It offers a range of features such as converting dates from a range of formats, and calculating relative dates.

The [Underscore](http://underscorejs.org) library is useful when dealing with complex data that needs to be processed and manipulated.

The [D3](http://d3js.org) library is useful for drawing interactive infographics.

These are just a few examples of open-source libraries written by other developers that are available and free to use.

There are lots more: [http://microjs.com/](http://microjs.com/)


### Finding and reviewing plugins and libraries

Often the trickiest part of a project is finding relevant jQuery plugins and libraries that can help.

There is no single location to start the search. Often a helpful method is to search in a few places such as [Stack Overflow](http://stackoverflow.com) and [Google](http://google.com) for a solution. If you read a few relevant articles and answers you may find that they converge on the same solution.

The majority of useful libraries will be stored on [GitHub](https://github.com/). This is a convenient location for developers to store open-source code for free, and allow others to contribute to their development.

When reviewing possible options, there are a few helpful pointers that can indicate their merits.

 - **Stars:** This indicates how many developers have *bookmarked* the library
 - **Issues:** Looking through the open issues can indicate possible issues developers have had with the library. A high number of open issues may indicate possible issues to consider. Likewise, issues with responses from the library developer(s) can indicate a reasonable level of support. It is also worth looking to see how many closed issues have been resolved successfully.
 - **PRs:** *Pull Requests* are contributions from other developers who are helping to create updates for the library. A number of open pull requests may indicate a library that is no longer under active development.
 - **Documentation and examples:** Learning how to use a new library may be complex at first. The availability of comprehensive documentation and/or code examples can help in the selection of a suitable library.

The most important method of all is to review the code itself. This depends on your level of comfort and ability with JavaScript. [Here are some tips for reviewing plugin code](https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin).


***Further reading:***

 - [http://davidwalsh.name/13-factors-choosing-javascript-charting-library](http://davidwalsh.name/13-factors-choosing-javascript-charting-library)
 - [https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin](https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin)


### Creating a plugin or library

A number of comprehensive guides exist for creating jQuery plugins:

 - [https://learn.jquery.com/plugins/basic-plugin-creation/](https://learn.jquery.com/plugins/basic-plugin-creation/)
 - [http://www.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/](http://www.smashingmagazine.com/2011/10/11/essential-jquery-plugin-patterns/)
 - [http://jqueryboilerplate.com/](http://jqueryboilerplate.com/)

There is no standard method for creating a standalone JavaScript library, but it could help to review a few popular ones to see how they are written and documented.


## JavaScript Frameworks

As has been discussed above, any website will benefit from a move away from the *code-soup* of a jQuery DOM-ready function. The first step is to separate logic into modules.

If the JavaScript continues to grow and increase in complexity, it may be time to stop creating a custom code structure and instead consider using a recognised framework.


### Issues that frameworks solve

The biggest issue with a custom application structure that frameworks attempt to solve is the separation of different types of JavaScript logic. Most JavaScript frameworks enforce a *separation of concerns* - the isolation of code into different functions that are used for different purposes.

The main parts of JavaScript that are traditionally separated are concerned with DOM interaction, data manipulation, templating and event handling.


#### MVC

The common pattern that most JavaScript frameworks follow is called *Model View Controller*, often shortened to *MVC*.

MVC is a complex pattern that is well documented elsewhere on the web. The following links provide a comprehensive explanation of its logic and how it applies to the context of JavaScript frameworks.

Following these principles should result in smaller structured modules that make code more maintainable.

***Further reading:***

 - [http://alistapart.com/article/javascript-mvc](http://alistapart.com/article/javascript-mvc)
 - [http://www.smashingmagazine.com/2012/07/27/journey-through-the-javascript-mvc-jungle/](http://www.smashingmagazine.com/2012/07/27/journey-through-the-javascript-mvc-jungle/)
 - [http://addyosmani.com/resources/essentialjsdesignpatterns/book/](http://addyosmani.com/resources/essentialjsdesignpatterns/book/)


### Deciding whether to use a framework

This is a complex subject with many developers expressing strong opinions for and against the use of frameworks. There are hundreds of articles published on this topic.

Ultimately the decision whether to use one is dependent on the context:

 - How complex is the required functionality?
 - How comfortable are the developers with JavaScript?
 - Do the developers have experience with any JavaScript frameworks?
 - Would the site benefit from being a *single page application*? Should the application logic be stored in the browser, or should the functionality come from the server?

There are several pros and cons that should be considered when making a decision about whether or not to use a JavaScript framework.


#### Pros

 - Most established JavaScript frameworks have been thoroughly tested, leaving you to focus on building your application without having to worry about flaws in the architecture.
 - JavaScript frameworks are usually well-documented, with active communities and plenty of useful articles and answers to common issues on websites such as Stack Overflow.
 - If a new developer has experience with a JavaScript framework they should be productive quickly, as they already have an understanding of its logic.


#### Cons

 - The additional file size of a JavaScript framework (and its dependencies) should be considered.
 - The complexity of JavaScript code required when using a framework can be difficult for inexperienced front-end developers.
 - Some JavaScript frameworks suffer from initial performance hits, taking a considerable amount of time to start the first time they are used.
 - JavaScript frameworks don't always help with SEO - at least not when compared with *traditional* websites.
 - The maturity of a JavaScript framework should be evaluated before it is used. New frameworks especially can change significantly, which could lead to large code rewrites.
 - Choosing a JavaScript framework can involve a long-term commitment and significant investment, based on an open source solution.

JavaScript frameworks are not the right choice for every project. If you’re building a website that still relies on the server for most of its logic, and if JavaScript is used primarily to make things a little more interactive, then a complex JavaScript framework may be overkill. 


### Popular Frameworks

There are no shortage of available JavaScript frameworks, with new ones being created constantly. Here are some of the more popular options:

 - [Backbone.js](http://backbonejs.org/)
 - [AngularJS](https://angularjs.org/)
 - [React](https://facebook.github.io/react/)

There are lots more: [http://todomvc.com/](http://todomvc.com/)

Consideration for the most appropriate framework should weigh up their relative pros and cons, for which there are plenty of comparison articles online.

***Further reading:***

 - [http://davidwalsh.name/6-reasons-to-use-javascript-libraries-frameworks](http://davidwalsh.name/6-reasons-to-use-javascript-libraries-frameworks)
 - [http://bitworking.org/news/2014/05/zero\_framework_manifesto](http://bitworking.org/news/2014/05/zero_framework_manifesto)
 - [http://netpoetica.com/why-i-dont-want-your-javascript-framework-but-i-love-you/](http://netpoetica.com/why-i-dont-want-your-javascript-framework-but-i-love-you/)
 - [https://andywalpole.me/#!/blog/142134/2015-the-end-the-monolithic-javascript-framework](https://andywalpole.me/#!/blog/142134/2015-the-end-the-monolithic-javascript-framework)
 - [http://tantek.com/2015/069/t1/js-dr-javascript-required-dead](http://tantek.com/2015/069/t1/js-dr-javascript-required-dead)


### Isomorphic JavaScript

The future of JavaScript frameworks may lie in a new concept called *Isomorphic JavaScript*. The idea behind this approach is to use the same code to render a web page, whether this is done on the server and in the client.

***Further reading:***

 - [http://isomorphic.net/javascript](http://isomorphic.net/javascript)
 - [http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/](http://nerds.airbnb.com/isomorphic-javascript-future-web-apps/)
 - [http://www.sitepoint.com/isomorphic-javascript-applications/](http://www.sitepoint.com/isomorphic-javascript-applications/)
 - [http://www.smashingmagazine.com/2015/04/21/react-to-the-future-with-isomorphic-apps/](http://www.smashingmagazine.com/2015/04/21/react-to-the-future-with-isomorphic-apps/)
 - [http://blog.neutrondrive.com/posts/252697-isomorphic-javascript-is-not-the-answer](http://blog.neutrondrive.com/posts/252697-isomorphic-javascript-is-not-the-answer)


## JavaScript module loaders

Many programming languages provide a native way to define and use modules. JavaScript currently doesn't (although a future version of JavaScript will introduce this ability).

In the meantime, tools exist to allow developers to use modules now. These *module loader* systems allow complex codebases to be organised in a simple, consistent and well-documented manner.

There are a few popular module loader tools. There are also two different popular methods for defining modules, known as *AMD* and *Common.js*.

 - [RequireJS](http://requirejs.org/) - One of the first module loaders to become popular, it uses the *AMD* method for declaring modules.
 - [Browserify](http://browserify.org/) - A module loader that uses the *Common.js* module declaration and usage
 - [Webpack](http://webpack.github.io/) - Another module loader that uses *Common.js*

Regardless of the tool and module definition system used, the principle is the same; create numerous files containing small isolated modules with individual purposes, then import them at the relevant point where they are used in the codebase.

Module loaders are often used in combination with a JavaScript framework to provide further code structure and separation.

***Further reading***

 - [https://web-design-weekly.com/2014/09/24/diving-webpack/](https://web-design-weekly.com/2014/09/24/diving-webpack/)
 - [https://github.com/substack/browserify-handbook](https://github.com/substack/browserify-handbook)
 - [http://webpack.github.io/docs/commonjs.html](http://webpack.github.io/docs/commonjs.html)


## Templating

When using JavaScript to create content to populate HTML elements, templating tools can help to separate application logic from template markup.

Using a templating system is advantageous when client-side HTML rendering is required, especially when loading data from a server and rendering a complex HTML structure.

A number of templating systems are available:

 - [ejs](http://www.embeddedjs.com/)
 - [Handlebars](http://handlebarsjs.com/)
 - [Mustache](https://github.com/janl/mustache.js)

There are lots more: [http://garann.github.io/template-chooser/](http://garann.github.io/template-chooser/)

Whichever templating language is chosen, they all offer superior functionality (and code separation) compared with creating HTML elements and populating them with jQuery.

However, it is worth considering whether rendering in the client is beneficial, as it may be slow and require the duplication of logic already present on the server. Instead, consider rendering partials on the server and returning HTML to be inserted directly into the DOM.

***Further reading:***

 - [http://www.smashingmagazine.com/2012/12/05/client-side-templating/](http://www.smashingmagazine.com/2012/12/05/client-side-templating/)
 - [http://www.sitepoint.com/creating-html-templates-with-mustachejs/](http://www.sitepoint.com/creating-html-templates-with-mustachejs/)
 - [http://nimbupani.com/mustache.html](http://nimbupani.com/mustache.html)


## Build tools

Regardless of whether a popular JavaScript framework or a custom application structure has been used, chances are that a number of individual JavaScript files have been created to provide a modular codebase.

This may help manage a codebase, but for a production environment these files could be combined to minimise HTTP requests and speed up the website.

A *task runner* can help automate the concatenation (and minification) of these files.

These tools can also help with other tasks such as optimising images, running a CSS pre-processor, linting files to check for errors, running tests and deploying code.

These tools are built to use of plugins to provide this functionality.

Many of these tools are built and configured using JavaScript.

 - [Grunt](http://gruntjs.com/) - The most popular task runner
 - [Gulp](http://gulpjs.com/) - Less popular than Grunt, but often quicker and easier to configure
 - [Brocolli](http://broccolijs.com/) - Another popular task runner

***Further reading***

 - [http://24ways.org/2013/grunt-is-not-weird-and-hard/](http://24ways.org/2013/grunt-is-not-weird-and-hard/)
 - [http://alistapart.com/blog/post/getting-started-with-gulp](http://alistapart.com/blog/post/getting-started-with-gulp)


## Dependency management

Most websites rely on third-party libraries and frameworks - jQuery being the most obvious and popular example. 

It may be fairly quick to manually download and add these third-party dependencies straight into the codebase, but using a *package manager* can simplify the management, installation and updating of these dependencies - especially handy when working across a team.

There are a number of popular package managers, including:

 - [bower](http://bower.io/)
 - [npm](https://www.npmjs.com/)
 - [component](https://github.com/componentjs/component)

There are lots more: [https://github.com/wilmoore/frontend-packagers](https://github.com/wilmoore/frontend-packagers) - *Note this list is missing several package managers that have become popular recently...*

***Further reading***

 - [http://frontendbabel.info/articles/bower-why-frontend-package-manager/](http://frontendbabel.info/articles/bower-why-frontend-package-manager/)
 - [https://css-tricks.com/whats-great-bower/](https://css-tricks.com/whats-great-bower/)


## Testing

Testing JavaScript can be fundamentally important, especially when supporting a large and complex website that undergoes constant development.

A number of frameworks exist for testing with JavaScript:

 - [Jasmine](http://jasmine.github.io/)
 - [Mocha](http://mochajs.org/)
 - [Intern](https://theintern.github.io/)

There are lots more: [http://stackoverflow.com/a/680713](http://stackoverflow.com/a/680713)


***Further reading***

 - [http://alistapart.com/article/writing-testable-javascript](http://alistapart.com/article/writing-testable-javascript)
 - [http://www.smashingmagazine.com/2012/06/27/introduction-to-javascript-unit-testing/](http://www.smashingmagazine.com/2012/06/27/introduction-to-javascript-unit-testing/)
 - [http://www.helpscout.net/blog/functional-testing-casperjs/](http://www.helpscout.net/blog/functional-testing-casperjs/)


## Code quality

When writing JavaScript, it is easy to make small errors that could potentially lead to issues if they go undetected.

[JSHint](http://jshint.com/) and [JSCS](http://jscs.info/) are two tools that can help to spot these issues. They can be configured to enforce coding rules across a team, ensuring all code meets a set of agreed standards.

JSHint and JSCS can be used at various times. Plugins exist to add them directly into lots of popular code editors, to help spot errors immediately. They can also be added to a *task runner* to identify issues as part of a build process. They could be added to a *pre-commit* stage of version control software, ensuring that the code is not accepted until it passes validation.

***Further reading***

 - [https://yannick.cr/posts/enforcing-coding-rules-in-your-team-with-jscs/post](https://yannick.cr/posts/enforcing-coding-rules-in-your-team-with-jscs/post)
 - [http://davetayls.me/blog/2013/07/01/how-will-i-keep-javascript-code-quality-hight-jshint/](http://davetayls.me/blog/2013/07/01/how-will-i-keep-javascript-code-quality-hight-jshint/)
 - [https://github.com/valueof/home/blob/master/pages/blog/why-jshint.md](https://github.com/valueof/home/blob/master/pages/blog/why-jshint.md)


## Node.js

[Node.js](https://nodejs.org/) is a platform that allows JavaScript to be run on a server. The asynchronous event-driven nature of JavaScript lends itself to certain types of application, such as real-time communication with *websockets*.

***Further reading***

 - [http://code.tutsplus.com/tutorials/nodejs-for-beginners--net-26314](http://code.tutsplus.com/tutorials/nodejs-for-beginners--net-26314)
 - [https://github.com/maxogden/art-of-node/#the-art-of-node](https://github.com/maxogden/art-of-node/#the-art-of-node)
 - [http://nodeguide.com/beginner.html](http://nodeguide.com/beginner.html)
 - [http://stackoverflow.com/a/5511507](http://stackoverflow.com/a/5511507)


## Graphics

There are two quite different methods for generating interactive graphics with JavaScript: *SVG* and *canvas*.

### SVG

SVG is an XML-based vector format for drawing images via the DOM. Using SVGs mean resolution-independent graphics at low filesizes.

Various tools exist to help create and interact with SVGs using JavaScript:

 - [SnapSVG](http://snapsvg.io/)
 - [D3](http://d3js.org/)
 - [Raphael](http://raphaeljs.com/)

***Further reading***

 - [https://css-tricks.com/using-svg/](https://css-tricks.com/using-svg/)
 - [http://davidwalsh.name/svg-animation](http://davidwalsh.name/svg-animation)


### Canvas

Canvas is an alternative method of using JavaScript to create graphics in a browser. Unlike SVG, it renders bitmap data. The advantage of using canvas is the ability to use WebGL to create hardware-rendered 3d graphics.

A number of tools exist to help use canvas:

 - [EaselJS](http://www.createjs.com/EaselJS)
 - [Paper.js](http://paperjs.org/)
 - [three.js](http://threejs.org/)

There are lots more: [http://www.softr.li/blog/2012/06/20/which-html5-canvas-javascript-library-should-i-use](http://www.softr.li/blog/2012/06/20/which-html5-canvas-javascript-library-should-i-use)

***Further reading***

 - [https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial)
 - [http://diveintohtml5.info/canvas.html](http://diveintohtml5.info/canvas.html)


## Future versions of JavaScript

Future versions of JavaScript - *ES 6/ES 2015* and beyond - will address many of the issues mentioned above. It will provide a true module loading system, methods for managing scope and creating templates amongst many others.

Although it isn't currently implemented across all browsers, tools such as [Traceur](https://github.com/google/traceur-compiler) and [Babel](https://babeljs.io/) allow JavaScript to be written in this way today, and *transpiled* back into the current version of JavaScript that browsers do understand.

***Further reading***

 - [https://leanpub.com/understandinges6/read](https://leanpub.com/understandinges6/read)
 - [http://24ways.org/2014/javascript-modules-the-es6-way/](http://24ways.org/2014/javascript-modules-the-es6-way/)
 - [https://babeljs.io/docs/learn-es6/](https://babeljs.io/docs/learn-es6/)


## Further reading

There is an overwhelming number of further links here:

 - [https://github.com/dypsilon/frontend-dev-bookmarks](https://github.com/dypsilon/frontend-dev-bookmarks)
