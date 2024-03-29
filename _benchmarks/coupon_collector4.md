---
name:           "Coupon Collector (4 Coupons)"
numvars:        "7"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "condition"
defective:      "No"
nonpolynomial:  "No"
---

<b>Coupon Collector Problem - Four Coupons (Source Code)</b>

```python
c0, c1, c2, c3 = 0, 0, 0, 0
new_box = 1
boxes = 0
while new_box == 1:
    coupon = Categorical(1/4,1/4,1/4,1/4)
    if coupon == 0:
        c0 = 1
    elif coupon == 1:
        c1 = 1
    elif coupon == 2:
        c2 = 1
    else:
        c3 = 1
    end
    boxes = boxes + new_box
    new_box = 1 - c0*c1*c2*c3
end
```

<br>
<b>Description</b>
<p>
There are boxes of cereals offering inside special coupons of two different types. 
One needs to collect at least one coupon of each different type to win an award.
<br>
<br>
<i>What is the expected number of boxes one needs to open in order 
to collect all different coupons at least one time ?</i>
<br>
<br>
A description of the general Coupon Collector Problem is explained <a href="https://en.wikipedia.org/wiki/Coupon_collector%27s_problem">here</a>.
<br>
<br>
Click <a href="https://probing-lab.github.io/benchmarks/coupon-collector3">here</a> to see the Coupon Collector Problem with three coupons.
<br>
Click <a href="https://probing-lab.github.io/benchmarks/coupon-collector4">here</a> to see the Coupon Collector Problem with four coupons.
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
            <td rowspan=6>(L) Linear <br> (NL) nonlinear <br><img src="/assets/dep_graphs/coupon-collector4.png" alt="Dependency Graph" style="width:400px;"/></td>
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
The expected number of boxes can be calculated using POLAR as: \[\mathbb{E} (boxes) = \frac{25}{3} - 16 \left (\frac{3}{4} \right)^n - \frac{16}{3} \left (\frac{1}{4} \right)^n +  \frac{12}{2^n} \]
</p>

```
python polar.py benchmarks/coupon_collector4.prob --goals "E(boxes)"

8888888b.   .d88888b.  888             d8888 8888888b.
888   Y88b d88P" "Y88b 888            d88888 888   Y88b
888    888 888     888 888           d88P888 888    888
888   d88P 888     888 888          d88P 888 888   d88P
8888888P"  888     888 888         d88P  888 8888888P"
888        888     888 888        d88P   888 888 T88b
888        Y88b. .d88P 888       d8888888888 888  T88b
888         "Y88888P"  88888888 d88P     888 888   T88b

By the ProbInG group



------------------
- Parsed program -
------------------
_t0 = 0
_t1 = 0
_t2 = 0
_t3 = 0
c0 = _t0
c1 = _t1
c2 = _t2
c3 = _t3
new_box = 1
boxes = 0
while new_box == 1:
    coupon = Categorical(1/4, 1/4, 1/4, 1/4)
    if coupon == 0:
        c0 = 1
    else if coupon == 1:
        c1 = 1
    else if coupon == 2:
        c2 = 1
    else:
        c3 = 1
    boxes = boxes + new_box
    new_box = 1 - c0*c1*c2*c3
end

-----------------------
- Transformed program -
-----------------------
types
    c0 : Finite(0, 1)
    c1 : Finite(0, 1)
    c2 : Finite(0, 1)
    c3 : Finite(0, 1)
    new_box : Finite(0, 1)
    _old4 : Finite(0, 1)
    coupon : Finite(0, 1, 2, 3)
end
c0 = 0
c1 = 0
c2 = 0
c3 = 0
new_box = 1
boxes = 0
while true:
    _old4 = new_box
    coupon = Categorical(1/4, 1/4, 1/4, 1/4)  |  _old4 == 1  :  coupon
    c0 = 1  |  (coupon == 0 ∧ _old4 == 1)  :  c0
    c1 = 1  |  ((¬(coupon == 0) ∧ coupon == 1) ∧ _old4 == 1)  :  c1
    c2 = 1  |  (((¬(coupon == 0) ∧ ¬(coupon == 1)) ∧ coupon == 2) ∧ _old4 == 1)  :  c2
    c3 = 1  |  (((¬(coupon == 0) ∧ ¬(coupon == 1)) ∧ ¬(coupon == 2)) ∧ _old4 == 1)  :  c3
    boxes = boxes + new_box  |  _old4 == 1  :  boxes
    new_box = 1 - c0*c1*c2*c3  |  _old4 == 1  :  new_box
end

-------------------
- Analysis Result -
-------------------

E(boxes) = 0; 1; 2; 3; 4; 157/32; 363/64; 3221/512; 6941/1024; 58617/8192; 121963/16384; 1004461/131072; 2052441/262144; 16682177/2097152; 33759863/4194304; 272458101/33554432; -16*(3/4)**n + 25/3 - 16*4**(-n)/3 + 12*2**(-n)
Solution is exact

Elapsed time: 2.2366819381713867 s
```

<br>
<b>Comparison with Monte Carlo simulation:</b>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |

| Exact E(boxes) | Approx. E(boxes) | 
| --- | --- |
| <input type="text" size="5" id="exact_boxes" name="exact_boxes"> | <input type="text" size="5" id="approx_boxes" name="approx_boxes"> | 

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>

<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }
    
    function sampleCategorical4(val_p){
    	if (Math.random() < val_p)     return 0;
    	if (Math.random() < 2 * val_p) return 1;
    	if (Math.random() < 3 * val_p) return 2;
        return 3;
    }

    
    function plotProbProgram (nit, nsim){
        var tot1, turn, cont, ahit, bhit;
        var x = [];
        
        tot1     = 0;
        var c0, c1, c2, c3, new_box, boxes, coupon;
        


        for (var i = 0; i < nsim; i++) { 
            c0      = 0;
        	c1      = 0;
        	c2      = 0;
        	c3      = 0;
        	new_box = 1;
        	boxes   = 0;
        	coupon  = 0;
        
             for (var j = 0; j < nit; j++){
                if (new_box == 1){
                    coupon = sampleCategorical4(1/4);
                    if (coupon == 0){
                        c0 = 1;
                    }else if (coupon == 1){
                        c1 = 1;
                    }else if (coupon == 2){
                        c2 = 1;
                    }else if (coupon == 3){
                        c3 = 1;
                    }
                    boxes = boxes + new_box;
                    new_box = 1 - c0*c1*c2*c3;
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
    	exact_boxes_elem.value = 25/3 - 16 * Math.pow(3/4, nit) - (16/3)*(Math.pow(1/4,nit)) + 12*(Math.pow(1/2,nit));
    	
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


