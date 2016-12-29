# Hover Configuration

The hover configuration is passed into the `options.hover` namespace. The global hover configuration is at `Chart.defaults.global.hover`.

Name | Type | Default | Description
--- | --- | --- | ---
## mode
**Type:** String
**Default:** `'nearest`
Sets which elements appear in the tooltip. See [Interaction Modes](../interaction-modes/interaction-modes.md#interaction-modes) for details.

## intersect
**Type:** Boolean
**Default:** `true`
if true, the hover mode only applies when the mouse position intersects an item on the chart.

## animationDuration
**Type:** Number
**Default:** `400`
Duration in milliseconds it takes to animate hover style changes.

## onHover
**Type:** Function
**Default:** `null`
Called when any of the events fire. Called in the context of the chart and passed the event and an array of active elements (bars, points, etc).