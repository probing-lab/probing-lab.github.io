---
name:           "Coupon Collector 4"
numvars:        "6"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

Coupon Collector 4 

```python
f = 0
g = 0
a = 0
b = 0
c = 0
d = 0
while true:
   f = Bernoulli(1/2)
   g = Bernoulli(1/2)
   a = a + (1-a)*f*g
   b = b + (1-b)*f*(1-g)
   c = c + (1-c)*(1-f)*g
   d = d + (1-d)*(1-f)*(1-g)
end
```

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
  <script>
    var x = [];
    var y = [];
    var z = [];
    var u = [];
    var o = [];
    var l = [];
    
    var sim = 1000;
    var n   = 100;
    
    var f   = 0;
    var g   = 0;
    var a   = 0;
    var b   = 0;
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
          if (Math.random() < 0.5){
             g = 1;
          }else{
             g = 0;
          }
          a = a + (1-a)*f*g;
          b = b + (1-b)*f*(1-g);
          c = c + (1-c)*(1-f)*g;
          d = d + (1-d)*(1-f)*(1-g);
       }
       x[i] = f;
       y[i] = g;
       z[i] = a;
       u[i] = b;
       o[i] = c;
       l[i] = d;
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
      name: 'Variable g',
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
      name: 'Variable a',
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
    var trace4 = {
      x: u,
      name: 'Variable b',
       type: 'histogram',
			histnorm: 'probability',
			  marker: { 
			     color: "rgba(155, 100, 50, 0.7)", 
                 line: { color:  "rgba(155, 100, 50, 1)", 
                         width: 1
                 }
              
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var trace5 = {
      x: o,
      name: 'Variable c',
       type: 'histogram',
			histnorm: 'probability',
			  marker: { 
			     color: "rgba(55, 50, 102, 0.7)", 
                 line: { color:  "rgba(55, 50, 102, 1)", 
                         width: 1
                 }
              
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var trace6 = {
      x: l,
      name: 'Variable d',
       type: 'histogram',
			histnorm: 'probability',
			  marker: { 
			     color: "rgba(55, 100, 102, 0.7)", 
                 line: { color:  "rgba(55, 100, 102, 1)", 
                         width: 1
                 }
              
              },
              autobinx: false, 
              xbins: { 
                 size: 1 
              }
    };
    var data = [trace1,trace2,trace3,trace4,trace5,trace6];
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
