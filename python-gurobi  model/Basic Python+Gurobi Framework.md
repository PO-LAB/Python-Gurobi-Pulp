# Basic Python+Gurobi Framework

*POLab*
<br>
*2017/09/27*
<br>
[【Return to Homepage】](https://github.com/PO-LAB/Python-Gurobi)


## (1) Python+Gurobi Architecture

### ● In the Python interface, the notation for mathematical expressions is similar to the original expressions, with the difference that the expressions are broken down.
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/python%E6%95%B8%E5%AD%B8%E5%BC%8F%E5%AD%90.png" width="550">

### ● When constructing a mathematical programming model using Python and Gurobi, it is typically done in the following order: variable definition, objective function formulation, and constraint specification.
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/Python%2Bgurobi%20%E6%9E%B6%E6%A7%8B.png" width="650">

### ● Commonly used for-loops and if-conditionals when modeling.
 In Python, after declaring a for-loop or an if-condition, remember to use a **":"** to end the declaration. Then, on the next line, write what you want to do within the for-loop or if-condition. It's essential to note that Python uses **indent** to distinguish between different code blocks. Therefore, before starting the next line, remember to press the **tab** to create the indentation. This way, the program knows that the code is part of the for-loop or if-condition.

<br>-**for-loop**
```python
for i in <some list>:
 <do something for each i here>
```
-**if-condition**
```python
if <condition>:
 <do something if condition is true here>
```

### ● quicksum() is equivalent to Python's sum() function and mathematical sigma (∑) notation.
#### e.g.
<br> <img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/quicksum_example.png" width="200">
<br>The above constraints are represented in Python+Gurobi as:
```python
for i in I:
    m.addConstr(quicksum(x[i,j] for j in J)<=5)
```

### ● Python String Formatting
In the final stage of creating a mathematical programming model, it is common to display the obtained optimal solution, such as the objective function value and the values of decision variables.<br>
At this time, we can use format specifiers to print various values and names for us. Here are several commonly used format specifiers:
#### ※If you are less familiar with the use of formatted strings, you can refer to [here](http://gohom.win/2015/09/13/PyStringFormat/)
|Symbol|Description|
|-----|-----|
|%s|String|
|%d|Format Integer|
|%f|Format Floating-Point Number|
|%e|Exponential, Scientific Notation|
|%g|Determines whether to use %f or %e based on value size|
#### e.g.
```python
print('She is %s. She weights %gkg and is %dcm tall.'%('Rima',50.4,166))
```
    She is Rima. She weights 50.4kg and is 166cm tall.

```python
print('obj:%d'%m.objVal)
```
```
obj:36
```

## (2) Common Functions and Properties

### 1.Three Major Functions
When creating a mathematical programming model, we need to incorporate our decision variables, objective function, and constraints. The following is a detailed explanation of the three major functions commonly used in setting up these variables and expressions.<br>
P.S. There are different ways to set the objective function and constraints in Gurobi. Here, we have introduced the applications of these three functions only. If you wish to gain a deeper understanding, you can visit the [Python](http://www.gurobi.com/documentation/7.5/refman/py_python_api_overview.html) section within the Gurobi website for further information. For details on other functions, you can click [here](http://www.gurobi.com/documentation/7.5/refman/py_python_api_details.html).

### ● Decision Variable Function

The default upper limit for variables is infinity, the lower limit is 0, and the variable type is continuous.<br>
 
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/m.addvar.png" width="700"><br>

### ● Objective Function
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/m.setobjective.png" width="700"><br>

### ● Constraint Function
<img src="https://github.com/wurmen/Gurobi-Python/blob/master/python-gurobi%20%20model/picture/m.addconstr.png" width="700">

### 2.Gurobi attributes
In Gurobi, you can query or modify the content of the created mathematical programming using various attributes. Here are some commonly used attributes:
<br>P.S. For more attribute queries, you can click [here](https://www.gurobi.com/documentation/7.0/refman/attributes.html).

### ● Model attributes:
|Attribute Name|Description|
|-----|-----|
|**NumVars**|Number of variables|
|**NumConstrs**|Number of linear constraints|
|**ObjVal**|objective value for current solution|

### ● Variable attributes:
|Attribute Name|Description|
|-----|-----|
|**LB**|Lower bound|
|**Obj**|Linear objective coefficient|
|**VarName**|Variable name|
|**X**|Value in the current solution|

### ● Linear constraint attributes:
|Attribute Name|Description|
|-----|-----|
|**ConstrName**|Constraint name|
|**Pi**|Dual value (also known as the shadow price)|
|**Slack**|Slack in the current solution|
