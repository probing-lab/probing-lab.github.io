---
name:           "Hawk Dove Symbolic"
numvars:        "5"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Hawk Dove Symbolic

```python
p1bal, p2bal = 0, 0
outcome = 0
player1, player2 = 0, 0
#v = 4 # common resource , objective
#c = 8 # penalty for losing a fight
while true:
    player1 = Bernoulli(v/c)
    player2 = Bernoulli(v/c)
    if player1 == 0: # Player1 Dove
        if player2 == 0: # Player2 Dove
            # collaborators split resources
            p1bal = p1bal + v/2
            p2bal = p2bal + v/2
        else:
            # hawk strategy > dove , winner takes all
            p2bal = p2bal + v
            # dove avoids fight
            p1bal = p1bal
        end
    else: # Player1 Hawk
        if player2 == 0: # Player2 Dove
            # hawk strategy > dove , winner takes all
            p1bal = p1bal + v
            # dove avoids fight
            p2bal = p2bal
        else:
            # both players fight , winner takes all
            # loser suffers penalty
            # outcome of fight is stochastic
            outcome = Bernoulli(1/2)
            if outcome == 0:
                p1bal = p1bal + v
                p2bal = p2bal - c
            else:
                p1bal = p1bal - c
                p2bal = p2bal + v
            end
        end
    end
end
```
