# Events

End-user triggers:
```
click
dblclick
mousedown
mouseup // when you let go of the mouse
// To check for mouse held, just check there was a mousedown and hasn't yet been a mouseup.
mousemove
mouseover
keydown
keyup
keypress
```
System triggers
```
load // when something is loading
ended // when a video finishes playing
```

Using listeners to check for events

```javascript
box.addEventListener("click", handler);
// The box is listening for when it gets clicked
```

# JQuery

Simplified querying in Javascript.

Allows Ajax which allows for asynchronous HTTP Requests.

Importing JQuery: 
```javascript
<script src="./js/jquery.min.js" type="text/script"></script>
// Use JQuery library, source is where you downloaded it to.
```

The downside is you need to know how many elements you are expecting to be returned, as singletons are not returned as arrays.