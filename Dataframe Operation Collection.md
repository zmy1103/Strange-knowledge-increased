## Dataframe Operation Collection

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

