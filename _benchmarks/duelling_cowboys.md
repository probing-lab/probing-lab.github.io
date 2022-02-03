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
Two cowboys A and B take turns to shoot at each other. 
During each turn, cowboy A can hit cowboy B with probability 
a while cowboy B can hit cowboy A with probability b.
The duel terminates until one cowboy succeeds to hit the other.
<br>
What is the probability that Cowboy A win ?
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

Elapsed time: 1.483273983001709 s
```


<p>
Solution: \[\mathbb{E} (ahit) = \frac{a (a (a + b - 1)^{(n - 1)} + b - (a + b - 1)^{(n - 1)} - 1)}{(a+b-2)}\]
</p>
