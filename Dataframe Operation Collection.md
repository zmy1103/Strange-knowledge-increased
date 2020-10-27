## Dataframe Operation Collection

[TOC]

### 一列拆成多列

![img](https://img-blog.csdnimg.cn/2018112217240267.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2018112217253836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)

![![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122174641269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)](https://img-blog.csdnimg.cn/201811221728521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122174957765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122175101627.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0FzaGVyMTE3,size_16,color_FFFFFF,t_70)

### 去重

DataFrame.drop_duplicates(subset=None, keep='first', inplace=False)

- subset : column label or sequence of labels, optional
  用来指定特定的列，默认所有列
- keep : {‘first’, ‘last’, False}, default ‘first’
  删除重复项并保留第一次出现的项
- inplace : boolean, default False
  是直接在原来数据上修改还是保留一个副本

### 修改列名

  a  b
0  1  1
1  2  2
2  3  3

1、修改列名a，b为A、B。

df.columns = ['A','B']

2、只修改列名a为A

df.rename(columns={'a':'A'})

### 保留或选择某些列

![img](https://img-blog.csdnimg.cn/20190514173426747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FhYV9hYWExc2Rm,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/20190514173506926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FhYV9hYWExc2Rm,size_16,color_FFFFFF,t_70)

### 两个dataframe横向表拼接（行对齐）

https://blog.csdn.net/qq_41853758/article/details/83280104

```python
#当axis = 1的时候，concat就是行对齐，然后将不同列名称的两张表合并
result = pd.concat([df1, df4], axis=1)
#加上join参数的属性，如果为’inner’得到的是两表的交集，如果是outer，得到的是两表的并集
result = pd.concat([df1, df4], axis=1, join='inner')
```

![这里写图片描述](https://img-blog.csdn.net/20160913195018721)

```python
#如果有join_axes的参数传入，可以指定根据那个轴来对齐数据 例如根据df1表对齐数据，就会保留指定的df1表的轴，然后将df4的表与之拼接
result = pd.concat([df1, df4], axis=1, join_axes=[df1.index])
```

![这里写图片描述](https://img-blog.csdn.net/20160913195355535)

```python
#append是series和dataframe的方法，使用它就是默认沿着列进行凭借（axis = 0，列对齐）
result = df1.append(df2)
```

![这里写图片描述](https://img-blog.csdn.net/20160913195644364)

### 两个dataframe相同字段的表首尾相接

![这里写图片描述](https://img-blog.csdn.net/20160913192849769)

```python
result = pd.concat(frames)
#要在相接的时候在加上一个层次的key来识别数据源自于哪张表，可以增加key参数
result = pd.concat(frames, keys=['x', 'y', 'z'])
```

![这里写图片描述](https://img-blog.csdn.net/20160913194106249)

### 两列合并

```python
df['ab'] = df['a']+df['b']
如果有一列不是str，在后面加上.map(str),str()会乱
df['ab']=df['a']+df['b'].map(str)
```

### 某一列->list

```python
df = pd.DataFrame({'a':[1,3,5,7,4,5,6,4,7,8,9], 'b':[3,5,6,2,4,6,7,8,7,8,9]})
把a列的元素转换成list：
df['a'].values.tolist()
df['a'].tolist()

把a列中不重复的元素转换成list：
df['a'].drop_duplicates().values.tolist()

转换成list[list]
df.values.tolist()
```



### datetime转成date

```python
单个数据：
datetime_object = datetime.now()
2020-10-20 08:48:07.101235
print(datetime.date(datetime_object))
2020-10-20

dataframe里面的操作：
   水果  数量  价格     date
0  苹果   3  10 2020-10-20 08:48:07.101235
1   梨   2   9 2020-10-20 08:48:07.101235
2  草莓   5   8 2020-10-20 08:48:07.101235
df['date'] = df['date'].apply(lambda x: datetime.date(x)) 
#不能直接df['date'] = datetime.date(df['date'])
```



### 遍历dataframe

- iterrows(): 按行遍历，将DataFrame的每一行迭代为(index, Series)对，可以通过row[name]对元素进行访问。

  ```python
  for index, row in df.iterrows(): 
  	print(index) # 输出每行的索引值
  ```

- itertuples(): 按行遍历，将DataFrame的每一行迭代为元祖，可以通过row[name]对元素进行访问，比iterrows()效率高。

- iteritems():按列遍历，将DataFrame的每一列迭代为(列名, Series)对，可以通过row[index]对元素进行访问。

### read_csv参数表

- pandas.read_csv(filepath_or_buffer, sep=', ', delimiter=None, header='infer', names=None, index_col=None, usecols=None, squeeze=False, prefix=None, mangle_dupe_cols=True, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skipinitialspace=False, skiprows=None, nrows=None, na_values=None, keep_default_na=True, na_filter=True, verbose=False, skip_blank_lines=True, parse_dates=False, infer_datetime_format=False, keep_date_col=False, date_parser=None, dayfirst=False, iterator=False, chunksize=None, compression='infer', thousands=None, decimal=b'.', lineterminator=None, quotechar='"', quoting=0, escapechar=None, comment=None, encoding=None, dialect=None, tupleize_cols=None, error_bad_lines=True, warn_bad_lines=True, skipfooter=0, doublequote=True, delim_whitespace=False, low_memory=True, memory_map=False, float_precision=None)

### csv读入时日期型数据的处理

- `parse_dates = ['B','c']`

### 删除某一列 

- 根据列名
  - `df.drop(['B', 'C'], axis=1)`
  - `df.drop(columns=['B', 'C'])`
- 根据列数（第几列）
  - `df.drop(df.columns[0],axis=1)`

### 删除某一行

- `df.drop([0, 1])`	
- `df.drop(index=[0, 1])`

### 获得行列名称

- `df._stat_axis.values.tolist() # 行名称`
- `df.columns.values.tolist()    # 列名称`
- 获得某一列名称`df.columns[列数]`
- 获得列名 `df.columns`

### 查看某一列的数据类型

- `df.dtypes`
- `df['B'].dtypes`

### Pandas分组（GroupBy）

![img](https://img-blog.csdn.net/20170704221210342?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMTUyMzc5Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

​	构建好的dataframe：

```python
    Points  Rank    Team  Year
0      876     1  Riders  2014
1      789     2  Riders  2015
2      863     2  Devils  2014
3      673     3  Devils  2015
4      741     3   Kings  2014
5      812     4   kings  2015
6      756     1   Kings  2016
7      788     1   Kings  2017
8      694     2  Riders  2016
9      701     4  Royals  2014
10     804     1  Royals  2015
11     690     2  Riders  2017
```

- 按列分组  

  ```python
  print (df.groupby('Team').groups)#一列
  得到的结果：
  {
  'Devils': Int64Index([2, 3], dtype='int64'), 
  'Kings': Int64Index([4, 6, 7], dtype='int64'), 
  'Riders': Int64Index([0, 1, 8, 11], dtype='int64'), 
  'Royals': Int64Index([9, 10], dtype='int64'), 
  'kings': Int64Index([5], dtype='int64')
  }
  ```

  ```python
  print (df.groupby(['Team','Year']).groups)#两列
  得到的结果：
  {
  ('Devils', 2014): Int64Index([2], dtype='int64'), 
  ('Devils', 2015): Int64Index([3], dtype='int64'), 
  ('Kings', 2014): Int64Index([4], dtype='int64'),
  ('Kings', 2016): Int64Index([6], dtype='int64'),
  ('Kings', 2017): Int64Index([7], dtype='int64'), 
  ('Riders', 2014): Int64Index([0], dtype='int64'), 
  ('Riders', 2015): Int64Index([1], dtype='int64'), 
  ('Riders', 2016): Int64Index([8], dtype='int64'), 
  ('Riders', 2017): Int64Index([11], dtype='int64'),
  ('Royals', 2014): Int64Index([9], dtype='int64'), 
  ('Royals', 2015): Int64Index([10], dtype='int64'), 
  ('kings', 2015): Int64Index([5], dype='int64')
  }
  ```

- 遍历，选择，分好的组

```python
grouped = df.groupby('Year')

for name,group in grouped:
    print (name)
    print (group)
结果：
2014
     Team  Rank  Year  Points
0  Riders     1  2014     876
2  Devils     2  2014     863
4   Kings     3  2014     741
9  Royals     4  2014     701
2015
      Team  Rank  Year  Points
1   Riders     2  2015     789
3   Devils     3  2015     673
5    kings     4  2015     812
10  Royals     1  2015     804
2016
     Team  Rank  Year  Points
6   Kings     1  2016     756
8  Riders     2  2016     694
2017
      Team  Rank  Year  Points
7    Kings     1  2017     788
11  Riders     2  2017     690

选择一个分组 print (grouped.get_group(2014))
```

- 聚合agg

![img](https://pic2.zhimg.com/80/v2-a0b4827a2829c7e4f9082b958f093f7d_1440w.jpg)

```python
grouped = df.groupby('Year')
print (grouped['Points'].agg(np.mean))

Year
2014    795.25
2015    769.50
2016    725.00
2017    739.00
Name: Points, dtype: float64

grouped = df.groupby('Team')
print (grouped.agg(np.size))

grouped = df.groupby('Team')
agg = grouped['Points'].agg([np.sum, np.mean, np.std])
print (agg)

         sum        mean         std
Team                                
Devils  1536  768.000000  134.350288
Kings   2285  761.666667   24.006943
Riders  3049  762.250000   88.567771
Royals  1505  752.500000   72.831998
kings    812  812.000000         NaN
```

- 转换

```python
grouped = df.groupby('Team')
score = lambda x: (x - x.mean()) / x.std()*10
print (grouped.transform(score))
```

- 过滤

```python
filter = df.groupby('Team').filter(lambda x: len(x) >= 3)
print (filter)
```

### DataFrameGroupBy

- 通过对`DataFrame`对象调用`groupby()`函数返回的结果是一个`DataFrameGroupBy`对象，而不是一个`DataFrame`或者`Series`对象，所以，它们中的一些方法或者函数是无法直接调用的，需要按照`GroupBy`对象中具有的函数和方法进行调用。
- 通过调用`get_group()`函数可以返回一个按照分组得到的`DataFrame`对象，所以接下来的使用就可以按照·DataFrame·对象来使用。

```python
可以把处理好的`DataFrameGroupBy`转换成dataframe
```

![](https://tvax4.sinaimg.cn/large/005IQUPRly1gjvk7nhzcoj30ry02a747.jpg)

![](https://tvax2.sinaimg.cn/large/005IQUPRly1gjvk6lc92kj30sx0dngme.jpg)

### 处理缺失值（三种处理方式）

- 去掉含有缺失值的样本（行）

  - ```python
    DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
    ```

  - axis:

    - axis=0: 删除包含缺失值的行
    - axis=1: 删除包含缺失值的列

  - how: 与axis配合使用

    - how=‘any’ :只要有缺失值出现，就删除该行货列
    - how=‘all’: 所有的值都缺失，才删除行或列

  - thresh： axis中至少有thresh个非缺失值，否则删除
    比如 axis=0，thresh=10：标识如果该行中非缺失值的数量小于10，将删除改行

  - subset: list
    在哪些列中查看是否有缺失值

- 将含有缺失值的列（特征向量）去掉

  - ```python
    DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')
    ```

    - labels: 要删除行或列的列表
    - axis: 0 行 ；1 列

- 将缺失值用某些值填充（0，平均值，中值等）

  - ```python
    DataFrame.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None, **kwargs)
    ```

    - value: scalar, dict, Series, or DataFrame
      dict 可以指定每一行或列用什么值填充

    - method： {‘backfill’, ‘bfill’, ‘pad’, ‘ffill’, None}, default None

      在列上操作

      - ffill / pad: 使用前一个值来填充缺失值
      - backfill / bfill :使用后一个值来填充缺失值

    - limit 填充的缺失值个数限制。*应该不怎么用*

