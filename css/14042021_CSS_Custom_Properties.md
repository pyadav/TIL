## CSS Custom Properties
CSS custom properties are prefixed with `--` like `--example-name` which can be used
using the `var()` function.
As with other CSS properties, custom properties cascade in the same way and 
are dynamic. This means they can be changed at any moment and the change is 
processed accordingly by the browser.

They can be defined
1. ### Using CSS @property rule
@property rule register a custom property in css without any JS like

```javascript
@property --my-color {
  syntax: '<color>';
  inherits: false;
  initial-value: #c0ffee;
}
```

2. ### Using JavaScript CSS.registerProperty:

```javascript
window.CSS.registerProperty({
  name: '--my-color',
  syntax: '<color>',
  inherits: false,
  initialValue: '#c0ffee',
});
```

### How to use
```javascript 
:root {
  /* Fallback for browsers without @property support. */
  --my-color: #c0ffee;
}
```

To use a variable, you have to use the var() CSS function and provide the name of the property inside:
```javascript 
.box {
  /* #c0ffee is used if --box-margin is not defined. */
  color: var(--my-color, #c0ffee);
}
```

## CSS Custom Properties Use Cases
1. ### EMULATE NON-EXISTENT CSS RULES
We just want to follow the DRY rule (don’t repeat yourself), 
so instead of repeating box-shadow’s entire value in the :hover 
section, we’ll just change its color. Custom properties to the rescue:

```javascript
.box {
  --box-shadow-color: yellow;
  box-shadow: 0 0 5px var(--box-shadow-color);
}

.test:hover {
  /* Instead of: box-shadow: 0 0 30px orange; */
  --box-shadow-color: orange;
}
```

2. ### COLOR THEMES
One of the most common use case of custom properties is for custom themes
in applications. This

```javascript
.btn {
  --color: #ffffff;
  --shadow-color: #777;
  --gradient-from-color: #3498db;
  --gradient-to-color: #2980b9;

  background-image: linear-gradient(
    to bottom,
    var(--gradient-from-color),
    var(--gradient-to-color)
  );
  box-shadow: 0px 1px 3px var(--shadow-color);
  text-shadow: 1px 1px 3px var(--shadow-color);
  color: var(--color);
}

body.dark .btn{
  --color: #000000;
  --shadow-color: #888888;
  --gradient-from-color: #CB6724;
  --gradient-to-color: #D67F46;
}
```

## Using Custom Properties With JavaScript
```javascript
/**
* Gives a CSS custom property value applied at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color');
*/
function readCssVar(element, varName){
  const elementStyles = getComputedStyle(element);
  return elementStyles.getPropertyValue(`--${varName}`).trim();
}

/**
* Writes a CSS custom property value at the element
* element {Element}
* varName {String} without '--'
*
* For example:
* readCssVar(document.querySelector('.box'), 'color', 'white');
*/
function writeCssVar(element, varName, value){
  return element.style.setProperty(`--${varName}`, value);
}
```