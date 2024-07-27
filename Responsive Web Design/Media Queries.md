#CSS #ResponsiveWebDesign #WebDesign 

A **media query** is a CSS technique using a *@media* rule to include a block of CSS properties only if a certain condition is true.

Media queries can be used to create breakpoints where certain parts of design behave differently on each side of the breakpoint.

Always design for mobile before desktop or any other device. Instead of changing styles for when width get smaller than 768px, *change design when width gets larger.*
``` CSS
[class*="col-"] {
	width: 100%;
}

@media only screen and (min-width: 768px) {
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
}
```

Can add as many breakpoints as you wish. For example, adding another query at 600px for devices larger than 600px but smaller than 768px.
``` css
@media only screen and (min-width: 600px) {
  .col-s-1 {width: 8.33%;}  
  .col-s-2 {width: 16.66%;}  
  .col-s-3 {width: 25%;}  
  .col-s-4 {width: 33.33%;}  
  .col-s-5 {width: 41.66%;}  
  .col-s-6 {width: 50%;}  
  .col-s-7 {width: 58.33%;}  
  .col-s-8 {width: 66.66%;}  
  .col-s-9 {width: 75%;}  
  .col-s-10 {width: 83.33%;}  
  .col-s-11 {width: 91.66%;}  
  .col-s-12 {width: 100%;}
}
```

Example for breakpoints and using column widths in HTML:
``` html
/* Desktop */
<div class="row">
	<div class="col-3 col-s-3">...</div>
	<div class="col-6 col-s-9">...</div>
	<div class="col-3 col-s-12">...</div>
</div>
```
For desktop, the first and third section will span 3 columns each, with the middle spanning 6 columns. For tablets, first section spans 3 columns, second spans 9 columns, and third will be displayed below the first 2 and span 12 columns.

Typical device breakpoints:
``` css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */  
@media only screen and (min-width: 992px) {...}  
  
/* Extra large devices (large laptops and desktops, 1200px and up) */  
@media only screen and (min-width: 1200px) {...}
```

Media queries can be used to change layout of a page depending on the orientation of the browser. CSS properties can apply to only a browser window wider than its height or landscape orientation.
``` css
@media only screen and (orientation: landscape) {
  body {
    background-color: lightblue;
  }
}
```

Media queries can also be used to hide elements on different screen sizes:
``` css
@media only screen and (max-width: 600px) {
  div.example {
    display: none;
  }
}
```

Font size can also vary depending on the breakpoint:
``` css
@media only screen and (min-width: 601px) {
  div.example {
    font-size: 80px;
  }
}

@media only screen and (max-width: 600px) {
  div.example {
    font-size: 30px;
  }
}
```