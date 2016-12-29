---
title: Chart Configuration
anchor: chart-configuration
---

Chart.js provides a number of options for changing the behaviour of created charts. These configuration options can be changed on a per chart basis by passing in an options object when creating the chart. Alternatively, the global configuration can be changed which will be used by all charts created after that point.

### Chart Data

To display data, the chart must be passed a data object that contains all of the information needed by the chart. The data object can contain the following parameters

Name | Type | Description
--- | --- | ----
datasets | Array[object] | Contains data for each dataset. See the documentation for each chart type to determine the valid options that can be attached to the dataset
labels | Array[string] | Optional parameter that is used with the [category axis](#scales-category-scale).
xLabels | Array[string] | Optional parameter that is used with the category axis and is used if the axis is horizontal
yLabels | Array[string] | Optional parameter that is used with the category axis and is used if the axis is vertical

### Creating a Chart with Options

To create a chart with configuration options, simply pass an object containing your configuration to the constructor. In the example below, a line chart is created and configured to not be responsive.

```javascript
var chartInstance = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        responsive: false
    }
});
```

### Global Configuration

This concept was introduced in Chart.js 1.0 to keep configuration [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), and allow for changing options globally across chart types, avoiding the need to specify options for each instance, or the default for a particular chart type.

Chart.js merges the options object passed to the chart with the global configuration using chart type defaults and scales defaults appropriately. This way you can be as specific as you would like in your individual chart configuration, while still changing the defaults for all chart types where applicable. The global general options are defined in `Chart.defaults.global`. The defaults for each chart type are discussed in the documentation for that chart type.

The following example would set the hover mode to 'nearest' for all charts where this was not overridden by the chart type defaults or the options passed to the constructor on creation.

```javascript
Chart.defaults.global.hover.mode = 'nearest';

// Hover mode is set to nearest because it was not overridden here
var chartInstanceHoverModeNearest = new Chart(ctx, {
    type: 'line',
    data: data,
});

// This chart would have the hover mode that was passed in
var chartInstanceDifferentHoverMode = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        hover: {
            // Overrides the global setting
            mode: 'index'
        }
    }
})
```

#### Global Font Settings

There are 4 special global settings that can change all of the fonts on the chart. These options are in `Chart.defaults.global`.

Name | Type | Default | Description
--- | --- | --- | ---
defaultFontColor | Color | '#666' | Default font color for all text
defaultFontFamily | String | "'Helvetica Neue', 'Helvetica', 'Arial', sans-serif" | Default font family for all text
defaultFontSize | Number | 12 | Default font size (in px) for text. Does not apply to radialLinear scale point labels
defaultFontStyle | String | 'normal' | Default font style. Does not apply to tooltip title or footer. Does not apply to chart title

### Common Chart Configuration

The following options are applicable to all charts. The can be set on the [global configuration](#chart-configuration-global-configuration), or they can be passed to the chart constructor.

Name | Type | Default | Description
--- | --- | --- | ---
events | Array[String] | `["mousemove", "mouseout", "click", "touchstart", "touchmove", "touchend"]` | Events that the chart should listen to for tooltips and hovering
onClick | Function | null | Called if the event is of type 'mouseup' or 'click'. Called in the context of the chart and passed the event and an array of active elements

### Element Configuration

The global options for elements are defined in `Chart.defaults.global.elements`.

Options can be configured for four different types of elements: arc, lines, points, and rectangles. When set, these options apply to all objects of that type unless specifically overridden by the configuration attached to a dataset.

#### Arc Configuration

Arcs are used in the polar area, doughnut and pie charts. They can be configured with the following options. The global arc options are stored in `Chart.defaults.global.elements.arc`.

Name | Type | Default | Description
--- | --- | --- | ---
backgroundColor | Color | 'rgba(0,0,0,0.1)' | Default fill color for arcs. Inherited from the global default
borderColor | Color | '#fff' | Default stroke color for arcs
borderWidth | Number | 2 | Default stroke width for arcs

#### Line Configuration

Line elements are used to represent the line in a line chart. The global line options are stored in `Chart.defaults.global.elements.line`.

Name | Type | Default | Description
--- | --- | --- | ---
tension | Number | 0.4 | Default bezier curve tension. Set to `0` for no bezier curves.
backgroundColor | Color | 'rgba(0,0,0,0.1)' | Default line fill color
borderWidth | Number | 3 | Default line stroke width
borderColor | Color | 'rgba(0,0,0,0.1)' | Default line stroke color
borderCapStyle | String | 'butt' | Default line cap style. See [MDN](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/lineCap)
borderDash | Array | `[]` | Default line dash. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash)
borderDashOffset | Number | 0.0 | Default line dash offset. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset)
borderJoinStyle | String | 'miter' | Default line join style. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin)
capBezierPoints | Boolean | true | If true, bezier control points are kept inside the chart. If false, no restriction is enforced.
fill | Boolean or String | true | If true, the fill is assumed to be to zero. String values are 'zero', 'top', and 'bottom' to fill to different locations. If `false`, no fill is added
stepped | Boolean | false | If true, the line is shown as a stepped line and 'tension' will be ignored

#### Point Configuration

Point elements are used to represent the points in a line chart or a bubble chart. The global point options are stored in `Chart.defaults.global.elements.point`.

Name | Type | Default | Description
--- | --- | --- | ---
radius | Number | 3 | Default point radius
pointStyle | String | 'circle' | Default point style
backgroundColor | Color | 'rgba(0,0,0,0.1)' | Default point fill color
borderWidth | Number | 1 | Default point stroke width
borderColor | Color | 'rgba(0,0,0,0.1)' | Default point stroke color
hitRadius | Number | 1 | Extra radius added to point radius for hit detection
hoverRadius | Number | 4 | Default point radius when hovered
hoverBorderWidth | Number | 1 | Default stroke width when hovered

#### Rectangle Configuration

Rectangle elements are used to represent the bars in a bar chart. The global rectangle options are stored in `Chart.defaults.global.elements.rectangle`.

Name | Type | Default | Description
--- | --- | --- | ---
backgroundColor | Color | 'rgba(0,0,0,0.1)' | Default bar fill color
borderWidth | Number | 0 | Default bar stroke width
borderColor | Color | 'rgba(0,0,0,0.1)' | Default bar stroke color
borderSkipped | String | 'bottom' | Default skipped (excluded) border for rectangle. Can be one of `bottom`, `left`, `top`, `right`

### Colors

When supplying colors to Chart options, you can use a number of formats. You can specify the color as a string in hexadecimal, RGB, or HSL notations. If a color is needed, but not specified, Chart.js will use the global default color. This color is stored at `Chart.defaults.global.defaultColor`. It is initially set to 'rgba(0, 0, 0, 0.1)';

You can also pass a [CanvasGradient](https://developer.mozilla.org/en-US/docs/Web/API/CanvasGradient) object. You will need to create this before passing to the chart, but using it you can achieve some interesting effects.

### Patterns

An alternative option is to pass a [CanvasPattern](https://developer.mozilla.org/en-US/docs/Web/API/CanvasPattern) object. For example, if you wanted to fill a dataset with a pattern from an image you could do the following.

```javascript
var img = new Image();
img.src = 'https://example.com/my_image.png';
img.onload = function() {
    var ctx = document.getElementById('canvas').getContext('2d');
    var fillPattern = ctx.createPattern(img, 'repeat');

    var chart = new Chart(ctx, {
        data: {
            labels: ['Item 1', 'Item 2', 'Item 3'],
            datasets: [{
                data: [10, 20, 30],
                backgroundColor: fillPattern
            }]
        }
    })
}
```

Using pattern fills for data graphics can help viewers with vision deficiencies (e.g. color-blindness or partial sight) to [more easily understand your data](http://betweentwobrackets.com/data-graphics-and-colour-vision/).

Using the [Patternomaly](https://github.com/ashiguruma/patternomaly) library you can generate patterns to fill datasets.

```javascript
var chartData = {
	datasets: [{
		data: [45, 25, 20, 10],
		backgroundColor: [
			pattern.draw('square', '#ff6384'),
			pattern.draw('circle', '#36a2eb'),
			pattern.draw('diamond', '#cc65fe'),
			pattern.draw('triangle', '#ffce56'),
		]
	}],
	labels: ['Red', 'Blue', 'Purple', 'Yellow']
};
```

### Mixed Chart Types

When creating a chart, you have the option to overlay different chart types on top of each other as separate datasets.

To do this, you must set a `type` for each dataset individually. You can create mixed chart types with bar and line chart types.

When creating the chart you must set the overall `type` as `bar`.

```javascript
var myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Item 1', 'Item 2', 'Item 3'],
        datasets: [
            {
                type: 'bar',
                label: 'Bar Component',
                data: [10, 20, 30],
            },
            {
                type: 'line',
                label: 'Line Component',
                data: [30, 20, 10],
            }
        ]
    }
});
```
