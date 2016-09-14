# css3-slider-panels

We will be building slider panels using only CSS. Like what can be found at the link below.

http://tympanus.net/Tutorials/CSS3SlidingImagePanels/index.html

#Step One
Create files for you html and css.

#Step Two
In your html file we'll need to create an element to act as a main container for our sliders and give it a class.

 - Within our container we'll be adding radio buttons and labels.

 ```HTML
   <input id="select-img-1" name="radio-set-1" type="radio" class="cr-selector-img-1" checked/>
   <label for="select-img-1" class="cr-label-img-1">1</label>
 ```

 - Add three more sets of the above. Keep the name attribute the same on each, but increment the numbers on the ids, classes and fors as well as the number between the label tags.

#Step Three
Next we need to add our panels. We can do this by creating another container div (give the div a class) after our buttons and labels. Within this div, we'll have four sets of divs, each filled with four spans. The slice number will increment in each set.

```HTML
       <div>
         <span>Slice 1 - Image 1</span>
         <span>Slice 1 - Image 2</span>
         <span>Slice 1 - Image 3</span>
         <span>Slice 1 - Image 4</span>
       </div>
```

#Step Four
Let's create our titles now with another div (give the div a class) that contains four sets of h3 tags containing two spans each.

```HTML
  <h3>
    <span>Serendipity</span>
    <span>What you've been dreaming of</span>
  </h3>
```
This will end our html.

#Step Five
Now for the stylings. Let's begin by styling the container div by giving it a white border and subtle box-shadow.

```CSS
.cr-container{
	width: 600px;
	height: 400px;
	position: relative;
	margin: 0 auto;
	border: 20px solid #fff;
	box-shadow: 1px 1px 3px rgba(0,0,0,0.1);
}
```

We can ensure we reach the proper 'slices' of our images and titles by using the sibling selector. We want our labels to appear on top of everything so we can use z-index and then add a top margin to get the proper position.

```CSS
.cr-container label{
	font-style: italic;
	width: 150px;
	height: 30px;
	cursor: pointer;
	color: #fff;
	line-height: 32px;
	font-size: 24px;
	float:left;
	position: relative;
	margin-top: 350px;
	z-index: 1000;
}
```

We can use pseudo elements to help make it pretty.

```CSS
.cr-container label:before{
	content:'';
	width: 34px;
	height: 34px;
	background: rgba(130,195,217,0.9);
	position: absolute;
	left: 50%;
	margin-left: -17px;
	border-radius: 50%;
	box-shadow: 0px 0px 0px 4px rgba(255,255,255,0.3);
	z-index:-1;
}
```

We can then use another pseudo element to create a separation between each panels.

```CSS
.cr-container label:after{
	width: 1px;
	height: 400px;
	content: '';
	background: linear-gradient(top, rgba(255,255,255,0) 0%,rgba(255,255,255,1) 100%);
	position: absolute;
	bottom: -20px;
	right: 0px;
}
```

We don't want this split to come after the fourth panel however so we can add the following to prevent this.

```CSS
.cr-container label.cr-label-img-4:after{
	width: 0px;
}
```

Now that we've taken care of the way the labels look, we can hide the inputs.

```CSS
.cr-container input{
	display: none;
}
```

When we click on an input, the respective input gets 'checked'. We can target the respective label and change it's color.

```CSS
.cr-container input.cr-selector-img-1:checked ~ label.cr-label-img-1,
.cr-container input.cr-selector-img-2:checked ~ label.cr-label-img-2,
.cr-container input.cr-selector-img-3:checked ~ label.cr-label-img-3,
.cr-container input.cr-selector-img-4:checked ~ label.cr-label-img-4{
	color: #68abc2;
}
```

We can also change the background color and box-shadow of its circle pseudo element.

```CSS
.cr-container input.cr-selector-img-1:checked ~ label.cr-label-img-1:before,
.cr-container input.cr-selector-img-2:checked ~ label.cr-label-img-2:before,
.cr-container input.cr-selector-img-3:checked ~ label.cr-label-img-3:before,
.cr-container input.cr-selector-img-4:checked ~ label.cr-label-img-4:before{
	background: #fff;
	box-shadow: 0px 0px 0px 4px rgba(104,171,194,0.6);
}
```
The container for the image panels will occupy all the width and it will be positioned absolutely. This container will be used later in order to set the background image to the currently selected image. We need to do this in order to have an image visible by default. So we’ll also add some background properties already.

```CSS
.cr-bgimg{
	width: 600px;
	height: 400px;
	position: absolute;
	left: 0px;
	top: 0px;
	z-index: 1;
	background-repeat: no-repeat;
	background-position: 0 0;
}
```

Since we have four panels/images. Each panel will be 150px (600 / 4). The panels will float left and we'll hide their overflow since we don't want them poking out of their panels.

```CSS
.cr-bgimg div{
	width: 150px;
	height: 100%;
	position: relative;
	float: left;
	overflow: hidden;
	background-repeat: no-repeat;
}
```
Each slice span will have a position of absolute and will initially be hidden by placing them our of the panel with a left of -150px.

```CSS
.cr-bgimg div span{
	position: absolute;
	width: 100%;
	height: 100%;
	top: 0px;
	left: -150px;
	z-index: 2;
	text-indent: -9000px;
}
```

Now let's our images and the respective image slices. (You can use the images included in this repo, or use your own, because of the way this is set up, it's better to use images that closely match the dimensions of the container div (600 width x 400 height). Otherwise your image may not display how you'd like and correcting the positioning may be difficult).

```CSS
.cr-container input.cr-selector-img-1:checked ~ .cr-bgimg,
.cr-bgimg div span:nth-child(1){
	background-image: url(../images/1.jpg);
}
.cr-container input.cr-selector-img-2:checked ~ .cr-bgimg,
.cr-bgimg div span:nth-child(2){
	background-image: url(../images/2.jpg);
}
.cr-container input.cr-selector-img-3:checked ~ .cr-bgimg,
.cr-bgimg div span:nth-child(3){
	background-image: url(../images/3.jpg);
}
.cr-container input.cr-selector-img-4:checked ~ .cr-bgimg,
.cr-bgimg div span:nth-child(4){
	background-image: url(../images/4.jpg);
}
```
We also need to ensure the slices show the correct portion of each image.

```CSS
.cr-bgimg div:nth-child(1) span{
	background-position: 0px 0px;
}
.cr-bgimg div:nth-child(2) span{
	background-position: -150px 0px;
}
.cr-bgimg div:nth-child(3) span{
	background-position: -300px 0px;
}
.cr-bgimg div:nth-child(4) span{
	background-position: -450px 0px;
}
```

When we click on a label we want the images to slide out to the right. We can do this with animation and keyframes.

```CSS
.cr-container input:checked ~ .cr-bgimg div span{
	animation: slideOut 0.6s ease-in-out;
}
@keyframes slideOut{
	0%{
		left: 0px;
	}
	100%{
		left: 150px;
	}
}
```

We want that to happen on all except the slices with the respective background image. Those will slide in from -150px to 0px:

```CSS
.cr-container input.cr-selector-img-1:checked ~ .cr-bgimg div span:nth-child(1),
.cr-container input.cr-selector-img-2:checked ~ .cr-bgimg div span:nth-child(2),
.cr-container input.cr-selector-img-3:checked ~ .cr-bgimg div span:nth-child(3),
.cr-container input.cr-selector-img-4:checked ~ .cr-bgimg div span:nth-child(4)
{
	transition: left 0.5s ease-in-out;
	animation: none;
	left: 0px;
	z-index: 10;
}
```

Lastly we want to style the h3 elements and their spans. We can give them a opacity transition and then once the respective label/input is checked the opacity will increase.

```CSS
.cr-titles h3{
	position: absolute;
	width: 100%;
	text-align: center;
	top: 50%;
	z-index: 10000;
	opacity: 0;
	color: #fff;
	text-shadow: 1px 1px 1px rgba(0,0,0,0.1);
	transition: opacity 0.8s ease-in-out;
}
.cr-titles h3 span:nth-child(1){
	font-family: 'BebasNeueRegular', 'Arial Narrow', Arial, sans-serif;
	font-size: 70px;
	display: block;
	letter-spacing: 7px;
}
.cr-titles h3 span:nth-child(2){
	letter-spacing: 0px;
	display: block;
	background: rgba(104,171,194,0.9);
	font-size: 14px;
	padding: 10px;
	font-style: italic;
	font-family: Cambria, Palatino, "Palatino Linotype", "Palatino LT STD", Georgia, serif;
}
.cr-container input.cr-selector-img-1:checked ~ .cr-titles h3:nth-child(1),
.cr-container input.cr-selector-img-2:checked ~ .cr-titles h3:nth-child(2),
.cr-container input.cr-selector-img-3:checked ~ .cr-titles h3:nth-child(3),
.cr-container input.cr-selector-img-4:checked ~ .cr-titles h3:nth-child(4){
	opacity: 1;
}
```
#Extra

If you don't want to use the label trick on mobile devices you could, for example, use a media query like this:

```CSS
@media screen and (max-width: 768px) {
	.cr-container input{
		display: inline;
		width: 24%;
		margin-top: 350px;
		z-index: 1000;
		position: relative;
	}
	.cr-container label{
		display: none;
	}
}
```
But this is just a quick solution.
