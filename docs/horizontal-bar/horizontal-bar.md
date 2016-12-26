# Introduction
A horizontal bar chart is a variation on a vertical bar chart. It is sometimes used to show trend data, and the comparison of multiple data sets side by side.

# Example
```javascript
var myBarChart = new Chart(ctx, {
    type: 'horizontalBar',
    data: data,
    options: options
});
```

# Dataset Properties
The dataset properties for a horizontal bar chart are the same as the [bar chart](../bar/dataset-properties.md#dataset-properties).

# Config Options
The configuration options for the horizontal bar chart are the same as for the [bar chart](../bar/config-options.md#config-options). However, any options specified on the x axis in a bar chart, are applied to the y axis in a horizontal bar chart.

The default horizontal bar configuration is specified in `Chart.defaults.horizontalBar`.