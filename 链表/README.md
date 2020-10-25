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
    
    //检测一个链表中是否有环，快行指针
    func hasCycle(_ head: ListNode?) -> Bool {
        
        var slow = head
        var fast = head
        
        while fast != nil && fast!.next != nil {
            slow = slow!.next
            fast = fast!.next!.next
            
            if slow == fast {//需要节点实现Equatable协议
                return true
            }
        }
        
        return false
    }
    
    //删除链表中倒数第n个节点（快行指针应用2）
    func removeNthFromEnd(_ head: ListNode?, _ n: Int) ->ListNode? {
        
        guard let head = head else { return nil }
        
        let dummy = ListNode(0)//占位节点
        dummy.next = head
        var prev: ListNode? = dummy//前节点
        var post: ListNode? = dummy//后节点
        
        //设置前后节点相差n个节点
        for _ in 0..<n {
            if post == nil {
                break
            }
            post = post?.next
        }
        
        //同时移动前后节点
        while post != nil && post?.next != nil {
            prev = prev?.next
            post = post?.next
        }
        
        //删除节点
        prev?.next = prev?.next?.next
        
        return dummy.next
    }
    
    //反转链表
    func reverseListNode(_ head: ListNode?) ->ListNode?{
        
        //定义3个指针，分别指向当前节点、它的前一个节点和后一个节点
        var pReverseHead: ListNode? = nil
        var pNode: ListNode? = head
        var pPrev: ListNode? = nil
        
        while pNode != nil {
            
            let pNext = pNode?.next
            if pNext == nil {
                pReverseHead = pNode
            }
            
            pNode?.next = pPrev
            pPrev = pNode
            pNode = pNext
        }
        
        return pReverseHead
    }
}

extension ListNode: Equatable {
    
    static func == (lhs: ListNode, rhs: ListNode) -> Bool {
        let result = (lhs.val==rhs.val)&&(lhs.next?.val==rhs.next?.val)
        return result
    }
}
```