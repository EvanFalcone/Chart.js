---
title: Line Chart
anchor: line-chart
---

### Scatter Line Charts

Scatter line charts can be created by changing the X axis to a linear axis. To use a scatter chart, data must be passed as objects containing X and Y properties. The example below creates a scatter chart with 3 points.

```javascript
var scatterChart = new Chart(ctx, {
	type: 'line',
	data: {
		datasets: [{
			label: 'Scatter Dataset',
			data: [{
				x: -10,
				y: 0
			}, {
				x: 0,
				y: 10
			}, {
				x: 10,
				y: 5
			}]
		}]
	},
	options: {
		scales: {
			xAxes: [{
				type: 'linear',
				position: 'bottom'
			}]
		}
	}
});
```

### Stacked Charts

Stacked area charts can be created by setting the Y axis to a stacked configuration. The following example would have stacked lines.

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
```