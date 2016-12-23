# Data Structure

The `data` property of a dataset for a line chart can be passed in two formats. 

## Number[]
```javascript
data: [20, 10]
```

When the `data` array is an array of numbers, the x axis is generally a [category](../axes/cartesian/category.md#Category Axis). The points are placed onto the axis using their position in the array.

## Point[]

```javascript
data: [{
        x: 10,
        y: 20
    }, {
        x: 15,
        y: 10
    }]
```

This alternate is used for sparse datasets, such as those in [scatter charts](../scatter/scatter.md#scatter-chart). Each data point is specified using an object containing `x` and `y` properties.