双向链表（double linked list）是有一组成为节点的顺序连接记录组成的连接数据结构。每个节点包含两个字段， 成为连接， 它们是对接点序列中上一个节点和下一个节点的引用。

```javascript
function Node(val) {
  this.val = val;
  this.prev;
  this.next;
}

function list() {
  this.head;
  this.tail;
  this.add;
  this.remove;
  this.reverseTraversal;
}
```

### 插入

```javascript
  Add
    Pre: value is the value to add the list
    post: value has been insert the list
    cur <- node(val)
    if head = ∅
      list.head = cur
      list.tail = cur
    else
      list.tail.next = cur
      cur.prev = list.tail
      list.tail = cur
    end if
  end Add

  function add(val) {
    let cur = new Node(val);

    if (!list.head) {
      list.head = cur;
      list.tail = cur;
    } else {
      list.tail.next = cur;
      cur.prev = list.tail;
      list.tail = cur;
    }
  }
```

### 删除

```javascript
  Remove
    Pre: value is the value in the list
    Post: value has been remove from the list, return true; otherwise false
    cur <- list.head
    if !cur
      return false
    end if
    if cur.val = val
      if cur = list.tail
        list.head <- ∅
        list.tail <- ∅
      else
        cur.next.prev <- null
        list.head <- cur.next
      end if
      return true
    cur <- cur.next
    while cur && cur.value != val
      cur = cur.next
    end while
    if cur = ∅
      return false
    else if cur = list.tail
      cur.prev.next = ∅
      list.tail = cur.prev
      return true
    else
      cur.prev.next = cur.next
      cur.next.prev = cur.prev
      return true
    end if
  end Remove


  function remove(val) {
    if (!list.head) {
      return false;
    }

    let cur = list.head;

    if (cur.val === val) {
      if (cur === list.tail) {
        list.head = null;
        list.tail = null
      } else {
        cur.next.prev = null;
        list.head = cur.next;
      }

      return true;
    }

    cur = cur.next;

    while(cur && cur.val !== val) {
      cur = cur.next;
    }

    if (!cur) {
      return false;
    } else if (cur === list.tail) {
      cur.prev.next = null;
      list.tail = cur.prev;

      return true;
    } else {
      cur.prev.next = cur.next;
      cur.next.prev = cur.prev;

      return cur;
    }
  }
```

### 反向遍历

```javascript
  ReserveTraversal
    Pre: tail is the node of the list to traversal
    Post: the list has been traversal in reverse list
    cur <- tail
    while cur.prev = ∅
      yield cur.value
      cur <- cur.prev
    end while
  end ReverseTraversal

  function ReserverTraversal(fn) {
    let cur = list.tail;

    while (!cur.prev) {
      fn(cur.val)
      cur = cur.prev
    }
  }
```

| Access | Search | Insertion | Deletion |
| ------ | ------ | --------- | -------- |
| O(n)   | O(n)   | O(1)      | O(1)     |
