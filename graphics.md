# HTML Graphics

### HTML SVG
- [HTML SVG Tutorial on w3schools](https://www.w3schools.com/graphics/svg_intro.asp)

- SVG (Scalable Vector Graphics) defines vector-based graphics in XML format
  - every element and attribute in SVG files can be animated
- Advantages of SVG
  - scalable
  - zoomable
  - can be printed with high quality at any resolution
  - can be searched, indexed, scripted, compressed

- SVG Shapes
  1. Rectable `<rect>`
    - CSS properties : `fill`, `stroke`, `stroke-width`, `fill-opacity`, `stroke-opacity`, `opacity` (range 0 to 1), 
    - attributes : `x`, `y` (left top : (0, 0)), `rx`, `ry` (rounds the corners of the rectangle)
    ```html
    <svg width="400" height="110">
      <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
    </svg>
    ```
  
  2. Circle <circle>
    - `cx`, `cy` : define the x, y coordinates of the center of the circle (default : (0, 0))
    - `r` : radius of the circle
    ```html
    <svg height="100" width="100">
      <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
    </svg>
    ```

  3. Ellipse <ellipse>
    - create an ellipse 
    - difference between ellipse and circle : ellipse has an x, y radius that diffeers from each other, while a circle has equal x, y radius
    ```html
    <!-- 3 ellipses on top of each other -->
    <svg height="150" width="500">
      <ellipse cx="240" cy="100" rx="220" ry="30" style="fill:purple" />
      <ellipse cx="220" cy="70" rx="190" ry="20" style="fill:lime" />
      <ellipse cx="210" cy="45" rx="170" ry="15" style="fill:yellow" />
    </svg>
    ```

  4. Line <line>
    - `x1`, `y1` : defines the start of the line on the x-axis and y-axis respectively
    - `x2`, `y2`: defines the end of the line
    - from (x1, y1) to (x2, y2)
    ```html
    <svg height="210" width="500">
      <line x1="0" y1="0" x2="200" y2="200" style="stroke:rgb(255,0,0);stroke-width:2" />
    </svg>
    ```

  5. Polyline <polyline>
    - 
  
  6. Polygon <polygon>
    - create a graphic that contains at least three sides // made of straight lines, and the shape is "closed" (all the lines connect up)
    - `points` : defines the x, y coordinates for each corner
    ```html
    <svg height="210" width="500">
      <polygon points="200,10 250,190 160,210" style="fill:lime;stroke:purple;stroke-width:1" />
    </svg>
    ```


  7. Path <path>

### HTML Canvas
- [HTML Canvas Tutorial on w3schools](https://www.w3schools.com/graphics/canvas_intro.asp)

- HTML `<canvas>` : a part of the document object model (DOM)
  - must have an `id` attributes so it can be referred to by JS
  - `width`, `height` attributes is necessary to define the size of the canvas
  - has no border and no content

- HTML Canvas Drawing
  1. Step 1: find the canvas element using the HTML DOM method `getElementById()`
  2. Step 2: create a drawing object with `getContext()`
    - `getContext()` is a built-in HTML object, with properties and methods for drawing
  3. Step 3: Draw on the canvas and set the fill style of the drawing object to any color
    - `fillStyle` property can be a CSS color, a gradient, or a pattern (the default is black)
    - `fillRect(x, y, width, height)` method draws a rectangle filled with the fill style on the canvas
  ```js
  var canvas = document.getElementById("myCanvas");
  var ctx = canvas.getContext("2d");
  ctx.fillStyle = "#FF0000";
  ctx.fillRect(0, 0, 150, 75); // start at the upper-left corner (0,0) and draw a 150x75 pixels rectangle
  ```

- HTML Canvas Coordinates
  - The HTML canvas is a two-dimensional grid.
  - The upper-left corner of the canvas has the coordinates (0,0)

- Draw a Line
  - `moveTo(x,y)` defines the starting point of the line
  - `lineTo(x,y)` defines the ending point of the line
  - `stroke()` : one of the ink methods

- Draw a Circle
  - `beginPath()` begins a path
  - `arc(x,y,r,startanle,endanle)` creates an arc/curve
    - Set start angle to 0 and end angle to 2*Math.PI
    - The r parameter defines the radius of the circle
  ```js
  var canvas = document.getElementById("myCanvas");
  var ctx = canvas.getContext("2d");
  ctx.beginPath();
  ctx.arc(95, 50, 40, 0, 2 * Math.PI); // x-, y- coordinates of the center of the circle // r defines the radius of the circle
  ctx.stroke();
  ```

- Canvas gradients
  - Gradients can be used to fill rectangles, circles, lines, text, etc.
  - Shapes on the canvas are not limited to solid colors.
    - `createLinearGradient(x,y,x1,y1)` creates a linear gradient
    - `createRadialGradient(x,y,r,x1,y1,r1)` creates a radial/circular gradient
  - Once we have a gradient object, must add two or more color stops.
    - `addColorStop()` specifies the color stops, and its position along the gradient
    - gradient positions can be anywhere between 0 to 1
  ```js
  var c = document.getElementById("myCanvas");
  var ctx = c.getContext("2d");

  // Create gradient
  var grd = ctx.createLinearGradient(0, 0, 200, 0);
  // var grd = ctx.createRadialGradient(75, 50, 5, 90, 60, 100); //for radial gradient
  grd.addColorStop(0, "red");
  grd.addColorStop(1, "white");

  // Fill with gradient
  ctx.fillStyle = grd;
  ctx.fillRect(10, 10, 150, 80);
  ```

- HTML Canvas Text
  - `font` defines the font properties for the text
  - `fillText(text,x,y)` draws filled text on the canvas
  - `strokeText(test,x,y)` draws text on the canvas (no fill)
  ```js
  var canvas = document.getElementById("myCanvas");
  var ctx = canvas.getContext("2d");
  ctx.font = "30px Arial";
  ctx.fillStyle = "red"; // wirte a filled red text
  ctx.textAlign = "center";
  ctx.fillText("Hello World", 10, 50);
  // ctx.strokeText("Hello World", 10, 50); // text with no fill
  ```

- HTML Canvas Images
  - `drawImage(image,x,y)` : define image first and draw it on the canvas
  ```js
  window.onload = function() {
    var canvas = document.getElementById("myCanvas");
    var ctx = canvas.getContext("2d");
    var img = document.getElementById("scream");
    ctx.drawImage(img, 10, 10);
  };
  ```