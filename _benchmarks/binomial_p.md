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

Parametric Binomial Source Code:

```python
x = 0
while true:
    x = x + 1 {p} x
end
```
<br>

Computing the first moment of variable x using POLAR/Mora:

```
python polar.py benchmarks/old/binomial --goals "E(x)"

8888888b.   .d88888b.  888             d8888 8888888b.
888   Y88b d88P" "Y88b 888            d88888 888   Y88b
888    888 888     888 888           d88P888 888    888
888   d88P 888     888 888          d88P 888 888   d88P
8888888P"  888     888 888         d88P  888 8888888P"
888        888     888 888        d88P   888 888 T88b
888        Y88b. .d88P 888       d8888888888 888  T88b
888         "Y88888P"  88888888 d88P     888 888   T88b

By the ProbInG group



-------------------
- Analysis Result -
-------------------

E(x) = 0; n*p
Solution is exact

Elapsed time: 0.3568592071533203 s
```
<p>
First moment solution: \[\mathbb{E} (x_n)   = n p\]
</p>

Computing the second moment of variable x using POLAR/Mora:

```
python polar.py benchmarks/old/binomial --goals "E(x^2)"

8888888b.   .d88888b.  888             d8888 8888888b.
888   Y88b d88P" "Y88b 888            d88888 888   Y88b
888    888 888     888 888           d88P888 888    888
888   d88P 888     888 888          d88P 888 888   d88P
8888888P"  888     888 888         d88P  888 8888888P"
888        888     888 888        d88P   888 888 T88b
888        Y88b. .d88P 888       d8888888888 888  T88b
888         "Y88888P"  88888888 d88P     888 888   T88b

By the ProbInG group



-------------------
- Analysis Result -
-------------------

E(x**2) = 0; n*p*(p*(n - 1) + 1)
Solution is exact

Elapsed time: 0.4016072750091553 s
```

<p>
Second moment solution: \[\mathbb{E} (x_n^2) = n p (p (n - 1) + 1)\]
</p>

Computing the third moment of variable x using POLAR/Mora:

```
python polar.py benchmarks/old/binomial --goals "E(x^3)"

8888888b.   .d88888b.  888             d8888 8888888b.
888   Y88b d88P" "Y88b 888            d88888 888   Y88b
888    888 888     888 888           d88P888 888    888
888   d88P 888     888 888          d88P 888 888   d88P
8888888P"  888     888 888         d88P  888 8888888P"
888        888     888 888        d88P   888 888 T88b
888        Y88b. .d88P 888       d8888888888 888  T88b
888         "Y88888P"  88888888 d88P     888 888   T88b

By the ProbInG group



-------------------
- Analysis Result -
-------------------

E(x**3) = 0; n*p*(n**2*p**2 - 3*n*p**2 + 3*n*p + 2*p**2 - 3*p + 1)
Solution is exact

Elapsed time: 0.5916872024536133 s
```

<p>
Third moment solution: \[\mathbb{E} (x_n^3) = n p (n^2 p^2 - 3 n p^2 + 3 n p + 2p^2 - 3p + 1)\]
</p>

Computing the fourth moment of variable x using POLAR/Mora:

```
python polar.py benchmarks/old/binomial --goals "E(x^4)"

8888888b.   .d88888b.  888             d8888 8888888b.
888   Y88b d88P" "Y88b 888            d88888 888   Y88b
888    888 888     888 888           d88P888 888    888
888   d88P 888     888 888          d88P 888 888   d88P
8888888P"  888     888 888         d88P  888 8888888P"
888        888     888 888        d88P   888 888 T88b
888        Y88b. .d88P 888       d8888888888 888  T88b
888         "Y88888P"  88888888 d88P     888 888   T88b

By the ProbInG group



-------------------
- Analysis Result -
-------------------

E(x**4) = 0; n*p*(n**3*p**3 - 6*n**2*p**3 + 6*n**2*p**2 + 11*n*p**3 - 18*n*p**2 + 7*n*p - 6*p**3 + 12*p**2 - 7*p + 1)
Solution is exact

Elapsed time: 0.7818460464477539 s
```

<p>
  Fourth moment solution: \[\mathbb{E} (x_n^4) = n p (n^3 p^3 - 6 n^2 p^3 + 6 n^2 p^2 + 11 n p^3 - 18 n p^2 + 7 n p - 6 p^3 + 12 p^2 - 7 p + 1)\]
</p>

Simulation 

<div>
  <label for="num_experiment">Number of program executions: </label>
  <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100">
  <br>
  <label for="num_iteration">Number of loop iterations: </label>
  <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10">
  <br>
  <label for="probability">Probability p: </label>
  <input type="range" id="probability" name="probability" min="0" max="1" step="0.1">
</div>

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
