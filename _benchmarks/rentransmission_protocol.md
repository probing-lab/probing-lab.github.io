---
name:           "Retransmission Protocol"
numvars:        "4"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Retransmission Protocol

```python
fail = 0
sent = 0
totalfail = 0
while true:
    success = Bernoulli(0.9)
    if success == 1:
        fail = 0
        sent = sent + 1
    else:
        fail = fail + 1
        totalfail = totalfail + 1
    end
end
```
