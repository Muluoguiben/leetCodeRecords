#  数组（Array）

##         Ⅰ.关于数组

- #### 数组是什么：数组是一种线性表数据存储结构，具有相连的内存，存储相同类型的数据.

- #### 数组的几种常见具体形式：

  1. ##### 存储整数的数组                       <img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/memory.png" alt="memory" style="zoom:33%;" />

     ​                                                                         

     - 给定特定位置的索引<img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/1.1.png" alt="1" style="zoom:33%;" />         <img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/2.png" alt="2" style="zoom:33%;" />

     - 索引内存位置公式

       > j[i]_address = base_address + i * data_type_size _

       > j[0]_address = 1000
       >
       > j[0]_value = 5
       >
       > j[5]_address = 1000 + 5 *1 = 1005
       >
       > j[5]_value = 4

       

  2. ##### 存储字符串的数组                                         <img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/string.png" alt="string" style="zoom:33%;" />

     - 同整数类型的索引与内存位置，除最后一位为<p>==二进制0 = 字符null，意味着字符串结尾==</p>

       > j = "STAN ROCKS"
       >
       > j[0] = "S"
       >
       > j[4] = 
       >
       > j[10] →IndexError: string index out of range
       >
       > print(j) = STAN ROCKS

       

  3. ##### 存储数组的数组，即矩阵       <img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/matrix.png" alt="matrix" style="zoom:33%;" />

     - 给定特定位置的索引<img src="https://first-1303075678.cos.ap-beijing.myqcloud.com/img/matrix2.png" alt="matrix2" style="zoom:33%;" />

       > address = base_address + ( i * n + j) * type_size

       > j = [[10,15,12],[8,7,42],[18,12,7]]
       >
       > j[0] = [10,15,12]
       >
       > j [1] [1] = 7
       >
       > j [2] [0] = 18
       >
       > j[0]_address = 1000
       >
       > j [1] [1]_address = 1000 + 3 *1 + 1 = 1004
       >
       > j [2] [0]_address = 1000 + 3 *2 + 0 = 1006
       >
       > print(j) = [[10, 15, 12], [8, 7, 42], [18, 12, 7]]

  

- #### 关于数组下标的疑惑

  ​		刚学习编程语言时，第一次接触到的数组是python中的列表，当时对取列表下标感到一点疑惑，为什么是从0开始而不是从1开始呢？

  > ​		从数组存储的内存模型上来看，“下标”最确切的定义应该是“**偏移**（offset）”。如果用 j 来表示数组，j[0]就是偏移为 0 的位置，也就是首地址，j[i]就表示偏移 i 个 type_size 的位置.

## Ⅱ.数组的查找，添加，删除操作

### 	数组的查找操作

基于数组中给定的索引位置进行查找.  例如，查找数组中第三个位置的元素，通过 j[2] 就可以直接取出来. 根据下标随机访问的时间复杂度为 O(1).

基于数组中的数值进行查找.  例如，查找数值为 9 的元素是否出现过，以及如果出现过，索引值是多少.   基于数值属性的查找操作，需要整体遍历一遍数组.  需要 O(n) 的时间复杂度.  即便使用二分查找，时间复杂度也是O（logn）.



###   数组的插入操作

假设数组的长度为 n，现在，如果我们需要将一个数据插入到数组中的第 k 个位置.  为了把第 k 个位置腾出来，给新来的数据，我们需要将第 k～n 这部分的元素都顺序地往后挪一位. 插入操作的时间复杂度是多少呢？

1. 数组的最后增加一个新的元素.  此时新增一条数据后，对原数据产生没有任何影响.  可以直接通过新增操作，赋值或者插入一条新的数据即可.  时间复杂度是 O(1).  
2. 数组的中间增加一个新的元素.  此时新增这条数据后，会对插入元素位置之后的元素产生影响，这些数据的位置需要依次向后挪动 1 个位置.  搬移操作（n- k ）与数组的数据量线性相关，时间复杂度是 O(n).
3. 数组的开头增加一个新的元素.  此时新增这条数据后，那所有的之后位置的数据都需要依次往后移动一位，最坏时间复杂度 O(n).
4. 如果对原数组数据顺序没有要求，直接在最后位置插入一个树，然后和第K个的数进行调换即可，时间复杂度为O(1)
5. 平均情况时间复杂度为 (1+2+…n)/n=O(n).



###  数组的删除操作

删除操作与插入操作类似，为了保证内存的连续性，也需要搬移数据.

1. 数组的最后删除一个数据元素.  由于此时删除这条数据后，对原数据没有产生任何影响.  我们可以直接删除该数据即可，时间复杂度是 O(1).

2. 数组的中间删除一个数据元素. 由于涉及查找全数组与要删除数据的后续数据的搬移操作，故时间复杂度是O(n).

3. 数组的开头删除一个数据元素.  最坏情况时间复杂度为 O(n).

4. 同插入4操作，如果有多次删除操作，可以合并并提高效率

5. 平均情况时间复杂度为 (1+2+…n)/n=O(n).

   

   

## Ⅲ.数组的特点小结

数组定义简单，访问方便，但在数组中所有元素类型必须相同，数组的最大长度必须在定义时给出，数组下标从0开始，下标取值范围[0,1,2,...,len-1]，数组使用的内存空间必须连续等.  

最大的特点就是支持随机访问，但插入、删除操作也比较低效，平均情况时间复杂度为 O(n).

数组适合在数据数量确定，即较少甚至不需要使用新增数据、删除数据操作的场景下使用.  在数据对位置敏感的场景下，比如需要高频根据索引位置查找数据时，数组就是个很好的选择了.  









## Ⅳ.实现数组的代码

###     1.普通数组

```python
class MyArray:

    def __init__(self, capacity: int):
        self._data = []                   //数据 
        self._capacity = capacity         //大小

    def __getitem__(self, position: int) -> object:
        return self._data[position]       //返回索引值

    def __setitem__(self, index: int, value: object):
        self._data[index] = value         //根据索引值获得值

    def __len__(self) -> int:
        return len(self._data)            //返回长度

    def __iter__(self):
        for item in self._data:
            yield item                    //返回全部数据元素

    def find(self, index: int) -> object:
        try:
            return self._data[index]      //找到返回索引
        except IndexError:
            return None

    def delete(self, index: int) -> bool:
        try:
            self._data.remove(index)        //去除索引值的数据
            return True
        except IndexError:
            return False

    def insert(self, index: int, value: int) -> bool:
        if len(self) >= self._capacity:
            return False
        else:
            return self._data.insert(index, value)    //如果数组还有位置，插入索引值和值

    def print_all(self):
        for item in self:
            print(item)                      //打印所有数据元素

def test_myarray():
    array = MyArray(5)
    array.insert(0, 3)
    array.insert(0, 4)
    array.insert(1, 5)
    array.insert(3, 9)
    array.insert(3, 10)
    assert array.insert(0, 100) is False
    assert len(array) == 5
    assert array.find(1) == 5
    assert array.delete(4) is True
    array.print_all()
    
if __name__ == "__main__":
    test_Myarray()  
    
    //引自 https://github.com/wangzheng0822/algo/blob/master/python/05_array/myarray.py
```





### 2.动态数组

```python
#通过python实现动态数组，主要差别在添加和删除的步骤上：  添加步骤39-50行   删除步骤130-145行
"""
数组特点：
  占用一段连续的内存空间，支持随机（索引）访问，且时间复杂度为O(1)
  添加元素时间复杂度：O(n)
  删除元素时间复杂度：O(n)
"""
  
class Arr:
  def __init__(self, capacity=10):
    """
    构造函数
    :param capacity: 数组最大容量，不指定的话默认为10
    """
    self._capacity = capacity
    self._size = 0                 # 数组有效元素的数目，初始化为0
    self._data = [None] * self._capacity  # 由于python的list是动态扩展的，而我们要实现
    #底层具有固定容量、占用一段连续的内存空间的数组，所以用None来作为无效元素的标识
  
  def get_all(self):
        return self._data[:self._size]
 
  def __getitem__(self, item):
        """让Arr类支持索引操作"""
        return self.get_all[item]
  
  def getSize(self):
    """返回数组有效元素的个数"""
    return self._size
  
  def getCapacity(self):
    """返回当前数组的容量"""
    return self._capacity
  
  def isEmpty(self):
    """判断当前数组是否为空"""
    return self._size == 0
  
  def add(self, index, elem):
    """
    时间复杂度：O(n)
    """
    if index < 0 or index > self._size:   # 插入的位置无效
      raise Exception('Add Filed. Require 0 <= index <= self._size')
    if self._size == self._capacity:    
      self._resize(self._capacity * 2)  # 容量翻倍要比容量加上一个固定值要好，这样做均摊复杂度为O(1)。
    for i in range(self._size - 1, index - 1, -1):# 从尾部开始挪动元素
      self._data[i + 1] = self._data[i]
    self._data[index] = elem    # 将该位置赋值为elem
    self._size += 1         # 数组有效元素数加1
  
  def addLast(self, elem):
    """
    向数组尾部添加元素
    时间复杂度：O(1)
    """
    self.add(self._size, elem) # 直接调用add方法，注意不用再次判定合法性了，因为add函数中已经判断过了
  
  def addFirst(self, elem):
    """
    向数组头部添加元素
    时间复杂度：O(n)
    """
    self.add(0, elem)  # 同理直接调用add方法
  
  def get(self, index):
    """
    获得索引处的值
    时间复杂度：O(1)
    """
    if index < 0 or index >= self._size:    # 判断index的合法性
      raise Exception('Get failed. Index is illegal.')
    return self._data[index]
  
  def getFirst(self):
    """
    获得数组首位置元素的值
    """
    return self.get(0)   
  
  def getLast(self):
    """
    获得数组末尾元素的值
    """
    return self.get(self._size - 1) 
  
  def set(self, index, elem):
    """
    将索引为index的元素的值设为elem
    时间复杂度：O(1)
    """
    if index < 0 or index >= self._size:    # 判断index的合法性
      raise Exception('Sat failed. Index is illegal.')
    self._data[index] = elem
  
  def contains(self, elem):
    """
    查看数组中是否存在元素elem
    时间复杂度：O(n)
    """
    for i in range(self._size):    
      if self._data[i] == elem:
        return True        # 找到返回True
    return False            # 遍历完还没找到，返回False
  
  def find(self, elem):
    """
    在数组中查找元素，并返回元素所在的索引。（如果数组中存在多个elem，只返回最左边elem的索引）
    时间复杂度：O(n)
    """
    for i in range(self._size):     # 遍历数组
      if self._data[i] == elem:
        return i          # 找到就返回索引
    return -1              # 没找到返回-1
  
  def findAll(self, elem):
    """
    找到值为elem全部元素的索引
    """
    ret_list = Arr()        # 建立一个新的数组用于存储索引值
    for i in range(self._size):   
      if self._data[i] == elem:
        ret_list.addLast(i)   # 找到就将索引添加进ret_list
    return ret_list
  
  def remove(self, index):
    """
    删除索引为index的元素。index后面的元素都要向前移动一个位置
    时间复杂度：O(n)
    """
    if index < 0 or index >= self._size:  # index合法性检查
      raise Exception('Remove failed.Require 0 <= index < self._size')
    ret = self._data[index]         # 拷贝一下index处的元素，便于返回
    for i in range(index + 1, self._size): # index后面的元素都向前挪一个位置
      self._data[i - 1] = self._data[i]
    self._size -= 1     # 数组有效元素数—1
    self._data[self._size] = None  # 最后一个元素的垃圾回收
  
    if self._size and self._capacity // self._size == 4:  # 如果当前有效元素为总容量的四分之一且还存在有效元素，则将容量缩减为原来的一半
      self._resize(self._capacity // 2)
    return ret
  
  def removeFirst(self):
    """
    删除数组首位置的元素
    时间复杂度：O(n)
    """
    return self.remove(0)  
  
  def removeLast(self):
    """
    删除数组末尾的元素
    时间复杂度:O(1)
    """
    return self.remove(self._size - 1)   
  
  def removeElement(self, elem):
    """
    删除数组中为elem的元素。如果存在多个相同的elem，只删除最左边的那个
    时间复杂度：O(n)
    """
    index = self.find(elem)     # 尝试找到目标元素（最左边的）的索引
    if index != -1:         # elem在数组中就删除，否则什么都不做
      self.remove(index)    
  
  def removeAllElement(self, elem):
    """
    删除数组内所有值为elem的元素，这里用的迭代的方法。
    """
    while True:
      index = self.find(elem)   # 循环来找elem，如果还存在就继续删除
      if index != -1:       # 若存在
        self.remove(index)
      else:
        break
  
  def get_Max_index(self):
    """
    获取数组中的最大元素的索引，返回最大元素的索引值，默认返回最左边那个的索引
    时间复杂度：O(n)
    """
    if self.isEmpty():
      raise Exception('Error, array is Empty!')
    max_elem_index = 0  # 记录最大值的索引，初始化为0 
    for i in range(1, self.getSize()):  # 从索引1开始遍历，一直到数组尾部
      if self._data[i] > self._data[max_elem_index]:  # 如果当前索引的值大于最大值索引处元素的值
        max_elem_index = i   # 更新max_elem_index，这样它还是当前最大值的索引
    return max_elem_index   # 遍历完后，将数组的最大值的索引返回
  
  def removeMax(self):
    """
    删除数组中的最大元素，返回最大元素的值，默认删除最左边那个的最大值
    时间复杂度：O(n)
    """
    return self.remove(self.get_Max_index())  # 直接调用remove函数删除最大值
  
  def get_Min_index(self):
    """
    获取数组中的最小元素的索引，返回最小元素的索引值，默认返回最左边那个的索引
    时间复杂度：O(n)
    """
    if self.isEmpty():
      raise Exception('Error, array is Empty!')
    min_elem_index = 0  # 记录最小值的索引，初始化为0 
    for i in range(1, self.getSize()):  # 从索引1开始遍历，一直到数组尾部
      if self._data[i] < self._data[min_elem_index]:  # 如果当前索引的值小于最小值索引处元素的值
        min_elem_index = i   # 更新min_elem_index，这样它还是当前最小值的索引
    return min_elem_index   # 遍历完后，将数组的最小值的索引返回
  
  def removeMin(self):
    """
    删除数组中的最小元素，返回最小元素的值，默认值删除最左边那个
    时间复杂度：O(n)
    """
    return self.remove(self.get_Min_index())
  
  def swap(self, index1, index2):
    """
    交换分别位于索引index1和索引index2处的元素
    """
    if index1 < 0 or index2 < 0 or index1 >= self._size or index2 >= self._size:    # 合法性检查
      raise Exception('Index is illegal')
    self._data[index1], self._data[index2] = self._data[index2], self._data[index1]   # 交换元素
  
  def printArr(self):
    """对数组元素进行打印"""
    for i in range(self._size):
      print(self._data[i], end=' ')
    print('\nSize: %d-----Capacity: %d' % (self.getSize(), self.getCapacity()))
  
  def _resize(self, new_capacity):
    """
    数组容量放缩至new_capacity
    """
    new_arr = Arr(new_capacity)     # 建立一个新的数组new_arr，容量为new_capacity
    for i in range(self._size):
      new_arr.addLast(self._data[i]) # 将当前数组的元素按当前顺序全部移动到new_arr中
    self._capacity = new_capacity    # 数组容量变为new_capacity
    self._data = new_arr._data     # 将new_arr._data赋值给self._data，从而完成数组的容量放缩操作
    
    //参考 https://blog.csdn.net/u013109501/article/details/88020739
```

## Ⅴ.常考题

1.数组的查找最大值、最小值、给定值、重复值

2.数组的排序，快排，归并排序等

3.多个数组的排序，合并、求交集、求并集

