---
title: Microsoft Azure Internship
subtitle: Azure Internet of Thing Time Series Insights Team, Redmond WA
date: 2019-08-02
externalLink: 
images:
tags: 
    - microsoft
    - typescript
    - react
    - d3
---
<div id="tsi-root" style="height: 400px;">
</div>
<div>
    <label>Time Slider</label>
    <select onchange='(function(){ toggleChartOption("isTemporal", (event.target.value === "true")) })(event)'>
            <option value="true">true</option>
            <option value="false" selected="">false</option>
    </select>
</div>

### Azure IOT TSI Internship
During the summer of 2019, I interned at Microsoft Redmond on the Azure Internet of Things (IOT) Time Series Insights (TSI) team. My project was to build a scatter plot visualization capable of displaying large sets of time-series data sourced from IOT sensors.  The visualization aids in understanding trends and anomalies in time-series data. Once the scatter plot component was complete, I integrated it into the team's <a href="https://insights.timeseries.azure.com/preview/demo" target="_blank">Time Series Insights data explorer dashboard</a>, using React, Redux, SCSS, and TypeScript.

Over the course of the 3 month internship, I learned how to use the <a href ="https://d3js.org/" target="_blank">D3.js</a> visualization library to create the SVG based web visualization you can see above.  I learned TypeScript, a JavaScript variant that allows strict syntactical typing.  I learned SCSS, a CSS extension language, making CSS styling easier and more consistent. I addition, I learned best React and Redux (a state management tool) practices from professional front-end engineers.

The scatter plot shown above visualizes 3 axes of data: a horizontal x-axis, a vertical y-axis, and radial r-axis (the diameter of each dot). This example illustrates two factories, each with three sensors transmitting IOT data (randomly generated in this case). Each factory is assigned a color and each sensor within that factory is assigned a shade of the factory color. On the left side (top on mobile) of the scatter plot, is a legend which allows the user to toggle factory and sensor visibility as well as highlight a specific sensor's data.  The legend can also be resized, which will dynamically scale each axis and its respective labels.  Clicking on a sensor data point or on a sensor legend label will highlight that sensors data and lock the mouse hover interaction to target only data from that sensor.

On the bottom left of the visualization, you'll see a toggle labeled **Time Slider**.  If toggled to *true*, the plot will visualize the data in chronological order, slicing up time, and visualizing only the sensor data for a given time slice. This allows the user to visualize specific times, locating timestamps using the slider at the bottom of the plot.

When you hover a mouse over the visualization, a crosshair and tooltip locates the closest point and gives more detailed information about the 3 axis values and that point's timestamp. This was achieved using a mathematical *voronoi diagram*, which partitions a plane into regions, divided by closeness to each point on the plane. Voronoi diagrams are really cool.  The image below shows the Voronoi diagram for a scatter plot with visible partitions.

**Scatter Plot Showing Voronoi Diagram**
![Voronoi Diagram](/img/azure_iot_internship/voronoi_grid_visible.png)


<script src="https://unpkg.com/tsiclient@1.3.19/tsiclient.js"></script>
<link rel="stylesheet" type="text/css" href="https://unpkg.com/tsiclient@1.3.19/tsiclient.css"></link>

<script>
let data;
let chartDataOptions;
let scatterPlot;

// Set chart options
let chartOptions = {
    theme: 'light',
    yExtent: [0,1], 
    legend: screen.width > 650 ? 'shown' : 'compact', 
    offset: 'Local', 
    tooltip: true, 
    canDownload: false, 
    hideChartControlPanel: false, 
    is24HourTime: false, 
    singleLineXAxisLabel: '',
    xAxisHidden: false, 
    yAxisHidden: false,
    includeDots: false,
    includeEnvelope: false,
    interpolationFunction: 'curveMonotoneX',
    yAxisState: 'stacked',
    brushHandlesVisible: false,
    snapBrush: false,
    stacked: false, 
    zeroYAxis: true,
    arcWidthRatio: 1,
    spMeasures: ['avg', 'min', 'max'],
    isTemporal: false,
    spAxisLabels: null
}

function toggleChartOption(property, value = null) {
    //if value is null, assume a toggle
    chartOptions[property] = (value === null) ? !chartOptions[property] : value; 
    scatterPlot.render(data, chartOptions, chartDataOptions);
}

window.onload = function(){
    // Create fake data
    data = [];
    let minute = 60*1000
    let from = new Date(Math.floor(new Date(new Date().valueOf() / minute)) * minute);
    let to;
    for(let i = 0; i < 2; i++){
        let lines = {};
        data.push({[`Factory ${i}`]: lines});
        for(let j = 0; j < 3; j++){
            let values = {};
            lines[`Sensor ${j}`] = values;
            for(let k = 0; k < 10; k++){
                // if(!(k%2 && k%3)){  // if check is to create some sparseness in the data
                    to = new Date(from.valueOf() + 1000*60*k);
                    let val = Math.random() / 2 + .25;
                    let minVal = val - (Math.random() / 10);
                    let maxVal = val + (Math.random() / 10);
                    values[to.toISOString()] = {avg: val, min: minVal, max: maxVal};
                // }
            } 
        }
    }
    
    // render the data in a chart
    let tsiClient = new TsiClient();
    let searchSpan = {
        from: from.toISOString(),
        to: to.toISOString(),
        bucketSize: '1d'
    }
    chartDataOptions = data.map(d => {
        return {searchSpan: searchSpan};
    });

    scatterPlot = new tsiClient.ux.ScatterPlot(document.getElementById('tsi-root'))
    scatterPlot.render(data, chartOptions, chartDataOptions);
}
</script>