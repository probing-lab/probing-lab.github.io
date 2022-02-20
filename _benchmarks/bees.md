---
name:           "Bees Model"
numvars:        "5"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

<b>Mathematical model describing the decision-making process of a swarm of honeybees for selecting one nest-site among many</b>

N.F. Britton, N.R. Franks, S.C. Pratt, T.D. Seeley, Deciding on a new home: how do honeybees agree ?, Proceedings of the Royal Society of London. Series B: Biological Sciences 269 (1498), 1383-1388 (2002)
    [<a href="https://royalsocietypublishing.org/doi/10.1098/rspb.2002.2001">Link</a>]
<p>
\[ \begin{array}{lcl}
X(0) & = & \mathcal{N} (475,5) \\
Y_1(0) & = & \mathcal{U} (350,500) \\
Y_2(0) & = & \mathcal{U} (100,150) \\
Z_1(0) & = & \mathcal{N} (35,1.5) \\
Z_2(0) & = & \mathcal{N} (35,1.5) \\
 &  &  \\
\dot{X} & = & -\beta_1 XY_1 - \beta_2 XY_2 \\
\dot{Y_1} & = & \beta_1 XY_1 -\gamma Y_1 + \delta \beta_1 Y_1 Z_1 + \alpha \beta_1 Y_1 Z_2\\
\dot{Y_2} & = & \beta_2 XY_2 -\gamma Y_2 + \delta \beta_2 Y_2 Z_2 + \alpha \beta_2 Y_2 Z_1\\
\dot{Z_1} & = & \gamma Y_1 - \delta \beta_1 Y_1 Z_1 - \alpha \beta_2 Y_2 Z_1\\
\dot{Z_2} & = & \gamma Y_2 - \delta \beta_2 Y_2 Z_2 - \alpha \beta_1 Y_1 Z_2\\
 &  &  \\
\beta_1,\beta_2 & = & 0.001\\
\gamma & = & 0.3\\
\delta & = & 0.5\\
\alpha & = & 0.7\\
\end{array}\] 
</p>

<b>Description</b>
<p align="justify">The population of the honeybees is divided in three main groups: X are the bees that 
are neutral (or unbelievers) in the decision, Y is the class of the bees that believes either
in one site (Y1) or in another site (Y2) and they are actively spreading their beliefs 
to the other bees, Z is the class of the bees that believes either
in one site (Z1) or in the other site (Z2) but they do not spread their beliefs 
to the others.</p>

<b>Probabilistic Program Computing the Bees Model (Source Code)</b>
```python
x = Normal(475, 5)
y1 = Uniform(350, 400)
y2 = Uniform(100, 150)
z1 = Normal(35, 1.5)
z2 = Normal(35, 1.5)

#dt = 0.1
#beta = 0.001         - We assume that beta = beta1 = beta2 
#gamma = 0.3
#delta_beta = 0.0005  - delta * beta
#alpha_beta = 0.0007  - alpha * beta 

while true:
    x, y1, y2, z1, z2 = x + dt*((-beta)*x*y1 - beta*x*y2), y1 + dt*(beta*x*y1 - gamma*y1 + delta_beta *y1*z1 + alpha_beta*y1*z2), y2 + dt*(beta*x*y2 - gamma*y2 + delta_beta*y2*z2 + alpha_beta*y2*z1), z1 + dt*(gamma*y1 - delta_beta*y1*z1 - alpha_beta*y2*z1), z2 + dt*(gamma*y2 - delta_beta*y2*z2 - alpha_beta*y1*z2)
end
```

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
            <td rowspan=6>(L) Linear <br> (NL) nonlinear <br><img src="/assets/dep_graphs/bees.png" alt="Dependency Graph" style="width:400px;"/></td>
        </tr>
        <tr>
            <td>State space</td>
            <td>Infinite, continuous</td>
        </tr>
        <tr>
            <td>Circular Dependency</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>Symbolic Constants</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>Effective Variables</td>
            <td>No</td>
        </tr>
        <tr>
            <td>Defective Variables</td>
            <td>Yes (x, y1, y2, z1, z2)</td>
        </tr>
    </tbody>
</table>

<br>


<b>Probabilistic Program Simulation:</b>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiments" name="num_experiments" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiments_slider" name="num_experiments_slider" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iterations" name="num_iterations" min="500" max="2000" step="10" value="500" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iterations_slider" name="num_iterations_slider" min="500" max="2000" step="10" value="500" onchange="updateNumIter(this.value)"> |
| Integration step (dt): | <input type="number" id="integration_step" name="integration_step" min="0.01" max="0.1" step="0.01" value="0.1" onchange="updateIntegrationStep(this.value)"> | <input type="range" id="integration_step_slider" name="integration_step_slider" min="0.01" max="0.1" step="0.01" value="0.1" onchange="updateIntegrationStep(this.value)"> |
| Parameter (beta): | <input type="number" id="parameter_beta" name="parameter_beta" min="0" max="0.1" step="0.01" value="0.01" onchange="updateParameterBeta(this.value)"> | <input type="range" id="parameter_beta_slider" name="parameter_beta_slider" min="0" max="0.1" step="0.01" value="0.01" onchange="updateParameterBeta(this.value)"> |
| Parameter (gamma): | <input type="number" id="parameter_gamma" name="parameter_gamma" min="0" max="1" step="0.1" value="0.3" onchange="updateParameterGamma(this.value)"> | <input type="range" id="parameter_gamma_slider" name="parameter_gamma_slider" min="0" max="1" step="0.1" value="0.3" onchange="updateParameterGamma(this.value)"> |
| Parameter (delta): | <input type="number" id="parameter_delta" name="parameter_delta" min="0" max="1" step="0.1" value="0.5" onchange="updateParameterDelta(this.value)"> | <input type="range" id="parameter_delta_slider" name="parameter_delta_slider" min="0" max="1" step="0.1" value="0.5" onchange="updateParameterDelta(this.value)"> |
| Parameter (alpha): | <input type="number" id="parameter_alpha" name="parameter_alpha" min="0" max="1" step="0.1" value="0.7" onchange="updateParameterAlpha(this.value)"> | <input type="range" id="parameter_alpha_slider" name="parameter_alpha_slider" min="0" max="1" step="0.1" value="0.7" onchange="updateParameterAlpha(this.value)"> |

<div id="myDiv"><!-- Plotly chart will be drawn inside this DIV --></div>
<script>

    function sampleBernoulli(val_p){
    	if (Math.random() < val_p) return 1;
        return 0;
    }
    
    function computeProgram(nit, nexps, dt, beta, gamma, delta, alpha){
             alert("Numero iterazioni:" + nit.toString() + " Numero di esperimenti: " + nexps.toString() + " dt=" + dt.toString() + " beta=" + beta.toString() + " gamma=" + gamma.toString() + " delta=" + delta.toString() + " alpha=" + alpha.toString());
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
    
    //var prob_elem = document.getElementById("probability_value");
    //var iter_elem = document.getElementById("num_iteration_value");
    //var exp_elem  = document.getElementById("num_experiment_value");
    
    //plotProbProgram (prob_elem.value, iter_elem.value, exp_elem.value);
    


	function updateNumIter(nit) {
  		var elem1 = document.getElementById("num_iterations_slider");
        elem1.value = nit;
        var elem2 = document.getElementById("num_iterations");
        elem2.value = nit;
        
        var elem3 = document.getElementById("num_experiments");
        var elem4 = document.getElementById("integration_step");
        var elem5 = document.getElementById("parameter_beta");
        var elem6 = document.getElementById("parameter_gamma");
        var elem7 = document.getElementById("parameter_delta");
        var elem8 = document.getElementById("parameter_alpha");
        computeProgram(nit, elem3.value, elem4.value, elem5.value, elem6.value, elem7.value, elem8.value);
	}
	function updateNumExp(nsim) {
  		var elem1 = document.getElementById("num_experiments_slider");
        elem1.value = nsim;
        var elem2 = document.getElementById("num_experiments");
        elem2.value = nsim;
	}
	
	function updateIntegrationStep(dt){
	    var elem1 = document.getElementById("integration_step_slider");
        elem1.value = dt;
        var elem2 = document.getElementById("integration_step");
        elem2.value = dt;
	}
	
	function updateParameterBeta(beta){
	    var elem1 = document.getElementById("parameter_beta_slider");
        elem1.value = beta;
        var elem2 = document.getElementById("parameter_beta");
        elem2.value = beta;
	}
	
    function updateParameterGamma(gamma){
	    var elem1 = document.getElementById("parameter_gamma_slider");
        elem1.value = gamma;
        var elem2 = document.getElementById("parameter_gamma");
        elem2.value = gamma;
	}
	
    function updateParameterDelta(delta){
	    var elem1 = document.getElementById("parameter_delta_slider");
        elem1.value = delta;
        var elem2 = document.getElementById("parameter_delta");
        elem2.value = delta;
	}
	
	function updateParameterAlpha(alpha){
	    var elem1 = document.getElementById("parameter_alpha_slider");
        elem1.value = alpha;
        var elem2 = document.getElementById("parameter_alpha");
        elem2.value = alpha;
	}
     
  </script>
