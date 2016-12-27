# Responsive Charts

Chart.js provides a few options for controlling resizing behaviour of charts.

## responsive
**Type:** Boolean
**Default:** `true`
Resizes the chart canvas when its container does.

```javascript
let options = {
    responsive: false
};
```

## responsiveAnimationDuration
**Type:** Number
**Default:** `0`
Duration in milliseconds it takes to animate to new size after a resize event.

```javascript
let options = {
    responsiveAnimationDuration: 100
};
```

## maintainAspectRatio
**Type:** Boolean
**Default:** `true`
Maintain the original canvas aspect ratio `(width / height)` when resizing.

```javascript
let options = {
    maintainAspectRatio: false
};
```