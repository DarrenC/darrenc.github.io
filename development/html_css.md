# HTML and CSS

## CSS

- <https://www.udemy.com/css-layout-made-easy/learn/#/lecture/3368194>

### Horizontal Lists

Unordered list of items in a horizontal line:

```css
.widgetMeteo ul {
    height: 100%;
    list-style-image: none;
    list-style-position: outside;
    list-style-type: none;
    margin-bottom: 0;
    margin-left: 0;
    margin-right: 0;
    margin-top: 0;
    padding-bottom: 0;
    padding-left: 0;
    padding-right: 0;
    padding-top: 0;
}
.widgetMeteo li {
    float: left;
}

```

### Forcing Refreshes of CSS or Script files

There are two ways of making sure that your CSS and script files are
reloaded by browser after you update them, they both basically change
the URL for the resource file by adding a query string to the url. The
file remains exactly the same but the browser will see it as a new file
because of the query string.

The two methods:

- Manually adding a version string that needs to be updated when you change the file:

```html
  <link rel="stylesheet" href="style.css?v=2.2" type="text/css" media="screen, projection" />
```

- Adding code to calculate a timestamp for the file change date. -  example in PHP -
    <http://markjaquith.wordpress.com/2009/05/04/force-css-changes-to-go-live-immediately/>

### Clickable background image

<http://haacked.com/archive/2006/01/13/ClickableBackgroundImagesViaCSS.aspx>

Basically the idea is to have a background image in your <div\>, then
add a link/h1 inside it, hide it and then size the link/h1 to be the
size of your div with the background image\...\...

``` html
<div id="main">
    <div id="header">
        <a href="/" title="Home"><h1>Title</h1></a>
    </div>
    <div id="body">Body</div>
    <div id="footer">Footer</div>
</div>
```

and the css

```css
#header{
    background: url(logoExample.jpg);
    width: 180px;
    height: 135px;
    position: relative;
}

#header a{
    position: absolute;
    top: 0;
    left: 0;
    width:180px;
    height: 135px;
}

#header a h1{
    display: none;
}
```
