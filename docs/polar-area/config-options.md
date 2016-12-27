# Config Options

These are the customisation options specific to Polar Area charts. These options are merged with the [global chart configuration options](#global-chart-configuration), and form the options of the chart.

## startAngle
**Type:** Number
**Default:** `-0.5 * Math.PI`
Starting angle to draw arcs for the first item in a dataset.

## animateRotate
**Type:** Boolean
**Default:** `true`
If true, the chart will animate in with a rotation animation. This property is in the `options.animation` object.

```javascript
options = {
    animation: {
        animateRotate: false
    }
};
```

## animateScale
**Type:** Boolean
**Default:** `true`
If true, will animate scaling the chart from the center outwards. This property is in the `options.animation` object.

```javascript
options = {
    animation: {
        animateScale: true
    }
};
```

# Default Options

We can also change these defaults values for each PolarArea type that is created, this object is available at `Chart.defaults.polarArea`. Changing the global options only affects charts created after the change. Existing charts are not changed.

For example, to configure all new polar area charts with `animateScale = false` you would do:
```javascript
Chart.defaults.polarArea.animation.animateScale = false;
```