title: The PayPal Logo Challenge
date: 2014-09-20 14:19:01
tags: ['html5', 'canvas', 'javascript']
---

Recently, I came across [an interesting blog post](https://www.paypal-engineering.com/2014/09/04/the-paypal-logo-challenge-one-solution-pseudo-elements/ 'this blog post') in PayPal Engineering blog site. It was an article about how the author curated a solution to generate PayPal's logo using just CSS3. One thing that kept me thinking was that the author at the end of the post, challenges and wishes to see other CSS based implementations of the PayPal logo. I, being a JavaScript enthusiast, decided to take up the challenge and implement the same using JavaScript!

#### How was it done?

The evolution of HTML5 gave us the super powerful HTML element Canvas and a set of JavaScript APIs to draw and manipulate graphic contexts. This proved the web could do many powerful things than just displaying a bunch of text and images. I am going to use the 2D Context Rendering APIs to draw the PayPal logo onto a Canvas.

_Step 1: Define the Canvas element into which the logo will be drawn._
```html
	<canvas id='paypal-logo' width='300' height='300'></canvas>
```

_Step 2: In JavaScript, start grabbing a 2D render context reference to the same canvas element._
```javascript
var canvas = document.getElementById('paypal-logo');
var ctx = canvas.getContext('2d');
```

_Step 3: Define some values to characterize the appearance of 'P'. I break down the letter 'P' into two parts and call the top part as 'Head' and the bottom part as 'Leg'._
```javascript
// define size 
// (some number which can be used to relatively scale up/down the 'P')
var size = 100;
// define the start point co-ordinates in the canvas 2d space.
var x = 20;
var y = 20;
// characteristic definitions for the appearance of Letter 'P'
var cornerRadius = 4;
var height = y + size;
var legWidth = x + size * 0.26;
var legHeight = height - size * 0.4;
var headWidth = legWidth + size * 0.60;
var headHeight = height - legHeight;
var topHeadProjection = legWidth + size * 0.23;
var bottomHeadCurveOffset = y + size * 0.22;
```

_Step 4: Now, I will start to draw the letter 'P' on the canvas context._
```javascript
// begin the path trace on the given context
ctx.beginPath();
// init the cursor to 
// start drawing head of 'P'
ctx.moveTo(x, y+cornerRadius);
// draw the top left curved corner and the top of
// 'P' till it starts to curve down.
ctx.quadraticCurveTo(x, y, x+cornerRadius, y);
ctx.lineTo(topHeadProjection, y);
// draw the curved Head portion of 'P'
ctx.bezierCurveTo(headWidth,y, 
        headWidth - 2*cornerRadius, headHeight + bottomHeadCurveOffset, 
        legWidth+ 2*cornerRadius,legHeight); 
// draw the right side of the leg and the 
// curved potion that connects
// this leg to the Head of 'P'
ctx.quadraticCurveTo(legWidth, legHeight, legWidth, legHeight+cornerRadius);
ctx.lineTo(legWidth, height-cornerRadius);
// draw the bottom potion of the leg and 
// the bottom two rounded corners
// for the leg of 'P'
ctx.quadraticCurveTo(legWidth, height, legWidth-cornerRadius, height);
ctx.lineTo(x+cornerRadius, height);
ctx.quadraticCurveTo(x, height, x, height-cornerRadius);
// finish by drawing the left side of the 'P'
ctx.lineTo(x, y+cornerRadius);
```

<p class='explanation'>
	sketch explaining the drawing

	<img src='/assets/paypal_logo_canvas_grid.png' alt='sketch explaining the drawing'/>
</p>

_Step 5: Color the drawn surface._
```javascript
// light colored 'P' in the PayPal Logo
var color = 'rgba(23,155,215,1)';
// stroke and fill the drawn path with the supplied color
ctx.fillStyle = color;
ctx.fill(); 
ctx.strokeStyle = color;
ctx.lineWidth = 1;
ctx.stroke();
```

<p class='explanation'>
	colored sketch

	<img src='/assets/pplogo_half.png' alt='colored sketch'/>
</p>

_Step 6: Next, repeat the same code above and draw another 'P' with a little offset so that it overlays on the existing drawing and fill it with a darker shade of blue._

_Step7: Finally, skew the canvas horizontally so that the logo appears a bit tilted._
```javascript
ctx.transform(1, 0, Math.sin(-0.1), 1, 0, 0);
```

<p class='explanation'>
	The finished canvas drawing looks like the below image

	<img src='/assets/pplogo_finished.png' alt='final appearance of the canvas after drawing'/>
</p>



#### Conclusion
I accomplished the challenge that I started within myself and published it as a reusable library here: https://github.com/samsel/paypal-logo-canvas. A working example of the library can be found here: http://jsfiddle.net/samsel/unqrods8/3/.

While executing this challenge, I was really overwhelmed by the power of the canvas element plus its associated JavaScript API. I wish we embrace the web more and push it to its limits!