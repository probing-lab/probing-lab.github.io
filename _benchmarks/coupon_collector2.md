---
name:           "Coupon Collector (2 Coupons)"
numvars:        "5"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "condition"
defective:      "No"
---

<b>Coupon Collector Problem - Two Coupons (Source Code)</b>

```python
c0, c1 = 0, 0
new_box = 1
boxes = 0
while new_box == 1:
    coupon = Bernoulli(1/2)
    if coupon == 0:
        c0 = 1
    else:
        c1 = 1
    end
    boxes = boxes + new_box
    new_box = 1 - c0*c1
end
```

<br>
<b>Description</b>
<p>
Imagine there are boxes of cereals offering inside special coupons of two different kind. 
In order to win an award one needs to collect at least one coupon of each different type. 
<br>
<br>
<i>What is the expected number of boxes one needs to open in order 
to collect all different coupons at least one time ?</i>
<br>
<br>
A description of the general problem of the Coupon collector is explained <a href="https://en.wikipedia.org/wiki/Coupon_collector%27s_problem">here</a>.
<br>
<br>
Click <a href="https://probing-lab.github.io/benchmarks/coupon-collector3">here</a> to see the Coupon Collector Problem with Three Coupons.
<br>
Click <a href="https://probing-lab.github.io/benchmarks/coupon-collector4">here</a> to see the Coupon Collector Problem with Four Coupons.
<br>
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
            <td rowspan=6>(L) Linear <br> (NL) nonlinear <br><img src="/assets/dep_graphs/coupon_collector2.png" alt="Dependency Graph" style="width:400px;"/></td>
        </tr>
        <tr>
            <td>State space</td>
            <td>Infinite, discrete</td>
        </tr>
        <tr>
            <td>Circular Dependency</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>Symbolic Constants</td>
            <td>No</td>
        </tr>
        <tr>
            <td>Effective Variables</td>
            <td>Yes (all)</td>
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
The expected number of boxes can be calculated using POLAR as: \[\mathbb{E} (boxes) = 3 - \frac{4}{2^n} \]
</p>

```
python polar.py benchmarks/coupon_collector2.prob --goals "E(boxes)"

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

E(boxes) = 0; 1; 2; 5/2; 3 - 4*2**(-n)
Solution is exact

Elapsed time: 0.44837403297424316 s
```

<br>
<b>Comparison with Monte Carlo simulation:</b>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="1" max="100" step="1" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="1" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |

| Exact E(boxes) | Approx. E(boxes) | 
| --- | --- |
| <input type="text" size="5" id="exact_boxes" name="exact_boxes"> | <input type="text" size="5" id="approx_boxes" name="approx_boxes"> | 

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>

<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }

    
    function plotProbProgram (nit, nsim){
        var tot1, turn, cont, ahit, bhit;
        var x = [];
        
        tot1     = 0;
        var c0, c1, new_box, boxes, coupon;
        


        for (var i = 0; i < nsim; i++) { 
            c0      = 0;
        	c1      = 0;
        	new_box = 1;
        	boxes   = 0;
        	coupon  = 0;
        
             for (var j = 0; j < nit; j++){
                if (new_box == 1){
                    coupon = sampleBernoulli(1/2);
                    if (coupon == 0){
                        c0 = 1;
                    }else{
                        c1 = 1;
                    }
                    boxes = boxes + new_box;
                    new_box = 1 - c0*c1;
                }else{
                    break;
                }
             }
             x[i] = boxes;
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
      		title: "Sampled Results (loop iteration=" + nit.toString()  + ", num. simulations = " + nsim.toString()  + ")", 
      		xaxis: {title: "Number of Boxes"}, 
      		yaxis: {title: "Probability"}
    	}
    	Plotly.newPlot('myDiv', data, layout);
    	
    	var exact_boxes_elem  = document.getElementById("exact_boxes");
    	exact_boxes_elem.value = 3 - 4/Math.pow(2, nit);
    	
    	var approx_boxes_elem   = document.getElementById("approx_boxes");
    	approx_boxes_elem.value = tot1/nsim;
    	
    	
    }
    
    
 
    
    var iter_elem = document.getElementById("num_iteration_value");
    var exp_elem  = document.getElementById("num_experiment_value");
    
    plotProbProgram (iter_elem.value, exp_elem.value);

    
    

	
	function updateNumIter(nit) {
  		var elem1 = document.getElementById("num_iteration_value");
        elem1.value = nit;
        var elem2 = document.getElementById("num_iteration");
        elem2.value = nit;
    	var exp_elem  = document.getElementById("num_experiment_value");
    	plotProbProgram (nit, exp_elem.value);
	}
	function updateNumExp(nsim) {
  		var elem1 = document.getElementById("num_experiment_value");
        elem1.value = nsim;
        var elem2 = document.getElementById("num_experiment");
        elem2.value = nsim;
    	var iter_elem = document.getElementById("num_iteration_value");
    	plotProbProgram (iter_elem.value, nsim);
	}
