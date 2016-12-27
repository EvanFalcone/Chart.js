# Updating Axis Defaults

The default configuration for a scale can be easily changed using the scale service. All you need to do is to pass in a partial configuration that will be merged with the current scale default configuration to form the new default.

For example, to set the minimum value of 0 for all linear scales, you would do the following. Any linear scales created after this time would now have a minimum of 0.

```javascript
Chart.scaleService.updateScaleDefaults('linear', {
    ticks: {
        min: 0
    }
});
```