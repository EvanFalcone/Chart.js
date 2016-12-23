# Configuration Options

The line chart defines the following configuration options. These options are merged with the [global chart configuration options, `Chart.defaults.global`, to form the options passed to the chart.

## showLines
**Type:** Boolean
**Default:** `true`
If false, the lines between points are not drawn.

## spanGaps
**Type:** Boolean
**Default:** `false`
If false, NaN data causes a break in the line.

# Default Options

It is common to want to apply a configuration setting to all created line charts. The global line chart settings are stored in `Chart.defaults.line`. Changing the global options only affects charts created after the change. Existing charts are not changed.

For example, to configure all line charts with `spanGaps = true` you would do:
```javascript
Chart.defaults.line.spanGaps = true;
```