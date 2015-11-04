TO RUN APPLICATION:

1. Load dist/index.html in browser.
check speed in: https://developers.google.com/speed/pagespeed/insights/

note: performance improves when web server does automatic gzipping.
the same page, published on github pages will do this:
http://tifred.github.io/frontend-nanodegree-mobile-portfolio/dist/index.html

2. Load dist/views/pizza.html
Scroll.
Frame rate should be 60 fps.

3. Load dist/views/pizza.html
Use slider to resize pizzas.
Time to resize pizzas, as reported in console.log, should be less than 5ms.


OPTIMIZATIONS:

1. For dist/index.html, to achieve a PageSpeed score of 90+:

Reduced Critical Rendering Path by:

--inlining style.css file into head of index.html.
--adding media condition to css relevant to printing only.
--puting print only css in separate file that is loaded as needed.
--compressing image "profilepic.jpg".
--cropping and compressing image "views/images/pizzeria.jpg".
--moving JS from js/perfmatters.js into index.html, with async tag.
--using async tag on two scripts related to Google Analytics.
--loading fonts with script, run with async, upon document load.
--minifying index.html and css/print.css.


2. For dist/views/pizza.html, to achieve a frame rate of 60 fps:

Re-factored code in updatePositions().
Moved scrolltop calculation out of for loop to eliminate FSL upon scrolling.
Replaced querySelectorAll with getElementsByClassName, as it is faster.
Replaced "phase" variable with an array that holds all 5 possible values.
See line 526.  Look for comment "START THIRD OPTIMIZATION".

Changed document.addEventListener function to only
make 40 pizzas upon document load.
See line 572.  Look for "OPTIMIZATION FOUR".

In dist/views/css/style.css:
Added css rule "will-change: left" to .mover class.
This promoted the .mover elements to be layers, which improved performance.
No bad side effects in mobile emulation mode.

In dist/views/images:
Resized and compressed pizzeria.jpg.


3. For dist/views/pizza.html, to resize pizzas in less than 5 ms:

Re-factored code in and around changePizzaSizes(size). 
Moved determination of width outside of for loop.
Replaced querySelectorAll with getElementsByClassName, as it is faster.
See line 463.  Look for comment "START SECOND OPTIMIZATION".

Re-factored code of determineDx.
Removed parameter "elem"; added parameter "oldwidth".
Calculates oldwidth only once, rather than twice.
See line 427.  Look for comment "START FIRST OPTIMIZATION".


OTHER IMPROVEMENTS:

Using build tools from gulp to minify JS, CSS, and HTML
from src folder and automatically place them in the dist folder.

All individual tasks run by one task named "build".
See gulpfile.js.
