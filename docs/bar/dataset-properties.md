# Dataset Properties
The bar chart allows a number of properties to be specified for each dataset. These are used to set display properties for a specific dataset. For example, the colour of the bars is generally set this way.

Some properties can be specified as an array. If these are set to an array value, the first value applies to the first bar, the second value to the second bar, and so on.

## label
**Type:** String
The label for the dataset which appears in the legend and tooltips.

## xAxisID
**Type:** String
The ID of the x axis to plot this dataset on. If not specified, this defaults to the ID of the first found x axis

## yAxisID
**Type:** String
The ID of the y axis to plot this dataset on. If not specified, this defaults to the ID of the first found y axis.

## backgroundColor
**Type:** Color or Color[]
The fill color of the bar. See [Colors](../colors/colors.md#chart-colors)

## borderColor
**Type:** Color or Color[] 
The color of the bar border. See [Colors](../colors/colors.md#chart-colors)

## borderWidth
**Type:** Number or Number[]
The stroke width of the bar in pixels.

## borderSkipped
**Type:** String
Which edge to skip drawing the border for. This setting is used to avoid drawing the bar stroke at the base of the fill. In general, this does not need to be changed except when creating chart types that derive from a bar chart.

Options are:
* 'bottom'
* 'left'
* 'top'
* 'right'

## hoverBackgroundColor
**Type:** Color or Color[]
The fill colour of the bars when hovered.

## hoverBorderColor
**Type:** Color or Color[]
The stroke colour of the bars when hovered.

## hoverBorderWidth
**Type:** Number of Number[]
The stroke width of the bars when hovered.
