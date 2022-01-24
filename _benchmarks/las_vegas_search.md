---
name:           "Las Vegas Search"
numvars:        "3"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Las Vegas Search

```python
element = 0
found = 0
while found == 0:
    random = DiscreteUniform(0, 20)
    if random == element:
        found = 1
    end
end
```
