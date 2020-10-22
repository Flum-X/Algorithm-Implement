# Algorithm-Implement
算法整理-链表

### Swift

```
class ListNode {//定义链表节点
    var val: Int
    var next: ListNode?
    
    init(_ val: Int) {
        self.val = val
        self.next = nil
    }
}

//实现链表
class List {
    var head: ListNode?
    var tail: ListNode?
    
    //头插法
    func appendToHead(_ val: Int) {
        
        if head == nil {
            head = ListNode(val)
            tail = head
        } else {
            let temp = ListNode(val)
            temp.next = head
            head = temp
        }
    }
    
    //尾插法
    func appendToTail(_ val: Int) {
        
        if tail == nil {
            tail = ListNode(val)
            head = tail
        } else {
            tail!.next = ListNode(val)
            tail = tail!.next
        }
    }
    
    //检测一个链表中是否有环，快慢指针
    
    func hasCycle(_ head: ListNode?) -> Bool {
        
        var slow = head
        var fast = head
        
        while fast != nil && fast!.next != nil {
            slow = slow!.next
            fast = fast!.next!.next
            
            if slow == fast {//Todo: 需要实现Equatable协议
                return true
            }
        }
        
        return false
    }
}
```