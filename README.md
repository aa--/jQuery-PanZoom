# Summary #

Pan and zoom an image within a parent div. Plugin can also read/write the co-ordinates of the image within the parent div to/from a (probably hidden) form field for easy integration into your own projects.

Live example available at: [http://benlumley.co.uk/dev/panzoom/example/index.html](http://benlumley.co.uk/dev/panzoom/example/index.html)

# Licence #

Copyright (c) 2011 Ben Lumley  
Examples and documentation at: https://github.com/benlumley/jQuery-PanZoom  

Dual licensed under the MIT and GPL licenses:  
 http://www.opensource.org/licenses/mit-license.php  
 http://www.gnu.org/licenses/gpl.html

# Usage #

In addition to this documentation, a working example showing all options is available from the github repository linked above.

Include jquery and the plugin's js files.

    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js"></script>
    <script type="text/javascript" src="/js/jquery-panzoom-0.9.0.js"></script>

First, you need a div with a width and height specified, and inside that place the image. This becomes the area within which your image can be panned and zoomed. Create html thats something like this:

    <div id="pan" style="width: 200px; height: 300px;">
      <img src="/images/myimage.jpg" >
    </div>

Then initialise the plugin by calling (best to use $(document).ready() for this, as in the eg):

    $(document).ready(function () {
    	$('#pan img').panZoom(options);
    });

You need to pass some options for the plugin to do anything - see below. So a working example might be (see below for an explanation of options):

    $(document).ready(function () {
    	$('#pan img').panZoom({
    	  'zoomIn'   	: 	$('#zoomin'),
    	  'zoomOut' 	: 	$('#zoomout'),
    	  'panUp'		  :		$('#panup'),
    	  'panDown'		:		$('#pandown'),
    	  'panLeft'		:		$('#panleft'),
    	  'panRight'	:		$('#panright'),
    	  'fit'       :   $('#fit')
    	});
    });

# A Note On How PanZoom Handles Co Ordinates #

The plugin stores and outputs the position of the top left corner of the image and the bottom right corner. The top left is x1,y1, the bottom right is x2,y2 and is equivalent to x1+width, y2+height.

# Options #

Where appropriate, defaults are given in brackets.

### zoomIn, zoomOut, panUp,  panDown, panLeft, panRight,

Pass a (different) jQuery dom node in to each of these options, the relevant action will be bound to the click event of that element. EG: 

    { zoomIn: $('#zoomIn') }. 

If you don't pass in at least one of these options, the plugin won't be able to do anything.

### fit

Pass in a jQuery dom node to bind the fit action to. This can be thought of as a reset button, it will center the image within the div and size it as large as possible within the div.

### out\_x1, out\_y1, out\_x2, out\_y2

Pass in jQuery dom nodes for the form elements to read/write the position of the image from. The plugin will initialise using the values in these fields if valid.

### zoom\_step, pan\_step (5, 5)

Percentage of the image's dimensions to zoom/pan at once when the controls are clicked. In short, increase to make the plugin zoom/pan in larger steps, and vice versa

### min\_width, min\_height (20, 20)

The width/height of the image (according to the output co-ordinates) can't be less than the respective value here.

### debug

The plugin will console.log the current co-ordinates. Beware, will break things if console.log isn't available in your browser.

### directedit (false)

Boolean. If true, the form will monitor the form fields passed in to out_x1 etc for changes and will update the image accordingly. Probably best used with form fields that aren't hidden :) 

### aspect (true)

boolean, whether the plugin should keep the original aspect ratio (length/width) of the source image.

### factor (1)

Pass a number in here if you wish to have the plugin scale up/down the values used in the form fields relative to the actual pixel offsets of the image within the div.

### animate (true)

Boolean - whether to animate the zoom in/out, pan actions, or just change them. (jQuery's css method or animate method). For animate, see following two options.

NB: Animate doesn't start until the plugin has initialised the first image properly, as doing so lets the user see the initial image shrinking etc, rather than it appearing instant. 

### animate\_duration (200)

If animate\_enabled is true, duration for the animations  - passed directly into jQuery's animate method.

### animate\_easing (linear)

If animate\_enabled is true, easing method for the animations  - passed directly into jQuery's animate method.

### double_click (true)

Boolean - whether double clicking the image should trigger zoom in.

### mousewheel

Boolean - whether to enable mousewheel to zoom or not. Requires mousewheel from jquery tools - http://flowplayer.org/tools/toolbox/mousewheel.html

### mousewheel_delta (1)

Amount of mousewheel movement thats equivalent to one click of the zoom button. Be warned that this seems to be influenced by browser choice as well as people's settings for their mousewheel in their operating system.

### draggable (true)

Should the image be made "draggable"? Requires jQuery UI - http://jqueryui.com/

# Methods #

// todo :(

# Tips #

## Swapping the image ##

A load event is bound to the image when the plugin is initialised, so if you swap the image via something like

    $('#pan img').attr('src', '/someimage.png');

the plugin will automatically fit the new image to the box once it loads.

## Manually setting image position ##

You can manually change the image position using something like:

    // retrieve the current position
    data = $('#pan img').data('panZoom');

    // set the four co-ordinates
    data.position.x1 = 10;
    data.position.y1 = 10;
    data.position.x2 = 50;
    data.position.y2 = 50;

    // write out the position
    $('#pan img').panZoom('updatePosition');
    
(yes, a utility method for this would be nicer/cleaner. Its on the list!)

## Feature Wishlist

Few extra utility methods  
Rotation (supported browsers only)  
Draggable snap
Moz hand draggy cursor
Fix diving to corner as you zoom out past limits


