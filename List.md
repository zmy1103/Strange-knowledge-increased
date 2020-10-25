## List

**array1 = [1,2,3,4,5]**
**array2 = [1,3,3,5,5]**

### **统计两个数组相同元素个数：** 

```python
len(set(array1) & set(array2))#输出直接print

print([x for x in array1 if x in array2])#继续操作的话
```

### 寻找list中最大元素对应的索引

```python
aa = [1,2,3,4,5]

aa.index(max(aa))
```

### 删除元素

```python
pop()：根据索引值删除元素
remove()：根据元素值进行删除
clear()：删除列表所有元素
del：根据索引值删除元素：del nums[2]
```

