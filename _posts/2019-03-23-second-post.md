---
title: "YBigTa Design Team Webstudy 01"
date: 2019-03-23 00:42:28 -0400
categories: jekyll update
---

겨울방학에 진행했던 웹스터디 결과물


<html>
<head>
  <!-- Plotly.js -->
  <meta charset="utf-8">
  <title>Plot.ly Map Visualization</title>
  <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
  <!-- Plotly chart will be drawn inside this DIV -->
  <div id="myDiv"></div>
    <!-- 'https://raw.githubusercontent.com/ybigtawebstudy/20190213_Charts/master/gangnam_cctv.csv' -->
    <script>
    Plotly.d3.csv('https://raw.githubusercontent.com/ybigtawebstudy/20190213_Charts/master/gangnam_cctv_eng.csv', function(err, rows){
    var classArray = unpack(rows, 'Purpose');
    var classes = [...new Set(classArray)];
    function unpack(rows, key) {
      return rows.map(function(row) { return row[key]; });
    }
    var data = classes.map(function(classes) {
      var rowsFiltered = rows.filter(function(row) {
          return (row.Purpose === classes);
      });
      return {
         type: 'scattermapbox',
         name: classes,
         lat: unpack(rowsFiltered, 'Latitude'),
         lon: unpack(rowsFiltered, 'Longitude')
      };
    });
    var layout = {
       title: '강남구 CCTV',
       hovermode: 'closest',
       font: {
           color: 'white'
       },
      dragmode: 'zoom',
      mapbox: {
        center: {
          lat: 37.500396,
          lon: 127.074379
        },
        domain: {
          x: [0, 1],
          y: [0, 1]
        },
        style: 'dark',
        zoom: 12
      },
      margin: {
        r: 20,
        t: 40,
        b: 20,
        l: 20,
        pad: 0
      },
      paper_bgcolor: '#191A1A',
      plot_bgcolor: '#191A1A',
      showlegend: true,
       annotations: [{
           x: 0,
         y: 0,
         xref: 'paper',
         yref: 'paper',
           showarrow: false
       }]
    };
  Plotly.setPlotConfig({
    mapboxAccessToken: 'pk.eyJ1IjoiZXRwaW5hcmQiLCJhIjoiY2luMHIzdHE0MGFxNXVubTRxczZ2YmUxaCJ9.hwWZful0U2CQxit4ItNsiQ'
  });
  Plotly.plot('myDiv', data, layout, {showSendToCloud: true});
});
          </script>
      </body>
</html>
