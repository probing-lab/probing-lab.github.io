---
name:           "Knuth-Yao Algorithm"
numvars:        "8"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Knuth-Yao Algorithm

```python
state, coin    = 0, 0
d1, d2, d3, d4, d5, d6 = 0, 0, 0, 0, 0, 0
while true:
    coin = Bernoulli (1/2)
    if   state == 0:
         state = 1 + coin
    elif state == 1:
         state = 3 + coin
    elif state == 2:
         state = 5 + coin
    elif state == 3:
         state = 2 * coin - 1            
         d1    = 1-coin 
    elif state == 4:
         d2     = coin
         d3     = 1 - coin
    elif state == 5:
         state = 3 * coin - 1
         d4    = 1-coin
    elif state == 6:
         d5    = coin
         d6    = 1 - coin
    end
end
```
