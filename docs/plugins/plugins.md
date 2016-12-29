# Plugins

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

Plugins must implement the following interface:
```javascript
{
    /**
     * At the start of the initialization process
     * @param chartInstance {Core.Controller} the chart that is initializing
     */
    beforeInit: function(chartInstance) { },

    /**
     * At the end of the initialization process
     * @param chartInstance {Core.Controller} the chart that is being created
     */
    afterInit: function(chartInstance) { },

    /**
     * When the chart resizes
     * @param chartInstance {Core.Controller} the chart that is resizing
     * @param newChartSize {Size} the new size of the chart
     */
    resize: function(chartInstance, newChartSize) { },

    /** 
     * At the start of the update process
     * @param chartInstance {Core.Controller} the chart that is updating
     */
    beforeUpdate: function(chartInstance) { },

    /** 
     * After scales have updated but before datasets update and before any new dataset controllers are created
     * @param chartInstance {Core.Controller} the chart that is updating
     */
    afterScaleUpdate: function(chartInstance) { }

    /**
     * Called when datasets begin updating
     * @param chartInstance {Core.Controller} the chart that is updating
     */
    beforeDatasetsUpdate: function(chartInstance) { }

    /** 
     * When datasets finish updating
     * @param chartInstance {Core.Controller} the chart that is updating
     */
    afterDatasetsUpdate: function(chartInstance) { }

    /**
     * At the end of the update process
     * @param chartInstance {Core.Controller} the chart that is updating
     */
    afterUpdate: function(chartInstance) { },

    /**
     * This is called at the start of a render. It is only called once, even if the animation will run for a number of frames. 
     * Use beforeDraw or afterDraw to do something on each animation frame
     * @param chartInstance {Core.Controller} the chart that is rendering
     */
    beforeRender: function(chartInstance) { },

    /**
     * Called at the start of drawing for each frame of an animation
     * @param chartInstance {Core.Controller} the chart that is drawing
     * @param easing {Number} In the range of [0, 1] which represents the percentage into the animation. A value of 1 represents the end of the animation.
     */
    beforeDraw: function(chartInstance, easing) { },

    /**
     * Called at the end of drawing for each frame of an animation
     * @param chartInstance {Core.Controller} the chart that is drawing
     * @param easing {Number} In the range of [0, 1] which represents the percentage into the animation. A value of 1 represents the end of the animation.
     */
    afterDraw: function(chartInstance, easing) { },

    /**
     * Called after scales are drawn but before the datasets (points, line, etc) are drawn
     * @param chartInstance {Core.Controller} the chart that is drawing
     * @param easing {Number} In the range of [0, 1] which represents the percentage into the animation. A value of 1 represents the end of the animation.
     */
    beforeDatasetsDraw: function(chartInstance, easing) { },

    /**
     * Called after drawing datasets for each frame of an animation
     * @param chartInstance {Core.Controller} the chart that is drawing
     * @param easing {Number} In the range of [0, 1] which represents the percentage into the animation. A value of 1 represents the end of the animation.
     */
    afterDatasetsDraw: function(chartInstance, easing) { },

    /**
     * When the chart is being destroyed
     * @param chartInstance {Core.Controller} the chart that is being destroyed
     */
    destroy: function(chartInstance) { }

    /**
     * Called when an event occurs on the chart
     * @param chartInstance {Core.Controller} the chart that received the event
     * @param e {Core.Event} the Chart.js wrapper around the native event. e.native is the original event
     * @return {Boolean} true if the chart is changed and needs to re-render
     */
    onEvent: function(chartInstance, e) {}
}
```