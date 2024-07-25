#ResponsiveWebDesign #WebDevelopment #WebDesign 

A **viewport** is the user's visible area of a webpage. The size of it varies depending on the type of device. 

Viewport can be set using:
``` html
<meta name="viewport" content="width=device-width, initial-scale=1.0">

# width=device-width : sets width of page to follow screen-width of device
# initial-scale=1.0  : sets initial zoom level when the page is first loaded
```

To size content to the viewport: 
	1. Do NOT use large fixed width elements
	2. Do NOT let content rely on particular viewport width to render well
	3. Use CSS media queries to apply different styling for small and large screens