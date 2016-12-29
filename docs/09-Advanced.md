---
title: Advanced usage
anchor: advanced-usage
---

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
