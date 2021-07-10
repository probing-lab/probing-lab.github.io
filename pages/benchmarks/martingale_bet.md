---
name:           "Martingale-Bet"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

Martingale-Bet

```python
bet, capital = 1, c0
while true:
    bet = 2*bet
    r = Bernoulli(p)
    if r == 1:
        capital = capital - bet
    else:
        capital = capital + bet
    end
end
```
