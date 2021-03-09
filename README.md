# chartjs-plugin-annotation.js

[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/chartjs/chartjs-plugin-annotation/Node.js%20CI)](https://github.com/chartjs/chartjs-plugin-annotation/actions/workflows/ci.yml)
[![release](https://img.shields.io/github/v/release/chartjs/chartjs-plugin-annotation?include_prereleases)](https://github.com/chartjs/chartjs-plugin-annotation/releases)
[![npm (latest)](https://img.shields.io/npm/v/chartjs-plugin-annotation/latest)](https://www.npmjs.com/package/chartjs-plugin-annotation/v/latest)
[![npm (next)](https://img.shields.io/npm/v/chartjs-plugin-annotation/next)](https://www.npmjs.com/package/chartjs-plugin-annotation/v/next)

An annotation plugin for Chart.js >= 3.0.0

For Chart.js 2.4.0 to 2.9.x support, use [version 0.5.7 of this plugin](https://github.com/chartjs/chartjs-plugin-annotation/releases/tag/v0.5.7)

This plugin draws lines, boxes, points and ellipses on the chart area.

Annotations work with line, bar, scatter and bubble charts that use linear, logarithmic, time, or category scales. Annotations will not work on any chart that does not have exactly two axes, including pie, radar, and polar area charts.

![Example Screenshot from Dropbox](https://www.dropbox.com/s/92cmt8zrth55z55/Screenshot%202017-05-20%2018.26.39.png?raw=1)

[View this example on CodePen](https://codepen.io/compwright/full/mmQMrZ/)

## Configuration

To configure the annotations plugin, you can simply add new config options to your chart config.

```javascript
{
    plugins: {
        annotation: {
            // Defines when the annotations are drawn.
            // This allows positioning of the annotation relative to the other
            // elements of the graph.
            //
            // Should be one of: afterDraw, afterDatasetsDraw, beforeDraw, beforeDatasetsDraw
            // See http://www.chartjs.org/docs/#advanced-usage-creating-plugins
            drawTime: 'afterDatasetsDraw', // (default)

            // Double-click speed in ms used to distinguish single-clicks from
            // double-clicks whenever you need to capture both. When listening for
            // both click and dblclick, click events will be delayed by this
            // amount.
            dblClickSpeed: 350, // ms (default)

            // Fires when an annotation is hovered.
            enter: function(context) {
                // context: {chart, element}
            },

            // Array of annotation configuration objects
            // or Object with the annotation configuration objects, one for each key
            // See below for detailed descriptions of the annotation options
            annotations: [{
                drawTime: 'afterDraw', // overrides annotation.drawTime if set
                display: true,
                type: 'line',
                scaleID: 'y',
                value: '25',
                borderColor: 'red',
                borderWidth: 2,

                // Event hooks can be defined per annotation (`click` below) or
                // at chart level (`enter` above). If defined in both places,
                // the one defined per annotation takes precedence.

                // Fires when the user clicks this annotation on the chart
                click: function(context) {
                   // context: {chart, element}
                }
            }]
        }
    }
}
```

### Line Annotations

```javascript
{
    type: 'line',

    // If true, display the annotation, default is true.
    // A callback can also be used:
    //   display(context) {
    //     // context: {chart, options}
    //     return true;
    //   },
    display: true,

    // optional drawTime to control layering, overrides global drawTime setting.
    drawTime: 'afterDatasetsDraw',

    // ID of the scale to bind onto.
    scaleID: 'y',

    // Data value to draw the line at.
    value: 25,

    // Optional value at which the line draw should end.
    endValue: 26,

    // Alternative configuration of values, using two scales.
    xScaleID: 'x',
    yScaleID: 'y',
    xMin: 'January',
    yMin: 25,
    xMax: 'February',
    yMax: 26,

    // Line color, default is 'options.color'.
    borderColor: 'red',

    // Line width, default is 2.
    borderWidth: 2,

    // Line dash, default is [].
    // https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/setLineDash
    borderDash: [2, 2],

    // Line Dash Offset, default is 0.
    // https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineDashOffset
    borderDashOffset: 5,

    label: {
        // Background color of label, default is 'rgba(0,0,0,0.8)'.
        backgroundColor: 'rgba(0,0,0,0.8)',

        // optional drawTime to control labels' layering; defaults to this element's drawTime.
        drawTime: 'afterDatasetsDraw',

        font: {
            // Font family of text, inherits from global
            family: "sans-serif",

            // Font size of text, inherits from global
            size: 12,

            // Font style of text, default is 'bold'
            style: "bold",
        },

        // Color of label text, default is '#fff'.
        color: '#fff',

        // Padding of label to add left/right, default is 6.
        xPadding: 6,

        // Padding of label to add top/bottom, default is 6.
        yPadding: 6,

        // Radius of label rectangle, default is 6.
        cornerRadius: 6,

        // Anchor position of label on line, can be one of: 'start', 'center', 'end', default is 'center'.
        position: 'center',

        // Adjustment along x-axis (left-right) of label relative to above number (can be negative)
        // Negative values move the label left, positive right, default is 0.
        xAdjust: 0,

        // Adjustment along y-axis (top-bottom) of label, in pixels. (can be negative)
        // Negative values move the label up, positive down, default is 0.
        yAdjust: 0,

        // Whether the label is enabled and should be displayed, default is false.
        enabled: true,

        // Content to display in label - default is null. It could be a text, an array of text or an image. Provide an array to display texts on a new line.
        content: "Test label",

        // Overrides the width of the image. Could be set in pixel by a number, or in percentage of current width of image by a string, default is undefined.
        // If undefined, uses the width of the image.
        // It is used only when the content is an image.
        width: '50%',

        // Overrides the height of the image. Could be set in pixel by a number, or in percentage of current height of image by a string, default is undefined.
        // If undefined, uses the height of the image.
        // It is used only when the content is an image.
        height: 200,

        // Rotation of label, in degrees, or 'auto' to use the degrees of the line, default is 0.
        rotation: 90,
    },

    // Event hooks - context: {chart, element}
    enter: function(context) {},
    leave: function(context) {},
    click: function(context) {},
    dblclick: function(context) {}
}
```

## To-do Items

The following features still need to be done:

* Box annotation labels
* Text annotations

## Installation

To download a zip, go to the Chart.Annotation.js on Github

To install via npm:

```bash
npm install chartjs-plugin-annotation --save
```

Prior to v0.2.0 this plugin was known as Chart.Annotation.js. You can still install this old version via NPM.

## Documentation

You can find documentation for Chart.js at [www.chartjs.org/docs](http://www.chartjs.org/docs).

## Contributing

Before submitting an issue or a pull request to the project, please take a moment to look over the [contributing guidelines](CONTRIBUTING.md) first.

## License

Chart.Annotation.js is available under the [MIT license](http://opensource.org/licenses/MIT).
