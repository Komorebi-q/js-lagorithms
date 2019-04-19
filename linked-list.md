## 链表

一个**链表**是数据元素的线性集合， 元素的线性数据不是由它们在内存中的物理位置给出的。相反， 每个元素只想下一个元素。它是由一组节点组成的数据结构， 这些节点一起， 标识序列。

在简单的形势下， 每个节点由数据和到序列中下一个节点的引用组成。

- ✅ 这种结构允在迭代期间有效地从薛烈中的任何位置插入或删除元素。
- ❌ 更快的访问，随机访问。

```javascript
function Node(ele) {
  this.ele = ele;
  this.next = null;
}

function LList() {
  this.head;
  this.tail;
  this.add;
  this.prepend;
  this.contains;
  this.search;
  this.remove;
  this.traverse;
  this.reverseTraverse;
}
```

### 插入

```javascript
  Add(value)
    Pre: value is the value to add to the list
    Post: value has been placed at the tail of the list
    n <- node(value)
    if head = ∅
      head <- n
      tail <- n
    else
      tail.next <- n
      tail <- n
    end if
  end Add

  function add(val) {
    let cur = new Node(val);

    if (!list.head) {
      list.head = node;
      list.tail = node;
    } else {
      list.tail.next = node;
      list.tail = node;
    }
  }
```

```javascript
  Prepend(value)
    pre: value is the value to add the list
    post: value has beeb placed at the head the list
    n <- node(value)
    n.next <- head
    head <- n
    if tail <- ∅
      tail <- n
    end if
  end

  function prepend(val) {
    const cur = new Node(val);

    if (!list.head) {
      list.head = cur;
      list.tail = cur;
    } else {
      cur.next = list.head;
      list.head = cur;
    }
  }
```

### 搜索

```javascript
  Contains(head, value)
    Pre: head is the value node in the list
         value is the value to search for
    Post: the item is either in the linked list, true; otherwise          false
    n <- head
    while n != ∅ and n.value != value
      n <- n.next
    end  while
    if n == ∅
      return false
    else
      return true

  function contains(head, val) {
    let cur = list.head;

    while(cur && cur.value !== val) {
      cur = cur.next;
    }

    return !!cur;
  }
```

### 删除

```javascript
  Remove(head, value)
  Pre: head is the head node in the list
       value is the value to remove from the list
  Post: value is remove form the list, true, otherwise false
    if head = ∅
      return false
    end if
    if n.value = value
      if head = tail
        head <- ∅
        tail <- ∅
      else
        head <- head.next
      end if
      return true
    end if
    while n.value != ∅ and n.next.value != ∅ and n.next.value != value
      n = n.next
    end while
    if n.next != ∅
      if n.next = tail
        tail <- n
      end if
      n.next <- n.next.next
      return true
    end if
    return false
  end remove

  function remove(val) {
    if (!list.head) {
      return false;
    }

    let cur = list.head;

    if (list.head.value === val) {
      if (list.head.value === list.tail.value) {
        list.head = undefined;
        list.tail = undefined;
      } else {
        list.head = list.head.next;
      }

      return true;
    } else {
      while (!cur.value && !cur.next.value && cur.next.value !== value) {
        cur = cur;
      }

      if (!cur.next) {
        if (cur.next.value === list.tail.value) {
          list.tail === cur;
        } else {
          cur.next = cur.next.next;
        }

        return true;
      } else {
        return false;
      }
    }

  }
```

### 遍历

```javascript
  Traverse(head)
    Pre: head is the head node in the list
    Post: the items in the list have been traversed
    n <- head
    while n != 0
      yield n.value
      n <- n.next
    end while
  end Traversed

  function traversed(fn) {
    let cur = list.head;

    while (cur.next) {
      fn(cur);
      cur = cur.next;
    }
  }
```

### 反向遍历

```javascript
  ReverseTraversal(head, tail)
    Pre: head an tail belong to same list
    Post: the items in the list have been traversed in reverse order
    if tail != ∅
      cur = tail
      while cur != head
        prev <- head
        while prev.next != cur
          prev <- prev.next
        end while
        yield cur.value
        cur <- prev
    end while
    end if
  end reverseTraversal

  function reverseTraversal() {
    let cur = list.tail;
    let prev = list.head

    if (list.tail) {
      while (cur !== list.head) {
        prev = list.head;

        while(prev.next.value !== cur.value){
          prev = prev.next;
        }

        fn(cur);
        cur = prev;
      }
    }
  }
```

| Access | Search | Insertion | Deletion |
| ------ | ------ | --------- | -------- |
| O(n)   | O(n)   | O(1)      | O(1)     |
