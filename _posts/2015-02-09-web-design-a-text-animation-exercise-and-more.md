---
title: "Web Design: A Text Animation Exercise and More"
date: "2015-02-09"
categories: 
  - "web-design"
---

With CSS3 transitions you can animate text as well as other elements in your web page without any JavaScript.  See my demo at [http://rodansotto.com/projects/css/TransitionIAmTitanium.html](http://rodansotto.com/projects/css/TransitionIAmTitanium.html "http://rodansotto.com/projects/css/TransitionIAmTitanium.html") (_just move mouse to center box to animate text and outside box to return to original state_).  In there I am also using a custom web font using CSS3 rule @font-face, HSL (or HSLA) to define color rather than using hex or RGB, text shadow, box shadow, radial gradient, repeating linear gradient, and viewport width and height to dynamically size my text and the other elements in the page.  Most of these CSS3 features may not be implemented yet in some browser versions but I tested this in Chrome and IE 11 and it works.  Below is the CSS code:

\[code language="csharp" light="true"\] /\* see https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face using web font from fontspring.com for more free web fonts, go to http://www.fontsquirrel.com/ \*/ @font-face { font-family: 'linottesemibold'; src: url('./fonts/Linotte-SemiBold-webfont.eot'); src: url('./fonts/Linotte-SemiBold-webfont.eot?#iefix') format('embedded-opentype'), url('./fonts/Linotte-SemiBold-webfont.woff2') format('woff2'), url('./fonts/Linotte-SemiBold-webfont.woff') format('woff'), url('./fonts/Linotte-SemiBold-webfont.ttf') format('truetype'), url('./fonts/Linotte-SemiBold-webfont.svg#linottesemibold') format('svg'); font-weight: normal; font-style: normal; }

body { /\* fallback for browsers not supporting radial-gradient, like IE 9 and below \*/ background-color: hsl(210, 30%, 90%); /\* see https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient \*/ background: radial-gradient(ellipse farthest-corner, white 70%, hsl(210, 30%, 80%) 100%); }

.container { /\* using viewport width vw and height vh, see https://developer.mozilla.org/en/docs/Web/CSS/length \*/ /\* with IE 9 and probably below too, they seem to have a much larger viewport width and height \*/ width: 90vw; margin-left: 5vw; height: 84vh; margin-top: 8vh; /\* fallback for browsers not supporting linear-gradient or repeating-linear-gradient, like IE 9 and below \*/ background-color: hsl(0, 0%, 62.5%); /\* see https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient \*/ background: linear-gradient(135deg, hsl(0, 0%, 25%), white 50%, hsl(0, 0%, 25%)); /\* see https://developer.mozilla.org/en-US/docs/Web/CSS/repeating-linear-gradient \*/ background: repeating-linear-gradient(to right, hsl(0, 0%, 25%) 0%, white 10%, hsl(0, 0%, 25%) 20%); border-radius: 2vw;

/\* see https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow \*/ box-shadow: 2vw 2vh 5vw 0vw black; /\*border: 1px solid red;\*/ }

.word { padding-top: 2vh; padding-left: 32vw; /\* see https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Using\_CSS\_transitions \*/ transition: all 2s ease-out; /\*border: 1px solid red;\*/ }

.container:hover .word { padding-top: 50vh; padding-left: 10vw; }

.letter { display: inline-block; font-family: 'linottesemibold' , Arial, Sans-Serif; /\* using viewport sized typography, see https://developer.mozilla.org/en/docs/Web/CSS/length \*/ font-size: 6vw; color: #262626; /\* hex \*/ color: rgb(38, 38, 38); /\* RGB \*/ color: rgba(38, 38, 38, 1); /\* RGB with alpha transparency channel \*/ /\* Alpha transparency channel - decimal value 0 for completely transparent 1 for completely opaque \*/ /\* see HSL color wheel: http://www.erinsowards.com/articles/2011/01/graphics/hsl-colors.png see HSL color picker: http://hslpicker.com/, it shows RGBA and hex too \*/ color: hsl(0, 0%, 15%); /\* HSL \*/ /\* HSL 1st value: hue color 2nd value: saturation (%) - higher for colorful appearance (not grayish-looking) 3rd value: lightnexx (%) - 0% for black, 100% for white \*/ color: hsla(0, 0%, 0%, 1); /\* HSL with alpha \*/

/\* see https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow \*/ text-shadow: hsla(0, 0%, 0%, 0.5) 0.5vw 0.5vh 0.5vw;

/\* see https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Using\_CSS\_transitions \*/ transition: all 1s ease-in 1s;

/\*border: 1px solid red;\*/ }

.letter\_i { transition: all 2s ease-out 0s; }

.letter\_am { transition: all 1.5s ease-out 0.5s; }

.container:hover .letter { font-size: 16vw; color: hsla(240, 100%, 50%, 1); /\* blue \*/ text-shadow: hsla(0, 0%, 0%, 0.5) 1vw 1vh 0.5vw; }

.container:hover .letter\_i { color: hsla(0, 100%, 50%, 1); /\* red \*/ }

.container:hover .letter\_am { color: hsla(120, 100%, 50%, 1); /\* green \*/ } \[/code\]
