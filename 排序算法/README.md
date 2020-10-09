# 常见排序算法

### 冒泡排序

#### Swift

```
//冒泡排序
func bubbleSort(_ nums: inout [Int]) {
        
        guard nums.count > 1 else {
            return
        }
        
        let n = nums.count
        
        for i in 0..<n-1 {
            for j in 0..<(n-1-i) {
                if nums[j] > nums[j+1] {
                    nums.swapAt(j, j+1)
                }
            }
        }
    }   
```

**冒泡排序优化一：**  
当发现在某一趟排序中发现没有发生交换，则说明排序已经完成，所以可以在此趟排序后结束排序。在每趟排序前设置flag，当其未发生改变时，终止算法；

```
//冒泡排序优化1（外层优化）
    func bubbleSort1(_ nums: inout [Int]) {
        
        guard nums.count > 1 else {
            return
        }
        
        let n = nums.count
        
        for i in 0..<n-1 {
            var flag = true
            for j in 0..<(n-1-i) {
                if nums[j] > nums[j+1] {
                    nums.swapAt(j, j+1)
                    flag = false
                }
            }
            
            if flag {
                break
            }
        }
    }
```

**冒泡排序优化二：**  
每趟排序中，最后一次发生交换的位置后面的数据均已有序，所以我们可以记住最后一次交换的位置来减少排序的趟数。

```
//冒泡排序优化2（内层优化）
    func bubbleSort2(_ nums: inout [Int]) {
        
        guard nums.count > 1 else {
            return
        }
        
        let n = nums.count
        var swap = 0//swap变量用来标记循环里最后一次交换的位置
        var k = n-1//内循环判断条件
        
        for _ in 0..<n-1 {
            var flag = true
            for j in 0..<k {
                if nums[j] > nums[j+1] {
                    nums.swapAt(j, j+1)
                    flag = false
                    swap = j
                }
            }
            
            k = swap
            
            if flag {
                break
            }
        }
    }
```
