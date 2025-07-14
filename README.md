## 🚀 SocialExplorer Fork

[![Fork Status](https://img.shields.io/badge/Fork-SocialExplorer-brightgreen.svg)](https://github.com/SocialExplorer) [![Enhanced Features](https://img.shields.io/badge/Enhanced-Parent%20Selection%20%7C%20CommonJS%20%7C%20AMD-blue.svg)](#)

**Enhanced LeaderLine with additional features:**
- ✨ Support for selecting parent elements
- 📦 CommonJS module support
- 🔧 AMD imports compatibility

---

# LeaderLine

[![npm](https://img.shields.io/npm/v/leader-line.svg)](https://www.npmjs.com/package/leader-line) [![GitHub issues](https://img.shields.io/github/issues/anseki/leader-line.svg)](https://github.com/anseki/leader-line/issues) [![dependencies](https://img.shields.io/badge/dependencies-No%20dependency-brightgreen.svg)](package.json) [![license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Draw a leader line in your web page.

**<a href="https://anseki.github.io/leader-line/">Document and Examples https://anseki.github.io/leader-line/</a>**

```html
<div id="start">start</div>
<div id="end">end</div>
```

```js
// Add new leader line from `start` to `end` (HTML/SVG element, basically).
new LeaderLine(
  document.getElementById('start'),
  document.getElementById('end')
);
```

[![ex-010](img/ex-010.png)](https://anseki.github.io/leader-line/)

It supports options to customize.

[![ex-020](img/ex-020.gif)](https://anseki.github.io/leader-line/)

Basically, it can indicate HTML/SVG element such as `<div>`, `<button>`, `<ul>`, `<td>`, `<circle>`, `<text>`, etc.

[![ex-021](img/ex-021.png)](https://anseki.github.io/leader-line/)

It can indicate a part of an element also instead of the element.

[![ex-030](img/ex-030.png)](https://anseki.github.io/leader-line/)

[![ex-031](img/ex-031.png)](https://anseki.github.io/leader-line/)

Also, it can indicate an element of another library.  
For example, the following uses LeaderLine with [D3.js](https://d3js.org/). Move the mouse on the list.

[![ex-040](img/ex-040.gif)](https://anseki.github.io/leader-line/)

## Usage

Load LeaderLine into your web page.

```html
<script src="leader-line.min.js"></script>
```

Pass two HTML/SVG elements to `LeaderLine` constructor. Then a leader line is drawn between those elements.

```js
new LeaderLine(
  document.getElementById('element-1'),
  document.getElementById('element-2')
);
```

[![ex-050](img/ex-050.png)](https://anseki.github.io/leader-line/)

Any element that has bounding-box is accepted. For example, `<div>`, `<button>`, `<ul>`, `<td>`, `<circle>`, `<text>`, and also, elements in another window (i.e. `<iframe>`). (See [`start` and `end`](#start-end) option.)

And, the constructor accepts options.

```js
var startElement = document.getElementById('element-1'),
  endElement = document.getElementById('element-2');

// New leader line has red color and size 8.
new LeaderLine(startElement, endElement, {color: 'red', size: 8});
```

[![ex-060](img/ex-060.png)](https://anseki.github.io/leader-line/)

Also, the options can be accessed via properties of the instance (readable and writable).

```js
var line = new LeaderLine(startElement, endElement);
line.color = 'red'; // Change the color to red.
line.size++; // Up size.
console.log(line.size); // Output current size.
```

You can change the style of the leader line via [`color`](#options-color), [`size`](#options-size), [`outlineColor`](#outlinecolor), and more [options](#options).

```js
new LeaderLine(startElement, endElement, {
  color: '#fff',
  outline: true,
  endPlugOutline: true,
  endPlugSize: 1.5
});
```

[![ex-070](img/ex-070.png)](https://anseki.github.io/leader-line/)

You can add effects to the leader line via some options.

```js
new LeaderLine(element1, element2, {
  startPlugColor: '#1a6be0',
  endPlugColor: '#1efdaa',
  gradient: true
});
new LeaderLine(element2, element3, {dash: {animation: true}});
new LeaderLine(element4, element5, {dropShadow: true});
new LeaderLine(element5, element6, {dash: true});
```

[![ex-080](img/ex-080.gif)](https://anseki.github.io/leader-line/)

You can change symbols that are shown at the end of the leader line via [`startPlug` and `endPlug`](#startplug-endplug) options.

```js
new LeaderLine(startElement, endElement, {
  startPlug: 'square',
  endPlug: 'hand'
});
```

[![ex-090](img/ex-090.png)](https://anseki.github.io/leader-line/)

You can indicate a point or area of an element instead of the element via [`pointAnchor`](#pointanchor) or [`areaAnchor`](#areaanchor) attachment. You can indicate a point or area of the document also.

You can specify additional labels via [`startLabel`, `middleLabel` and `endLabel`](#startlabel-middlelabel-endlabel) options. Also, [`captionLabel`](#captionlabel) and [`pathLabel`](#pathlabel) attachments can be specified as labels.

```js
new LeaderLine(
  startElement1,
  LeaderLine.pointAnchor(endElement, {
    x: 60,
    y: 20
  }),
  {endLabel: LeaderLine.pathLabel('This is additional label')}
);

new LeaderLine(
  startElement2,
  LeaderLine.areaAnchor(endElement, {
    x: 80,
    y: 60,
    width: 50,
    height: 80,
  }),
  {endLabel: 'This is additional label'}
);
```

[![ex-100](img/ex-100.png)](https://anseki.github.io/leader-line/)

You can show and hide the leader line with effects by [`show` and `hide`](#show-hide) methods.  
[`mouseHoverAnchor`](#mousehoveranchor) attachment allows it to implement showing and hiding with mouse moving, easily.

```js
new LeaderLine(LeaderLine.mouseHoverAnchor(startElement), endElement);
```

[![ex-110](img/ex-110.gif)](https://anseki.github.io/leader-line/)

For more details, refer to the following.

## Constructor

```js
line = new LeaderLine(options)
```

Or

```js
line = new LeaderLine(start, end[, options])
```

The `options` argument is an Object that can have properties as [options](#options). [`hide`](#hide-option) option also can be contained.

The `start` and `end` arguments are shortcuts to `options.start` and `options.end`. The following two codes work same.

```js
new LeaderLine({start: element1, end: element2});
new LeaderLine({start: element3, end: element4, color: 'red'});
```

```js
new LeaderLine(element1, element2);
new LeaderLine(element3, element4, {color: 'red'});
```

The instance has properties that have the same name as each option to get or set those values (other than [`hide`](#hide-option) option).

```js
var line = new LeaderLine(startElement, endElement);

upButton.addEventListener('click', function() {
  if (line.size < 20) { line.size++; }
}, false);

downButton.addEventListener('click', function() {
  if (line.size > 4) { line.size--; }
}, false);
```

If you want to set multiple options after it was constructed, using [`setOptions`](#setoptions) method instead of the properties may give better performance.

When you will do something about HTML document regardless of the LeaderLine, you typically do that after the HTML document is ready (i.e. the HTML document has been loaded and parsed by web browser).  
For example:

```js
// Wait for HTML document to get ready
window.addEventListener('load', function() { // NOT `DOMContentLoaded`
  // Do something about HTML document
  var line = new LeaderLine(
    document.getElementById('start'),
    document.getElementById('end')
  );
});
```

If you don't wait for HTML document to be ready, you might not be able to get a target element yet, or problems with incomplete layout may occur. Also, you should do so asynchronous like the above for the performance because synchronous code blocks parsing HTML.

### `hide` option

Only the constructor accepts `hide` option. That is, the instance doesn't have `hide` property. (Note that the instance has [`hide`](#show-hide) method.)  
If `true` is specified, the leader line is not shown, it is shown by [`show`](#show-hide) method.  
This is used to hide it without using [`hide`](#show-hide) method, it is not shown at all until `show` method is called.

```js
// The leader line is never shown until the button is clicked.
var line = new LeaderLine(startElement, endElement, {hide: true});
button.addEventListener('click', function() { line.show(); });
```

## Methods

### `setOptions`

```js
self = line.setOptions(options)
```

Set one or more options.  
The `options` argument is an Object that can have properties as [options](#options).

Since this method updates a view only once after it sets all specified options, it may give better performance than setting options via the properties when multiple options are set to the instance that already exists.

### `show`, `hide`

```js
self = line.show([showEffectName[, animOptions]])
```

```js
self = line.hide([showEffectName[, animOptions]])
```

Show or hide the leader line.

```js
var line = new LeaderLine(startElement, endElement, {hide: true});
showButton.addEventListener('click', function() { line.show(); }, false);
hideButton.addEventListener('click', function() { line.hide(); }, false);
```

#### <a name="methods-show-hide-showeffectname"></a>`showEffectName`

*Type:* string  
*Default:* Value that was specified last time, or `fade` at first time

One of the following keywords as effect:

- `none`
- `fade`  
Default `animOptions`: `{duration: 300, timing: 'linear'}`
- `draw`  
Default `animOptions`: `{duration: 500, timing: [0.58, 0, 0.42, 1]}`

#### <a name="methods-show-hide-animoptions"></a>`animOptions`

*Type:* Object  
*Default:* See above

An Object that can have properties as [Animation Options](#animation-options).

### `position`

```js
self = line.position()
```

Re-position the leader line with current position and size of the elements as [`start` or `end`](#start-end) option.  
By default, the position of each leader line is fixed automatically when the window that loads LeaderLine was resized. You should call `position` method if your web page moved or resized the elements without resizing the window. For example, animation, a box that was scrolled or `<iframe>` that was resized.

```js
scrollableBox.addEventListener('scroll', AnimEvent.add(function() {
  line.position();
}), false);
```

(The code above uses [AnimEvent](https://github.com/anseki/anim-event) for a better performance.)

If you want to disable the fixing the position automatically, set `LeaderLine.positionByWindowResize` to `false`.

### `remove`

```js
line.remove()
```

Remove the leader line from the web page. It can't be used anymore.

## Options

The following options are specified by [constructor](#constructor) or [`setOptions`](#setoptions) method. And also, those are accessed via each property of instance.

### `start`, `end`

*Type:* HTML/SVG element or [Attachment](#attachments)

The leader line is drawn from the `start` element to the `end` element.

```js
line.end = document.getElementById('end-element');
```

Any element that has bounding-box is accepted. For example, `<div>`, `<button>`, `<ul>`, `<td>`, `<circle>`, `<text>`, and also, elements in another window (i.e. `<iframe>`).

Note: if you want to handle elements in another window regardless of LeaderLine, you should understand about security.

Or you can specify an [attachment](#attachments) instead of HTML/SVG element to indicate something.

### <a name="options-color"></a>`color`

*Type:* string  
*Default:* `'coral'`

A color (see [Color Value](#color-value)) of the leader line.

```js
line.color = 'rgba(30, 130, 250, 0.5)';
```

### <a name="options-size"></a>`size`

*Type:* number  
*Default:* `4`

The width of the leader line, in pixels.

```js
line.size = 20;
```

### `path`

*Type:* string  
*Default:* `'fluid'`

One of the following keywords to indicate how to draw the line:

- `straight`
- `arc`
- `fluid`
- `magnet`
- `grid`

[![ex-180](img/ex-180.png)](https://anseki.github.io/leader-line/)

### `startSocket`, `endSocket`

*Type:* string  
*Default:* `'auto'`

The string to indicate which side of the element the leader line connects. It can be `'top'`, `'right'`, `'bottom'`, `'left'` or `'auto'`.

```js
line.setOptions({startSocket: 'bottom', endSocket: 'top'});
```

If `'auto'` (default) is specified, the closest side is chosen automatically.

### `startSocketGravity`, `endSocketGravity`

*Type:* number, Array or string  
*Default:* `'auto'`

The force of gravity at a socket.

If a number is specified, the leader line is pulled in the direction of the socket. The number is pull strength.

```js
line.startSocketGravity = 400;
```

If an Array that is coordinates `[x, y]` is specified, the leader line is pulled in the direction of the coordinates. The distance between the coordinates and `[0, 0]` is pull strength.  
For example, if `[50, -100]` is specified, it is pulled in the direction of the rightward and upward (The strength in the Y axis direction is larger than the X axis direction). If `[-50, 0]` is specified, it is pulled in the direction of the leftward (no strength in the Y axis direction).

For example, parabola:

```js
line.setOptions({
  startSocketGravity: [192, -172],
  endSocketGravity: [-192, -172]
});
```

If `'auto'` (default) is specified, it is adjusted to gravity suitable for current [`path`](#path) option automatically.

### `startPlug`, `endPlug`

*Type:* string  
*Default:* `startPlug`: `'behind'` | `endPlug`: `'arrow1'`

One of the following keywords to indicate type of plug (symbol that is shown at the end of the leader line):

- `disc`  
`outlineMax`: `4`
- `square`  
`outlineMax`: `4`
- `arrow1`  
`outlineMax`: `1.5`
- `arrow2`  
`outlineMax`: `1.75`
- `arrow3`  
`outlineMax`: `2.5`
- `hand`  
[`startPlugOutline`/`endPlugOutline`](#startplugoutline-endplugoutline) option is ignored  
[`startPlugColor`/`endPlugColor`](#startplugcolor-endplugcolor) option is ignored
- `crosshair`  
[`startPlugOutline`/`endPlugOutline`](#startplugoutline-endplugoutline) option is ignored
- `behind`  
[`startPlugOutline`/`endPlugOutline`](#startplugoutline-endplugoutline) option is ignored  
[`startPlugColor`/`endPlugColor`](#startplugcolor-endplugcolor) option is ignored

[![ex-220](img/ex-220.png)](https://anseki.github.io/leader-line/)

### `startPlugColor`, `endPlugColor`

*Type:* string  
*Default:* `'auto'`

Each option for when a plug that accepts this option is specified for [`startPlug`/`endPlug`](#startplug-endplug) option.

A color (see [Color Value](#color-value)) of a plug.  
It is painted separately from the line (i.e. Those don't overlap each other). Therefore one of [`color`](#options-color) and `startPlugColor`/`endPlugColor` or both options can have an alpha channel.

```js
lineA.setOptions({ // element-1, element-2
  color: 'rgba(30, 130, 250, 0.5)', // translucent
  startPlugColor: 'rgb(241, 76, 129)',
  endPlugColor: 'rgba(241, 76, 129, 0.5)' // translucent
});

lineB.setOptions({ // element-3, element-4
  color: 'rgb(30, 130, 250)',
  startPlugColor: 'rgb(241, 76, 129)',
  endPlugColor: 'rgba(241, 76, 129, 0.5)' // translucent
});
```

If `'auto'` (default) is specified, a value of `color` option is set synchronously (i.e. it is changed when `color` was changed).

### `startPlugSize`, `endPlugSize`

*Type:* number  
*Default:* `1`

Each option for when a value other than `behind` is specified for [`startPlug`/`endPlug`](#startplug-endplug) option.

A multiplying factor of the size of a plug.  
The plugs are resized synchronously, with the following options that contain [`size`](#options-size):

Plug Size: `size` * [default-plug-scale] * [`startPlugSize` or `endPlugSize`]

```js
new LeaderLine(element1, element2, {
  startPlug: 'arrow1',
  size: 4,
  startPlugSize: 1,
  endPlugSize: 2
});

new LeaderLine(element3, element4, {
  startPlug: 'arrow1',
  size: 8,
  startPlugSize: 1,
  endPlugSize: 2
});
```

### `outline`

*Type:* boolean  
*Default:* `false`

If `true` is specified, an outline of the leader line is enabled.

```js
line.outline = true;
```

### `outlineColor`

*Type:* string  
*Default:* `'indianred'`

An option for when `true` is specified for [`outline`](#outline) option.

A color (see [Color Value](#color-value)) of an outline of the leader line.  
It is painted separately from inside of the line (i.e. Those don't overlap each other). Therefore one of [`color`](#options-color) and `outlineColor` or both options can have an alpha channel.

```js
lineA.setOptions({ // element-1, element-2
  color: 'rgb(248, 205, 30)',
  outlineColor: 'rgb(30, 130, 250)'
});

lineB.setOptions({ // element-3, element-4
  color: 'rgba(248, 205, 30, 0.5)', // translucent
  outlineColor: 'rgba(30, 130, 250, 0.5)' // translucent
});

lineC.setOptions({ // element-5, element-6
  color: 'rgba(248, 205, 30, 0.5)', // translucent
  outlineColor: 'rgb(30, 130, 250)'
});

lineD.setOptions({ // element-7, element-8
  color: 'rgb(248, 205, 30)',
  outlineColor: 'rgba(30, 130, 250, 0.5)' // translucent
});
```

### `outlineSize`

*Type:* number  
*Default:* `0.25`

An option for when `true` is specified for [`outline`](#outline) option.

A multiplying factor of the size of an outline of the leader line, it is greater than `0` and is less than or equal to `0.48`.  
The outline is resized synchronously, with the following options that contain [`size`](#options-size):

Outline Size: `size` * `outlineSize`

```js
lineA.setOptions({ // element-1, element-2
  size: 12,
  outlineSize: 0.4
});

lineB.setOptions({ // element-3, element-4
  size: 24,
  outlineSize: 0.08
});
```

### `startPlugOutline`, `endPlugOutline`

*Type:* boolean  
*Default:* `false`

Each option for when a plug that accepts this option is specified for [`startPlug`/`endPlug`](#startplug-endplug) option.

If `true` is specified, an outline of the plug is enabled.

```js
line.endPlugOutline = true;
```

### `startPlugOutlineColor`, `endPlugOutlineColor`

*Type:* string  
*Default:* `'auto'`

Each option for when `true` is specified for [`startPlugOutline`/`endPlugOutline`](#startplugoutline-endplugoutline) option.

A color (see [Color Value](#color-value)) of an outline of the plug.  
It is painted separately from inside of the plug (i.e. Those don't overlap each other). Therefore one of [`startPlugColor`/`endPlugColor`](#startplugcolor-endplugcolor) and `startPlugOutlineColor`/`endPlugOutlineColor` or both options can have an alpha channel.

```js
lineA.setOptions({ // element-1, element-2
  startPlugColor: 'rgb(248, 205, 30)',
  startPlugOutlineColor: 'rgb(30, 130, 250)',
  endPlugColor: 'rgba(248, 205, 30, 0.5)', // translucent
  endPlugOutlineColor: 'rgb(30, 130, 250)'
});

lineB.setOptions({ // element-3, element-4
  startPlugColor: 'rgb(248, 205, 30)',
  startPlugOutlineColor: 'rgba(30, 130, 250, 0.5)', // translucent
  endPlugColor: 'rgba(248, 205, 30, 0.5)', // translucent
  endPlugOutlineColor: 'rgba(30, 130, 250, 0.5)' // translucent
});
```

If `'auto'` (default) is specified, a value of [`outlineColor`](#outlinecolor) option is set synchronously (i.e. it is changed when `outlineColor` was changed).

### `startPlugOutlineSize`, `endPlugOutlineSize`

*Type:* number  
*Default:* `1`

Each option for when `true` is specified for [`startPlugOutline`/`endPlugOutline`](#startplugoutline-endplugoutline) option.

A multiplying factor of the size of an outline of the plug, it is greater than or equal to `1` and is less than or equal to `outlineMax` that is shown in [`startPlug`/`endPlug`](#startplug-endplug) option.  
The outline is resized synchronously, with the following options that contain [`size`](#options-size):

Plug Outline Size: `size` * [default-plug-scale] * [[`startPlugSize` or `endPlugSize`](#startplugsize-endplugsize)] * [default-plug-outline-scale] * [`startPlugOutlineSize` or `endPlugOutlineSize`]

```js
lineA.setOptions({ // element-1, element-2
  size: 4,
  startPlugSize: 1.5,
  startPlugOutlineSize: 2.5,
  endPlugSize: 3,
  endPlugOutlineSize: 1
});

lineB.setOptions({ // element-3, element-4
  size: 10,
  startPlugSize: 1.5,
  startPlugOutlineSize: 1,
  endPlugSize: 3,
  endPlugOutlineSize: 2.5
});
```

### `startLabel`, `middleLabel`, `endLabel`

*Type:* string or [Attachment](#attachments)  
*Default:* `''`

An additional label that is shown on the leader line.

```js
new LeaderLine(startElement, endElement, {
  startLabel: 'START',
  middleLabel: 'MIDDLE',
  endLabel: 'END'
});
```

Or you can specify an [attachment](#attachments) instead of a string.

### <a name="options-dash"></a>`dash` (effect)

*Type:* boolean or Object  
*Default:* `false`

Enable the effect with specified Object that can have properties as the following options.  
Or `true` to enable it with all default options.

```js
new LeaderLine(startElement, endElement, {dash: true});
```

#### `len`, `gap`

*Type:* number or string  
*Default:* `'auto'`

The size of parts of the dashed line, in pixels.  
`len` is length of drawn lines, `gap` is gap between drawn lines.

If `'auto'` (default) is specified, the following each value is set synchronously (i.e. it is changed when `size` was changed).

`len`: [`size`](#options-size) * 2
`gap`: `size`

```js
new LeaderLine(element1, element2, {
  dash: {len: 4, gap: 24}
});

new LeaderLine(element3, element4, {
  size: 8,
  dash: true // len: 16, gap: 8
});
```

#### `animation`

*Type:* boolean or Object  
*Default:* `false`

An Object that can have properties as [Animation Options](#animation-options) to animate the effect.  
Or `true` to animate it with the following default options.

Default Animation Options: `{duration: 1000, timing: 'linear'}`

```js
new LeaderLine(startElement, endElement, {dash: {animation: true}});
```

### `gradient` (effect)

*Type:* boolean or Object  
*Default:* `false`

Enable the effect with specified Object that can have properties as the following options.  
Or `true` to enable it with all default options.

```js
new LeaderLine(startElement, endElement, {startPlugColor: '#a6f41d', gradient: true});
```

#### `startColor`, `endColor`

*Type:* string  
*Default:* `'auto'`

The start color (see [Color Value](#color-value)) and end color of the gradient.

If `'auto'` (default) is specified, each value of [`startPlugColor` and `endPlugColor`](#startplugcolor-endplugcolor) is set synchronously (i.e. it is changed when `startPlugColor`