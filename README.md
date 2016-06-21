# Website Performance Optimization
___
### Udacity Frontend Nanodegree - Project 4


## Getting Started:

1.  Clone or pull repository
2.  Open index.html in your browser.
3.  To check PageSpeed Insights score:

  1.
  ```
  bash:
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```
  2.  Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  3.  (In a seperate terminal window/tab):
  ```
  bash:
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```
  4.  Copy the link provided by ngrok into the textbox at [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)

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
## Optimizations made to main.js

- Changed `changePizzaSizes` function:
  - Moved local variable assignments `dx` and `newwidth` outside of the `for loop`
    - Changed their `querySelectorAll` selectors to `querySelector`
  - Assigned new variable `randomPizzaCount` to the total number of `.randomPizzaContainer` elements
    -  This took stress off the `for loop`, which had previously called `querySelectorAll.length` on `.randomPizzaContainer` each loop cycle
- Changed `UpdatePositions` function:
  - Restructured the `phase` variable declaration
    - Created new variable `ScrollNum` outside of the `for loop`
    - Assigned it to `... .scrollTop /1250`
      - This removed the calculation from being called within the `for loop`
- Changed `addEventListener` function @line 536:
  - Changed the `for loop` interations from `200` to `20`
    - There were way too many pizza images floating around that the user couldn't see
  - Changed the `cols` variable from `8` to `4`
    - The additional columns were offscreen

___
## Results:

1. index.html has a PageSpeed Insight score of 95/100.
2. pizza.html scrolls at ~60 fps
3. pizza.html's `#sizeSlider` changes all pizza images in less than 5ms
