# Data Structure

For a bubble chart, datasets need to contain an array of data points. Each point must implement the [bubble data object](#bubble-data-object) interface.

## Bubble Data Object

Data for the bubble chart is passed in the form of an object. The object must implement the following interface. It is important to note that the radius property, `r` is **not** scaled by the chart. It is the raw radius in pixels of the bubble that is drawn on the canvas.

```javascript
{
    // X Value
    x: <Number>,

    // Y Value
    y: <Number>,

    // Radius of bubble. This is not scaled.
    r: <Number>
}
```