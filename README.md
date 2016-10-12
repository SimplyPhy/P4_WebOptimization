# Website Performance Optimization

___
### Udacity Frontend Nanodegree - Project 4
    
**Notes**:  
- Because of the way Udacity's performance algorithms are implemented, this project isn't supported on Safari.
- Click on the link to "Cam's Pizzaria" to see the page where most of the performance enhancements were implemented.  
  
The site is available to view [here](https://simplyphy.github.io/P4_WebOptimization/).

___
## Optimizations made to index.html

- Minified HTML and CSS
- Inlined CSS styles
- Replaced web font link with web font loader
- Resized pizzeria.png to 256px width (1/8th original)
- Optimized all images using [Image Optim](https://imageoptim.com/mac)
- Changed analytics code to run asynchronously
- Added a media query to the print-only stylesheet

___
## Optimizations made to views/css/style.css

- Added `transform: translateZ(0)` and `backface-visibility: hidden` to `.mover`
  - These will automatically set hardware acceleration on for CSS in many environments

___
## Optimizations made to views/js/main.js

- Changed multiple `querySelector` and `querySelectorAll` methods to the equivalent `getElementById` and `getElementsByClassName` where applicable
  - These methods are faster
- Changed `changePizzaSizes` function:
  - Moved local variable assignments `dx` and `newwidth` outside of the `for loop`
  - Assigned new variable `randomPizzaCount` to the total number of `.randomPizzaContainer` elements
    -  This took stress off the `for loop`, which had previously called `querySelectorAll.length` on `.randomPizzaContainer` each loop cycle
- Initialized `randomPizzaCountainer` variable to store an array of its corresponding class elements
  - Used this variable's zero index value inside `dx` and `newwidth` function calls to avoid unnecessary DOM searches by the browser
- Initialized `pizzaBox` variable outside of `changePizzaSizes`'s `for loop` and assigned it to an array containing all `randomPizzaCountainer` elements
  - Called `pizzaBox` inside of the `for loop` to avoid unnecessary DOM searches by the browser
- Moved `pizzaDiv` variable initialization outside of the `for loop` where it had originally been, thereby having the browser only search the DOM once 
- Changed `UpdatePositions` function:
  - Instantiated `items.length` as `len` variable during the `for loop` initialization
    - This prevents repeat `.length` calculations from running unnecessarily
  - Restructured the `phase` variable declaration
    - Instantiated it as an empty variable outside of the `for loop`
      - This prevents the variable from being recreated each loop cycle
    - Created new variable `ScrollNum` outside of the `for loop`
    - Assigned it to `... .scrollTop /1250`
      - This removed the calculation from being called within the `for loop`
- Changed `addEventListener` function @line 536:
  - Changed the `for loop` interations from `200` to `24`
    - There were way too many pizza images floating around that the user couldn't see

___
## Results:

1. index.html has a PageSpeed Insight score of 95/100.
2. pizza.html scrolls at ~60 fps
3. pizza.html's `#sizeSlider` changes all pizza images in less than 5ms
4. CSS hardware acceleration will be activated when available

___
## My Original Workflow:
(Now I would use gulp with browsersync and gh-pages for pagespeed testing)

  1. Create a simple HTTP server.

    ```
    bash:
    $> cd /path/to/your-project-folder
    $> python -m SimpleHTTPServer 8080
    ```

  2. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  3. (In a seperate terminal window/tab):  

    ```
    bash:
    $> cd /path/to/your-project-folder
    $> ./ngrok http 8080
    ```

  4. Copy the link provided by ngrok into the textbox at [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
