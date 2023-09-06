# Modeling Python+Gurobi

*POLab*
<br>
*2017/10/08*
<br>
[【Return to Homepage】](https://github.com/PO-LAB/Python-Gurobi)

## (1) Optimization Process
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Python%2Bgurobi%E5%BB%BA%E6%A8%A1/%E6%9C%80%E4%BD%B3%E5%8C%96%E6%B5%81%E7%A8%8B.png" width="650">

## (2) Probelm Definition
● There are three activities, X, Y, and Z, that need to be held on the same day.<br>
● The total available time for the venue is only four hours.<br>
● Activity Z has a value that is twice that of activities X and Y.<br>
● At least one of activities X or Y must be selected.<br>
● Activity X requires 1 hour.<br>
● Activity Y requires 2 hours.<br>
● Activity Z requires 3 hours.<br>
● Which combination of activities can maximize the value?<br>

## (3) Mathematical Programming

<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Python%2Bgurobi%E5%BB%BA%E6%A8%A1/%E5%BB%BA%E6%A8%A1%E7%AF%84%E4%BE%8B.png" width="850">


## (4) Python+Gurobi Optimization
## 1. Modeling Process
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Python%2Bgurobi%E5%BB%BA%E6%A8%A1%E6%B5%81%E7%A8%8B.png" width="750">

## 2. Modeling Python+Gurobi
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Python%2Bgurobi%E5%BB%BA%E6%A8%A1/example.png" width="450">

## Import gurobipy


```python
# Import Gurobi package
from gurobipy import *
```

## Model


```python
# Build a new model and assign to 'm'
m = Model('mip1')
```

## Add decision variable


```python
# Add variables using m.addVar()
x = m.addVar(vtype=GRB.BINARY, name="x")
y = m.addVar(vtype=GRB.BINARY, name="y")
z = m.addVar(vtype=GRB.BINARY, name="z")
```

## Update


```python
# Update model
m.update()
```

## Add objective and constraints


```python
# Set objective using m.setObjective()
m.setObjective(x + y + 2 * z, GRB.MAXIMIZE) 

# Add constraints using m.addConstr()
# Add constraint: x + 2 y + 3 z <= 4
m.addConstr(x + 2 * y + 3 * z <= 4, "c0") 
# Add constraint: x + y >= 1
m.addConstr(x + y >= 1, "c1")
```








## Result
- If you do not want to display the solving process, you can add this code before optimize():
**m.setParam('OutputFlag', 0)**

```python
m.optimize() # solve
# Display name and value of variables using attributes .varName and .x
for v in m.getVars():
    print('%s %g' % (v.varName, v.x))
# Display optimal solution using attribute .objVal
print('Obj: %g' % m.objVal)
```
```
Optimize a model with 2 rows, 3 columns and 5 nonzeros
Variable types: 0 continuous, 3 integer (3 binary)
Coefficient statistics:
  Matrix range     [1e+00, 3e+00]
  Objective range  [1e+00, 2e+00]
  Bounds range     [1e+00, 1e+00]
  RHS range        [1e+00, 4e+00]
Found heuristic solution: objective 2
Presolve removed 2 rows and 3 columns
Presolve time: 0.06s
Presolve: All rows and columns removed

Explored 0 nodes (0 simplex iterations) in 0.23 seconds
Thread count was 1 (of 4 available processors)

Solution count 2: 3 2 

Optimal solution found (tolerance 1.00e-04)
Best objective 3.000000000000e+00, best bound 3.000000000000e+00, gap 0.0000%
x 1
y 0
z 1
Obj: 3
```
