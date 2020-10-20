## networkx Common Operations

[学习文档](https://www.osgeo.cn/networkx/index.html)

[TOC]

### 有向图

- ```python
  DG = nx.DiGraph()
  DG.add_weighted_edges_from([(1, 2, 0.5), (3, 1, 0.75)])
  DG.out_degree(1,weight='weight')#出度边的权值之和0.5
  DG.degree(1,weight='weight')#所有边的权值之和1.25
  DG.sucessors(1)#继承者[2]
  DG.neighbors(1)#邻居 等于继承者[2]
  ```

### 有向图转无向图

```python
Graph.to_undirected() 
或
H = nx.graph(G)
```

### 多重图

```python
MG = nx.MultiGraph()
MG.add_weighted_edges_from([(1, 2, 0.5), (1, 2, 0.75), (2, 3, 0.5)])
dict(MG.degree(weight='weight'))
{1: 1.25, 2: 1.75, 3: 0.5}
```

### 图形分析

[图形算法](https://www.osgeo.cn/networkx/reference/algorithms/index.html)

### 图形绘制

```python
import matplotlib.pyplot as plt
```

### 图形操作

#### 经典图形操作

| `subgraph` \（G ，N启动）                  | 返回在nbunch中的节点上诱导的子图。 |
| ------------------------------------------ | ---------------------------------- |
| `union` （g，h） [, rename, name] ）       | 返回图g和h的并集。                 |
| `disjoint_union` （g，h）                  | 返回图G和图H的不相交的并集。       |
| `cartesian_product` （g，h）               | 返回g和h的笛卡尔积。               |
| `compose` （g，h）                         | 返回由h组成的g的新图。             |
| `complement` （g）                         | 返回g的图补。                      |
| `create_empty_copy` （g） [, with_data] ） | 返回图形G的副本，并删除所有边。    |
| `to_undirected` [（图）]                   | 返回图表的无向视图 `graph` .       |
| `to_directed` [（图）]                     | 返回图形的定向视图 `graph` .       |

#### 调用一个经典的小图

| `petersen_graph` \ [create_using] ）       | 返回彼得森图。             |
| ------------------------------------------ | -------------------------- |
| `tutte_graph` \ [create_using] ）          | 返回图特图。               |
| `sedgewick_maze_graph` \ [create_using] ） | 返回一个带有循环的小迷宫。 |
| `tetrahedral_graph` \ [create_using] ）    | 返回3-正则柏拉图四面体图。 |

#### 对经典图形使用（构造）生成器

| `complete_graph` n（n） [, create_using] ）               | 返回完整图形 `K_n` 具有n个节点。     |
| --------------------------------------------------------- | ------------------------------------ |
| `complete_bipartite_graph` （N1，N2） [, create_using] ） | 返回完整的二部图 `K_{{n_1,n_2}}` .   |
| `barbell_graph` （M1，M2） [, create_using] ）            | 返回杠铃图：由路径连接的两个完整图。 |
| `lollipop_graph` （m，n） [, create_using] ）             | 返回棒棒糖图； `K_m` 连接到 `P_n` .  |

#### 使用随机图形生成器

| `erdos_renyi_graph` （n，p） [, seed, directed] ） | 返回一个$G{n，p}$随机图，也称为Erdős-Rényi图或二项式图。 |
| -------------------------------------------------- | -------------------------------------------------------- |
| `watts_strogatz_graph` （n，k，p） [, seed] ）     | 返回Watts–Strogaz小世界图。                              |
| `barabasi_albert_graph` （n，m） [, seed] ）       | 根据barab_si–albert优先连接模型返回随机图。              |
| `random_lobster` \（N、P1、P2）[, seed] ）         | 返回随机龙虾图。                                         |

#### 文件->图

使用常用的图形格式读取存储在文件中的图形，如边列表、邻接列表、gml、graphml、pickle、leda等。

```python
nx.write_gml(red, "path.to.file")
>>> mygraph = nx.read_gml("path.to.file")
```

### 查看图的元素

```python
G.nodes#所有节点
G.edges#所有边
G.adj[1]#节点1的相邻节点
G.degree[1]#节点1的度
```

### 属性（图形，节点，边）

- 图形属性

```python
G = nx.Graph(day="Friday")
G.graph['day'] = "Monday"
G.graph #{'day': 'Monday'}
```

- 节点属性

```python
G.add_node(1, time='5pm')
G.add_nodes_from([3], time='2pm')
G.nodes[1]['room'] = 714
#将节点添加到 G.nodes 不将其添加到图表中，使用 G.add_node() 添加新节点
```

- 边缘属性

```python
G.add_edge(1, 2, weight=4.7)
G.add_edges_from([(3, 4), (4, 5)], color='red')
G[1][2]['weight'] = 4.7
G.edges[3, 4]['weight'] = 4.2
```

### 获取/设置边的属性

```python
G[1][2]=G.edge[1,2]#获取/设置边的属性

!=G.edges(1,2)#EdgeDataView([(1, 2, None)])
!=G.edges([1,2])#EdgeDataView([(1, 2)])
```

