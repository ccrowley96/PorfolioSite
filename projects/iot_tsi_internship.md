---
title: Microsoft Azure Internship
subtitle: Azure Internet of Thing Time Series Insights Team, Redmond WA
date: 2019-08-02
externalLink: 
images:
tags: 
    - microsoft
    - javascript
    - react
    - d3
---

## Project 

## Responsibity 

## Tech Stack 

<div id="tsi-root" style="height: 400px;">
</div>
<div>
    <label>isTemporal </label>
    <select onchange='(function(){ toggleChartOption("isTemporal", (event.target.value === "true")) })(event)'>
            <option value="true">true</option>
            <option value="false" selected="">false</option>
    </select>
</div>


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
    legend: 'compact', 
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
        data.push({[`Factory${i}`]: lines});
        for(let j = 0; j < 3; j++){
            let values = {};
            lines[`Station${j}`] = values;
            for(let k = 0; k < 5; k++){
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