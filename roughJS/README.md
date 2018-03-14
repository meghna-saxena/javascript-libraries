# RoughCanvas
This is the main interface when drawing on Canvas using RoughJS.

Instantiate RoughCanvas by passing in the canvas node to `rough.canvas()` method.

- config is optional.

> rough.canvas (canvasElement, [, config])

```
let roughCanvas = rough.canvas(document.getElementById('myCanvas'));
```

## Methods
For each method, options is an optional argument - it configures how the shape is drawn/filled. Default options can be configured in the rough.canvas instantiator described above.

> line (x1, y1, x2, y2 [, options])
Draws a line from (x1, y1) to (x2, y2).

```
roughCanvas.line(60, 60, 190, 60);
roughCanvas.line(60, 60, 190, 60, {strokeWidth: 5});
```

> rectangle (x, y, width, height [, options])
Draws a rectangle with the top-left corner at (x, y) with the specified width and height.

```
roughCanvas.rectangle(10, 10, 100, 100);
roughCanvas.rectangle(140, 10, 100, 100, { fill: 'red'});
```