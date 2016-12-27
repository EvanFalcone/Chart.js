# Axes

Axes are an integral part of a chart. They are used to determine how data maps to a pixel value on the chart. In a cartesian chart, there is 1 or more X axis and 1 or more Y axis to map points onto the 2 dimensional canvas. These axes are know as ['cartesian axes'](../axes/cartesian-axes.md#cartesian-axes).

In a radial chart, such as a radar chart or a polar area chart, there is a single axis that maps points in the angular and radial directions. These are known as ['radial axes'](../axes/radial-axes.md#radial-axes).

Scales in Chart.js >V2.0 are significantly more powerful, but also different than those of v1.0.
* Multiple X & Y axes are supported.
* A built-in label auto-skip feature detects would-be overlapping ticks and labels and removes every nth label to keep things displaying normally.
* Scale titles are supported
* New scale types can be extended without writing an entirely new chart type
