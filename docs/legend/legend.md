# Legend Configuration

The chart legend displays data about the datasets that area appearing on the chart.

## Configuration options
The legend configuration is passed into the `options.legend` namespace. The global options for the chart legend is defined in `Chart.defaults.global.legend`.

### display
**Type:** Boolean
**Default:** `true`
Is the legend displayed.

### position
**Type:** String
**Default:** `'top'`
Position of the legend. Options are:
* `'top'`
* `'left'`
* `'bottom'`
* `'right'`

### fullWidth
**Type:** Boolean
**Default:** `true`
Marks that this box should take the full width of the canvas (pushing down other boxes). This is unlikely to need to be changed in day-to-day use.

### onClick
**Type:** Function
**Default:** `function(event, legendItem) {}`
A callback that is called when a 'click' event is registered on top of a label item.

### onHover
**Type:** Function
**Default:** `function(event, legendItem) {}`
A callback that is called when a 'mousemove' event is registered on top of a label item

### labels
**Type:** Object
See the [Legend Label Configuration](#legend-label-configuration) section below.

### reverse
**Type:** Boolean
**Default:** `false`
Legend will show datasets in reverse order.

## Legend Label Configuration

The legend label configuration is nested below the legend configuration using the `labels` key.

### boxWidth
**Type:** Number
**Boolean:** `40`
Width of coloured box.

### fontSize
**Type:** Number
**Boolean:** `12`
Font size of text in legend.

### fontStyle
**Type:** String
**Boolean:** `'normal'`
Font style of text in the legend.

### fontColor
**Type:** Color
**Boolean:** `'#666'`
Font color of text in legend.

### fontFamily
**Type:** String
**Boolean:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Font family of legend text.

### padding
**Type:** Number
**Boolean:** `10`
Padding between rows of colored boxes.

### generateLabels
**Type:** Function
**Boolean:** `function(chart) {  }`
Generates legend items for each thing in the legend. Default implementation returns the text + styling for the color box. See [Legend Item](#chart-configuration-legend-item-interface) for details.

### filter
**Type:** Function
**Boolean:** `null`
Filters legend items out of the legend. Receives 2 parameters, a [Legend Item](#chart-configuration-legend-item-interface) and the chart data.

### usePointStyle
**Type:** Boolean
**Boolean:** `false`
Label style will match corresponding point style (size is based on fontSize, boxWidth is not used in this case).

## Legend Item Interface

Items passed to the legend `onClick` function are the ones returned from `labels.generateLabels`. These items must implement the following interface.

```javascript
{
    // Label that will be displayed
    text: String,

    // Fill style of the legend box
    fillStyle: Color,

    // If true, this item represents a hidden dataset. Label will be rendered with a strike-through effect
    hidden: Boolean,

    // For box border. See https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D/lineCap
    lineCap: String,

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash
    lineDash: Array[Number],

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset
    lineDashOffset: Number,

    // For box border. See https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineJoin
    lineJoin: String,

    // Width of box border
    lineWidth: Number,

    // Stroke style of the legend box
    strokeStyle: Color

    // Point style of the legend box (only used if usePointStyle is true)
    pointStyle: String
}
```

## Example

The following example will create a chart with the legend enabled and turn all of the text red in color.

```javascript
var chartInstance = new Chart(ctx, {
    type: 'bar',
    data: data,
    options: {
        legend: {
            display: true,
            labels: {
                fontColor: 'rgb(255, 99, 132)'
            }
        }
}
});
```