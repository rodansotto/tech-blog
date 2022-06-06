---
title: "Display Bootstrap’s Navbar Dropdown Menu On Hover"
date: "2015-11-19"
categories: 
  - "web-design"
---

![]({{ site.baseurl }}/assets/images/csslogo.png)

[DEMO](http://rodansotto.com/projects/css/BSNavbar_AutoDropdownOnHover.htm)

Using only 3 simple CSS rules, you can have your Bootstrap’s navbar menu dropdown display on hover seamlessly.  Below is the CSS code:

```css
/* display dropdown menu on hover
   only when navbar is not in mobile mode (hamburger menu mode) */
@media (min-width: 768px) 
{
	/* display submenu on hover */
	.dropdown:hover .dropdown-menu {
		display: block;
	}

	/* since submenu gets displayed too when dropdown menu is clicked 
		and remains displayed until dropdown menu is clicked again,
		we need to hide submenu */
	.open > .dropdown-menu {
		display: none;
	}

	/* also dropdown menu is highlighted when clicked,
		so we need to unhighlight dropdown menu */
	.navbar-default .navbar-nav > .open > a, 
	.navbar-default .navbar-nav > .open > a:focus {
		background-color: transparent;
	}
}
```

  



