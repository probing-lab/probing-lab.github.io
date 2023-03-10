---
title: Amber
style: fill
color: secondary
description: Amber is an academic prototype to decide the probabilistic termination behavior of Prob-solvable loops.
---

<p align="center" style="float:right;margin:50px">
  <a href="https://github.com/probing-lab/amber">
    <img src="../assets/logo/amber-logo.svg" width="300px" alt="Amber logo" />
  </a>
</p>


# Amber

Amber is an academic prototype to decide the probabilistic termination behavior of Prob-solvable loops.

## Run Amber with Docker

The repository comes with a Dockerfile.
This is the easiest way to run Amber.

1. Make sure Docker is installed on your local machine
([docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)).

2. Execute the following command, to run a docker container containing Amber and connect to the container:
```
docker run -ti marcelmoosbrugger/amber
```

Now you can run Amber on a given benchmark file with the following command:
```
./amber benchmarks/past/2d_bounded_random_walk
```

If you want to use your own benchmarks within the Docker container please see the Docker documentation on volumes ([docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)).


## Local Installation

Amber needs the following dependencies:
- Python version &ge; 3.8 and pip
- scipy
- diofant
- lark-parser

To install these you can do the following steps.

1. Make sure you have python (version &ge; 3.8) and pip installed on your system.
Otherwise install it in your preferred way.

2. Clone the repository:
```
git clone git@github.com:probing-lab/amber.git
cd amber
```

3. Create a virtual environment in the `.venv` directory:
```
pip3 install --user virtualenv
python3 -m venv .venv
```

4. Activate the virtual environment:
```
source .venv/bin/activate
```

5. Install the required dependencies with pip:
```
pip install -r requirements.txt
```

If the previous command failed, try the following instead:
```
python -m pip install -r requirements.txt
```


## Run Amber

Having all dependencies installed, you can run Amber for example like this:
```
python ./amber.py --benchmarks benchmarks/past/2d_bounded_random_walk
```

A more extensive help can be obtained by:
```
python ./amber.py --help
```

## Run Automatic Tests

You can run all automatic tests with:
```
python -m unittest
```


## Writing your own Prob-solvable loop

A Prob-solvable loop consist of initial assignments (one per line), a loop head `while P > Q:`
and a loop body consisting of multiple variable updates (also one per line).
The loop guard `P > Q` consists of two polynomials `P` and `Q` over the program variables.

Initial assignments:
- format:  `var = value`
- comment: not all variables have to have initial value specified
- example: `x = 123`

Variable updates:
- format:  `var = option1 @ probability1; option2 @ probability2 ...`
- comment: last probability can be omitted, it's assumed to be whatever
values is needed for probabilities to sum up to 1.
- comment: variables can depend only on previous variables non-linearly,
and on itself linearly - e.g. `x = x + 1` followed by `y = y + x^2` is allowed.
However, `x = x + y` followed by `y = y + 1`, or `x = x^2` is not allowed.
- example: `x = x @ 1/2; x + u`

An example program would be:

```
# this is a comment
y = 0.01
x = 5
while x > 0:
    y = 2*y
    x = x + 200*y**2 @ 1/2; x - y**3
```
More examples can be found in the `benchmarks` folder.
