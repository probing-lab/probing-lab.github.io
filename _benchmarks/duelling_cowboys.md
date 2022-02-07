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

<b>Duelling Cowboys (Source Code)</b>

```python
turn = 0
stop = 0
ahit = 0
bhit = 0
while true:
    if turn == 0:
        ahit = Bernoulli(a)
        if ahit == 1:
            stop = 1
        else:
            turn = 1
        end
    else:
        bhit = Bernoulli(b)
        if bhit == 1:
            stop = 1
        else:
            turn = 0
        end
    end
end
```



<br>
<b>Description</b>
<p>
Two cowboys A and B take turns to shoot at each other.  During each turn, cowboy A can hit cowboy B with probability  a while cowboy B can hit cowboy A with probability b. The duel terminates until one cowboy succeeds to hit the other.
<br><br>
Which is the probability that one of the two cowboys wins the duel ?
<br>
<br>
<br>
<br>
A similar example was first introduced in: 
<ol>
    <li>A. McIver, C. Morgan, Abstraction, Refinement and Proof for Probabilistic Systems. Monographs in Computer Science, Springer 2005, ISBN 978-0-387-40115-7, (pag. 211), 
    [<a href="https://link.springer.com/book/10.1007/b138392">Link</a>]</li>
</ol>
</p>
<br>
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
            <td rowspan=6>(L) Linear <br> (NL) nonlinear <br><img src="/assets/dep_graphs/duelling_cowboys.png" alt="Dependency Graph" style="width:400px;"/></td>
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

<b>Solving the problem using POLAR:</b>
<p>
The probability that Cowboy A will finally win can be calculated using POLAR as: \[\mathbb{E} (ahit) = \frac{a (a (a + b - 1)^{(n - 1)} + b - (a + b - 1)^{(n - 1)} - 1)}{(a+b-2)}\]
</p>

<p>POLAR transforms the original program by replacing the if-then-else conditions as 
polynomial assignments as follows:
</p>

```python
types
    turn : Finite(0, 1)
    stop : Finite(0, 1)
    ahit : Finite(0, 1)
    bhit : Finite(0, 1)
    _old0 : Finite(0, 1)
    _stop1 : Finite(0, 1)
    _turn1 : Finite(0, 1)
end
turn = 0
stop = 0
ahit = 0
bhit = 0
while true:
    _old0 = turn
    ahit = Bernoulli(a)  |  _old0 == 0  :  ahit
    _stop1 = 1  |  (ahit == 1 ∧ _old0 == 0)  :  stop
    _turn1 = 1  |  (¬(ahit == 1) ∧ _old0 == 0)  :  turn
    bhit = Bernoulli(b)  |  ¬(_old0 == 0)  :  bhit
    stop = 1  |  (bhit == 1 ∧ ¬(_old0 == 0))  :  _stop1
    turn = 0  |  (¬(bhit == 1) ∧ ¬(_old0 == 0))  :  _turn1
end
```

<p>This is the command line and the solution of the expected value for the ahit variable:</p>

```
python polar.py benchmarks/prinsys/duelling_cowboys.prob --goals "E(ahit)"

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

E(ahit) = 0; a*(a*(a + b - 1)**(n - 1) + b - (a + b - 1)**(n - 1) - 1)/(a + b - 2)
Solution is exact

Elapsed time: 1.5186586380004883 s
```


<p>
If <i>a</i> and <i>b</i> are both equal to 1 then the program becomes deterministic and 
in that case Cowboy A will always win since is the first to shoot. If either <i>a</i> or 
<i>b</i> is less than 1 then the limit for n to infinity of <i>(a + b - 1) < 1</i> is:
\[\lim_{n \to \infty} (a + b - 1)^{(n - 1)} = 0\]
<br>
Consequently we have that: \[ \lim_{n \to \infty} \frac{a (a (a + b - 1)^{(n - 1)} + b - (a + b - 1)^{(n - 1)} - 1)}{(a+b-2)} = \frac{a(b - 1)}{a + b - 2}\]
</p>


<b>Comparison with Monte Carlo simulation:</b>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |
| Probability (a): | <input type="number" id="probability_value_a" name="probability_value_a" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_a(this.value)"> | <input type="range" id="probability_a" name="probability_a" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_a(this.value)"> |
| Probability (b): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_b" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> |

| Exact E(ahit) | Approx. E(ahit) | 
| --- | --- |
| <input type="text" size="5" id="exact_ahit" name="exact_ahit"> | <input type="text" size="5" id="approx_ahit" name="approx_ahit"> | 

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>

<b>Limitation of POLAR in this example:</b>

<p>
While we can compute the exact probability for the Cowboy A to win, 
we have issues to compute the exact probability for the Cowboy B to win using 
symbolic constants due to some limitations of the library sympy that 
POLAR is using.
</p>

```
python polar.py benchmarks/prinsys/duelling_cowboys.prob --goals "E(bhit)"

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

sorted roots not supported over ZZ[a,b]
```

However, if we set <i>a</i> and <i>b</i> to a specific value (for example both to 0.5): 

```python
turn = 0
stop = 0
ahit = 0
bhit = 0
while true:
    if turn == 0:
        ahit = Bernoulli(0.5)
        if ahit == 1:
            stop = 1
        else:
            turn = 1
        end
    else:
        bhit = Bernoulli(0.5)
        if bhit == 1:
            stop = 1
        else:
            turn = 0
        end
    end
end
```

Then, we can compute the solution for Cowboy B as follows:

```
python polar.py benchmarks/prinsys/duelling_cowboys.prob --goals "E(bhit)"

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

E(bhit) = 0; 0; 1/4; 1/4; 1/2 - 2**(-n)
Solution is exact

Elapsed time: 0.47222185134887695 s
```


<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }

    
    function plotProbProgram (val_a, val_b, nit, nsim){
        var tot1, turn, cont, ahit, bhit;
        var x = [];
        
        tot1     = 0;
        turn     = 0;
        cont     = 1;
        ahit     = 0;
        bhit     = 0;

        for (var i = 0; i < nsim; i++) { 
             for (var j = 0; j < nit; j++){
                 if (turn == 0){
                     ahit = sampleBernoulli(val_a);
                     if (ahit == 1){
                         cont = 0;
                     }else{
                         turn = 1;
                     }
                 }else{
                     bhit = sampleBernoulli(val_b);
                     if (bhit == 1){
                         cont = 0;
                     }else{
                         turn = 0;
                     }
                 }
             }
             x[i] = ahit * (1 - cont);
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
      		xaxis: {title: "Cowboy A wins (1) or does not win (0)."}, 
      		yaxis: {title: "Probability"}
    	}
    	Plotly.newPlot('myDiv', data, layout);
    	
    	
    	var factor = Number(val_a) + Number(val_b) - 1.0;
    	temp = 1;
    	for (var j = 0; j < nit-1; j++){
    	     temp *= factor;   
    	}
    	
    	var exact_ahit_elem   = document.getElementById("exact_ahit");
    	exact_ahit_elem.value = Number(val_a) * (Number(val_a) * temp + Number(val_b) - temp - 1) / (Number(val_a) + Number(val_b) - 2);
    	
    	var approx_ahit_elem   = document.getElementById("approx_ahit");
    	approx_ahit_elem.value = tot1/nsim;
    	
    }
    
    
 
    
    var prob_elem_a = document.getElementById("probability_value_a");
    var prob_elem_b = document.getElementById("probability_value_b");
    var iter_elem = document.getElementById("num_iteration_value");
    var exp_elem  = document.getElementById("num_experiment_value");
    
    plotProbProgram (prob_elem_a.value, prob_elem_b.value, iter_elem.value, exp_elem.value);

    
    
    function updateProbability_a(val_a) {
  		var elem1 = document.getElementById("probability_value_a");
        elem1.value = val_a;
        var elem2 = document.getElementById("probability_a");
        elem2.value = val_a;
    	var iter_elem = document.getElementById("num_iteration_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
    	var prob_elem_b = document.getElementById("probability_value_b");
        plotProbProgram (val_a, prob_elem_b.value, iter_elem.value, exp_elem.value);
	}
	
	function updateProbability_b(val_b) {
  		var elem1 = document.getElementById("probability_value_b");
        elem1.value = val_b;
        var elem2 = document.getElementById("probability_b");
        elem2.value = val_b;
        var prob_elem_a = document.getElementById("probability_value_a");
    	var iter_elem = document.getElementById("num_iteration_value");
    	var exp_elem  = document.getElementById("num_experiment_value");
        plotProbProgram (prob_elem_a.value, val_b, iter_elem.value, exp_elem.value);
	}
	
	function updateNumIter(nit) {
  		var elem1 = document.getElementById("num_iteration_value");
        elem1.value = nit;
        var elem2 = document.getElementById("num_iteration");
        elem2.value = nit;
        var prob_elem_a = document.getElementById("probability_value_a");
        var prob_elem_b = document.getElementById("probability_value_b");
    	var exp_elem  = document.getElementById("num_experiment_value");
    	plotProbProgram (prob_elem_a.value, prob_elem_b.value, nit, exp_elem.value);
	}
	function updateNumExp(nsim) {
  		var elem1 = document.getElementById("num_experiment_value");
        elem1.value = nsim;
        var elem2 = document.getElementById("num_experiment");
        elem2.value = nsim;
    	var prob_elem_a = document.getElementById("probability_value_a");
    	var prob_elem_b = document.getElementById("probability_value_b");
    	var iter_elem = document.getElementById("num_iteration_value");
    	plotProbProgram (prob_elem_a.value, prob_elem_b.value, iter_elem.value, nsim);
	}
     
  </script>
