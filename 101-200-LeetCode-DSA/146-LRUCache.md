# <u>146. LRU Cache</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/lru-cache/

---

## 🧠 Intuition:
* 🔹 An **LRU (Least Recently Used) Cache** removes the least recently accessed item when capacity is full

* 🔹 We need both operations in O(1) time:
    - `get(key)`
    - `put(key, value)`

* 🔹 To achieve this, combine:
    - **Array (`map`)** → Direct access to nodes using keys
    - **Doubly Linked List** → Maintains usage order

* 🔹 The doubly linked list stores nodes in this order:
    - Most recently used node → near `head`
    - Least recently used node → near `tail`

* 🔹 Dummy `head` and `tail` nodes simplify insertion/deletion operations

🔹 **`get(key)`**
    - If the key does not exist → return `-1`
    - Otherwise:
        * Remove the node from its current position
        * Move it to the front (most recently used position)
        * Return its value
🔹 **`put(key, value)`**
    - If key already exists:
        * Update its value
        * Move it to the front since it was recently used
    - If key does not exist:
        * Create a new node
        * If cache is full:
            - Remove the node before tail (least recently used node)
            - Remove it from the map as well
        * Insert the new node at the front

#### 🔹 Helper Functions
    * `deleteNode(node)` → Removes a node from the doubly linked list
    * `addToHead(node)`→ Inserts a node right after the head

* 🔹 This ensures the cache always keeps track of recently used elements efficiently.

---

## ⏱ Time Complexity

#### `get(key)`
    * Direct access + linked list updates
    * 👉 **O(1)**

#### `put(key, value)`
    * Insertion/deletion in linked list + array access
    * 👉 **O(1)**

---

## 📦 Space Complexity

**O(capacity)**
  
* One node stored for each cache entry

---

## 💻 Java Code

```java
class LRUCache {
    class Node {
        int key;
        int value;
        Node prev;
        Node next;

        Node(int key, int value) {
            this.key = key;
            this.value = value;
            this.prev = null;
            this.next = null;
        }
    }

    public Node[] map; //store each node
    public int count, capacity;
    public Node head, tail; //store the order of recently used node
    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.count = 0;
        this.map = new Node[10000+1]; //0 <= key <= 10000

        this.head = new Node(0, 0);
        this.tail = new Node(0, 0);
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    //Deleting the node in LRU cache
    private void deleteNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    //Adding the node at the head of LRU cache
    private void addToHead(Node node) {
        node.next = this.head.next;
        node.prev = this.head;

        node.next.prev = node;
        this.head.next = node;
    }
    
    public int get(int key) {
        //Check if node is present in LRU cache
        if(map[key] != null) {
            Node node = map[key];
            deleteNode(node); //Delete the node in LRU cache
            addToHead(node); //Then add it at the head and make it as the most recently used node
            return node.value;
        } else {
            return -1;
        }
    }
    
    public void put(int key, int value) {
        //Check if node is present in LRU cache
        if(map[key] != null) {
            //If exist, replace the value and make the node as the most recently used node
            Node node = map[key];
            node.value = value; //Replace with the new value
            //Make the node as the most recently used node
            deleteNode(node);
            addToHead(node);
        } else {
            //Create a new node
            Node node = new Node(key, value);
            map[key] = node;

            //Check if space is available
            if(count < capacity) {
                //Add it directly
                count++;
                addToHead(node);
            } else {
                //Delete the least recently used node
                Node least = tail.prev;
                map[least.key] = null;
                deleteNode(least);
                //Make the curr node be the most recently used node
                addToHead(node);
            }
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

---