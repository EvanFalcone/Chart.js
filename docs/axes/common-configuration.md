# Common Configuration

The following properties are common to all axes provided by Chart.js

## display
**Type:** Boolean
**Default:** `true`
If set to `false` the axis is hidden from view. Overrides *gridLines.display*, *scaleLabel.display*, and *ticks.display*.

Every scale extends a core scale class with the following options:

## Callbacks
There are a number of config callbacks that can be used to change parameters in the scale at different points in the update process.

### beforeUpdate
Callback called before the update process starts. Passed a single argument, the scale instance.

`beforeUpdate: function(scaleInstance)`

### beforeSetDimensions
Callback that runs before dimensions are set. Passed a single argument, the scale instance.

`beforeSetDimensions: function(scaleInstance)`

### afterSetDimensions
Callback that runs after dimensions are set. Passed a single argument, the scale instance.

`afterSetDimensions: function(scaleInstance)`

### beforeDataLimits
Callback that runs before data limits are determined. Passed a single argument, the scale instance.

`beforeDataLimits: function(scaleInstance)`

### afterDataLimits
Callback that runs after data limits are determined. Passed a single argument, the scale instance.

`afterDataLimits: function(scaleInstance)`

### beforeBuildTicks
Callback that runs before ticks are created. Passed a single argument, the scale instance.

`beforeBuildTicks: function(scaleInstance)`

### afterBuildTicks
Callback that runs after ticks are created. Useful for filtering ticks. Passed a single argument, the scale instance.

`afterBuildTicks: function(scaleInstance)`

### beforeTickToLabelConversion
Callback that runs before ticks are converted into strings. Passed a single argument, the scale instance.

`beforeTickToLabelConversion: function(scaleInstance)`

### afterTickToLabelConversion
Callback that runs after ticks are converted into strings. Passed a single argument, the scale instance.

`afterTickToLabelConversion: function(scaleInstance)`

### beforeCalculateTickRotation
Callback that runs before tick rotation is determined. Passed a single argument, the scale instance.

`beforeCalculateTickRotation: function(scaleInstance)`

### afterCalculateTickRotation
Callback that runs after tick rotation is determined. Passed a single argument, the scale instance.

`afterCalculateTickRotation: function(scaleInstance)`

### beforeFit
Callback that runs before the scale fits to the canvas. Passed a single argument, the scale instance.

`beforeFit: function(scaleInstance)`

### afterFit
Callback that runs after the scale fits to the canvas. Passed a single argument, the scale instance.

`afterFit: function(scaleInstance)`

### afterUpdate
Callback that runs at the end of the update process. Passed a single argument, the scale instance.

`afterUpdate: function(scaleInstance)`