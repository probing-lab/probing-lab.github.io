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

Duelling Cowboys

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