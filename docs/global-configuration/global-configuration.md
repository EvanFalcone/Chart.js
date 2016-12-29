# Global Configuration

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

## Global Font Settings

There are 4 special global settings that can change all of the fonts on the chart. These options are in `Chart.defaults.global`. The global font settings only apply when more specific options are not included in the config.

For example, in this chart the text will all be red except for the labels in the legend.

```javascript
Chart.defaults.global.defaultFontColor = 'red';
let chart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        legend: {
            labels: {
                // This more specific font property overrides the global property
                fontColor: 'black'
            }
        }
    }
});
```

### defaultFontColor
**Type:** Color
**Default:** `'#666'`
Default font color for all text.

### defaultFontFamily
**Type:** String
**Default:** `"'Helvetica Neue', 'Helvetica', 'Arial', sans-serif"`
Default font family for all text.

### defaultFontSize
**Type:** Number
**Default:** `12`
Default font size (in px) for text. Does not apply to radialLinear scale point labels.

### defaultFontStyle
**Type:** String
**Default:** `'normal'`
Default font style. Does not apply to tooltip title or footer. Does not apply to chart title.