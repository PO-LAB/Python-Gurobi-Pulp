
# Python+Gurobi特殊資料結構

在GurobI的Python介面中，會經常使用下列的資料結構，前四者為Python原有的資料結構，tuplelist是Gurobi為Python介面客製化的結構，可使Python Gurobi在資料處理上更加有效率和靈活。
### ● list(列表)
### ● tuple(元組)
### ● dictionary(字典)
### ● list comprehension(列表解析)
### ● tuplelist



## (一)Lists(列表) and Tuples(元組)
- 兩者皆為**有序集合**，索引位置由<span style="color:red">**’0’**</span>開始數起
- 內部可放任何物件，ex:數字、字串、字典、列表、元組等
- 都可以透過索引、切片取得內部物件

### ● Lists(列表)

- 以**[ ]**形成 <br>
  ex.[‘Pen’,’Denver’,’New York’]<br>
- 可以新增、刪除、修改內容


```python
#創建一個list a
a=[1,2,3,'list']
#索引位置由0開始
print a[0]
print a[3]
```

    1
    list
    


```python
#利用append為list最後加入一個元素
a.append(4)
print a
```

    [1, 2, 3, 'list', 4]
    


```python
#利用remove刪除list中符合條件的元素
a.remove(3)
print a
```

    [1, 2, 'list', 4]
    

### ● tuple(元組)

- 以**()**形成 <br>
  ex.(‘Pen’,’Denver’,’New York’) <br>
- tuple是**不可變的**，一旦被建立就不能修改<br>
- 由於不可變的特性，因此可利用tuples當成dictionaries的索引



```python
#創建一個tuple b
b=(1,2,3,'tuple')
#索引位置由0開始
print b[0]
print b[3]
```

    1
    tuple
    

## (二)Dictionaries(字典)and multidict

### ● Dictionaries(字典)
- 使用**”{ }”**建立新的字典，字典以**「鍵值（key）:值(value)」**表示一個元素，並以’:’來辨別鍵值與值<br>
- 任一不可變的python物件皆可做為一個鍵值(key):<br>
an integer、a oating-point number、a string、a tuple<br>
- 透過’鍵值’來搜尋對應的’值’<br>
- 在Python Gurobi 中可以透過字典來儲存gurobi的決策變數


```python
#建立一個字典對象values，並將各數值與相對應的鍵值(key)進行連結
values={}
values['zero']=0
values['one']=1
values['two']=2
print values
```

    {'zero': 0, 'two': 2, 'one': 1}
    


```python
#透過初始化資料結構的方式建立字典
numbers={'three':3,'four':4,'five':5}
print numbers
```

    {'four': 4, 'five': 5, 'three': 3}
    


```python
#利用鍵值(key)尋找所對應的值(value)
print values['zero']
print numbers['three']
```

    0
    3
    

## ● multidict
- 可以一次初始化一個或多個字典<br>
- 參數是一個字典對象，每一個鍵值都對應一個長度為n的列表，該函數會將每一個列表拆成n個單項，並創造出n個字典<br>



```python
from gurobipy import*
names,lower,upper=multidict({'x':[0,1],'y':[1,2],'z':[0,3]})
```


```python
#顯示共享鍵值列表
print names
```

    ['y', 'x', 'z']
    


```python
#顯示所創立的兩個字典
print lower
print upper
```

    {'y': 1, 'x': 0, 'z': 0}
    {'y': 2, 'x': 1, 'z': 3}
    

## (三)List comprehension(列表解析) and tuplelist
### ● List comprehension(列表解析)
- 以更簡潔的方式產生列表



```python
print [x*x for x in [1,2,3,4,5]]
```

    [1, 4, 9, 16, 25]
    

- 一個列表解析可包含多個for迴圈及if條件句



```python
 print [(x,y) for x in range(3) for y in range(3) if x != y] 
```

    [(0, 1), (0, 2), (1, 0), (1, 2), (2, 0), (2, 1)]
    

### ●  tuplelist
- 能夠有效的在元組列表中檢索符合要求的子列表
- 透過tuplelist中的**select**方法返回所有滿足特定條件的元組子集，此方法可以提高資料選擇的效率
- 透過符號<span style="color:red">‘*’</span>表示元組中相應位置元素配對成功的值



```python
from gurobipy import*
l=tuplelist([(1,2),(1,3),(2,3),(2,4)])
print l.select(1,'*')
```

    <gurobi.tuplelist (2 tuples, 2 values each):
     ( 1 , 2 )
     ( 1 , 3 )
    >
    


```python
print l.select('*',3)
```

    <gurobi.tuplelist (2 tuples, 2 values each):
     ( 1 , 3 )
     ( 2 , 3 )
    >
    


```python
print l.select(1,3)
```

    <gurobi.tuplelist (1 tuples, 2 values each):
     ( 1 , 3 )
    >
    


```python
print l.select('*','*')
```

    <gurobi.tuplelist (4 tuples, 2 values each):
     ( 1 , 2 )
     ( 1 , 3 )
     ( 2 , 3 )
     ( 2 , 4 )
    >
    

## ●  List comprehension v.s.tuplelist
- 列表解析也可以達到與tuplelist同樣的搜尋結果，但是會較沒效率



```python
print l.select(1,'*')
```

    <gurobi.tuplelist (2 tuples, 2 values each):
     ( 1 , 2 )
     ( 1 , 3 )
    >
    


```python
 print [(x,y) for x,y in l if x ==1] 
```

    [(1, 2), (1, 3)]
    


```python

```
