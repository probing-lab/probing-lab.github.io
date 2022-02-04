---
name:           "Duelling Cowboys"
numvars:        "4"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Duelling Cowboys (Source Code)

```python
turn = 0
continue = 1
ahit = 0
bhit = 0
while true:
    if turn == 0:
        ahit = Bernoulli(a)
        if ahit == 1:
            continue = 0
        else:
            turn = 1
        end
    else:
        bhit = Bernoulli(b)
        if bhit == 1:
            continue = 0
        else:
            turn = 0
        end
    end
end
```

<br>
Description
<p>
Two cowboys A and B take turns to shoot at each other.  During each turn, cowboy A can hit cowboy B with probability  a while cowboy B can hit cowboy A with probability b. The duel terminates until one cowboy succeeds to hit the other.
<br><br>
What is the probability that Cowboy A or Cowboy B wins ?
</p>

<br>
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
            <td>Yes</td>
            <td rowspan=6>(L) Linear <br> (NL) nonlinear <br><img src="/assets/dep_graphs/duelling_cowboys_.png" alt="Dependency Graph" style="width:100px;"/></td>
        </tr>
        <tr>
            <td>State space</td>
            <td>Finite, discrete</td>
        </tr>
        <tr>
            <td>Circular Dependency</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>Symbolic Constants</td>
            <td>Yes (a, b)</td>
        </tr>
        <tr>
            <td>Effective Variables</td>
            <td>Yes (turn, continue, ahit, bhit)</td>
        </tr>
        <tr>
            <td>Defective Variables</td>
            <td>No</td>
        </tr>
    </tbody>
</table>

<br>

```
python polar.py benchmarks/prinsys/duelling_cowboys.prob --goals "E(ahit * (1 - continue))"

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

E(ahit*(1 - continue)) = 0; a*(a*(a + b - 1)**(n - 1) + b - (a + b - 1)**(n - 1) - 1)/(a + b - 2)
Solution is exact

Elapsed time: 1.5660450458526611 s
```


<p>
The probability that Cowboy A wins is: \[\mathbb{E} (ahit * (1 - continue)) = \frac{a (a (a + b - 1)^{(n - 1)} + b - (a + b - 1)^{(n - 1)} - 1)}{(a+b-2)}\]
</p>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |
| Probability (a): | <input type="number" id="probability_value_a" name="probability_value_a" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_a(this.value)"> | <input type="range" id="probability_a" name="probability_a" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability(this.value)"> |
| Probability (b): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_a" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability(this.value)"> |

| Exact E(ahit) | Approx. E(ahit) | 
| --- | --- |
| <input type="text" size="5" id="exact_ahit" name="exact_ahit"> | <input type="text" size="5" id="approx_ahit" name="approx_e_x"> | 

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }
    /*
    function plotProbProgram (val_a, val_b, nit, nsim){
        var x = [];
        var tot1 = 0;
        var turn     = 0;
        var continue = 1;
        var ahit     = 0;
        var bhit     = 0;
    	for (var i = 0; i < nsim; i++) { 
             for (var j = 0; j < nit; j++){
                 if (turn == 0){
                     ahit = sampleBernoulli(val_a);
                     if (ahit == 1){
                         continue = 0;
                     }else{
                         turn = 1;
                     }
                 }else{
                     bhit = sampleBernoulli(val_b);
                     if (bhit == 1){
                         continue = 0;
                     }else{
                         turn = 0;
                     }
                 }
             }
             x[i] = ahit;
             tot1 += x[i];
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
      		title: "Sampled Results (a=" + val_a.toString() + ", b=" + val_b.toString() + " loop iteration=" + nit.toString()  + ", num. simulations = " + nsim.toString()  + ")", 
      		xaxis: {title: "X Value"}, 
      		yaxis: {title: "Probability"}
    	}
    	Plotly.newPlot('myDiv', data, layout);
    	
    	var exact_ahit_elem   = document.getElementById("exact_ahit");
    	//exact_ahit_elem.value = val_a * nit;
    	
    	var approx_ahit_elem   = document.getElementById("approx_ahit");
    	approx_ahit_elem.value = tot1/nsim;
    	
    }
    
    var prob_elem_a = document.getElementById("probability_value_a");
    var prob_elem_b = document.getElementById("probability_value_b");
    var iter_elem = document.getElementById("num_iteration_value");
    var exp_elem  = document.getElementById("num_experiment_value");
    
    plotProbProgram (prob_elem_a.value, prob_elem_b.value, iter_elem.value, exp_elem.value);
    
    */
    
    function updateProbability_a(val_a) {
  		var elem1 = document.getElementById("probability_value_a");
        elem1.value = val_a;
        var elem2 = document.getElementById("probability_a");
        elem2.value = val_a;
    	var iter_elem = document.getElementById("num_iteration_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
    	var prob_elem_b = document.getElementById("probability_value_b");
        //plotProbProgram (val_a, prob_elem_b.value, iter_elem.value, exp_elem.value);
	}
	
	function updateProbability_b(val_b) {
  		var elem1 = document.getElementById("probability_value_b");
        elem1.value = val_b;
        var elem2 = document.getElementById("probability_b");
        elem2.value = val_b;
        var prob_elem_a = document.getElementById("probability_value_a");
    	var iter_elem = document.getElementById("num_iteration_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
        //plotProbProgram (prob_elem_a.value, val_b, iter_elem.value, exp_elem.value);
	}
	
	function updateNumIter(nit) {
  		var elem1 = document.getElementById("num_iteration_value");
        elem1.value = nit;
        var elem2 = document.getElementById("num_iteration");
        elem2.value = nit;
        var prob_elem_a = document.getElementById("probability_value_a");
        var prob_elem_b = document.getElementById("probability_value_b");
    	var exp_elem  = document.getElementById("num_experiment_value");
    	//plotProbProgram (prob_elem_a.value, prob_elem_b.value, nit, exp_elem.value);
	}
	function updateNumExp(nsim) {
  		var elem1 = document.getElementById("num_experiment_value");
        elem1.value = nsim;
        var elem2 = document.getElementById("num_experiment");
        elem2.value = nsim;
    	var prob_elem_a = document.getElementById("probability_value_a");
    	var prob_elem_b = document.getElementById("probability_value_b");
    	var iter_elem = document.getElementById("num_iteration_value");
    	//plotProbProgram (prob_elem_a.value, prob_elem_b.value, iter_elem.value, nsim);
	}
     
  </script>
