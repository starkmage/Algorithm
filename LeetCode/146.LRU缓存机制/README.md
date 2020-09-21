### 146.LRU缓存机制

---

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例:
```
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得关键字 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得关键字 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
```

---

#### 思路

因为 Vue 中的 keep-alive 用到的就是 LRU 缓存机制，所以练习了一下这道题

不过 Vue 中好像没用到双向链表，用的是数组 keys 存储 key，然后同样的思路，调整 key 在数组 keys 的位置

``` js
// 双向链表
function ListNode(key, value) {
  this.key = key
  this.value = value
  this.next = null
  this.prev = null
}

var LRUCache = function(capacity) {
  this.capacity = capacity
  this.count = 0
  this.map = {}
  this.head = new ListNode()
  this.tail = new ListNode()
  this.head.next = this.tail
  this.head.prev = this.head
};

// 添加节点到头部
LRUCache.prototype.addToHead = function(node) {
  node.prev = this.head
  node.next = this.head.next
  this.head.next.prev = node
  this.head.next = node
}

// 从链表中移除节点
LRUCache.prototype.removeFromList = function(node) {
  let tempPrev = node.prev
  let tempNext = node.next
  tempPrev.next = tempNext
  tempNext.prev = tempPrev
}

// 将一个节点移到头部
LRUCache.prototype.moveToHead = function(node) {
  // 1. 先择出来
  this.removeFromList(node)
  // 2. 放到头部
  this.addToHead(node)
}

// 获取 key 的 value
LRUCache.prototype.get = function(key) {
  const node = this.map[key]
  if (node === undefined) return -1
  this.moveToHead(node)
  return node.value
};

// 添加 key - value 键值对
LRUCache.prototype.put = function(key, value) {
  let node = this.map[key]
  if (node === undefined) {
    let newNode = new ListNode(key, value)
    this.map[key] = newNode
    this.addToHead(newNode)
    this.count++
    if (this.count > this.capacity) {
      this.removeLRUItem()
    }
  } else {
    node.value = value
    this.moveToHead(node)
  }
};

// 从 map 删除最早没使用过的节点
LRUCache.prototype.removeLRUItem = function() {
  let node = this.popTail()
  delete this.map[node.key]
  this.count--
}

// 从双向链表中删除最早没使用的节点
LRUCache.prototype.popTail = function() {
  let tailNode = this.tail.prev
  this.removeFromList(tailNode)
  return tailNode
}
```
