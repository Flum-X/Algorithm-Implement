# Algorithm-Implement
###求斐波那契数列的第n项

#### C  

递归实现

```
long long Fib(int n) {
    
    if (n < 2) {
        return n;
    }
    
    return Fib(n-1) + Fib(n-2);
}
```

循环实现

```
long long Fib1(int n) {
    
    if (n < 2) {
        return n;
    }
    
    long long firstNum = 0;
    long long secondNum = 1;
    long long fibN = 0;
    
    for (int i=2; i<=n; i++) {
        fibN = firstNum + secondNum;
        firstNum = secondNum;
        secondNum = fibN;
    }
    
    return fibN;
}
```

**递归相对于循环的优缺点对比**  
优点：代码简洁。  
缺点：  
1）效率低。递归是函数调用自身，而函数调用是有时间和空间的消耗的，函数调用时往栈里压入和弹出数据都需要时间。  
2）可能导致调用栈溢出。每一次函数调用都需要在内存栈中分配空间，而每个进程的栈的容量是有限的，当递归调用的层级太多时，就会超出栈的容量，从而导致调用栈溢出。  

### Swift

可变数组实现

```
func fib(_ num: Int) -> Int {
        
        var arr: [Int] = [0,1]
        if num > 1 {
            for i in 2...num {
                let temp = arr[i-1] + arr[i-2]
                arr.append(temp)
            }
        }
        return arr[num]
    }
```
由于arr中元素不能超过Int的最大取值范围，所以num不能取太大。

