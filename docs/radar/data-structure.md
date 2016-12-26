# Data Structure

The `data` property of a dataset for a radar chart is specified as a an array of numbers. Each point in the data array corresponds to the label at the same index on the x axis. 

```javascript
data: [20, 10]
```

For a radar chart, to provide context of what each point means, we include an array of strings that show around each point in the chart.

```javascript
data: {
    labels: ['Running', 'Swimming', 'Eating', 'Cycling'],
    datasets: [{
        data: [20, 10, 4, 2]
    }]
}
```