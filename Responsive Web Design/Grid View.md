#GridView #ResponsiveWebDesign #WebDesign 

A **grid view** means that a page is divided into columns. This is helpful for designing since it makes placing elements easier. Grid-view often has *12 columns* and a width of *100%* that shrink and expand as you resize.

All HTML elements need to have **box-sizing** property set to border-box to ensure that padding and border are included in the total width and height of the elements. 
``` CSS
* {
	box-sizing: border-box;
}
```

CSS styling such as the one below creates a simple responsive page with 2 columns.
``` CSS
.menu {
	width: 25%;
	float: left;
}

.main {
	width: 75%;
	float: left;
}
```

In a RWD grid-view since there are 12 columns and a width of 100%, then each column accounts for **8.33%**.
``` CSS
.col-1 {width: 8.33%;}  
.col-2 {width: 16.66%;}  
.col-3 {width: 25%;}  
.col-4 {width: 33.33%;}  
.col-5 {width: 41.66%;}  
.col-6 {width: 50%;}  
.col-7 {width: 58.33%;}  
.col-8 {width: 66.66%;}  
.col-9 {width: 75%;}  
.col-10 {width: 83.33%;}  
.col-11 {width: 91.66%;}  
.col-12 {width: 100%;}

[class*="col-"] {
	float: left;
	padding: 15px;
	border: 1px solid red;
}
```

Each row should be wrapped in a div and the # of columns inside a row should always add up to 12.
``` HTML
<div class="row">
	<div class="col-3"> ... </div> <!-- 25% -->
	<div class="col-9"> ... </div> <!-- 75% -->
</div>
```