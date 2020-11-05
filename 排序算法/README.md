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

### 选择排序

工作原理：首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到所有元素均排序完毕。

#### Swift
```
//选择排序
func selectSort(_ nums: inout [Int]) {
        
        guard nums.count > 1 else {
            return
        }
        
        let n = nums.count
        var min = 0
        
        for i in 0..<n {
            min = i
            for j in i+1..<n {
                
                if nums[min] > nums[j] {
                    min = j
                }
            }
            
            if min != i {
                nums.swapAt(min, i)
            }
        }
    }   
```

### 快速排序

工作原理：

1）首先设定一个分界值，通过该分界值将数组分成左右两部分；  
2）将大于或等于分界值的数据集中到数组右边，小于分界值的数据集中到数组的左边。此时，左边部分中各元素都小于或等于分界值，而右边部分中各元素都大于或等于分界值；  
3）然后，左边和右边的数据可以独立排序。对于左侧的数组数据，又可以取一个分界值，将该部分数据分成左右两部分，同样在左边放置较小值，右边放置较大值。右侧的数组数据也可以做类似处理；  
4）重复上述过程，可以看出，这是一个递归定义。通过递归将左侧部分排好序后，再递归排好右侧部分的顺序。当左、右两个部分各数据排序完成后，整个数组的排序也就完成了；  

#### Swift

```
    func partition(nums: inout [Int], low: Int, high: Int) -> Int {
        
        let root = nums[high]
        var index = low
        for i in low...high {
            if nums[i] < root {
                if i != index {
                    nums.swapAt(i, index)
                }
                index = index+1
            }
        }
        
        if high != index {
            nums.swapAt(high, index)
        }
        return index
    }
    
    func quickSort(_ nums: inout [Int], low: Int, high: Int) {
        
        if low > high {
            return
        }
        
        let sortIndex = partition(nums: &nums, low: low, high: high)
        quickSort(&nums, low: low, high: sortIndex-1)
        quickSort(&nums, low: sortIndex+1, high: high)
    }
    
    //测试代码
    func test() {
        
        var nums = [1,3,6,5,0,7,9,8,2,4]
        quickSort(&nums, low: 0, high: nums.count-1)
        print(nums)
    }
    
    //快速排序2
    func quickSort2(_ array: [Int]) -> [Int] {
        
        guard array.count > 1 else {
            return array
        }
        
        let pivot = array[array.count/2]
        let left = array.filter{$0 < pivot}
        let middle = array.filter{$0 == pivot}
        let right = array.filter{$0 > pivot}
        
        return quickSort(left) + middle + quickSort(right)
    }
```