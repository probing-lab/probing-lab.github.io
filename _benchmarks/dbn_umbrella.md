---
name:           "DBN Umbrella"
numvars:        "2"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

DBN Umbrella

```python
rain = Bernoulli(r0)
umbrella = Bernoulli(u0)
while true:
    if rain == 1:
        rain = Bernoulli(r1)
    else:
        rain = Bernoulli(r2)
    end

    if rain == 1:
        umbrella = Bernoulli(u1)
    else:
        umbrella = Bernoulli(u2)
    end
end

```


<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
  <script>
    var rain     = [];
    var umbrella = [];
    
    var sim = 1000;   //Number of simulations
    var n   = 100;    //Number of iterations
    
    var r0 = 0.5;
    var u0 = 0.5;
    
    var r1 = 0.3;
    var r2 = 0.8;
    
    var u1 = 0.3;
    var u2 = 0.8;
    
    for (var i = 0; i < sim; i++) {
       rain_v     = (Math.random() < r0);
       umbrella_v = (Math.random() < u0);
       
       for (var j = 0; j < n; j++){
          if (rain_v){
             rain_v     = (Math.random() < r1);
             umbrella_v = (Math.random() < u1);
          }else{
             rain_v     = (Math.random() < u1);
             umbrella_v = (Math.random() < u2);
          }
       }
       rain[i]     = rain_v;
       umbrella[i] = umbrella_v;
    } 
    var trace1 = {
      x: rain,
      name: 'Variable Rain',
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
      x: umbrella,
      name: 'Variable Umbrella',
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
    var data = [trace1,trace2];
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
