---
name:           "Bees Model"
numvars:        "5"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
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

<b>Probabilistic Program Simulation:</b>

| Parameter | Current Value | Tuning |
| --- | ----------- | ----------- |
| Number of program executions: | <input type="number" id="num_experiment_value" name="num_experiment_value" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> | <input type="range" id="num_experiment" name="num_experiment" min="100" max="10000" step="100" value="1000" onchange="updateNumExp(this.value)"> |
| Number of loop iterations (n): | <input type="number" id="num_iteration_value" name="num_iteration_value" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)">  | <input type="range" id="num_iteration" name="num_iteration" min="10" max="100" step="10" value="10" onchange="updateNumIter(this.value)"> |
| Integration step (dt): | <input type="number" id="integration_step" name="integration_step" min="0.01" max="0.1" step="0.01" value="0.1" onchange="updateIntegrationStep(this.value)"> | <input type="range" id="integration_step_slider" name="integration_step_slider" min="0.01" max="0.1" step="0.01" value="0.1" onchange="updateIntegrationStep(this.value)"> |
| Parameter (beta): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_b" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> |
| Parameter (gamma): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_b" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> |
| Parameter (deltabeta): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_b" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> |
| Parameter (alphabeta): | <input type="number" id="probability_value_b" name="probability_value_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> | <input type="range" id="probability_b" name="probability_b" min="0" max="1" step="0.1" value="0.5" onchange="updateProbability_b(this.value)"> |

