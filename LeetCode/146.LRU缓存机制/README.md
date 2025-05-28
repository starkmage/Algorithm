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

因为 Vue 中的 keep-alive 用到的就是 LRU 缓存机制，所以练习了一下这道题，参考[这里的思路](https://leetcode-cn.com/problems/lru-cache/solution/bu-yong-yu-yan-nei-jian-de-map-gua-dang-feng-zhuan/)

不过 Vue 中好像没用到双向链表，用的是数组 keys 存储 key，然后同样的思路，调整 key 在数组 keys 的位置

``` js
function ListNode(key, value) {
    this.key = key
    this.value = value
    this.next = null
    this.prev = null
}

function LRUCache(capacity) {
    if (capacity <= 0) {
        throw new Error('Capacity must be greater than 0')
    }
    this.capacity = capacity
    this.count = 0
    this.map = {}
    // 虚拟头节点
    this.head = new ListNode()
    // 虚拟尾节点
    this.tail = new ListNode()
    this.head.next = this.tail
    this.tail.prev = this.head
}

LRUCache.prototype.addToHead = function(node) {
    node.prev = this.head
    node.next = this.head.next
    this.head.next.prev = node
    this.head.next = node
}

LRUCache.prototype.removeFromList = function(node) {
    node.prev.next = node.next
    node.next.prev = node.prev
}

LRUCache.prototype.moveToHead = function(node) {
    this.removeFromList(node)
    this.addToHead(node)
}

LRUCache.prototype.put = function(key, value) {
    if (key === null || key === undefined) {
        return
    }
    const node = this.map[key]
    if (node === undefined) {
        const newNode = new ListNode(key, value)
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
}

LRUCache.prototype.get = function(key) {
    if (key === null || key === undefined) {
        return -1
    }
    const node = this.map[key]
    if (node === undefined) {
        return -1
    }
    this.moveToHead(node)
    
    return node.value
}

LRUCache.prototype.popTail = function() {
    const tailNode = this.tail.prev
    this.removeFromList(tailNode)

    return tailNode
}

LRUCache.prototype.removeLRUItem = function() {
    if (this.count <= 0) {
        return
    }
    const node = this.popTail()
    delete this.map[node.key]
    this.count--
}
```
