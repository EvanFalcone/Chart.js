---
title: Advanced usage
anchor: advanced-usage
---


### Prototype Methods

For each chart, there are a set of global prototype methods on the shared `ChartType` which you may find useful. These are available on all charts created with Chart.js, but for the examples, let's use a line chart we've made.

```javascript
// For example:
var myLineChart = new Chart(ctx, config);
```

#### .destroy()

Use this to destroy any chart instances that are created. This will clean up any references stored to the chart object within Chart.js, along with any associated event listeners attached by Chart.js.
This must be called before the canvas is reused for a new chart.

```javascript
// Destroys a specific chart instance
myLineChart.destroy();
```

#### .update(duration, lazy)

Triggers an update of the chart. This can be safely called after replacing the entire data object. This will update all scales, legends, and then re-render the chart.

```javascript
// duration is the time for the animation of the redraw in milliseconds
// lazy is a boolean. if true, the animation can be interrupted by other animations
myLineChart.data.datasets[0].data[2] = 50; // Would update the first dataset's value of 'March' to be 50
myLineChart.update(); // Calling update now animates the position of March from 90 to 50.
```

#### .reset()

Reset the chart to it's state before the initial animation. A new animation can then be triggered using `update`.

```javascript
myLineChart.reset();
```

#### .render(duration, lazy)

Triggers a redraw of all chart elements. Note, this does not update elements for new data. Use `.update()` in that case.

```javascript
// duration is the time for the animation of the redraw in milliseconds
// lazy is a boolean. if true, the animation can be interrupted by other animations
myLineChart.render(duration, lazy);
```

#### .stop()

Use this to stop any current animation loop. This will pause the chart during any current animation frame. Call `.render()` to re-animate.

```javascript
// Stops the charts animation loop at its current frame
myLineChart.stop();
// => returns 'this' for chainability
```

#### .resize()

Use this to manually resize the canvas element. This is run each time the canvas container is resized, but you can call this method manually if you change the size of the canvas nodes container element.

```javascript
// Resizes & redraws to fill its container element
myLineChart.resize();
// => returns 'this' for chainability
```

#### .clear()

Will clear the chart canvas. Used extensively internally between animation frames, but you might find it useful.

```javascript
// Will clear the canvas that myLineChart is drawn on
myLineChart.clear();
// => returns 'this' for chainability
```

#### .toBase64Image()

This returns a base 64 encoded string of the chart in it's current state.

```javascript
myLineChart.toBase64Image();
// => returns png data url of the image on the canvas
```

#### .generateLegend()

Returns an HTML string of a legend for that chart. The legend is generated from the `legendCallback` in the options.

```javascript
myLineChart.generateLegend();
// => returns HTML string of a legend for this chart
```

#### .getElementAtEvent(e)

Calling `getElementAtEvent(event)` on your Chart instance passing an argument of an event, or jQuery event, will return the single element at the event position. If there are multiple items within range, only the first is returned

```javascript
myLineChart.getElementAtEvent(e);
// => returns the first element at the event point.
```

#### .getElementsAtEvent(e)

Looks for the element under the event point, then returns all elements at the same data index. This is used internally for 'label' mode highlighting.

Calling `getElementsAtEvent(event)` on your Chart instance passing an argument of an event, or jQuery event, will return the point elements that are at that the same position of that event.

```javascript
canvas.onclick = function(evt){
	var activePoints = myLineChart.getElementsAtEvent(evt);
	// => activePoints is an array of points on the canvas that are at the same position as the click event.
};
```

This functionality may be useful for implementing DOM based tooltips, or triggering custom behaviour in your application.

#### .getDatasetAtEvent(e)

Looks for the element under the event point, then returns all elements from that dataset. This is used internally for 'dataset' mode highlighting

```javascript
myLineChart.getDatasetAtEvent(e);
// => returns an array of elements
```

#### .getDatasetMeta(index)

Looks for the dataset that matches the current index and returns that metadata. This returned data has all of the metadata that is used to construct the chart.

The `data` property of the metadata will contain information about each point, rectangle, etc. depending on the chart type.

Extensive examples of usage are available in the [Chart.js tests](https://github.com/chartjs/Chart.js/tree/master/test).

```javascript
var meta = myChart.getDatasetMeta(0);
var x = meta.data[0]._model.x
```

### External Tooltips

You can enable custom tooltips in the global or chart configuration like so:

```javascript
var myPieChart = new Chart(ctx, {
	type: 'pie',
	data: data,
	options: {
		tooltips: {
			custom: function(tooltip) {
				// tooltip will be false if tooltip is not visible or should be hidden
				if (!tooltip) {
					return;
				}

				// Otherwise, tooltip will be an object with all tooltip properties like:

				// tooltip.caretSize
				// tooltip.caretPadding
				// tooltip.chart
				// tooltip.cornerRadius
				// tooltip.fillColor
				// tooltip.font...
				// tooltip.text
				// tooltip.x
				// tooltip.y
				// tooltip.caretX
				// tooltip.caretY
				// etc...
			}
		}
	}
});
```

See `samples/tooltips/line-customTooltips.html` for examples on how to get started.

### Writing New Chart Types

Chart.js 2.0 introduces the concept of controllers for each dataset. Like scales, new controllers can be written as needed.

```javascript
Chart.controllers.MyType = Chart.DatasetController.extend({

});


// Now we can create a new instance of our chart, using the Chart.js API
new Chart(ctx, {
	// this is the string the constructor was registered at, ie Chart.controllers.MyType
	type: 'MyType',
	data: data,
	options: options
});
```

#### Dataset Controller Interface

Dataset controllers must implement the following interface.

```javascript
{
	// Create elements for each piece of data in the dataset. Store elements in an array on the dataset as dataset.metaData
	addElements: function() {},

	// Create a single element for the data at the given index and reset its state
	addElementAndReset: function(index) {},

	// Draw the representation of the dataset
	// @param ease : if specified, this number represents how far to transition elements. See the implementation of draw() in any of the provided controllers to see how this should be used
	draw: function(ease) {},

	// Remove hover styling from the given element
	removeHoverStyle: function(element) {},

	// Add hover styling to the given element
	setHoverStyle: function(element) {},

	// Update the elements in response to new data
	// @param reset : if true, put the elements into a reset state so they can animate to their final values
	update: function(reset) {},
}
```

The following methods may optionally be overridden by derived dataset controllers
```javascript
{
	// Initializes the controller
	initialize: function(chart, datasetIndex) {},

	// Ensures that the dataset represented by this controller is linked to a scale. Overridden to helpers.noop in the polar area and doughnut controllers as these
	// chart types using a single scale
	linkScales: function() {},

	// Called by the main chart controller when an update is triggered. The default implementation handles the number of data points changing and creating elements appropriately.
	buildOrUpdateElements: function() {}
}
```

### Extending Existing Chart Types

Extending or replacing an existing controller type is easy. Simply replace the constructor for one of the built in types with your own.

The built in controller types are:
* `Chart.controllers.line`
* `Chart.controllers.bar`
* `Chart.controllers.radar`
* `Chart.controllers.doughnut`
* `Chart.controllers.polarArea`
* `Chart.controllers.bubble`

#### Bar Controller
The bar controller has a special property that you should be aware of. To correctly calculate the width of a bar, the controller must determine the number of datasets that map to bars. To do this, the bar controller attaches a property `bar` to the dataset during initialization. If you are creating a replacement or updated bar controller, you should do the same. This will ensure that charts with regular bars and your new derived bars will work seamlessly.

### Creating Plugins

Starting with v2.1.0, you can create plugins for chart.js. To register your plugin, simply call `Chart.plugins.register` and pass your plugin in.
Plugins will be called at the following times
* Start of initialization
* End of initialization
* Start of update
* After the chart scales have calculated
* Start of datasets update
* End of datasets update
* End of update (before render occurs)
* Start of draw
* End of draw
* Before datasets draw
* After datasets draw
* Resize
* Before an animation is started
* When an event occurs on the canvas (mousemove, click, etc). This requires the `options.events` property handled

Plugins should derive from Chart.PluginBase and implement the following interface
```javascript
{
	beforeInit: function(chartInstance) { },
	afterInit: function(chartInstance) { },

	resize: function(chartInstance, newChartSize) { },

	beforeUpdate: function(chartInstance) { },
	afterScaleUpdate: function(chartInstance) { }
	beforeDatasetsUpdate: function(chartInstance) { }
	afterDatasetsUpdate: function(chartInstance) { }
	afterUpdate: function(chartInstance) { },

	// This is called at the start of a render. It is only called once, even if the animation will run for a number of frames. Use beforeDraw or afterDraw
	// to do something on each animation frame
	beforeRender: function(chartInstance) { },

	// Easing is for animation
	beforeDraw: function(chartInstance, easing) { },
	afterDraw: function(chartInstance, easing) { },
	// Before the datasets are drawn but after scales are drawn
	beforeDatasetsDraw: function(chartInstance, easing) { },
	afterDatasetsDraw: function(chartInstance, easing) { },

	destroy: function(chartInstance) { }

	/**
	 * Called when an event occurs on the chart
	 * @param e {Core.Event} the Chart.js wrapper around the native event. e.native is the original event
	 * @return {Boolean} true if the chart is changed and needs to re-render
	 */
	onEvent: function(chartInstance, e) {}
}
```

### Building Chart.js

Chart.js uses <a href="http://gulpjs.com/" target="_blank">gulp</a> to build the library into a single JavaScript file.

Firstly, we need to ensure development dependencies are installed. With node and npm installed, after cloning the Chart.js repo to a local directory, and navigating to that directory in the command line, we can run the following:

```bash
npm install
npm install -g gulp
```

This will install the local development dependencies for Chart.js, along with a CLI for the JavaScript task runner <a href="http://gulpjs.com/" target="_blank">gulp</a>.

Now, we can run the `gulp build` task.

```bash
gulp build
```
