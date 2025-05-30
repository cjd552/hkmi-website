# Responsive layouts

Standard laptop: 1920 x 1080
Standard phone: ~350 x ~600

The size should be relative to the browser window, not the device's screen size

There is a device preview button in the developer tools in Chrome browser, which has a list of devices available.

Only HTML5 supports responsive layout. (DOCTYPE html and meta tag in heading)

Start by making the PC version, as it usually has a more complex layout since there is more real estate.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

This is metadata that needs to be set for responsive layouts. Add this to the head before the title.

Other metadata can be set such as SEO terms (locale, site name, type), character set...

## Bootstrap breakpoints

Has preset sizes. Typically use `xl`, `md`, `sm`

`sm` or smaller = phone

Between `sm` and `md` = tablet

`md` or above = computer

## Setting CSS for screen size

```css
@media only screen and (max-width:600px){

}
```
i.e. these display settings will only apply if the screen size is less than 600px

Put this afterwards so it is checked after the default.

Note that if there is `!important`, this will be used even if there is a later override. Unless they both have the tag, then the latter is taken.

CSS has a built in `calc()` function to do maths.

## Priority of layering

Within CSS, `z-index` which can hold a value up to 999, but recommended to use 1 to 10.


# Javascript

> Javascript is case sensitive and has semicolons at the end

> Add Javascript at the very end of the `<body>`. It must be contained within a `<script>` block or a separate document.

To import an existing Javascript file / library, you can add to the head

```html
<script type="text/javascript" src="filepath"></script>
<!-- Don't put anything in between the tags>
```

```javascript
"cat" + 1;
```
Converts 1 to a string, then appends it to `"cat"`. The string has to come first.

```javascript
var name; // public variable
let name; // private variable (stays within a file)
const pi = 3.14152926; // constant, set once then read only
```

Can set a variable value at the same time as defining it.

Javascript has `++` and `--` and uses `&&` and `||` and `%`

Arrays are 0 indexed.
```javascript
new Array(); // create an array with size 0
new Array(10); // MOST TRADITIONAL AND RECOMMENDED, create an array with size 10
var a = []; // create an empty array
a.length;
```

For Loop
```javascript
for(var i=0; i<a; i++){

};
```

Defining text
```javascript
var name = "cat"; // shorter version. double quote is varchar, single quote is char. Must be double quote for Chinese
var name = new String("cat");
```

String manipulation
```javascript
charAt(position);
indexOf("text to find");
substring(start,end);
toLowerCase();
toUpperCase();
```

Mathematical functions
```javascript
random(); // gets random value between 0 and 1
abs(no);
pow(x,y);
round(no);
floor(no);
ceil(no); // give the next full number no matter what
sqrt(no);
```

```javascript
if (){

}else if (){

}else{

}

while(){

}
```
There are also case switch statements, and you can use `break` and `continue` in loops.

Functions
```javascript
functionName(); // call a function

// Define a function
function message(value){
    // Add a popup with a given message
    alert(value);
    return; // best practice to include even if there is nothing to return
}

function add(n1,n2){
    return n1+n2;
}

//is equivalent to

var add = function(n1,n2){
    return n1+n2;
}
```

You don't need to make classes. Just make objects

```javascript
var man = new Object();
man.age=25; // attributes begin existing as you set them
man.name="Bill";
man.talk = function({alert("Hello");});
```

`this` is the equivalent of `self`

# HTML Document Object Model (DOM)

Always present if file is being accessed in a browser.

Tree structure:
- Window
    - History: browsing history
    - Document (Global variable): The HTML file's contents.
        - Body
            - e.g. h3, div, span and so on
    - Screen: the size of the monitor

Javascript functions can refer to elements using this tree structure. Elements can be fetched such as using ID, CSS selectors.

Can refer to `window.x` or `document.x`

```javascript
window.confirm("Are you sure?");
var divObject=document.getElementById("title"); // Returns 1 object
// Beware as fetching by other features may return an array.
divObject.className;
alert(divObject.innerHTML); //print out the contents of divObject element
```

CSS is modified by `object.style.value` e.g. `divObject.style.color` (names may differ slightly between CSS and Javascript)