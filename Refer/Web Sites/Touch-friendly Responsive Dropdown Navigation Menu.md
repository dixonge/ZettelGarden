# Touch-friendly Responsive Dropdown Navigation Menu with CSS

[https://w3bits.com/css-responsive-nav-menu/](https://w3bits.com/css-responsive-nav-menu/)

In today’s world of Responsive Web design, people want every part of their website to look perfect on all the devices. One of the toughest parts that I have experienced while working with RWD is coding touch-friendly multilevel navigation menus.

**Update**: Looking for a better baseline? See [CSS-only Dropdown Menu](https://w3bits.com/css-dropdown-menu/)

With navigation menus that has many levels, you need to take care of a number of things, some important ones are:

- Adding support to show the sub-menus as hover drop-down on bigger screens (desktops)
- Making the menu to break down adaptively as per the device screen resolution
- Controlling the drop-down behavior of sub-menus on smaller screens (mobile and tablet devices)
- Changing the hover control to touch on mobile devices

Besides the above points, you are also required to keep the styles and markup as good (minimal) as possible.

A responsive hover-only menu is pretty easy thing you can do with just CSS. But how about a touch-friendly menu? With only CSS? It could be a tricky job to do.

![[Touch-friendly%20Responsive%20Dropdown%20Navigation%20Menu%20cd871d00a90c4de793da268547f76076 touch-friendly-responsive-menu.gif]]

I don’t know if there are some cool JavaScript-based solutions for this purpose, but I have a working CSS-only solution for responsive, touch-friendly multilevel navigation menus. It may not be an ideal solution to achieve that, but still I recommend you to give it a go.

I’m going to share the tutorial and the demonstration in the rest of this post. Explaining each and every bit of code is difficult, so I’ll try to cover all the important points only.

Before going any further, please check out [the menu in action](https://w3bits.com/labs/css-responsive-nav/).

## What it’s gonna take

Not a miracle, but the *Checkbox hack* that I discovered on [this article on Codrops](http://tympanus.net/codrops/2012/12/17/css-click-events/). If you know what it is, you might have already drawn a rough picture of our responsive menu idea.

The checkbox hack is all about making a click-event-kind-of-effect with just CSS. We use the `:checked` pseudo element and the sibling selector (+) to see if the checkbox is checked, then “do something” with the sibling of it. And we are going to use it for our menu.

### HTML5

I’m posting a small piece of code from the demonstration markup to ease up the explanation.

```
<nav id="menu">
  <label for="tm" id="toggle-menu">Navigation <span class="drop-icon">▾</span></label>
  <input type="checkbox" id="tm">
  <ul class="main-menu clearfix">
    <li><a href="#">Sample</a></li>
    <li><a href="#">2-level DD 
        <span class="drop-icon">▾</span>
        <label title="Toggle Drop-down" class="drop-icon" for="sm1">▾</label>
      </a>
      <input type="checkbox" id="sm1">
      <ul class="sub-menu">
        <li><a href="#">Item 2.1</a></li>
        <li><a href="#">Item 2.2
            <span class="drop-icon">▾</span>
            <label title="Toggle Drop-down" class="drop-icon" for="sm2">▾</label>
          </a>
          <input type="checkbox" id="sm2">
          <ul class="sub-menu">
            <li><a href="#">Item 2.2.1</a></li>
            <li><a href="#">Item 2.2.2</a></li>
            <li><a href="#">Item 2.2.3</a></li>
          </ul>
        </li>
        <li><a href="#">Item 3.4</a></li>
      </ul>
    </li>
    <li><a href="#">Another Sample</a></li>
  </ul></nav>
```

Above given are just some nested unordered lists (`<ul>`) inside an HTML5 `nav` element. The main thing to notice in the above code is the checkbox and label element.

The first `<ul>` in the `#menu` is the main navigation and the rest of the others are sub-menus.

The idea here is to place a checkbox above each menu and then trigger it as the sibling of the checkbox with the help of the label element (`<label for="#...` makes all our touch-friendly approach possible).

Each of our menu-items that consists of a sub-menu carries a checkbox input and a label inside it. As you may have noticed, I’m using the hyperlinks to act as the “actually accessible” menu-item here, they are stretched all over their respective list-item. I’ve placed the label inside the hyperlink to maintain the flow.

You can see two elements with the same class in the menu-items that has a sub-menu: `span.drop-icon` and `label.drop-icon`. The former is for representing that a menu-item contains a sub-menu, and the latter one acts as both the drop-down representative and the touch-trigger for the respective sub-menu on smaller screens.

I’ve used HTML entities in both the `span.drop-icon` and `label.drop-icon`; triangle pointing left ▸ (`&#9656;`) and the triangle pointing down ▾ (`&#9662;`) to show to drop icons on the menu.

The label element will be kept hidden on the desktop resolution, and will only be visible on smaller screens. The checkbox element will be hidden no matter what resolution it is, as we don’t want the user to notice that.

On top of the main navigation list, I’ve placed another trigger (`#toggle-menu`) to toggle on and off the whole menu.

I expect the above explanation have given you the rough idea of what we are doing. Lets move to the styling section.

**Note**: I’ve made use of [micro-clearfix](https://w3bits.com/clearfix/) to clear floats in the above markup.

### CSS & Magic

I tried to keep it as simple as possible, and came up with the following CSS:

```
#menu ul {
  margin: 0;
  padding: 0;}#menu .main-menu {
  display: none;}#tm:checked + .main-menu {
  display: block;}#menu input[type="checkbox"], #menu ul span.drop-icon {
  display: none;}#menu li, #toggle-menu, #menu .sub-menu {
  border-style: solid;
  border-color: rgba(0, 0, 0, .05);}#menu li, #toggle-menu {
  border-width: 0 0 1px;}#menu .sub-menu {
  background-color: #444;
  border-width: 1px 1px 0;
  margin: 0 1em;}#menu .sub-menu li:last-child {
  border-width: 0;}#menu li, #toggle-menu, #menu a {
  position: relative;
  display: block;
  color: white;
  text-shadow: 1px 1px 0 rgba(0, 0, 0, .125);}#menu, #toggle-menu {
  background-color: #09c;}#toggle-menu, #menu a {
  padding: 1em 1.5em;}#menu a {
  transition: all .125s ease-in-out;
  -webkit-transition: all .125s ease-in-out;}#menu a:hover {
  background-color: white;
  color: #09c;}#menu .sub-menu {
  display: none;}#menu input[type="checkbox"]:checked + .sub-menu {
  display: block;}#menu .sub-menu a:hover {
  color: #444;}#toggle-menu .drop-icon, #menu li label.drop-icon {
  position: absolute;
  right: 1.5em;
  top: 1.25em;}#menu label.drop-icon, #toggle-menu span.drop-icon {
  border-radius: 50%;
  width: 1em;
  height: 1em;
  text-align: center;
  background-color: rgba(0, 0, 0, .125);
  text-shadow: 0 0 0 transparent;
  color: rgba(255, 255, 255, .75);}#menu .drop-icon {
  line-height: 1;}
```

Starting off with the styling, I’ve used mobile-first approach to code it down. All of menu-items are stretched to fit available screen, the sub-menus are given some horizontal margin and different background to appear distinct from the menu-items.

`span.drop-icon` is set to hidden for the mobile view and the label element is visible. I’ve styled them both to look exactly what they are meant for.

Implementing the checkbox hack, I’ve checked each of our checkbox inputs with `:checked`, and then with the sibling selector (+), the display of our sub-menus has been controlled.

Next part completes our menu.

### For Responsive & Touch-friendly behavior

This section covers how our menu looks on different screen resolutions. For desktops, I’ve unset the checkbox hack as I wanted to display the sub-menus on hover on desktops. The list-items in the main nav are floated left to create a horizontal list.

List-items are relatively-positioned, the sub-menus inside them are absolute positioned, and are adjusted according to their levels.

`label.drop-icon` is hidden here, and `span.drop-icon` is visible as we don’t need triggers to control the checkbox on desktops.

The menu-items get an equal width (33.33%) at a certain resolution to avoid any collapsed view.

```
@media only screen and (max-width: 64em) and (min-width: 52.01em) {
  #menu li {
    width: 33.333%;
  }

  #menu .sub-menu li {
    width: auto;
  }}@media only screen and (min-width: 52em) {
  #menu .main-menu {
    display: block;
  }

  #toggle-menu, 
  #menu label.drop-icon {
    display: none;
  }

  #menu ul span.drop-icon {
    display: inline-block;
  }

  #menu li {
    float: left;
    border-width: 0 1px 0 0;
  }

  #menu .sub-menu li {
    float: none;
  }

  #menu .sub-menu {
    border-width: 0;
    margin: 0;
    position: absolute;
    top: 100%;
    left: 0;
    width: 12em;
    z-index: 3000;
  }

  #menu .sub-menu, 
  #menu input[type="checkbox"]:checked + .sub-menu {
    display: none;
  }

  #menu .sub-menu li {
    border-width: 0 0 1px;
  }

  #menu .sub-menu .sub-menu {
    top: 0;
    left: 100%;
  }

  #menu li:hover > input[type="checkbox"] + .sub-menu {
    display: block;
  }}
```

The menu is ready now!

That’s it. I guess it has gone a bit lengthy, hope it has explained it well.

Let me know if you liked this menu, or if you’ve noticed something not working, or any other thoughts you have in mind, please use the comments section to have the say.