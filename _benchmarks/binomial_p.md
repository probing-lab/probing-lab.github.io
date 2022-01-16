---
name:           "Binomial(p)"
numvars:        "2"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Binomial(p)

```python
x = 0
while true:
    x = x + 1 {p} x
end
```

<p>
  When \(a \ne 0\), there are two solutions to \(ax^2 + bx + c = 0\) and they are
  \[x = {-b \pm \sqrt{b^2-4ac} \over 2a}.\]
  </p>

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
  <script>
    var x = [];
    sim = 10000;
    n   = 10;
    f   = 0;
    for (var i = 0; i < sim; i++) {
       f = 0;  
       for (var j = 0; j < n; j++){
          if (Math.random() < 0.5){
             f += 1;
          }
       }
       x[i] = f;
    } 
    var trace = {
      x: x,
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
    var data = [trace];
    var layout = {
      bargap: 0.05, 
      bargroupgap: 0.2, 
      barmode: "overlay", 
      title: "Sampled Results (p=0.5, loop iteration=10, num. simulations = 10000)", 
      xaxis: {title: "X Value"}, 
      yaxis: {title: "Probability"}
    }
    Plotly.newPlot('myDiv', data, layout);
     
  </script>
