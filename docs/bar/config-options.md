# Configuration Options

The bar chart defines the following configuration options. These options are merged with the global chart configuration options, `Chart.defaults.global`, to form the options passed to the chart.

## barPercentage
**Type:** Number
**Default:** `0.9`
Percent (0-1) of the available width each bar should be within the category percentage. 1.0 will take the whole category width and put the bars right next to each other. [Read More](#bar-chart-barpercentage-vs-categorypercentage)

This setting applies to the axis configuration for a bar chart. If axes are added to the chart, this setting will need to be set for each new axis.

```javascript
options = {
    scales: {
        xAxes: [{
            barPercentage: 0.8
        }]
    }
}
```

## categoryPercentage
**Type:** Number
**Default:** `0.8`
Percent (0-1) of the available width (the space between the gridlines for small datasets) for each data-point to use for the bars. [Read More](#bar-chart-barpercentage-vs-categorypercentage)

This setting applies to the axis configuration for a bar chart. If axes are added to the chart, this setting will need to be set for each new axis.

```javascript
options = {
    scales: {
        xAxes: [{
            categoryPercentage: 0.8
        }]
    }
}
```

## barThickness
**Types:** Number

Manually set width of each bar in pixels. If not set, the bars are sized automatically using [barPercentage](#barPercentage) and [categoryPercentage](#categoryPercentage);

This setting applies to the axis configuration for a bar chart. If axes are added to the chart, this setting will need to be set for each new axis.

```javascript
options = {
    scales: {
        xAxes: [{
            barThickness: 25
        }]
    }
}
```

## offsetGridLines
**Type:** Boolean
**Default:** `true`
If true, the bars for a particular data point fall between the grid lines. If false, the grid line will go right down the middle of the bars. It is unlikely that this will ever need to be changed in practice. It exists more as a way to reuse the axis code by configuring the existing axis slightly differently.

This setting applies to the axis configuration for a bar chart. If axes are added to the chart, this setting will need to be set for each new axis.

```javascript
options = {
    scales: {
        xAxes: [{
            gridLines: {
                offsetGridLines: true
            }
        }]
    }
}
```

# Default Options

It is common to want to apply a configuration setting to all created bar charts. The global bar chart settings are stored in `Chart.defaults.bar`. Changing the global options only affects charts created after the change. Existing charts are not changed.

# barPercentage vs categoryPercentage

The following shows the relationship between the bar percentage option and the category percentage option.

```text
// categoryPercentage: 1.0
// barPercentage: 1.0
Bar:        | 1.0 | 1.0 |
Category:   |    1.0    |   
Sample:     |===========|

// categoryPercentage: 1.0
// barPercentage: 0.5
Bar:          |.5|  |.5|
Category:  |      1.0     |   
Sample:    |==============|

// categoryPercentage: 0.5
// barPercentage: 1.0
Bar:            |1.||1.|
Category:       |  .5  |   
Sample:     |==============|
```