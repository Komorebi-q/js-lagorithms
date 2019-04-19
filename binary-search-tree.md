## 二叉查找树（BST）

有序二叉树，排序二叉树

BST 保证键是有序的，所以查找和其他操作可以使用二级制查找的原理：当在 BST 查找一个键（或者代替/插入）时, 从根节点到叶子节点遍历 BST，通过对比存储在树上的子节点的键的不同来决定接下来遍历当前节点的左子树还是右子树。平均上说，这意味着每次对比允许操作跳过一半的树的内容，所以每次操作花费的时间与存储在树上的节点事成比例的。

```javascript
function Node(val, left, right) {
  this.val = val;
  this.left = left;
  this.right = right;
}

function BST(root) {
  this.root = root;
  this.insert;
  this.search;
  this.remove;
  this.findParentOfNode;
  this.findNode;
  this.findMin;
  this.findMax;
  this.forEach;
  this.reverseForEach;
}
```

#### 插入

```javascript
  insert(val)
    Pre: value has passed custom type checks for type T
    Post: value has been placed in the correct location in the tree
    if root = ∅
      root <- node(val)
    else
      insertNode(root, val)
    end if
  end insert

  insertNode(cur, val)
    Pre: cur is the node to start from
    Post: value has been placed in the current location in the tree
    if val < cur.val
      if cur.left = ∅
        cur.left <- node(val)
      else
        insertNode(cur.left, val)
      end if
    else
      if cur.right = ∅
        cur.right = node(val)
      else
        insertNode(cur, val)
      end if
    end if
  end insertNode

  BST.prototype.insert = function (val: T) {
    if (!this.root) {
      this.root = new Node(val);
    } else {
      this.insertNode(this.root, val);
    }
  }

  BST.prototype.insertNode = function (cur: Node, val: T) {
    if (val < cur.val ) {
      if (!cur.left) {
        cur.left = new Node(val);
      } else {
        this.insertNode(cur.left, val);
      }
    } else {
       if (!cur.right) {
        cur.right = new Node(val);
      } else {
        this.insertNode(cur.left, val);
      }
    }
  }
```

#### 查询

```javascript
  contains(root, val)
    Pre: root is the root node of the tree, value is what we should like to locate
    Post: value is either located or not
    if root = ∅
      return false
    end if
    if root.val = val
      return true
    else
      if val < root.val
        return contains(root.left, val)
      else
        return contains(root.right, val)
      end if
    end if
  end contains


  BST.prototype.contains = function(cur: Node, val: T) {
    if (!cur) {
      return false;
    }

    return this.contains(val < cur.val ? cur.left : cur.right, val);
  }
```

#### 查找

```javascript
  findParent(root, val)
    Pre: value is the value of the node we want to find the parent of root is the root node of the BST and is != ∅
    Post: a reference to the parent node of value if found; otherwise ∅
    if node = ∅
      return ∅
    end if
    if val < root.val
      if root.left = ∅
        return ∅
      else if  val = root.left.val
        return root
      else
        return findParent(root.left, val)
      end if
    else
      if root.right = ∅
        return ∅
      else if  val = root.right.val
        return root
      else
        return findParent(root.right, val)
      end if
    end if
  end findParent

  BST.prototype.findParent = function(cur, val) {
    if (!cur) {
      return null;
    }

    if (val < cur.val) {
      if (!cur.left) {
        return null;
      } else if (cur.left.val === val) {
        return cur;
      } else {
        return this.findParent(cur.left, val);
      }
    } else {
      if (!cur.right) {
        return null;
      } else if (cur.right.val === val) {
        return cur;
      } else {
        return this.findParent(cur.right, val);
      }
    }
  }
```

```javascript
  findNode(root, val)
  Pre: value is the value of the node we wat to find the parent of       root is the root node of the BST
  Post: a reference to the node of value if found; otherwise ∅
  if root = ∅
    return ∅
  end if
  if val = root.val
    return root
  else if val < root.val
    return findNode(root.left, val)
  else
    return findNode(root.right, val)
  end if

  BST.prototype.findNode = function(root, val) {
    if (!root) {
      return null;
    }

    if (val === root.val) {
      return root;
    } else  {
      return this.findNode(val < root.val ? root.left : root.right, val);
    }
  }
```

```
  findMin(root)
    Pre: root is the root node of the BST
    Post: the smallest value in the BST is located
    if root = ∅
      return null
    end if
    if root.left = ∅
      return root
    end if
    return findMin(root)
  end findMin

  BST.prototype.findMin(root: Node) {
    if (!root) {
      return null;
    }

    if (!root.left) {
      return root;
    }

    return this.findMin(root)
  }

```

#### 删除

```javascript
  remove(val)
    Pre: value is the value of the node to remove, root is the node of the BST
         count is the number of items in the BST
    Post: node with value is removed if found in which case yields true, otherwise false
    nodeToRemove <- findNode(val)
    if nodeToRemove = ∅
      return false;
    end if
    parent <- findParent(val)
    if nodeToRemove.left = ∅ and nodeToRemove.right = ∅
      if parent.left.val = nodeToRemove.val
        parent.left <- ∅
      else
        parent.right <- ∅
      end if
    else if nodeToRemove.left != ∅ and nodeToMove.right != ∅
      next <- nodeToRemove.right
      while next.left != ∅
        next <- next.left
      end while
      if next = nodeToRemove.right
        remove(next.val)
        nodeToRemove.val <- next.val
      else
        nodeToRemove.val <- next.val
        nodeToRemove.right <- next.right
      end if
    else
      if nodeToRemove.left = ∅
        next <- nodeToRemove.right
      else
        next <- nodeToRemove.left
      end if
      if root = nodeToRemove
        root <- next
      else if parent.left = nodeToRemove
        parent.left = next
      else
        parent.right = next
      end if
    end if
  end remove

  BST.prototype.remove = function(root: Node, val: T) {
    if (!root) {
      return false;
    }

    let cur = this.findNode(val);
    let parent = this.findNodeParent(val);
    let next;

    if (!cur) {
      return false;
    }

    if (!cur.left && !cur.right) {
      if (cur.left.val === val) {
        parent.left = null;
      } else {
        parent.right = null;
      }
    } else if (cur.left && cur.right) {
      next = cur.right;

      while (next.left) {
        next = next.left;
      }

      if (next.val !== cur.right.val) {
        this.remove(next, next.val);
        cur.val = next.val;
      } else {
        cur.val = cur.right.val;
        cur.right = next.right;
      }
    } else {
      if (cur.left) {
        next = cur.left;
      } else {
        next = cur.right;
      }

      if (root.val === cur.val) {
        root = next;
      } else if (parent.left.val === cur.val) {
        parent.left = next;
      } else if (parent.right.val === cur.val) {
        parent.right = next;
      }
    }
  }
```

#### 遍历

```javascript
  inorder(root)
    Pre: root is the root node of the BST
    POST: the nodes in the BST have been visited in inorder
    if root != ∅
      inorder(root.left)
      yield root.val
      inorder(root.right)
    end if
```

```javascript
  preorder(root)
    Pre: root is the root node of the BST
    POST: the nodes in the BST have been visited in preorder
    if root != ∅
      yield root.val
      inorder(root.left)
      inorder(root.right)
    end if
```

```javascript
  postorder(root)
    Pre: root is the root node of the BST
    POST: the nodes in the BST have been visited in postorder
    if root != ∅
      inorder(root.left)
      inorder(root.right)
      yield root.val
    end if
```

| Access    | Search    | Insertion | Deletion  |
| --------- | --------- | --------- | --------- |
| O(log(n)) | O(log(n)) | O(log(n)) | O(log(n)) |
