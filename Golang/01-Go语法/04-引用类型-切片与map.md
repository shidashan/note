## 一 切片
#### 1.1 切片介绍
在很多应用场景中，数组并不能满足我们的需求。在初始定义数组时，我们并不知道需要多大的数组，因此我们就需要“动态数组”。在Go里面这种数据结构叫slice。
切片解决了数组长度不能扩展，以及基本类型数组传递时产生副本的问题。
#### 1.2 切片创建
##### 1.2.1 常用创建方式
```
	var s1 []int				//和声明数组一样，只是没有长度，但是这样做没有意义，因为底层的数组指针为nil
	s2 := []byte {'a','b','c'}
	fmt.Println(s1)				//输出 []
	fmt.Print(s2)				//输出 [97 98 99]
```
###### 1.2.2 从数组创建
slice可以从一个数组或一个已经存在的slice中再次声明。slice通过array[i:j]来获取，其中i是数组的开始位置，j是结束位置，但不包含array[j]，它的长度是j-i。
```
	// 声明一个含有10个元素元素类型为byte的数组
	var arr = [10]byte {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}

	// 声明两个含有byte的slice
	var a, b []byte

	// a指向数组的第3个元素开始，并到第五个元素结束，
	a = arr[2:5]			//现在a含有的元素: ar[2]、ar[3]和ar[4]
	// b是数组arr的另一个slicre
	b = arr[3:5]			// b的元素是：ar[3]和ar[4]
```
注意：声明数组时，方括号内写明了数组的长度或使用...自动计算长度，而声明slice时，方括号内没有任何字符。
###### 1.2.3 从切片创建
```
oldSlice := []int{1,2,3} newSlice := oldSlice[:6]	//基于切片前6个元素创建，没有的默认0
```
注意：如果选择的旧切片长度超出了旧切片的cap()值（切片存储长度），则不合法。
###### 1.2.4 使用make函数创建
```
	slice1 := make([]int,5)		//	创建初始值为0，个数为5的切片
	slice2 := make([]int,5,10)	//创建初始值为10，个数为5的切片
	slice3 := []int{1,2,3,4,5}	//创建并初始化
```
#### 1.3 切片内置函数
切片常用内置函数：
len()		返回切片产后度
cap()		返回切片底层数组容量
append()	对切片追加元素
copy()		复制一个切片

与数组相比，切片多了一个存储能力值的概念，即元素个数与分配空间可以是两个不同的值。合理设置存储能力，可以大幅提升性能，比如知道最多元素个数为50，那么提前设置为50，而不是先设为30，可以明显减少重新分配内存的操作。
```
slice := make([]int,5,10)  //10即为存储的个数，使用 cap(slice)获得
```
```
	//切片增加
	slice1 = append(slice1,1,2)
	fmt.Println(slice1)						//输出[0 0 0 0 0 1 2]

	//切片增加一个新切片
	sliceTemp := make([]int,3)
	slice1 = append(slice1,sliceTemp...)
	fmt.Println(slice1)						//输出[0 0 0 0 0 1 2 0 0 0]
```
注意：没有...会编译错误，默认第二个参数后是元素值，传入切片需要展开。如果追加的长度超过当前已分配的存储空间，切片会自动分配更大的内存。
#### 1.4 切片的一些简便操作
slice有一些简便的操作
slice的默认开始位置是0，ar[:n]等价于ar[0:n]
slice的第二个序列默认是数组的长度，ar[n:]等价于ar[n:len(ar)]
如果从一个数组里面直接获取slice，可以这样ar[:]，因为默认第一个序列是0，第二个是数组的长度，即等价于ar[0:len(ar)]
```
// 声明一个数组
var array = [10]byte{'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}
// 声明两个slice
var aSlice, bSlice []byte

// 演示一些简便操作
aSlice = array[:3] // 等价于aSlice = array[0:3] aSlice包含元素: a,b,c
aSlice = array[5:] // 等价于aSlice = array[5:10] aSlice包含元素: f,g,h,i,j
aSlice = array[:] // 等价于aSlice = array[0:10] 这样aSlice包含了全部的元素

// 从slice中获取slice
aSlice = array[3:7] // aSlice包含元素: d,e,f,g，len=4，cap=7
bSlice = aSlice[1:3] // bSlice 包含aSlice[1], aSlice[2] 也就是含有: e,f
bSlice = aSlice[:3] // bSlice 包含 aSlice[0], aSlice[1], aSlice[2] 也就是含有: d,e,f
bSlice = aSlice[0:5] // 对slice的slice可以在cap范围内扩展，此时bSlice包含：d,e,f,g,h
bSlice = aSlice[:] // bSlice包含所有aSlice的元素: d,e,f,g

```
#### 1.5 切片的拷贝
```
s1 := []int{1,2,3,4,5}
s2 := []int{1,2,3}
copy(s1,s2) //复制s1前三个元素到slice2
copy(s2,s1) //复制s23的个元素到slice1前3位置
```
#### 1.6 切片的截取
![](/images/Golang/01-04-01.png)
#### 1.7 字符串转切片
```
	str := "hello,世界"
	a := []byte(str)		//字符串转换为[]byte类型切片
	b := []rune(str)		//字符串转换为[]rune类型切片
```
#### 1.8 切片存储结构
切片其实是一个维护了多份数据的结构：
```
type slice struct {
	arrat=y unsafe.Pointer		//指向底层数组的指针
	len int						//切片元素数量
	cap int						//底层数组的容量
}
```
所以切片通过内部的指针和相关属性引用数组片段，实现了变长方案，Slice并不是真正意义上的动态数组，而是一个引用类型，slice总是指向一个底层的array。那么slice的声明也可以像数组一样，只是不需要长度。
![](/images/Golang/01-04-02.png)

## 二 集合map
#### 2.1 map的创建
Go内置了map类型，map是一个无序键值对集合（也有一些书籍翻译为字典）。
```
	//map的简单创建
	//声明一个map类型，[]内的类型指任意可以进行比较的类型 int指值类型
	m := map[string]int{"a":1,"b":2}
	fmt.Print(m["a"])
```

使用make方式创建map：
```
type Person struct{
	ID string
	Name string
}

func main() {

	var m map[string] Person				
	m = make(map[string] Person)
	m["123"] = Person{"123","Tom"}
	p,isFind := m["123"]
	fmt.Println(isFind)		//true
	fmt.Println(p)			//{123 Tom}

}
```
#### 2.2 map的使用
map的读取和设置也类似slice一样，通过key来操作，只是slice的index只能是｀int｀类型，而map多了很多类型，可以是int，可以是string及所有完全定义了==与!=操作的类型。
```
// 声明一个key是字符串，值为int的字典,这种方式的声明需要在使用之前使用make初始化
var numbers map[string]int
// 另一种map的声明方式
numbers = make(map[string]int)
numbers["one"] = 1 //赋值
numbers["ten"] = 10 //赋值
numbers["three"] = 3

fmt.Println("第三个数字是: ", numbers["three"]) // 读取数据
// 打印出来如:第三个数字是: 3
```

注意：
map是无序的，每次打印出来的map都会不一样，它不能通过index获取，而必须通过key获取；
map的长度是不固定的，也就是和slice一样，也是一种引用类型	
内置的len函数同样适用于map，返回map拥有的key的数量
map的值可以很方便的修改，通过numbers["one"]=11可以很容易的把key为one的字典值改为11
map和其他基本型别不同，它不是thread-safe，在多个go-routine存取时，必须使用mutex lock机制

#### 2.3 删除元素
```
// 初始化一个字典
rating := map[string]float32{"C":5, "Go":4.5, "Python":4.5, "C++":2 }
// map有两个返回值，第二个返回值，如果不存在key，那么ok为false，如果存在ok为true
csharpRating, ok := rating["C#"]
if ok {
    fmt.Println("C# is in the map and its rating is ", csharpRating)
} else {
    fmt.Println("We have no rating associated with C# in the map")
}

delete(rating, "C") // 删除key为C的元素
```
#### 2.4 mpa的安全问题
Go内置的map不是并发安全的，并发安全的map可以使用标准包sync中的map


