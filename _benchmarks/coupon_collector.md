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

Coupon Collector Problem - Two Coupons (Source Code)

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

    
    function plotProbProgram (nit, nsim){
        var tot1, turn, cont, ahit, bhit;
        var x = [];
        
        tot1     = 0;
        var c0, c1, new_box, boxes, coupon;
        
        c0      = 0;
        c1      = 0;
        new_box = 1;
        boxes   = 0;
        coupon  = 0;

        for (var i = 0; i < nsim; i++) { 
             for (var j = 0; j < nit; j++){
                if (new_box == 1){
                    coupon = sampleBernoulli(1/2);
                    if (coupon == 0){
                        c0 = 1;
                    }else{
                        c1 = 1;
                    }
                    boxes = boxes + new_box
                    new_box = 1 - c0*c1
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
      		xaxis: {title: "Cowboy A wins (1) or does not win (0)."}, 
      		yaxis: {title: "Expected number of Boxes"}
    	}
    	Plotly.newPlot('myDiv', data, layout);
    	
    	var exact_boxes_elem  = document.getElementById("exact_boxes");
    	//exact_boxes_elem.value = Number(val_a) * (Number(val_a) * temp + Number(val_b) - temp - 1) / (Number(val_a) + Number(val_b) - 2);
    	
    	var approx_boxes_elem   = document.getElementById("approx_boxes");
    	approx_boxes_elem.value = tot1;
    	
    	
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
