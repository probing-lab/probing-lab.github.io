---
name:           "Binomial (Parametric)"
numvars:        "2"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Parametric Binomial Code

```python
x = 0
while true:
    x = x + 1 {p} x
end
```

Computing Moments using POLAR/Mora

<p>
```
python polar.py benchmarks/old/binomial --goals "E(x)"
```

  \[\mathbb{E} (x_n)   = n p\]
  \[\mathbb{E} (x_n^2) = n p (p (n - 1) + 1)\]
  \[\mathbb{E} (x_n^3) = n p (n^2 p^2 - 3 n p^2 + 3 n p + 2p^2 - 3p + 1)\]
  \[\mathbb{E} (x_n^4) = n p (n^3 p^3 - 6 n^2 p^3 + 6 n^2 p^2 + 11 n p^3 - 18 n p^2 + 7 n p - 6 p^3 + 12 p^2 - 7 p + 1)\]
</p>

Simulation 
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
