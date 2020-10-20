## List

**array1 = [1,2,3,4,5]**
**array2 = [1,3,3,5,5]**

### **统计两个数组相同元素个数：** 

```python
len(set(array1) & set(array2))#输出直接print

print([x for x in array1 if x in array2])#继续操作的话
```

