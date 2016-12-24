# Stacked Area Chart

Line charts can be configured into stacked area charts by changing the settings on the y axis to enable stacking. Stacked area charts can be used to show how one data trend is made up of a number of smaller pieces.

```javascript
var stackedLine = new Chart(ctx, {
    type: 'line',
    data: data,
    options: {
        scales: {
            yAxes: [{
                stacked: true
            }]
        }
    }
});