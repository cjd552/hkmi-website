Each website has a setting for what the default home page is. Usually `index.html`

The client browser sends out a HTTP request. The URL can have variables e.g. `http://a.com/ok.php?x=3`
These variables can be read by HTML and CSS to provide dynamic features. Most commonly language translation.

Usually given in key-value pairs:

```html
category=game&order=popular
```

If & is actually in your value, or there are Chinese characters, you need to use ASCII to represent it. You can look these up with URL encoder.

# AJAX

## Sending data in forms

```html
<form method="post" action="http://a.com/test.php">
    phone: <input type="text" name="phone"/> <br/>
    <input type="submit" value="send"/>
</form>
```

## Old style AJAX 
Replaces the XMLHTTPRequest from Javascript, as it is limited and finnicky, only giving responses in text.
```javascript
var req= new XMLHTTPRequest();
req.open("get", "http://a.com/test.php?phone=12345678");
req.send();
req.onload=function(){
    // Put the response function here
    alert(this.responseText);
    };
```

If you did want to use images, you'd have to convert the image to base 64 and account for that in the front end to convert it back to an image.

Recommended to use `POST` requests over `GET` for privacy.

```javascript
var req= new XMLHttpRequest();
req.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
req.open("post", "http://localhost:8080/pop.php");
req.send("city=hsinchu");
```

## JSON style AJAX

Creating an object
```javascript
var point={};
point.x=3;
point.y=4;
```

Creating an array
```javascript
var names=[];
names[0]="Bob";
names[1]="Mary";
```

Using AJAX
```javascript
$.ajax(
    {
        type: "POST", // or methods: 'post' also ok
        url: "demo_test.txt",
        data: data,
        success: function(result){
            $("#div1").html(result);
        },
        dataType: dataType //xml, html, script, json, jsonp, text
    }
);

