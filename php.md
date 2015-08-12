# PHP notes

A few notes prepared while writing training courses...


## Overview

### Server-side processing

When you visit (or request) a URL in your browser, there's a lot going on behind the scenes to render the page you see

There are several steps to the rendering process, before the page you see is generated

Various different technologies and languages serve specific roles in this process

The rendering process can be split into two distinct categories, those on the client-side and those on the server-side

 - *Servers* are computers used to store data and host/generate web pages
 - *Clients* are computers distributed around the network that use the services provided by servers - typically a user's machine

For example, a web browser is a program on a user's computer that requests data from a web server.

 - *Server-side processing* - takes place on the server
 - *Client-side processing* - takes place on your own machine


### Programming & Markup

A markup language (e.g. HTML) is static - it is used to dictate the appearance and format of the displayed information

A programming language (e.g. PHP, JavaScript) is dynamic - it is used to perform specific tasks/actions such as filtering or manipulating data


### PHP

PHP is just one of many languages that can be used for server-side programming

It is widely available on web servers

There are plenty of books and online documentation to aid your learning

Lots of third-party resources - PHP scripts written by others freely available online

In use on numerous big websites


### Getting started

PHP needs to be run (parsed) by a web server

If you open a PHP file in a web browser directly, you'll see the unprocessed code

You need to run PHP scripts through a web server (typically Apache), the server will process the code and output the results

Luckily, installation is easy. These can be installed separately, or together using something like WAMP, MAMP etc

Apache is a continually running process on the server - think of it as a computer program that you never close

Most web servers run a version of Linux. There are a number of advantages to Linux servers (over for example Windows-based servers). The most important one is that it's free!


### Advantages of server-side processing

Imagine having a website made up of static HTML pages

 - To edit any information you need HTML skills
 - To update the page structure, you need to do it in every file
 - You can't re-use the data anywhere else
 - You can't manipulate the data, e.g. To extract just the page titles as a list of links

It makes sense to separate out data and logic from the presentation

 - Easier to manage any one aspect without having to touch the others
 - Separation of concerns
 - Data can be re-used elsewhere
 - Only have to have one 'template' file that contains how the content will be rendered
 - Data can be edited using a simple form - no HTML knowledge required

A few more reasons why server-side processing is useful:

 - Automate monotonous tasks: e.g. adding a date entry select from 1900 to 201x:

```
<option>1900<option>
<option>1901<option>
<option>1902<option>
```

 - No way to automatically put today's date in to a web page
 - No way to automate tasks or generate content
 - File includes - the earliest form of server-side scripting (e.g. storing repetitive content in a separate file so you only need to write it once)
 - Display specific content only if certain conditions are met
 - Process the information entered into an HTML form
 - It can send emails
 - It can read and write files on the web server
 - It can read web pages (sometimes known as screen or data scraping)
 - It can interact with other web services through APIs

etc... hopefully by now you've been convinced by the advantages of using a server-side language


## Fundamentals

### Getting started

PHP code is identified by being placed within specific script tags:

```
<?php

  // PHP code goes here

?>
```

How to start using PHP:

 - Create a new file
 - Give it a file extension of .php (e.g. index.php)
 - (Or, change an existing file from .html to .php)
 - Write some PHP code within the tags <?php and ?>
 - View the public URL in a browser

PHP code can be freely interspersed with normal HTML.

The PHP interpreter on the server reads the instructions and generates HTML that is sent to the browser

A static HTML file might look like this:

```
<!DOCTYPE html>
<html>
  <head>
    <title>The day today</title>
  </head>
  <body>
    <h1>What day is it today?</h1>
  </body>
</html>
```

Add some PHP:

```
<!DOCTYPE html>
<html>
  <head>
    <title>The day today</title>
  </head>
  <body>
    <h1>What day is it today?</h1>
    <p>
    <?php
      echo date("l");
    ?>
    </p>
  </body>
</html>
```

The server will interpret this PHP and generate:

```
<!DOCTYPE html>
<html>
  <head>
    <title>The day today</title>
  </head>
  <body>
    <h1>What day is it today?</h1>
    <p>
      Friday
    </p>
  </body>
</html>
```

Some rules to note immediately:

 - When ending a PHP command, ensure you use a semi-colon to avoid an error (more on this later)
 - The `echo` command is used to insert content into the HTML page.
 - PHP is case sensitive


### Variables

```
$x = 4;
$y = 10;
$z = $x + $y;
echo $z;
// $z === 14
```

Using `=` to assign values to a variable

Using `+` to add two variables together

Using `===` to check the value of a variable

```
$word1 = "hello";
$word2 = "world";
$sentence = $word1 . $word2;
echo $sentence;

// $sentence === "helloworld"
```

```
$sentence2 = $word1 . " " . $word2;
// $sentence2 === "hello world"
```
Using `.` to concatenate strings and variables

```
$x = 3;
$y = 5;

$z = $x + $y;
echo $z;
// $z === 8

$z = $x . $y;
echo $z;
// $z === "35"
```
Note the difference in using `.` or `+` to concatenate or add variables


#### What is a variable?

A variable is a container, or a reference to something we want the computer to remember (we say to store in memory)

In the cases we've just seen, it is a number or a string of text

We can assign a value to a variable, and can change or read its value at any time

In PHP, all variable names start with the $ symbol.

What you call the variable isn't important!

Variable names are case sensitive, and can't contain spaces or hyphens.

To use mulitple words in a variable name, the convention is either to `$use_underscores_to_seperate`, or `$camelCaseVariableNames`
(try to stick to one convention or the other)

Be careful when re-using variable names, using the same one twice will overwrite the old value stored in the variable

PHP will create a new variable (place in its memory) for any name it doesn’t recognize as a previously used variable

Variables can be used to store different types of data:

 - Integer: `$num = 4;`
 - Float: `$number = 3.14;`
 - String: `$str = "this is some text!";`
 - Boolean: `$something = true;` // or `false`


### Quotes

Use quotes (single or double) to surround standard text

Quote marks around strings of text differentiates these strings from program commands like functions - more on this later

There is a difference between using single-quotes and double-quotes: when a variable name appears in text surrounded by double quotes, its current value is automatically put into the string

```
$name = "Pete";
echo "Hello $name";
// "Hello Pete";
```


### Comments

Single-line comments which begin with two forward slashes (`//`) or an octothorpe - hash/pound - sign (`#`).

```
// one-line comment
# another one-line comment
```

Text to the right of these is ignored by the interpreter, until we start a new line.

Multiline comments use `/*` and `*/` (just like JavaScript and CSS)

```
/*
  Multi-line
  comment
*/
```


### Operators

These are used in PHP to check or assign a value to variables

We've seen a few examples already, the rest will come in useful as we continue to learn

 - `=` asign a value to a variable
 - `.` concatenate two values
 - `+` add two values


#### Comparison operators

 - `===` check if something is identical to something else
 - `!==` check if something is not identical to something else

(We tend to use three === more often than two, it also checks the 'type' of the variable and is therefore more precise and so less likely to lead to unexpected errors)

 - `>` check if something is greater than something else
 - `<` check if something is less than something else
 - `>=` check if something is greater than or equal to something else
 - `<=` check if something is less than or equal to something else


#### Maths operators

 - `+` add
 - `-` subtract
 - `*` multiply
 - `/` divide

You can use parentheses to control the order an equation is calculated:

```
$total = (($x * $y) + $z) / 3.14
```


### Arrays

We use arrays when we want to store a collection of related bits of data

```
$planet = "Mercury";
$anotherPlanet = "Venus";
$planet3 = "Earth";
...
$planetEight = "Neptune";
```

This is 'related' information, so we should store it together

```
$planets = array(
  "Mercury",
  "Venus",
  "Earth",
  "Mars",
  "Jupiter",
  "Saturn",
  "Uranus",
  "Neptune"
);
```

We can access an item within an array by referring to its 'index'

```
echo $planets[2]; // === "Earth"
```

Each item within an array behaves like a variable

Individual array elements are accessed by following the array’s variable name with an index enclosed in square brackets `$stuff[2]`

Note that indexes start at 0 not 1!

The function `count()` returns the total number of elements in the array:

```
echo count($planets); // === 8
```

#### Associative Arrays

These are arrays with non-numeric indices

```
$earth = array(
  "radius" => 6371,
  "distanceFromSun" => 149600000
);
```

This means we can refer to an item in the array via its name rather than a numeric index

```
echo $earth["radius"]; // === 6371
```

Associative arrays are often used when we want to store more complex collections of data

The value to the left of the `=>` operator is the index, the value to the right is the item's value

Arrays are a handy way to store and use information

When we access data from submitted forms, we often use arrays

When we access data from databases, we often use arrays


### File includes

It can be useful to split different parts of a web page up into a number of includable files

For example, on a typical website the header and footer will be consistent across all pages

Having these stored in a single importable file means they would only have to be updated in one place in order to update the entire site

A static HTML file might look like this:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Lorem ipsum</title>
  </head>
  <body>
    <!-- this is where page content goes -->
  </body>
</html>
```

Our header.php include file might look like this:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Lorem ipsum</title>
  </head>
  <body>
```

Our footer.php include file might look like this:

```
  </body>
</html>
```

This simplifies all of the pages in the site:

```
<?php include_once "header.php"; ?>

<h1>Page content...</h1>

<?php include_once "footer.php"; ?>
```

To import files into the page, use one of the following PHP functions:

 - `include`
 - `include_once`
 - `require`
 - `require_once`

`include_once` and `require_once` are used when importing specific functionality you'd only need once in a site, for example database connection details

`include` and `require` can be used multiple times in a single page, and so are handy when importing repeated functionality (e.g. a 'back-to-top' link) throughout a page

When trying to import a file with `include` or `include_once`, if the file doesn't exist the server issues a warning and continues.

When trying to import a file with `require` or `require_once`, if the file doesn't exist the server issues an error and stops.

(You'll learn to use one of the four options, depending on the requirements of the include)


### Control Structures

PHP can perform a specific action only if certain conditions are met

The main types of conditional logic structures are:

 - if/else
 - for
 - foreach

(Again, these are common in most programming languages, not just PHP)


#### if/else

Use different logic based on whether a statement is true or false

```
$today = date("l");

if ($today === "Friday") {

  echo "Hooray, it's Friday!";

} else {

  echo "Is it Friday yet?";

}
```

To use more than one condition you can use:

 - `||` (which means OR)
 - `&&` (which means AND)

We can combine multiple possible if/else with statements "else if"

```
$today = date("l");
$hour = date("G");

if ($today === "Friday" && $hour >= 17) {
  echo "Beer o'clock!";
} else if ($today === "Saturday" || $today === "Sunday"
 || $hour < 9 || $hour >= 17) {
  echo "Time to relax";
} else {
  echo "Get back to work!";
}
```


#### for loops

Allow us to repeat logic until a condition is met:

```
for ($counter=1900; $counter <= date("Y"); $counter++) {

  echo "<option>".$counter."</option>";

}
```

The result:

```
<option>1900<option>
<option>1901</option>
...
<option>201x</option>
```


#### foreach loops

Used for iterating (looping) through arrays

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune");
foreach ($planets as $key => $planet) {
  echo "<p> Planet " . $key . " = " . $planet . "</p>";
}
```

The result:

```
<p>Planet 0 = Mercury</p>
<p>Planet 1 = Venus</p>
...
<p>Planet 7 = Neptune</p>
```

Starts with the array to iterate through, followed by the keyword as, followed by two variables — the first is assigned the index of the element and the second is assigned the value of that index’s element.

(If only one variable is listed after as, it is assigned the value of the array element.)

In our example, the foreach instruction moves through the array `$planets`, assigning each element in turn to the variable `$planet`


### Forms

Here's a basic HTML form:

```
<form action="" method="post">
  <fieldset>
    <legend>What is your name?</legend>

    <label for="name">Your name</label>
    <input id="name" name="name" type="text" />

    <input type="submit" value="Submit" />
  </fieldset>
</form>
```

There are two important attributes on a form: action and method:


#### Action

The action attribute for an HTML form element refers to the URL that the form should send its data to when submitted.

The action attribute can be left blank, in which case the form will send data to the current URL.

Alternatively, form data can be sent to a different script/URL when the form is submitted.


#### Method

The method attribute has two possible options, GET and POST

When using a form to GET or POST values, PHP automatically turns the form data into variables, setting it to the value which was entered by the user.

Depending on whether the form action is set to GET or POST, the values will be available as `$_GET['field-name']` or `$_POST['field-name']`

Whether you use GET or POST depends on which is more suitable for the current situation.


#### GET (appends the values to the URL)

PROs:

 - useful for URL hacking (the values in the URL are the input names and values separated by ?, & and =)
 - useful for bookmarking or adding links

CONs:

 - Insecure, so shouldn't be used for sensitive data (such as passwords)
 - Can only handle a limited amount of data
 - Can only be used for simple form data

#### POST (doesn't append the values to the URL)

PROs:

 - Can be used to post images
 - Can handle more data than a GET request
 - Posted content is hidden from the user, so can contain passwords etc

CONs:

 - Can't be bookmarked or linked to directly
 - Can't be updated via the URL

When the form is submitted, we can access the values that have been entered via PHP


### Errors

Unlike with HTML, when the server encounters a PHP error it is likely to stop, resulting in no page being generated

The error messages should be helpful, showing on which line the error occurred, and hopefully a message indicating what went wrong. These messages are often cryptic!

Errors with PHP are far more common than with HTML/CSS:

 - Syntax errors
 - Missing semi-colons at the end of a line
 - Not enough (or too many) quotes, parentheses, curly brackets or other punctuation


## Arrays

### Working with arrays

With simple variables like strings and numbers, we can echo their value at any point to see what they currently contain:

```
$planets = 5;
$planets = $planets + 3;
echo $planets; // 8
```

```
$sentence = "There are " . $planets . " planets";
echo $sentence;
// "There are 8 planets"
```

If you try to echo an array, you'll get... `Array`

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter");
echo $planets; // Array
```

We have seen that to loop through every item in an array, you can use `foreach`:

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter");
foreach ($planets as $planet) {
  echo "<p>" . $planet . "</p>";
}
```

Which results in:

```
<p>Mercury</p>
<p>Venus</p>
```

This is fine when you know the structure of the array, but this isn't always the case

If you have an array of data that you don't know the structure of, PHP provides an easy way to preview its contents

To preview the contents of an array, you can use the `print_r()` function

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter");
print_r($planets);
Array ( [0] => "Mercury" [1] => "Venus" [2] => "Earth" [3] => "Mars" [4] => "Jupiter" )
```

This works, but it can be difficult to read

When using `print_r()` it usually helps to echo this with HTML `<pre>` tags surrounding it:

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter");
echo "<pre>";
print_r($planets);
echo "</pre>";
```

Which results in:

```
Array (
  [0] => Mercury
  [1] => Venus
  [2] => Earth
  [3] => Mars
  [4] => Jupiter
)
```

`print_r()` works well with associative arrays too:

```
$earth = array(
  "radius" => 6371,
  "distanceFromSun" => 149600000
);

echo "<pre>";
print_r($earth);
echo "</pre>";
```

Which results in:

```
Array (
  [radius] => 6371
  [distanceFromSun] => 149600000
)
```

`print_r()` isn't useful for a final product - you wouldn't want to display information in this way

But during development it's a handy way to check the current value of an array variable


### Why arrays are useful

Arrays are a useful way to use/manipulate/filter information

Later we won't be creating these arrays manually

Instead we'll be retrieving data from external sources - e.g. from a database

We won't know what the content of the array is, but we will have an idea of its structure

When we recieve this data, we need to put it into a format that we can manipulate with PHP

We will be learning how to extract information from a database and turn it into an array

If you learn how to use arrays, then you'll know how to use data from various sources, such as a database or an API call from another website


### Multi-dimensional arrays

Arrays can contain a mixture of different types of content:

```
$things = array(1, 5, "hello", 3.14);
foreach ($things as $thing) {
  echo "<p>". $thing . " = " . gettype($thing) . "</p>";
}

1 = integer
5 = integer
hello = string
3.14 = double
```

Using our planetary examples from before, imagine that we would want to store information about each planet as an array

```
$mercury => array(
  "size" => 0.3,
  "distance" => 0.3
);
```

```
$venus => array(
  "size" => 0.9,
  "distance" => 0.6
);
```

The previous example allows us to store information about each planet

But it doesn't provide an easy way to group together all the planets

The reason for using arrays is to group together content

We want to put each of these planetary arrays into a single array

We can instead contain these in a single array that contains other arrays:

```
$planets = array(
  "mercury" => array(
    "size" => 0.3,
    "distance" => 0.3
  ),
  "venus" => array(
    "size" => 0.9,
    "distance" => 0.6
  ),
  "earth" => array(
    "size" => 1,
    "distance" => 1
  )
);
```

We call arrays that contain other arrays *Multi-dimensional arrays*

We can access values from within the arrays in the same way as before:

```
foreach ($planets as $planetName => $planetData) {
  echo "<p>". $planetName . " size = " . $planetData["size"] . "</p>";
}
mercury size = 0.3
venus size = 0.9
earth size = 1
```

The ability to create multi-dimensional arrays is useful as it allows us to use a more complex information structure

In most real-world examples, the data you'll be using will be more complex than a simple row of information

While we're working this out, the print_r() function we saw earlier will allow us to preview all of the values in the array

One way to access all information within a multi-dimensional array is to use a foreach loop within another foreach loop

```
foreach ($planets as $planetName => $planetData) {
  echo "<h2>".$planetName."</h2>";

  foreach($planetData as $attribute => $value) {
    echo "<p><strong>".$attribute."</strong>: <em>".$value."</em></p>";
  }
}
```

We can manipulate the information in different ways, use different parts in different situations

For example, we may not want to display all of the detailed information for every item in one long page

We may just want to summarise each item initially, then if one is selected display the detailed information only for this item

Let's just output the name of each planet for now:

```
foreach($planets as $planetName => $planetData) {
  echo '<li><a href="?planet='.$planetName.'">'.$planetName.'</a></li>';
}
```


### Superglobal variables

Super-global variables are special variables that are automatically created by PHP.

They are associative arrays that contain values acquired from user input or the server

They are called super-global because they are accessible in any variable scope (more on this later)

The important super-global arrays:

 - `$_SERVER`
 - `$_GET`
 - `$_POST`
 - `$_COOKIE`
 - `$_SESSION`

We have already seen two examples of these: `$_GET` and `$_POST`. These arrays are automatically populated when you submit a form

The 'name' attribute of each form input element is used in these arrays

e.g. if you have a form element:

```
<input type="text" name="firstname" id="firstname" />
```

When the form is submitted, this will be available as either `$_GET['firstname']` or `$_POST['firstname']`

The main way to populate the `$_POST` superglobal variable is to post a form.

`$_GET` parameters can also be populated by forms, but this isn't the only way to add values

We can create links that populate the `$_GET` array

To pass variables via the URL, add parameters to the end of a URL

At the end of a standard URL add a `?` followed by a variable as a key/value pair, separated by an `=`

```
<a href="index.php?index=value">
<a href="index.php?name=pete">
```

To add multiple variables via the URL, separate them with an `&`

Don't forget when you add an `&` in your HTML you should add `&amp;` or it won't validate

```
<a href="file.php?key=value&amp;lorem=ipsum&amp;foo=bar">
<a href="file.php?name=pete&amp;colour=orange">
```

This is a useful way to pass simple variables around between different pages

Back to our planets example, so far we have a list of every planet name

We created links that will append the selected planet name to the URL

When a planet has been selected, `$_GET['planet']` will have a value

We can use this, combined with a simple if/else statement checking whether the variable has been set, to detect whether to display the overview list or detail view


### $_SERVER

This contains useful information related to the server

For example, you can detect the URL of the current page, the file we're currently using, or the user's browser

you can use `print_r()` to see all the possible values of the `$_SERVER` array


## State, sessions and cookies

One important point to note: variables aren't automatically stored or remembered when you move between pages

The `$_POST` array will only be populated on a page after a form submit has occurred

The `$_GET` array will only be populated if a form submit has occurred on the previous page, or if parameters are appended to the URL

In order to save variables between page refreshes, we have to use an alternative technique

HTTP is a "stateless protocol"

This means that every server request is independent - every time you finish requesting a page, the server forgets about you

It doesn't maintain a connection between client and server, there is no way of identifying a sequence of requests as coming from the same user

In order to remain logged in to a site, you need a way to establish credentials across multiple requests

It is possible to transfer information by appending a value to the URL

It can also be added as a hidden fields in a form

In both cases, however, the information is potentially visible at the client end, either in the location bar of the browser or in the source html of the constructed page

A better technique is needed!


### Cookies

Cookies are small pieces of data passed between browser and server as part of the http message header rather than in the document body

They are saved as a file on the client machine

They can be saved for a single browser session (until you close the browser), or for any specified period of time

They can be read and written by PHP and JavaScript

If any cookies exist for the site in question, they are available to the `$_COOKIE` super-global variable

(JavaScript can access the same cookies by referencing the `document.cookie` object)

Cookies are created in PHP using the built-in function `setcookie()`

If, for example, we wished to hold a supplied username throughout a single browser session, we would use the following commands:

```
$username = $_GET['username'];
setcookie('username', $username);
```

This would then be accessible as `$_COOKIE['username']` no matter how many times a user refreshed the page, until the browser was closed.

It is possible to make a cookie last longer than a browser session - you can set your own expiry date:

```
// store the cookie for 30 days from today
setcookie('username', $username, time() + 60*60*24*30)
```

```
// store the cookie until the eighteenth of July, 2026
setcookie('username', $username, mktime(0,0,0,7,18,2026));
```

The third parameter for the `setcookie()` function takes a numeric value that equates to the time that the cookie should expire

To remove a cookie, just set its date value to a date in the past

```
setcookie('username', NULL, -1);
```

Commands to set or change cookie values involve writing a document header, so they must occur before any other document content is output

PHP code to set cookies cannot be interspersed with normal HTML, it must be at the top of a page before any HTML is output

(Even a single space at the beginning of a PHP file before the `<?php` tag is enough to produce an error.)

PROs

 - Cookies make it easier to remember data without having to send it back and forth all the time

CONs

 - Browsers can be set to refuse cookies, limit their lifespan or warn of their arrival
 - Users can view, edit and delete cookies

You can use cookies, but don't rely on them...


### Sessions

Sessions are an alternative to cookies

PHP allows you to define the start of a uniquely-identified session, and associate with it any number of variables which are accessible to any script executed during that session.

A session is initialised by calling the PHP function `session_start()`

This must be placed before any HTML has been outputted

Put this at the very start of a php file:

```
<?php

session_start();

  // .. the rest of the code starts here
?>
```

Once a session has been started, we can reference variables using the `$_SESSION` super-global array

Session variables can be assigned to or retrieved from the `$_SESSION` associative array at any time

```
// start the session - must always happen at the top of the page
session_start();

// (assuming form has been posted, set session variable)
$_SESSION['username'] = $_POST['username'];

// this is now accessible anywhere we have a session
echo $_SESSION['username'];
```

Once you set a session variable, it will exist until you remove it or end the browser session

To remove a session variable, useunset()

```
unset($_SESSION['username']);
```

Use sessions rather than cookies:

 - Session values are stored in temporary files at the server end rather than in the client
 - Therefore sessions are far more secure and reliable than cookies


## PHP and MySQL

***(It may be worth reading the database notes before continuing)***


### Connecting to a MySQL Database with PHP

To connect to a MySQL database with PHP we use a class called mysqli

The line of PHP code we need to do this is:

```
$db = new mysqli("host", "username", "password", "database");
```

We can create a simple PHP script to test to see if we can connect to the database correctly

```
// connect
$db = new mysqli("server","u","p","db");

// check if there was an error
if ($db->connect_error) {
  echo "Connect failed: " . $db->connect_error;
  exit();

// no error!
} else {
  echo "Database connected!";
}
```

An explanation of the database connection code:

 - We're storing the database connection in a variable called `$db` (We'll use this variable again later when we query the database)
 - We test to see if there was an error connecting (for example because of incorrect credentials) by seeing if `$db->connect_error` has a value
 - If there was an error connecting then we display it
 - Otherwise the database connection was successful!

Note that from now on in these examples I'm going to store the connection details in a separate file for convenience

I've also created a generic header and footer PHP file, and a CSS file

I'll import the PHP files into future scripts using require_once

This approach means you only need to update the content for these in one place

(A good practice to get in to!)


### Executing SQL queries with PHP

Once we have established a connection to the database, we can query it with SQL

A basic SQL example is to select everything from the answers table:

```
SELECT * FROM `answers`
```

This should return the following content:


| id | question_id | user_id | answer    | tweet_id    | date_added          |
|----|-------------|---------|-----------|-------------|---------------------|
| 1  | 1           | 1       | Edam      | 23741876128 | 2013-03-19 18:34:23 |
| 2  | 2           | 1       | Charles   | 23741456214 | 2013-03-21 18:35:51 |
| 3  | 1           | 2       | Melted    | 23723849723 | 2013-03-22 09:02:12 |


When we get it into PHP, this data will be represented as an associative array, like those we have seen previously

To execute this with PHP, first we add our SQL query to a variable:

```
$query = "SELECT * FROM `answers`";
```

Then we execute the query...

```
$result = $db->query($query);
```

...and fetch the results

```
$row = $result->fetch_assoc();
```

This will return us the relevant data in an associative array, stored in the variable `$row`


Here is the example code

```
// include connection settings
require_once "../includes/connect.php";

// get a list of all answers in the database
$query = "SELECT * FROM `answers`";

// perform the query
$result = $db->query($query);

// loop through the results as an associative array
while ($row = $result->fetch_assoc()) {
  echo "<pre>";
  print_r($row);
  echo "</pre>";
}
```


### while() loops

We want to turn each row in the table into a simple PHP associative array

We're going to deal with each result individually, looping through them one by one

We will use a `while()` loop, which is similar in many ways to the `foreach()` loops that we've seen previously

The while loop will set the variable $row to an array containing the values of the current row in the table

The `$row` array keys will be the table column names

The first time the while loop is run, the following values are present

```
echo $row['id'];            // 1
echo $row['answer'];        // 'Edam'
echo $row['date_added'];    // '2013-03-19 18:34:23'
```

When the script reaches the end of the while loop - the closing } - it will go back to the start of the while loop, but this time the value of $row will be set to the next row in the table

This will continue until it has run through every row that has been returned by the SQL query


### Multiple SQL Queries

It's easy to change the SQL query to update the data we'll receive

In the next example I've just changed the query from the `answers` to `questions` table to get different results

```
$question_query = "SELECT * FROM `questions`";
```


### SQL Errors

It is a good idea to wrap an if/else conditional statement around the query

This will help to identify any errors with the SQL query

```
// get a list of all content from an unknown table
$query = "SELECT * FROM `lorem_ipsum`";

// perform the query
if ($result = $db->query($query)) {

  // ... display results as before

// if there was an error with your query
// this will display it
} else {
  echo "SQL Error: " . $db->error;
}
```


### CRUD

We have SELECT SQL queries working with PHP

We'll come back to these again in a little while

Let's get the other CRUD commands working

 - Create = `INSERT`
 - Request = `SELECT`
 - Update = `UPDATE`
 - Delete = `DELETE`

We can also write PHP scripts to create, update and delete data with SQL

These examples use a value called `affected_rows` to test how many rows (if any) they have changed in the database

To check that they have changed the data, we'll go back and look at one of the `SELECT` examples


#### INSERT

This SQL command will add a new entry to the `questions` table:

```
INSERT INTO `questions` (`id`, `question`, `date_added`) VALUES (3, 'Favourite Fish', 2013-03-25 18:34:13);
```

This can be executed by a PHP script in a similar way to the SELECT commands we saw earlier

```
// add new question
$query = "INSERT INTO `questions` (`id`, `question`, `date_added`) VALUES (3, 'Favourite Fish', 2013-03-25 18:34:13);";

// perform the query
$result = $db->query($query);
if ($result) {

  // output a count of how many rows were changed
  echo "SQL successful, affected rows: "
  . $db->affected_rows;

// there was an SQL error
} else {
    echo "SQL Error: " . $db->error;
}
```


#### UPDATE

This SQL command will update the question field of the entry we just added to the `questions` table:

```
UPDATE `questions` SET `question` = 'Favourite Fruit' WHERE `id` = 3;
```

This can be executed by a PHP script in the same way as the INSERT command

```
// update question
$query = "UPDATE `questions` SET `question` = 'Favourite Fruit' WHERE `id` = 3";

// perform the query
$result = $db->query($query);
if ($result) {

  // output a count of how many rows were changed
  echo "SQL successful, affected rows: "
  . $db->affected_rows;

// there was an SQL error
} else {
    echo "SQL Error: " . $db->error;
}
```


#### DELETE

This SQL command will delete the question we just added to the `questions` table:

```
DELETE FROM `questions` WHERE `id` = 3;
```

This can be executed by a PHP script in the same way as the INSERT and UPDATE commands

```
// delete question
$query = "DELETE FROM `questions` WHERE `id` = 3;";

// perform the query
$result = $db->query($query);
if ($result) {

  // output a count of how many rows were changed
  echo "SQL successful, affected rows: "
  . $db->affected_rows;

// there was an SQL error
} else {
    echo "SQL Error: " . $db->error;
}
```


### Displaying results

At this point we have basic SELECT SQL queries working with PHP

For now we're just using `print_r()` to test that we have data in a variable, in a similar way to the examples we saw earlier

This is fine while developing to test that we're receiving data, but you don't want to display content in this way for a live site

We need to learn how to take the SQL query results array we recieve, and display it properly with HTML

Using a while loop to access each row individually:

```
// query the database
$query = "SELECT `id`, `answer`, `date_added` FROM `answers`";

// fetch all results
$result = $db->query($query);

// loop through each result one at a time
while ($row = $result->fetch_assoc()) {
  // do something with $row
}
```

The while loop will set the variable $row to an array containing the values of the current row in the table

The $row array keys will be the table column names

The first time the while loop is run, the following values are present

```
echo $row['id'];            // 1
echo $row['answer'];        // 'Edam'
echo $row['date_added'];    // '2013-03-19 18:34:23'
```

To add these to the HTML:

```
// query the database
$query = "SELECT `id`, `answer`, `date_added` FROM `answers`";

// fetch all results
$result = $db->query($query);

// loop through each result one at a time
while ($row = $result->fetch_assoc()) {
    echo '
      <p>Answer ' . $row['id'] . ' = ' .
      $row['answer'] . ' (added on ' .
      $row['date_added'] . ')</p>
    ';
}
```

### Counting results

You may only want to display results if there are any to display

To do this you can use `num_rows()` to count the number of rows that have been returned


```
$result = $db->query($query);

// check we have a result
if ($result->num_rows > 0) {

  // do something
  echo "There were " . $result->num_rows . " results";

// if there are no results
} else {

  // do something else
  echo "Sorry, there were no results";

}
```


### Adjusting queries based on user input

Up to this point we have seen fixed SQL queries

We can use PHP to adjust our SQL queries dynamically by using variables, rather than hard-coding values

For example, we could use an HTML form to allow a user to enter a value, then search our database for this

```
$query = "SELECT * FROM `answers` WHERE `answer` LIKE '%".$_GET['suggestion']."%''";
```


#### Dynamic CRUD queries

We saw earlier some basic examples of other CRUD commands, used to INSERT, UPDATE and DELETE data from the database

We can combine these with HTML forms to make this more dynamic

```
<form method="post" action="">
  <fieldset>
    <legend>Add question</legend>

    <label for="question">Question</label>
    <input id="question" name="question" type="text" value="" />

    <input type="submit" value="Submit" />
  </fieldset>
</form>
```

This form can be used to add new questions:

```
// check if form has been posted
if (!empty($_POST) && !empty($_POST['question'])) {

// create insert SQL query
$query = "INSERT INTO `questions` (`question`, `date_added`) VALUES ('".$_POST['question']."', NOW())";

$result = $db->query($query);
```

There is a problem with this insert form - it doesn't check for existing data before adding a new row to the database

Before adding a new question, it should first check to see if the question code already exists

(This same technique may come in handy when you are thinking about adding users to your website - you shouldn't have two users with the same username)

```
// only add to the database if the form has been submitted
if (!empty($_POST) && !empty($_POST['question'])) {

  // save a reference to the question
  $question = $_POST['question'];

  // check whether question exists already
  $query = "SELECT COUNT(*) AS `count` FROM `questions` WHERE `question` = '".$question."'";
  $result = $db->query($query);
  $data = $result->fetch_assoc();

  // if question exists already, don't add a new one
  if ($data['count'] > 0) {

    echo "<p>This question exists already, please add a different one</p>";

  // no question, so add it
  } else {

    // insert SQL query
    $query = "INSERT INTO `questions` (`question`, `date_added`) VALUES ('".$question."', NOW())";

    // perform the query
    $result = $db->query($query);

    // check the query was successful
    if ($result) {

      // output a count of how many rows were changed
      echo "<p>SQL successful, affected rows: " . $db->affected_rows . "</p>";

    // there was an SQL error
    } else {
        echo "SQL Error: " . $db->error;
    }
  }
}
```


#### Updating and deleting

When updating or deleting data, it often makes sense to turn this into a two-step process

Firstly, the user should be able to select the item to update or delete

Once an item has been selected for updating, we pre-fill the values of a form to make it easier to update

Once an item has been selected for deleting, we offer the user a final chance to change their mind. (Remember there is no undo!)


## Misc. tips

Many of these topics are independent from one another, some may be more relevant or interesting than others...


### Site architecture

When creating a website, it is important to decide on the site structure (or architecture)

 - What sections (or pages) will the website have?
 - Will there be sub-sections?
 - Can any user access every part of the site, or do you have to be logged-in in order to access certain aspects?


An example page list:

 - Home page
 - Item details page
 - User login page
 - User registration page
 - Add an item page
 - (etc)

Once you've decided on the site architecture you can put the file structure together in a logical manner

You could create a PHP file for every page in the site

You could either have these all in the same folder, and name them differently:

 - index.php
 - details.php
 - login.php
 - register.php
 - add.php

Or you could call them all index.php and put them into directories:

 - /index.php
 - /details/index.php
 - /login/index.php
 - /register/index.php
 - /add/index.php

The advantage of the second approach is that you don't need to reference the file name, which makes your URLs look cleaner

 - http://url.com/details.php
 - http://url.com/register.php

vs.

 - http://url.com/details/
 - http://url.com/register/

(subjective opinion!)

Consider creating an includes (or assets) directory for any files that aren't displayed directly in a browser

Examples of files that could go into this directory are:

 - a CSS file
 - a folder to contain images
 - a JavaScript file (or a folder containing JavaScript files)
 - PHP include files
    - database connection include file
    - header and footer include files

Consider separating functionality into files:

 - You may find yourself adding the same functionality in numerous files
 - Any time you repeat the same code, remember there is probably a more efficient way to do it

Consider putting this code into a separate file and including it every time you need it (as we have done with the db connection, header, footer)

 - You could put your session-handling logic into one file that you include at the top of every page
 - You could put your database calls into a separate file to keep them together
 - Additionally, you could then use functions to reference each one as and when you need it (We'll look at functions a little later on)


### Header Include Files And Page Titles

We've seen examples of header and footer include files:

```
<?php require_once "header.php"; ?>

  <!-- page content goes here -->

<?php require_once "footer.php"; ?>
```

In the previous example, the same title was used for every page

To set a different page title for each page, you could set a variable above the header include:

```
<?php
  $title = "Details page";
  require_once "header.php";
?>
```

The `$title` variable would then be available to echo in the header.php file, meaning you could output a different title on every page


### Functions

Functions are a way to group together a set of commands so that we can re-use them whenever we need to

Functions are useful because you can write them once, then use them wherever and whenever you need

There are two types of function:

 - Those that are native (built-in) to the language already
 - Functions that we write ourselves - or alternatively 'third-party' functions that someone else has written, we can include and use them


#### Native functions

There are lots of built-in functions in PHP which allow us to easily perform a specific task. For example:

 - `date()` - Get the current date/time
 - `mail()` - Send an email
 - `scandir()` - List all files and folders in a specific directory on the web server

There is a comprehensive list at php.net - using the search box is a good place to start


#### Third-party functions

Third-party functions are useful when you want to do something that has probably be done many times before

Often you can find that someone else has created a solution and put their example online

Websites like stack overflow, are good places to look for these

Code libraries and frameworks often contain a number of useful functions - more on that later...


#### Writing functions

Creating our own functions is a useful way to reduce code repetition

If you find yourself writing the same code several times, it could be made more efficient by creating a function

```
function doSomething() {
  // code
}
```

As you build a website, you may start to notice situations where a function could help

How you define a function

```
function name() {
  // do something
}
```

Then, to call this function at any time:

```
name();
```

Here's a function to output a link we may use lots of times

```
// output a back to top HTML link
function backToTop() {
  echo '
    <p><a href="#top">Back to top</a></p>
  ';
}
```

To use this function:

```
backToTop();
```

Every time you call it, a back to top link will be output


#### Function parameters

To pass variables into a function, you pass them through as arguments (or parameters)

You reference the names of these variables between the parentheses when you define the function

You then use the same variable name within the function declaration

```
function square($num) {
  echo $num * $num;
}

square(3); // === 9
square(5); // === 25
```

To return a value from a function use the `return` keyword:

```
function square($num) {
  return $num * $num;
}

$threeSquared = square(3); // === 9
$fiveSquared  = square(5); // === 25
```

These are simple examples to show how to create and use functions

In the real world you are likely to use more complex functions

You could use functions to move some of the code you're writing into separate files

For example, you could create a function that checks whether the current user is logged in

Something like this could be used at the top of every page of a website to determine whether to show content for a logged-in user or a member of the public

***Further information:***

 - [http://www.brandonsavage.net/how-to-write-a-function-in-php/](http://www.brandonsavage.net/how-to-write-a-function-in-php/)
 - [http://webhole.net/2010/03/14/php-functions-tutorial/](http://webhole.net/2010/03/14/php-functions-tutorial/)
 - [http://www.tuxradar.com/practicalphp/4/15/0](http://www.tuxradar.com/practicalphp/4/15/0)

#### Variable scope

When using functions, any variables that are defined outside of the function are not available within it

Conversely any variable created within the function is not available outside it

This is known as scope, and is very useful!

There are some exceptions to this; as mentioned earlier, superglobal variables are accessible everywhere (globally)

 - [Variable Scope documentation](http://www.elated.com/articles/php-variable-scope-all-you-need-to-know/)


### Formatting data

In most of the examples we've seen so far, we've output data directly from the database to the page:

```
echo $something;
```

Sometimes you may want to format this information before outputting it on the page

We have already seen a few basic examples of this:

Concatenating strings - when outputting a name we've combined strings like so:

```
echo "<p>" . $firstname . " " . $surname . "</p>";
```

Date functions - to output today's date:

```
echo date_format("d/m/y");
```

#### Changing case

There are further options we could use to manipulate strings of text:

To change the case of a text string we can use `strtolower()` or `strtoupper()`

```
$firstname = "Pete";
$surname = "Goodman";

echo "<p>" .
  strtolower($firstname) . " " .
  strtoupper($surname) .
"</p>";

// <p>pete GOODMAN</p>
```

#### Limiting characters

To limit text to a certain number of characters we can use substr()

```
$text = "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.";

// first param = string
// second param = start position
// third param = number of characters to output
echo "<p>" . substr($text, 0, 140) . "</p>";
```

(Could be useful if for example you want to output a limited summary of a review)


#### Replacing characters

To replace some text with some other text you can use str_replace()

$original = "hello world";

// first param = replace
// second param = with
// third param = original string
$replaced = str_replace("world", "universe", $original);

echo $replaced; // hello universe

There are lots more examples of string functions on the PHP website:

 - [http://www.php.net/manual/en/ref.strings.php](http://www.php.net/manual/en/ref.strings.php)


#### Formatting numbers

There are also lots of functions we could use to manipulate numbers:

You could use `round()`, `floor()` and `ceil()` to round up or down a number with a decimal point, into a whole number

```
$lower = 3.254; $upper = 3.836;

echo round($lower); // === 3
echo round($upper); // === 4
echo floor($lower); // === 3
echo floor($upper); // === 3
echo ceil($lower);  // === 4
echo ceil($upper);  // === 4
```
Could be useful for calculating an average rating for an item, site statistics, etc


#### Generating random numbers

You can generate a random whole number with rand()

rand(1,10) will generate a random whole number between 1 and 10 (inclusive)

Could be used to display a random item from an array

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune");
$rand = rand(0, count($planets) - 1);
echo $planet[$rand];
```

There are lots more examples of number functions on the PHP website:

 - [http://www.php.net/manual/en/book.math.php](http://www.php.net/manual/en/book.math.php)


### Sorting arrays

The examples we saw earlier show how we can manipulate simple variables - numbers and strings

We can also sort and filter arrays

```
$planets = array("Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune");
```

This is a standard PHP array, we already know how to access an individual item:

```
echo $planets[2]; // === "Earth"
```

To pick a random entry from an array we can use rand()

```
$rand = array_rand($planets);
echo $planets[$rand];
```

`count($array)` will give you the number of items in the array

```
echo count($planets); // === 8
```

`shuffle($array)` will shuffle (randomise) the array

```
shuffle($planets);
print_r($planets);
```

`array_reverse($array)` will...reverse an array

```
$reversedPlanets = array_reverse($planets);
print_r($reversedPlanets);
```

`array_unique()` will remove any duplicates

We can add to or remove from the array:

 - `array_pop()` to retrieve and remove the last value
 - `array_shift()` to put a value at the start of an array
 - `array_push()` to put a value at the end of an array
 - `array_unshift()` to retrieve and remove the first value from an array

There are lots more examples of array functions on the PHP website:

 - [http://www.php.net/manual/en/ref.array.php](http://www.php.net/manual/en/ref.array.php)


### Using PHP Or MySQL To Sort Data

When choosing between sorting data with PHP or MySQL, it is more efficient to do as much as possible in the original SQL query

For example, you could `SELECT * FROM questions`, then loop through all the results in PHP to decide whether to output the current question

But it is more efficient to filter in the SQL query...

...unless you are going to re-use the data elsewhere


### File Uploading

We can use HTML forms to upload files to the server

We've already seen the standard structure of an HTML form

In order to enable a form to upload data, add an extra attribute:

```
<form method="post" action="" enctype="multipart/form-data">
```

Then in the form we add a new `<input>` element with a `type` attribute of `file`

```
<input name="upload" id="upload" type="file" />
```

This is all we have to do on the client-side to enable a file to be uploaded

The rest of the work required to upload a file takes place on the server-side

We need to identify when a file has been uploaded

PHP puts the uploaded file data into a superglobal variable called `$_FILES`

The uploaded file will be identified by the name of its HTML element

In the case of the form we have just seen, it will be available as `$_FILES['upload']`

`$_FILES['upload']` will be an array with five key values:

 - `name` is the original filename
 - `type` specifies its mime-type
 - `tmp_name` shows the full pathname of where the temporary file on the server is stored
 - `error` indicates success or failure (0 = false, so no errors)
 - `size` shows the file size, in bytes.

These values are available at `$_FILES['upload']['name']` etc

To upload a file to the web server:

```
// set directory to upload to
$uploadTo = 'path/to/images/';

// get the file name of uploaded file
$filename = basename($_FILES['upload']['name']);

// set location to store uploaded file
$uploadedFile = $uploadTo . $filename;

// get the temporary file name
$tempFile = $_FILES['upload']['tmp_name'];

// move file to its new home
if (move_uploaded_file($tempFile, $uploadedFile)) {
  // file upload was successful
} else {
  // file upload was not successful
}
```

Be aware of security issues when allowing people to upload files to your server!

***Further information:***

 - [http://uk3.php.net/manual/en/features.file-upload.post-method.php](http://uk3.php.net/manual/en/features.file-upload.post-method.php)
 - [http://www.zymic.com/tutorials/php/creating-a-file-upload-form-with-php/](http://www.zymic.com/tutorials/php/creating-a-file-upload-form-with-php/)


### Displaying Images From A Database

You don't need to store images in your database in order to display images in your website

You could just store the name of an image file

We've just seen how to upload a file

As you upload a file you could store its file name in the database

For example, when outputting data from the database, use the filename field as the src for an image:

```
<img src="images/'.$row['filename'].'" alt="'.$row['description'].'" />
```

### Sending emails

To send an email you can use PHP's `mail()` function

```
mail('to', 'subject', 'message', 'headers');
```

An example:

```
// set up mail settings
$to       = "you@email.com";
$from     = "me@email.com";
$fromName = "Me";
$subject  = "Email subject";
$message  = "This is where you put your email content";

// set up technical bits needed to send mail
$headers = "From: ".$fromName." <" .$from. ">\r\n" .
    "Reply-To: ". $from . "\r\n" .
    "X-Mailer: PHP/" . phpversion();

// send mail!
if (mail($to, $subject, $message, $headers)) {
  // email sent successfully
} else {
  // there was a problem
}
```

This doesn't always work - many server doesn't support emails

The `mail()` function is sometimes disabled by web server administrators (for good reason)

Don't over-use it or you'll get into trouble with your web hosts

Your message may be identified as spam because it hasn't come from a recognised email server

You could use a third-party library, but these are often complex to set up


### Search

To add a simple search field/page you can use a form

Identify the columns that you would like to search

Use an SQL command such as:

```
$query = "SELECT * FROM `answers` WHERE `answer` LIKE '%".$answer_search."%'";
```

This will return a list of all items in the database that match the query parameter

We saw the str_replace function earlier

We could use it to find the term that has been searched for, and making it bold

```
// make searched term bold
$answer = str_replace($search_term, "<strong>".$search_term."</strong>", $row['answer']);
```


### Third-party libraries

"Why re-invent the wheel"

You may require a specific bit of functionality for your website

Often someone else has come across the problem you currently face, has solved it, and has released their solution free and open sourced

There are plenty of third-party scripts, plug-ins, libraries and frameworks you could use

These range in size from small specific pieces of functionality up to blogs, shopping carts, and CMSs

Some are free and open source, others require payment

Places like GitHub are great places to search for these scripts


## Security

Generally, visitors to your website will be nice people...

...but some people are not so nice.

They will try to find and exploit security flaws in your website

 - Sanitise input variables
 - Protect against SQL injection
 - Protect passwords
 - Improve session management

Remove any unwanted or potentially harmful content before processing the information

 - Coutent output content to the browser
 - Content added by a user into a form
 - Parameters used to create SQL queries
 - Content saved to a database


### Displaying content

When displaying content from the database we could improve our security:

```
// get a list of all questions in the database
$query = "SELECT * FROM `questions`";
$result = $db->query($query);

// loop through data returned by database
while ($row = $result->fetch_assoc()) {

  // THIS IS THE POINT WHERE WE SHOULD ESCAPE OUTPUTS!
  $question = $row['question'];

  // output content to page
  echo '
    <li>'.$code.': <strong>'.$question.'</strong></li>
  ';
}
```

### Storing content

When entering content into the database we could improve our security:

```
// THIS IS THE POINT WHERE WE SHOULD FILTER INPUTS!
$answer = $_POST['answer'];

// create SQL query to insert new answer
$query = "
  INSERT INTO `answers` (`answer`)
  VALUES ('".$answer."')";

// execute query
$result = $db->query($query);
```

### Escaping content

Essentially, the website is taking input from a user, storing it in a database, and then outputting it for display

If we don't sanitise the content before we output it:

 - Someone adding HTML to their content could affect the layout of our page
 - Someone adding PHP or JavaScript to their content could be far more malicious...


#### Test case

The following examples will use a simple test case

We will try adding the following piece of JavaScript into a form:

```
<script>alert('hacked');</script>
```

You need to stop people being able to enter this code into a form and save it to your database

If you don't escape this content before displaying it, the JavaScript will be executed and create an alert message box

(This JavaScript is harmless, but if someone can enter JavaScript they could easily use `window.location.href` to redirect a user to another site)

There are multiple options to sanitise content before outputting it onto a page

(Which one you choose often depends on how strict you want to be)

 - `htmlspecialchars();`
 - `htmlentities();`
 - `strip_tags();`


#### htmlspecialchars();

converts `' " & < >` into their HTML entity format

 - `'` = `&apos;`
 - `"` = `&quot;`
 - `&` = `&amp;`
 - `<` = `&lt;`
 - `>` = `&gt;`

Using `htmlspecialchars();` makes the text safe to output

```
$content = "<script>alert('hacked');</script>";

$escaped = htmlspecialchars($content);

echo $escaped;

// &lt;script&gt;alert('hacked');&lt;/script&gt;
```


#### htmlentities();

Converts all (applicable) characters into their HTML entity format

In this example, the output will be the same as in the last example

This function will also convert additional characters, such as turning é into &eacute;

Using `htmlentities();` makes the text safe to output

```
$content = "<script>alert('hacked');</script>";

$escaped = htmlentities($content);

echo $escaped;

// &lt;script&gt;alert('hacked');&lt;/script&gt;
```


#### strip_tags();

Removes all HTML, JavaScript and PHP tags

This function does not validate the HTML, so partial or broken tags can result in the removal of more content than expected

Using `strip_tags();` makes the text safe to output

```
$content = "<script>alert('hacked');</script>";

$escaped = strip_tags($content);

echo $escaped;

// alert('hacked');
```

*In summary:*

We should pass any content through one of these functions before outputting it

The choice of function is dependent on how strict you need to be with content


### Filtering form inputs

You may want to run one of these functions before you process the form input, so you don't store the malicious code in your database

This ensures that no malicious code will be stored or executed by our website

Consider all data invalid unless it can be proven valid

We need to validate and sanitise all user input before doing anything with this data


### SQL injection

When allowing users to enter values that will be used in an SQL statement, we also need a way to ensure that our SQL statements can be protected

SQL injection is not always malicious, it could be accidental:

```
$sql = "SELECT * FROM `users` WHERE `surname` = '$_GET['name']'";
```

Someone enters a value with an apostrophe, turning this SQL into:

```
$sql = "SELECT * FROM `users` WHERE `surname` = '<strong>O'Connor</strong>'";
```

(The extra apostrophe makes the query syntactically invalid...)

#### What is a typical SQL injection?

*Extra apostrophes*

Statements that will always equate to true - e.g. adding `OR 1 = 1` to the end of a `WHERE` query

see also:

 - `' OR 1=1--`
 - `" OR 1=1--`
 - `OR 1=1--`
 - `' OR 'a'='a`
 - `" OR "a"="a`
 - `') OR ('a'='a`

Think about a basic og-in script:

```
SELECT `username`, `password` FROM `users` WHERE `username` = '$_POST['u']' AND `password` = '$_POST['p']';
```

When we execute this SQL query, if > 0 records are returned, we assume the user credentials are valid, and log them in

```
SELECT `username`, `password` FROM `users` WHERE `username` = 'xx' AND `password` = '' OR 1 = 1;
```

1 = 1 will always be true, so will return > 0 records

We need a way to filter (or sanitise) all user input, so we don't run into these issues

To avoid SQL injection, we can use `mysqli_real_escape_string()` on all user inputs

```
$escaped_text = mysqli_real_escape_string($db, $text);
```

this function takes two parameters:

 - `$db` = the mysqli database connection variable (you must have already connected to the MySQL database)
 - `$text` = text to escape

Example usage:

```
$username = mysqli_real_escape_string($db, $_POST['username']);
```

This should be used on EVERY user input field

Note that on some servers, slashes are automatically added to escape the extra apostrophes issue we saw earlier

If this is the case, you will also need to remove these slashes:

```
$username = mysqli_real_escape_string($db, stripslashes($_POST['username']));
```


### Prepared statements

Prepared statements are an alternative way to write SQL queries

They have a slightly different syntax to the SQL queries we've seen previously

They are a more secure way of writing SQL queries, as they entirely separate the query structure from the query parameters

When declaring query parameters, first use a question mark symbol - ? - in your query, in place of a variable

```
$query = $db->prepare("INSERT INTO `users` (`username`, `password`, `name`) VALUES (?, ?, ?)")
```

Then bind the variables that you want to use in your query:

```
$query->bind_param('ss', $lorem, $ipsum);
$query->execute();
```

The first parameter should identify the 'type' of each variable:

 - `s` = string
 - `i` = integer - whole number
 - `d` = double/float - number with a decimal point

Instead of mixing parameters with the main query statement, parameters are passed through separately before you query the database

The order of parameters should match the order you want to use them

Prepared statements can be mixed with the filtering functions we saw earlier for extra security


***Further information:***

 - [Documentation](http://php.net/manual/en/mysqli.quickstart.prepared-statements.php)
 - [bind_param documentation](http://uk3.php.net/manual/en/mysqli-stmt.bind-param.php)


#### 'Classic' SQL SELECT statement

```
$sql = 'SELECT `id`, `username` FROM `users` WHERE `username` = "'.$username.'" AND `password` = "'.$password.'"';

$result = $db->query($sql);
```


#### 'Prepared' SQL SELECT statement

```
// prepare the query
if ($query = $db->prepare("SELECT `id`, `username`, `name` FROM `users` WHERE `username` = ? `OR `password` = ?")) {

  // set the parameters to substitute for the ? in the query above
  $query->bind_param('ss', $_POST['username'], $_POST['password']);

  // run the query
  $query->execute();

  // set variable names for each field/attribute you're returning from the query
  $query->bind_result($id, $username, $name);

  // loop through query results
  while ($query->fetch()) {
    echo '
      <p>User: '.$id.' - '.$username.': '.$name.' </p>
    ';
  }

// check for any db query errors
} else {
  echo "SQL Error: " . $db->error;
}
```


#### 'Classic' SQL INSERT statement

```
$sql = 'INSERT INTO `users` (`username`,`password`, `name`) VALUES ("'.$username.'","'.$password.'","'.$name.'")';

$result = $db->query($sql);
```


#### 'Prepared' SQL INSERT statement...

```
// prepare the query
if ($query = $db->prepare("INSERT INTO `users` (`username`, `password`, `name`) VALUES (?, ?, ?)")) {

  // set the parameters to substitute for the ? in the query above
  $query->bind_param('sss', $_POST['username'], $_POST['password'], $_POST['name']);

  // run the query
  $query->execute();

  // check the query was successful
  if ($query->affected_rows > 0) {
    echo "Query executed: affected rows: ".$query->affected_rows;
  }

// check for any db query errors
} else {
  echo "SQL Error: " . $db->error;
}
```


### Storing passwords

Don't store passwords in plain text!

 - It's sensitive information
 - If someone gains access to your database, they gain access to all the passwords you've stored
 - Consider that for a lot of internet users, no matter how many times you tell them not to, they'll use the same password across sites
 - We need to find a way to make the passwords we store useless to anyone who can access them

We need a way to encrypt passwords

#### Hashing

The method of encrypting passwords that we will use is known as hashing

Hashing turns passwords into long random strings of text

For example, the word password run through the `SHA-1` hashing algorithm is `5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8`

It is a one-way process (easy to encrypt, difficult to decrypt)

This means it is difficult to recover the original text from a hashed password

You can easily generate a hash for any string of text

It is highly unlikely that any two strings of text will generate an identical hash

If someone were to access your database and steal your list of password hashes, they can't (easily) use these to reveal the actual passwords

There are lots of different hashing algorithms available

These will all take a string and convert it to a hash of a certain length (and complexity)

They perform the same task in different ways, using different algorithms to calculate the hash

To create a hash with PHP we can choose one of the different hashing functions

```
$string = 'password';
echo "Original string: ". $string;
echo "MD5 hash: ". md5($string);
echo "SHA-1 hash: ". sha1($string);
```

Using these algorithms, any password generated with a string will always produce the same result

`sha1("password")` will always be 5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8

So we can store a hashed value rather than the actual password


#### A log-in scenario

  - Store the hash of someone's password, rather than the password itself
  - When someone tries to log in, encrypt the submitted password using the same method
  - Check this against the stored encrypted version
  - (Instead of comparing the submitted plaintext password to the stored plaintext password)


#### How to generate and store a hash in your PHP/MySQL website

```
// Hash the password
$passwordHash = sha1($_POST['password']);

// Prepare SQL statement
$sql = 'INSERT INTO user (username, password) VALUES ("'.$_POST['username'].'", "'.$passwordHash.'")';

// Insert user
$result = $db->query($sql);
```

#### How to check a hash when logging in to your PHP/MySQL website

```
$passwordHash = sha1($_POST['password']);

$sql = 'SELECT username FROM user WHERE username = "'.$_POST['username'].'" AND password = "'.$passwordHash.'"';

$result = $db->query($sql);

if ($result->numRows() < 1) {
  // user not recognised
} else {
  // user has logged in successfully
}
```

### Salts

This level of encryption is a start, but it's not secure enough for password storage

If someone gains access to your database, they will be able to see your password hashes

A common technique employed to try to decrypt the original plain text passwords from their hashes is called cracking, or 'brute forcing'

Someone who has access to your hashed passwords can generate their own hashes for common passwords

The hashes generated are compared with those in your database

Any matches will reveal the password for the user in question

Modern computers can generate MD5 and SHA-1 hashes very quickly - thousands every second

Hashes can be generated for every word in an entire dictionary

You can suggest users set up strong passwords, which would provide a reasonable level of protection against such attacks...

...but you cannot guarantee that your users will actually do this!


#### Password hashing with a salt

Before generating a hash, we should add a 'salt' to the password

A salt is a random string of characters of a set length

Every time we add a user, we should generate a unique salt for them

We then use both the salt and the password to create a unique password

This provides an additional level of security and protects against brute force attacks

 - [This article explains how to use them](http://phpsec.org/articles/2005/password-hashing.html)


### File Uploads

Previously we have seen a basic example of a file upload script

It doesn't currently run any form of validation the file that's being uploaded

This could be improved!

When allowing users to upload files, there are a couple of precautions you could take:

 - limit the allowed file types
 - limit the allowed file size

Otherwise, if a malicious user knows that you have a PHP server, and you allow them to upload a PHP file, they could write and upload a script that would allow them access to your server

```
// Set allowed file types
$allowedMimeTypes = array(
  "image/jpg", "image/jpeg", "image/pjpeg", "image/JPG",
  "image/X-PNG", "image/PNG", "image/png", "image/x-png"
);

// Check whether to allow this type of file
if (in_array($_FILES['upload']['type'], $allowedMimeTypes)) {
  // file type is allowed
} else {
  // invalid file type, echo error
}
```

### File includes

If you ever use a submitted variable as part of a file name or path, first use `basepath()` to filter it

```
$filePath = basepath("/path/to/file.php"); // file.php
```

This also avoids remote file inclusion

```
$fileInclude = basepath("http://malicious.url/file.php");
// file.php
```


### Misc tips

Don't differentiate betwen invalid usernames and passwords in error messages - If someone is trying to maliciously access an account, you shouldn't let them know that they've identified a valid username but the password is wrong

Limit the number of times someone can log in incorrectly - After a few attempts from the same IP address, consider blocking it, at least temporarily

Turn off PHP error reporting for a live site - It's useful for debugging during development, but you don't want end users to see this information

***Further information:***

 - [http://phpsecurity.org/](http://phpsecurity.org/)
 - [http://www.addedbytes.com/writing-secure-php/](http://www.addedbytes.com/writing-secure-php/)
 - [http://www.sk89q.com/2009/08/definitive-php-security-checklist/](http://www.sk89q.com/2009/08/definitive-php-security-checklist/)
 - [http://code.google.com/p/doctype-mirror/wiki/ArticleIntroductionToXSS](http://code.google.com/p/doctype-mirror/wiki/ArticleIntroductionToXSS)
 - [http://www.dvwa.co.uk/](http://www.dvwa.co.uk/)
 - [http://phpsecurity.org/ch02.pdf](http://phpsecurity.org/ch02.pdf)
 - [http://phpsecurity.org/ch04.pdf](http://phpsecurity.org/ch04.pdf)
 - [http://shiflett.org/articles/sql-injection](http://shiflett.org/articles/sql-injection)
 - [http://www.nyphp.org/phundamentals/5_Storing-Data-Submitted-Form-Displaying-Database](http://www.nyphp.org/phundamentals/5_Storing-Data-Submitted-Form-Displaying-Database)
 - [http://unixwiz.net/techtips/sql-injection.html](http://unixwiz.net/techtips/sql-injection.html)
 - [http://shiflett.org/articles/the-truth-about-sessions](http://shiflett.org/articles/the-truth-about-sessions)
 - [http://shiflett.org/articles/storing-sessions-in-a-database](http://shiflett.org/articles/storing-sessions-in-a-database)
 - [http://shiflett.org/articles/file-uploads](http://shiflett.org/articles/file-uploads)


## XML And JSON

We have seen how easy it was to import files when generating an HTML page, using the PHP functions `include` and `require`

We used the example of a generic header and footer include for a website

We can also use this for repetitive content, information you only really want to store once

### File includes - HTML

Let's say we're creating a form

In this form we want to import a list of countries as a select dropdown list

If it were a static HTML page:

```
<html>
...
<form>
  <select name="country" id="country">
    <option>Afghanistan</option>
    <option>Albania</option>
    ...
    <option>Zimbabwe</option>
  </select>
</form>
...
</html>
```

We could just include the HTML file at the relevant point:

```
<html>
...
<form>
  <select name="country" id="country">
    <?php include "countries.html"; ?>
  </select>
</form>
...
</html>
```

This is one way to store information, as ready-made HTML

But there are some issues:

 - It's not a true separation of data from its display
 - You can't re-use this information in other ways
 - (Each country name is surrounded by an <option> element so couldn't be used in any other way)
 - There are more efficient ways of doing this - we could use PHP to transform it dynamically


Looking at the structure of the original countries HTML, there is a new line (or row) for each item of data

On each line there is the country name with an `<option>` element surrounding it

If we had just a list of country names, we could recreate this programatically using PHP

Now rather than just inserting the file into the page, we'll need to read and process it with PHP

To read the file we use the built-in PHP functions file() and file_get_contents()

```
<html>
...
<form>
  <select name="country" id="country">
    <?php
      $countries = file("countries.txt");
      foreach ($countries as $country) {
        echo "<option>" . $country . "</option>";
      }
    ?>
  </select>
</form>
...
</html>
```

We're now using 'raw' data that could be used elsewhere in different contexts

We aren't restricted to doing this just from a local file on our server

We could use file() and file_get_contents() to retrieve data from any URL*


### file() and file_get_contents()

There is a difference between these two functions.

Which one you use depends on what it is you need to do:


#### file()

reads the contents of a file, and will put each new line into an array

useful when reading in the contents of a file or web page containing listed content

(we're all array experts by now!)


#### file_get_contents()

reads the contents of a file and put this all into a string

useful when reading in the contents of a file or web page containing prose, code (or anything that isn't listed content)


#### Security

(remember that asterisk?)

We can't use file() or file_get_contents() on many servers to access remote files

(they work fine for local files)

Due to security issues - "code injection vulnerabilities" - we'll cover this in a later week

There is an alternative way to import remote files from other servers, to work around the security concern

Put this in a separate file (e.g. 'curl.php'), use require_once at the top of the file if you need to use it

```
function file_get_contents_curl($url) {
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
  $contents = curl_exec($ch);
  curl_close($ch);
  if ($contents) {
    return $contents;
  } else {
    return false;
  }
}

function file_curl($url) {
  return split("\n", file_get_contents_curl($url));
}
```

We are now using 'raw' data that could be used in other contexts

We could also manipulate the data before outputting it

PHP has lots of different functions to manipulate or sort arrays

But the information is not structured

This method is fine for simple single-value information, not so good for complex data

We have seen how to use arrays to manipulate or loop through structured information

What we need is a way to store complex information, so we can turn it into arrays

There are a few options:

 - CSV
 - XML
 - JSON
 - Databases


### CSV

Comma-separated values are another way to store information, often as plain-text static files

Uses a similar storage technique as the last example, but this time we have separate items of data are separated with commas (or another agreed delimiter such as a tab)

```
<?php
// get the country csv data as an array (one country per line)
$countries = file("countries.csv");

// loop through the array, one country at a time
foreach ($countries as $country) {

  // turn each country string into an array of separate values
  // split on the comma
  $countryData = explode(",", $country, 4);

  // output country data!
  echo "<p>Country " . $countryData[0] . ": ".$countryData[1] .
  " - Languages: " . $countryData[3] . "</p>";
}
?>
```

We now have a way to store multiple pieces of data for each item

This system is used widely (e.g. Excel files can be imported/exported as .csv)

Still not got much structure - assuming 'flat' information, one row for each item

We turned information into an array, so we can access the data...

...but each value in the array is indexed by number, based on where it occurs in the row

We don't actually know what that data represents

We're relying on standard formatting. What if there was an extra tab or comma in one row?

Better systems exist for storing complex data


### XML

eXtensible Markup Language

"data interchange format"

Similar to HTML, in that it uses elements and attributes to surround information

It's an open standard defined by the W3C

This is important, it means everyone agrees on how to use it

I should be able to expect XML data from an external source to obey the rules

(But! You can't assume it always will...)

The syntax rules are simple and easy to adhere to

It is self-documenting, the element names describe the content

It allows us to store complex information

It allows two systems written in different technologies to exchange data


#### XML syntax rules

Most tags must have matching opening and closing tags

```
<p>O Rose thou art sick.</p>
<img src="filename.jpg" alt="Image description" />
```

Tags should be 'properly nested'

```
<p>O <strong>Rose</strong> thou art sick.</p>
```

Tags should match case (just use lower-case)

```
<strong>O Rose thou art sick.</strong>
```


#### Aside: XML, HTML and XHTML

HTML looks a lot like XML...

But HTML is not strictly an XML format:

 - Don't need to close tags
 - Case-insensitive opening and closing tags
 - XHTML was an attempt to map XML rules onto HTML

With HTML5 you can pick and choose whether you support XML or not


#### Using XML with PHP

As with the plain-text and CSV examples earlier, we can use PHP to parse XML files too

We can load an XML file in to PHP using the simplexml_load_file() function


```
// load the XML file into a variable
$countries = simplexml_load_file("countries.xml");

// loop through the country data array
foreach ($countries as $country) {
  echo "<p>Country " . $country->id . ": ".
    $country->names->english . " (Local name: " .
    $country->names->local . ")>/p>";
}
```

There is one important difference with the syntax for accessing the data we've loaded from an XML file

The XML is loaded as an object rather than an associative array

Objects in PHP are beyond the scope of this document, but in this situation we use them in a similar way to an array

The key difference is how we access the data

Array syntax:

```
$array['property'] // == value;
```

Object syntax:

```
$object->property // == value;
```

For example to access the English language name we must use:

```
$country->names->english
```

Whereas the more familiar array syntax would have been:

```
$country['names']['english']
```

These are a huge number of standards using the syntax of XML

Each of these has an agreed list of elements and structure

Some examples:

 - SVG for vector image data
 - KML for map data
 - RSS for syndicating web content
 - epub for ebooks
 - (etc...)


### JSON

JSON is used for similar reasons to XML - to share information between systems

It uses JavaScript syntax (as opposed to XML syntax) to store data

JSON has advantages over XML:

It is (usually) less dense (it requires less code) to describe data

This is important: when sharing vast quantities of data across a network you want it to be efficient

The smaller the file size (the fewer the characters) the better

For users of the data, it often doesn't particularly matter if it is stored in XML or JSON format

As with the XML example, we can use PHP to parse JSON files

We load a JSON file into PHP using file_get_contents(), then turn it into a PHP array using the json_decode() function

```
// load the JSON file into a variable as a string
$json = file_get_contents("countries.json");

// turn the string into an array
$countryData = json_decode($json, true);

// loop through the country data array
foreach ($countryData["countries"] as $country) {
  echo "<p>Country " . $country["id"] . ": ".
  $country["names"]["english"] . " (Local name: " .
  $country["names"]["local"] . ")</p>";
}
```

### Why are XML and JSON important

Useful way to store (or represent) complex data

Useful way for different services to exchange data

We can read and manipulate the data with PHP


### Static files and generated content

You don't necessarily have to store data in static files

To keep the data up-to-date you have to manually update the files

Also means you need access to the web server, and the technical skills to do this

You can generate XML/JSON to represent data that has been requested

Many websites now offer XML/JSON feeds


### Data feeds and APIs

Rather than storing data yourself, you can use third-party services to store and manage your data

Why store photos when you can use flickr, why store short pieces of data when you can use twitter

These companies won't give direct access to their databases to anyone

They supply alternative ways to access their information - data feeds and APIs

Data feeds generally allow us access to data, usually in XML/JSON format

APIs are usually more complex as they often also allow us to manipulate data, so we can update content without having to visit the site itself

We could consider using third-party services to replace a local database, or to provide supplimentary information about a selected item from our website