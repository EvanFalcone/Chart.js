#
Selecting the Correct Build

Chart.js provides two different builds that are available for your use.

## Stand-Alone Build
Files:
* `dist/Chart.js`
* `dist/Chart.min.js`

This version only includes Chart.js. If this version is used and you require the use of the time axis, [Moment.js](http://momentjs.com/) will need to be included before Chart.js.

## Bundled Build
Files:
* `dist/Chart.bundle.js`
* `dist/Chart.bundle.min.js`

The bundled version includes Moment.js built into the same file. This version should be used if you wish to use time axes and want a single file to include. Do not use this build if your application already includes Moment.js. If you do, Moment.js will be included twice, increasing the page load time and potentially introducing version issues.