---
name:           "Randomized Response"
numvars:        "7"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Randomized Response (Differential Privacy)

```python
data_entry = 0
p1         = 0
n1         = 0
c1         = 0
c2         = 0
ntrue      = 0
nfalse     = 0
while true:
    data_entry = Bernoulli(p)
    c1 = Bernoulli(0.5)
    c2 = Bernoulli(0.5)
    if c1 == 1:
       if data_entry == 1:
          p1 = p1 + data_entry
       else:
          n1 = n1 + (1 - data_entry)
       end
       ntrue = ntrue + 1
    else:
       if c2 == 1:
          p1 = p1 + 1
       else:
          n1 = n1 + 1
       end
       if data_entry == c2:
          ntrue = ntrue + 1
       else:
          nfalse = nfalse + 1
       end
    end
end
```
