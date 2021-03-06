## 7.树

到目前为止，介绍了一些顺序数据结构（例如：数组、队列、链表等），介绍的第一个非顺序数据结构是散列表。
现在学习另一种非顺序数据结构——树，它以分层的方式存储数据，对于存储需要快速查找的数据非常有用。

优势：选择树而不是那些基本数据结构，是因为： 
* 二叉树上进行查找非常快（链表上查找较慢）； 
* 二叉树添加或删除元素也非常快（数组执行添加或删除较慢）
 
### 7.1树的相关关系

一个树结构包含一系列存在父子关系的节点。每个节点都有一个父节点（除了顶部的第一个节点）以及零个或多个子节点：

![树](https://img-blog.csdn.net/20180809155858647?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIwOTAxMzk3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

* 位于树顶部的节点叫作根节点（11）。它没有父节点。树中的每个元素都叫作节点，节点分为内部节点和外部节点。至少有一个子节点的节点称为内部节点（7、5、9、15、13和20是内部节点）。没有子元素的节点称为外部节点或叶节点（3、6、8、10、12、14、18和25是叶节点）。

* 一个节点可以有祖先和后代。一个节点（除了根节点）的祖先包括父节点、祖父节点、曾祖父节点等。一个节点的后代包括子节点、孙子节点、曾孙节点等。例如，节点5的祖先有节点7和节点11，后代有节点3和节点6。

* 有关树的另一个术语是子树。子树由节点和它的后代构成。例如，节点13、12和14构成了上图中树的一棵子树。

* 节点的一个属性是深度，节点的深度取决于它的祖先节点的数量。比如，节点3有3个祖先节点（5、7和11），它的深度为3。

* 树的高度取决于所有节点深度的最大值。一棵树也可以被分解成层级。根节点在第0层，它的子节点在第1层，以此类推。上图中的树的高度为3（最大高度已在图中表示——第3层）。

### 7.2二叉树与二叉搜索树：

二叉树中的节点最多只能有两个子节点：一个是左侧子节点，另一个是右侧子节点。

二叉搜索树（BST）是二叉树的一种，但是它只允许你在左侧节点存储（比父节点）小的值，在右侧节点存储（比父节点）大（或者等于）的值。上一节的图中就展现了一棵二叉搜索树。

····未完！