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

