---
name:           "Variable Swap"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
---

Variable Swap

```python
x = 0 {1/2} 5
y = 4 {1/2} 7
while true:
    unif1 = Uniform(-1,1)
    unif2 = Uniform(-2,2)
    x, y = y + unif1, x + unif2
end
```
