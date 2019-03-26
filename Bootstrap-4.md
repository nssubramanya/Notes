# Bootstrap 4



## Editor
### Free Editor Choice
Atom, Brackets, Visual Studio Code, Visual Slick-edit, Eclipse

### Plugins
* Emmet
* Live Server
* Color Preview
* CSS Peek
* Bootstrap-4 Snippets
* Auto format on Save
* Lorem ipsum generator (Emmet can also do this!)

### Editor F
## Emmet Commands
h1>lorem5

## BS - Text Classes
* __lead__ **: 
* __display-1, display-2, ...__
* __h1, h2, h3 etc. __: can also be used as classes
* __text-muted __: Muted Text
* __<mark></mark>__ tag: Highlight text inbetween
* __Blockquote__:
* __Blockquote Footer, Citation__:

### Text Alignment
* text-left
* text-right
* text-center
* text-justify

* text-sm-<left/right/center/justify>: Small viewport text aligment
* text-md- : text alignment on viewports sized MD (medium)
* text-lg- : large
* text-xl- : Extra large

### Text Transform
* text-lowercase
* text-uppercase
* text-capitalize

### Font Weights
* font-weight-bold
* font-weight-normal
* font-weight-light
* font-italic

### Monospace Text
* text-monospace

### Lists
* __list-inline__: Removes the Bullet/Numbering in Unordered/Ordered Lists 
* __list-inline-item__: Makes the list items in one line - Useful in constructing menus

### Special ONes
* __<kbd>ctrl</kbd>__: Shows the 'ctrl' in a block - Useful for showing Keyboard shortcuts
* __letter-spacing__: Increase or decrese letter spacing


## Images

### Free Stock Images
* [Free Images @ __Pixabay__](www.pixabay.com)

### Classes
* __img-fluid__: Automatically resizes the images
* __img-thumbnail__: Puts a border around the image
* __rounded__: puts rounded edge around image
* __float-right__: Floats the image to the right i.e. right align
* __text-center__: Centers the image

##### Covering image entire body
```css
body{
	background: url(watch.png) no-repeat center center fixed;
	background-size: cover;
}
```
##### Ways to Center an image

```html
<div class="container">
	<img src="test.jpg" class="img-thumbnail d-block mx-auto" alt="Watch">
</div>
```
or 

```html
<div class="text-center">
	<img src=test.jpg" class="img-thumbnail" atl="watch">
</div>
```

## Fonts
### Linking google Fonts
* Open google fonts and select the font

```html
<link href="https://fonts.googleapis.com/css?family=Revalia" rel="stylesheet">


<div class="container">
	<h1 class="hero">We are coming up with <span class="display-1">Watches</span></h1>
</div>
```

```css
.hero{
	font-family: 'Revalia', cursive;
}
```

## Containers 

## Media Breakpoints
1. __XS (Extra Small)__: max-width: 575px
2. __SM (Small)__: min-width: 576px and max-width: 767px
3. __MD (Medium)__: min-width: 768px and max-width: 991px
4. __LG (Large)__: min-width: 992px and max-width: 1199px
5. __XL (Extra Large)__: min-width: 1200px



