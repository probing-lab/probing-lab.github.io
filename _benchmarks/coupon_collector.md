---
name:           "Coupon Collector"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

Coupon Collector

```python
f = 0
c = 0
d = 0
while true:
   f = 1 {1/2} 0
   c = 1 - f + c*f
   d = d + f - d*f
end
```

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
  <script>
    var x = [];
    var y = [];
    var z = [];
    
    var sim = 1000;
    var n   = 100;
    var f   = 0;
    var c   = 0;
    var d   = 0;
    for (var i = 0; i < sim; i++) {
       f = 0;
       c = 0;
       d = 0; 
       for (var j = 0; j < n; j++){
          if (Math.random() < 0.5){
             f = 1;
          }else{
             f = 0;
          }
          c = 1 - f + c*f;
          d = d + f - d*f;
       }
       x[i] = f;
       y[i] = c;
       z[i] = d;
    } 
    var trace1 = {
      x: x,
      name: 'Variable f',
       type: 'histogram',
			histnorm: 'probability',
			  marker: { 
			     color: "rgba(255, 100, 102, 0.7)", 
                 line: { color:  "rgba(255, 100, 102, 1)", 
                         width: 1
                 }
              
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var trace2 = {
      x: y,
      name: 'Variable c',
       type: 'histogram',
			histnorm: 'probability',
			   marker: {
			       color: "rgba(100, 200, 102, 0.7)",
			       line: { color:  "rgba(100, 200, 102, 1)", 
                      width: 1 } 
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var trace3 = {
      x: z,
      name: 'Variable d',
       type: 'histogram',
			histnorm: 'probability',
			  marker: { 
			     color: "rgba(155, 100, 102, 0.7)", 
                 line: { color:  "rgba(155, 100, 102, 1)", 
                         width: 1
                 }
              
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var data = [trace1,trace2,trace3];
    var layout = {
      bargap: 0.05, 
      bargroupgap: 0.2, 
      barmode: "overlay", 
      title: "Sampled Results (Num. simulations: 1000, Num. iterations: 100)", 
      xaxis: {title: "Value"}, 
      yaxis: {title: "Probability"}
    }
    Plotly.newPlot('myDiv', data, layout);
     
  </script>
