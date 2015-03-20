***Website Performance Optimization portfolio project***

A.	PageSpeed
Changes made to the index.html file to achieve a 90 or above score in PageSpeed Insights:
1) Optimize the JS script - external scripts were asynchronously ("async") executed to eliminate render-blocking
                          - inline script was repositioned after the external scripts to allow for parallel downloading
2) Optimize the CSS script - inline the small CSS (style.css) file in the index.html.
			   - inline the portion of the font CSS used by the HTML and remove the link to the CSS file
			     "<link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">", 
			     again to eliminate render-blocking.
3) Optimize Image - set the width and height attributes
                  - compress or resize the image
                  
To further optimize the web performance, the following can be done on the file with a reliable tool:
4) Minify - to eliminate any unnecessary characters in the code (I don't have a reliable tool at this time).

B.	Optimize Frames per Second and Time to resize
Changes made to views/js/main.js:
DOM elements which were being retrieved or used in calculations inside a loop were moved outside of the for loop.

line 451-461:
	//retrieve the randomPizzaContainer element and calculate the new width one time,
	//there is no need to retrieve/calculate it for each element in the for loop.
	var rPC = document.querySelectorAll(".randomPizzaContainer");
	var dx = determineDx(rPC[0], size);
	var newwidth = (rPC[0].offsetWidth + dx) + 'px';
	// Iterates through pizza elements on the page and changes their widths
	function changePizzaSizes(size) {
		for (var i = 0; i < rPC.length; i++) {
			rPC[i].style.width = newwidth;
			}
	}

line 474-479	
	//retrieve the element once, there is no need to retrieve it for each element in the for loop.
	var pizzasDiv = document.getElementById("randomPizzas");
	// This for-loop actually creates and appends all of the pizzas when the page loads
	for (var i = 2; i < 100; i++) {
		pizzasDiv.appendChild(pizzaElementGenerator(i));
	}

line 511-516
	//retrieve the element once, there is no need to retrieve it for each element in the for loop.
	var scrTop = document.body.scrollTop;
	for (var i = 0; i < items.length; i++) {
		var phase = Math.sin((scrTop / 1250) + (i % 5));
		items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
	}

