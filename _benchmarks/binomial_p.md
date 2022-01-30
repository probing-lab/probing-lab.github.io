---
name:           "Binomial (Parametric)"
numvars:        "1"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Parametric Binomial (Source Code):

```python
x = 0
while true:
    x = x + 1 {p} x
end
```
<br>

Dependency Graph of Program Variables:
(L) Linear dependency, (N) nonlinear dependency

<img src="/assets/dep_graphs/binomial-p.png" alt="Dependency Graph" style="width:100px;"/>

<br>

| Program features | Value |
| --- | --- |
| if statements | No |
| State space | infinite, discrete |
| Circular dependency | No |
| Symbolic Constants | Yes (p) |
| Effective Variables | Yes (x) |
| Defective Variables | No |

<table>
    <thead>
        <tr>
            <th>Program features</th>
            <th>Value</th>
            <th>Dependency Graph</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>if statements</td>
            <td>No</td>
            <td rowspan=6><img src="/assets/dep_graphs/binomial-p.png" alt="Dependency Graph" style="width:100px;"/></td>
        </tr>
        <tr>
            <td>State space</td>
            <td>infinite, discrete</td>
        </tr>
        <tr>
            <td>Circular Dependency</td>
            <td>No</td>
        </tr>
        <tr>
            <td>Symbolic Constants</td>
            <td>Yes (p)</td>
        </tr>
        <tr>
            <td>Effective Variables</td>
            <td>Yes (x)</td>
        </tr>
        <tr>
            <td>Defective Variables</td>
            <td>No</td>
        </tr>
    </tbody>
</table>

<br>
Computing the first moment for the random variable x using POLAR:

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
Solution for first moment: \[\mathbb{E} (x_n)   = n p\]
</p>

<br>

Computing the second moment for the random variable x using POLAR:

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
Solution for the second moment: \[\mathbb{E} (x_n^2) = n p (p (n - 1) + 1)\]
</p>

<br>


Computing the third moment for the random variable x using POLAR:

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
Solution for the third moment: \[\mathbb{E} (x_n^3) = n p (n^2 p^2 - 3 n p^2 + 3 n p + 2p^2 - 3p + 1)\]
</p>

<br>

Computing the fourth moment for the random variable x using POLAR:

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
  Solution for the fourth moment: \[\mathbb{E} (x_n^4) = n p (n^3 p^3 - 6 n^2 p^3 + 6 n^2 p^2 + 11 n p^3 - 18 n p^2 + 7 n p - 6 p^3 + 12 p^2 - 7 p + 1)\]
</p>

<br>


Program simulation:

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |
| Probability (p): | <input type="number" id="probability_value" name="probability_value" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability(this.value)"> | <input type="range" id="probability" name="probability" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability(this.value)"> |

| Exact E(x) | Approx. E(x) | Exact E(x<sup>2</sup>)| Approx. E(x<sup>2</sup>) | 
| --- | --- | --- | --- | --- | --- | --- | --- |
| <input type="text" size="5" id="exact_e_x" name="exact_e_x"> | <input type="text" size="5" id="approx_e_x" name="approx_e_x"> | <input type="text" size="5" id="exact_e_x2" name="exact_e_x2"> |  <input type="text" size="5" id="approx_e_x2" name="approx_e_x2"> |  

| Exact E(x<sup>3</sup>)| Approx. E(x<sup>3</sup>) | Exact E(x<sup>4</sup>)| Approx. E(x<sup>4</sup>) |
| --- | --- | --- | --- |
|  <input type="text" size="5" id="exact_e_x3" name="exact_e_x3">   |  <input type="text" size="5" id="approx_e_x3" name="approx_e_x3">     |  <input type="text" size="5" id="exact_e_x4" name="exact_e_x4">    | <input type="text" size="5" id="approx_e_x4" name="approx_e_x4">     |



<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }
    function plotProbProgram (val_p, nit, nsim){
        var x = [];
        var tot1 = 0;
        var tot2 = 0;
        var tot3 = 0;
        var tot4 = 0;
    	for (var i = 0; i < nsim; i++) {
             x[i] = 0;  
             for (var j = 0; j < nit; j++)
            	x[i] += sampleBernoulli(val_p);
             tot1 += x[i];
             tot2 += x[i]*x[i];
             tot3 += x[i]*x[i]*x[i];
             tot4 += x[i]*x[i]*x[i]*x[i];
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
      		title: "Sampled Results (p=" + val_p.toString() + ", loop iteration=" + nit.toString()  + ", num. simulations = " + nsim.toString()  + ")", 
      		xaxis: {title: "X Value"}, 
      		yaxis: {title: "Probability"}
    	}
    	Plotly.newPlot('myDiv', data, layout);
    	
    	var exact_e_x_elem   = document.getElementById("exact_e_x");
    	exact_e_x_elem.value = val_p * nit;
    	
    	var approx_e_x_elem   = document.getElementById("approx_e_x");
    	approx_e_x_elem.value = tot1/nsim;
    	
    	var exact_e_x2_elem   = document.getElementById("exact_e_x2");
    	exact_e_x2_elem.value = val_p * nit * (val_p * (nit - 1) + 1);
    	
    	var approx_e_x2_elem   = document.getElementById("approx_e_x2");
    	approx_e_x2_elem.value = tot2/nsim;
    	
    	var exact_e_x3_elem   = document.getElementById("exact_e_x3");
    	exact_e_x3_elem.value = val_p * nit * (val_p * val_p * nit * nit - 3 * nit * val_p * val_p + 3 * nit * val_p + 2 * val_p * val_p - 3 * val_p + 1);
    	
    	var approx_e_x3_elem   = document.getElementById("approx_e_x3");
    	approx_e_x3_elem.value = tot3/nsim;
    	
    	var exact_e_x4_elem   = document.getElementById("exact_e_x4");
    	exact_e_x4_elem.value = val_p * nit * (val_p * val_p * val_p * nit * nit * nit - 6 * nit * nit * val_p * val_p * val_p + 6 * nit * nit * val_p * val_p + 11 * nit * val_p * val_p * val_p - 18 * nit * val_p * val_p + 7 * nit * val_p - 6 * val_p * val_p * val_p + 12 * val_p * val_p - 7 * val_p + 1);
    	
    	var approx_e_x4_elem   = document.getElementById("approx_e_x4");
    	approx_e_x4_elem.value = tot4/nsim;
    }
    
    var prob_elem = document.getElementById("probability_value");
    var iter_elem = document.getElementById("num_iteration_value");
    var exp_elem  = document.getElementById("num_experiment_value");
    
    plotProbProgram (prob_elem.value, iter_elem.value, exp_elem.value);
    

    
    function updateProbability(val_p) {
  		var elem1 = document.getElementById("probability_value");
        elem1.value = val_p;
        var elem2 = document.getElementById("probability");
        elem2.value = val_p;
    	var iter_elem = document.getElementById("num_iteration_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
        plotProbProgram (val_p, iter_elem.value, exp_elem.value);
	}
	function updateNumIter(nit) {
  		var elem1 = document.getElementById("num_iteration_value");
        elem1.value = nit;
        var elem2 = document.getElementById("num_iteration");
        elem2.value = nit;
        var prob_elem = document.getElementById("probability_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
    	plotProbProgram (prob_elem.value, nit, exp_elem.value);
	}
	function updateNumExp(nsim) {
  		var elem1 = document.getElementById("num_experiment_value");
        elem1.value = nsim;
        var elem2 = document.getElementById("num_experiment");
        elem2.value = nsim;
    	var prob_elem = document.getElementById("probability_value");
    	var iter_elem = document.getElementById("num_iteration_value");
    	plotProbProgram (prob_elem.value, iter_elem.value, nsim);
	}
     
  </script>
