# Configuration Options

Unlike other charts, the radar chart has no chart specific options.

# Scale Options

The radar chart supports only a single scale. The options for this scale are defined in the `scale` property.

```javascript
options = {
    scale: {
        // Hides the scale
        display: false
    }
};
```

# Default Options

It is common to want to apply a configuration setting to all created radar charts. The global radar chart settings are stored in `Chart.defaults.radar`. Changing the global options only affects charts created after the change. Existing charts are not changed.