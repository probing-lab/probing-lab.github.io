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
