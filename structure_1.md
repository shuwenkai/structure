
#声明：

**写这篇文档纯属无聊，看过别人的基本照搬的，本篇文章与 [百度](http://www.baidu.com) 达成战略合作伙伴，如果不懂也不用问我，请自行搜索,非商业性质，如有侵权请联系删除**


#一、面向对象编程

  JavaScript里的对象就是普通名值对的集合。常见创建一个普通对象有以下几种方式。
  
  * 第一种方式是:
  ```js
  var obj = new Object();
  ```
  * 第二种方式是：
  ```js
  var obj = {};
  ```
  * 第三种方式:
  ```js
  function Car (desc) {
    this.desc = desc;
    this.color = "red";
    }
    Car.prototype = {
    getInfo: function() {
      return `A ${this.color}  ${this.desc}.`;
    }
    };
    //使用构造函数函数实例化对象
    var car =  Object.create(Car.prototype);
    car.color = "blue";
    console.log(car.getInfo());//A blue undefined.
  ```

  在面向对象编程（OOP）中，对象是类的实例，一个类定义了对象的特征。我们会创建很多类来表示算法和数据结构。例如我们声明了一个类来表示书：
  ```js
    function Book(title, pages, isbn){
        this.title = title;
        this.pages = pages;
        this.isbn = isbn;
    }
```

  下面用代码来实例化这个类：

```js

var book = new Book('title', 'pag', 'isbn');

```
    然后我们可以访问和修改对象的属性：
```js
    console.log(book.title);
    book.title = 'new title';
    console.log(book.title);
```
    类可以包含函数。可以声明和使用函数，如下在原型上定义实例共享函数：
```js
    Book.prototype.printTitle = function(){
        console.log(this.title);
    }
    book.printTitle();
```
    也可以直接在类的定义里声明函数。

##1.数组

###1.1 创建和初始化数组: 

两种方式：

```js
let array = new Array();
let array = [];
```

###1.2 添加和删除元素: 后进后出（push、pop）、前进前出（unshift、shift）、splice

###1.3 常用方法:

方法名|描述
--|:-|--:
concat|连接两个或更多数组，并返回结果，不影响原数组
slice|传入索引值，将数组里对应索引范围内的元素作为新数组返回，不影响原数组
splice|	指定位置/索引，就可以删除相应位置和数量的元素，并以新元素代替，影响原数组
reverse|	数组元素反转，影响原数组
toString|	将数组整体作为字符串返回，不影响原数组
join|	将所有的数组元素以指定字符连接成字符串，不影响原数组
indexOf|	返回第一个与给定参数相等的数组元素的索引，没有找到则返回-1
lastIndexOf|	返回与给定参数相等的数组元素索引的最大值
sort|	按照字符对应的ASCII值对数组排序，支持传入指定排序方法的函数作为参数
map|	对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组
forEach	|对数组中的每一项运行给定函数，不影响原数组中的项
filter|	对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组
every|	对数组中的每一项运行给定函数，如果该函数中每一项都返回true，则返回true
some|	对数组中的每一项运行给定函数，如果该函数中任一项返回true，则返回true
reduce|	接收一个函数作为参数，做数组的累加器，或者拼接数组项作为字符串,不改变原数组

```js
//其它函数都比较常用，reduce函数用的少，举例说明一下
function compute(total, currentValue){
    return total + currentValue;
}
let arr = [2, 5, 13];
let res = arr.reduce(compute);
console.log(res);  //20

let strArr = ["s", "r", "f"];
let str = strArr.reduce(compute);
console.log(str);  //"srf"
```
##2、栈

栈是一种遵从后进先出原则的有序集合。新添加的或待删除的元素都保存在栈的末尾，称作栈顶，另一端就叫栈底。

###2.1 创建栈: 

我们将创建一个类来表示栈，选择数组来保存栈里的元素,然后为栈声明如下方法： 
* push(element(s))：添加一个（或几个）新元素到栈顶； 
* pop()：移除栈顶的元素，同时返回被移除的元素； 
* peek()：返回栈顶的元素，不对栈做任何修改； 
* isEmpty()：如果栈里没有任何元素就返回true，否则返回false； 
* clear()：移除栈里的所有元素； 
* size()：返回栈里的元素个数。 
实现代码如下：
```js
function Stack(){
    let items = [];
    //push方法
    this.push = function(element){
        items.push(element);
    }
    //pop方法
    this.pop = function(){
        return items.pop();
    }
    //peek方法
    this.peek = function(){
        return items[items.length-1];
    }
    //isEmpty方法
    this.isEmpty = function(){
        return items.length == 0;
    }
    //clear方法
    this.clear = function(){
        items=[];
    }
    //size方法
    this.size = function(){
        return items.length;
    }
}
//使用栈
let stack = new Stack();
console.log(stack.isEmpty());    //true
stack.push(1);
stack.push(5);
console.log(stack.size());      //2
console.log(stack.peek());      //5
console.log(stack.pop());       //5
stack.clear();
console.log(stack.isEmpty());   //true
```
###2.2 栈的应用
```js
//1、用于进制换算
function baseConverter(number){
    let stack  = new Stack();
    while(number){
        stack.push(number % 2);
        number = Math.floor(number/2);
    }
    let baseString = "";
    while( !stack.isEmpty() ){
        baseString += stack.pop();
    }
    return baseString;
}
console.log(baseConverter(8));   //1000

//2、用于判断字符串是否是回文字符串
function isPalindrome(word){
    let stack = new Stack();
    for(let i=0,len=word.length; i<len; i++){
        stack.push(word[i]);
    }
    let newword="";
    while(stack.size() !== 0){
        newword += stack.pop();
    }
    if(newword == word){
        return true;
    }else{
        return false;
    }
}
console.log(isPalindrome("abdcse"));    //false
console.log(isPalindrome("abccba"));    //true

//3、使用栈模拟递归过程
//阶乘递归实现
function factorial(n){
    if(n === 0){
        return 1;
    }else{
        return n*factorial(n-1);
    }
}
console.log(factorial(4));      //24
//栈实现递归
function stackFactorial(n){
    let stack  = new Stack();
    while(n){
        stack.push(n--);
    }
    let res = 1;
    while(stack.size() !== 0){
        res *= stack.pop();
    }
    return res;
}
console.log(stackFactorial(4));     //24
```
##3.队列

队列是遵循先进先出的一组有序的项，队列在尾部添加新的元素，并从顶部移除元素

###3.1创建队列

创建一个类来表示队列，使用数组用于村粗队列中的元素，然后为队列声明以下方法：（与栈结构非常类似）
* enquene(element(s)):向队列尾部添加一个或者多个新的项；
* dequene()):移除队列的第一项（排在最前面的项），并返回被移除的元素；
* front:返回队列第一个元素，队列无变动；
* isEmpty:队列是否为空，返回true or false；
* clear:清空队列；
* size:返回队列包含元素个数；
实现代码如下：
```js
function Quene(){
    let item = [];
    this.enquene = fucntion(element){
        item.push(element);
    }
    this.dequene = fucntion(){
        return item.shift();
    }
    this.front = fucntion(){
        return item[0];
    }
    this.isEmpty = function(){
        return item.length === 0;
    }
    this.clear = function(){
        item = [];
    }
    this.size = function(){
        return item.length;
    }
}
//使用队列
let quene = new Quene();
console.log(quene.isEmpty());    //true
quene.enquene(1);
quene.enquene(5);
console.log(quene.size());      //2
console.log(quene.front());     //1
console.log(quene.dequene());   //1
quene.clear();
console.log(quene.isEmpty());   //true
```
###3.2队列的改进版

```js
//1、优先队列（额外创建一个特殊元素，他包含了要添加到队列的元素及其优先级）
//元素的添加和移除是基于优先级的,对于优先级相同的元素，依旧遵循先进先出的原则
function PriorityQuene(){
 let items = [];
    function QueneElement(element, priority){
        this.element = element;
        this.priority = priority;
    }
    this.enquene = function(element, priority){
        let queneElement = new QueneElement(element, priority);
        //队列为空时，元素直接放置；不为空时，先比较优先级
        if(this.isEmpty()){
            items.push(queneElement);
        }else{
            let added = false;
            for(let i=0; i<items.length; i++){
                if(queneElement.priority < items[i].priority){
                    items.splice(i, 0, queneElement); //将元素插入下标为i的位置
                    added = true;
                    break;
                }   
            }
            if(!added){
                items.push(queneElement);
            }
        }
    };
    //其他方法
}

//2、循环队列 (击鼓传花游戏)
//孩子们围成一个圈，把花尽快传给旁边的人，某一刻传花停止，花在谁手里，谁就淘汰，知道最后只剩一个孩子,返回这个孩子
function hotPotato(nameList,num){
    let quene = new Quene();
    for(let i=0; i<nameList.length; i++){
        quene.enquene(nameList[i]);
    }
    while(quene.size() > 1){
        for(let j=0; j<num; j++){
            quene.enquene(quene.dequene());
        }
        quene.dequene();
    }
    return quene.dequene();
}
var names = ['John','Jack','Camila','Ingrid','Carl'];
var winner = hotPotato(names, 7);
console.log('胜利者：' + winner);      //胜利者：John
```

##4.链表

要存储多个元素，数组可能是最常见的数据结构。数组查询数据方便,但是在数组中插入移除元素成本太高，因为需要移动元素。

链表是存储有序元素的集合，但不同于数组，链表中的元素在内存中并不是连续放置的，每个元素由一个存储元素本身的节点和一个指向下一个元素

的引用（亦称之为指正或者链接）组成。相对于传统的数组，链表的一个好处在于，添加或者移除元素的时候不需要移动其他的元素。但是数组

可以直接访问任何位置的元素，而想要访问链表中的某个元素，需要从起点（表头）开始迭代列表直到找到所需要的元素。


###4.1单向链表

下图展示一个单向链表的结构：

![链表](https://img-blog.csdn.net/2018080722563439?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIwOTAxMzk3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**单向链表实现代码：**

```js
function Node(element){//node类表示要加入链表的项
    this.element = element;//要添加到列表的值
    this.next = null;//指向下一个节点的指针
}

function LinkedList(){
    let length = 0;
    let head = null;
    //链表方法
    this.append = append;//向链表尾部添加元素
    this.insert = insert;//向指定位置添加元素
    this.remove = remove;//移除元素
    this.removeAt = removeAt;//移除指定位置元素
    this.indexOf = indexOf;//返回元素在链表中的位置，没有返回-1
    this.isEmpty = isEmpty;//判断链表是否为空
    this.size = size;//返回链表的长度
    this.toString = toString;//由于链表使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值
    this.getHead = getHead;//获取表头
}
//List 的验证:
let list = new LinkedList();
list.append(15);
list.append(10);
list.insert(1,44);
console.log(list.size());   //3
list.removeAt(1);
list.remove(10);
console.log(list.size());    //1
console.log(list.indexOf(15));  //0
list.removeAt(0);
console.log(list.isEmpty());    //true

//1.向链表尾部添加元素
function append(element){
    let node = new Node(element);
    let current;
    if(this.head === null){
        this.head = node;
    }else{
        current = this.head;
        while(current.text){
            current = current.text;//循环到最后一个元素
        }
        current.next = node;//将新节点赋值给最后一个元素的next指针，建立连接
    }
    length++;//更新链表长度
}

//2.向特定位置插入元素
function insert(position,element){
    //检查越界值
    if(position<0 || position>length){
        return false;
    }
     let node = new Node(element);
    let current = this.head, index = 0, previous;
    if(position == 0){  
        //在第一个位置添加
        node.next = current;
        this.head = node;
    }else{
        while((index++)<position){
            previous = current;
            current = current.next;
        }
        node.next = current;
        previous.next = node;
    }
    length++;
    return true;
}

//3.移除元素，根据元素的值移除元素
function removeAt(position){
    if(position<0 || position>length){
        return null;
    }
    let current = this.head;
    let previous,index = 0;
    if(position === 0){
        this.head = current.next;
    }else{
        while((index++)<position){
            previous = current;
            current = current.next;
        }
        previous.next = current.next;
    }
    length--;
    return current.element;//返回被删除的元素
}

//4、toString方法，会把LinkedList对象转换成一个字符串
function toString(){
    let current = this.head;
    let str = '';
    while(current){
        str += current.element;
        current = current.next;
    }
    return str;
}
//5.indexof方法
function indexOf(){
 let current = this.head;
    let index = 0;
    while(current){
        if(current.element == element){
            return index;
        }
        current = current.next;
        index++;
    }
    return -1;
}

//6、remove方法（可以依靠indexOf方法和removeAt方法实现）
function remove(element){
    let index = this.indexOf(element);
    return this.removeAt(index);
}

//7、isEmpty方法（链表的length是内部控制的，因为LinkedList是从头构建的）
function isEmpty(){
    return length === 0;
}
//8、size方法
function size(){
    return length;
}
//9、getHead方法
//因为head变量是LinkedList类的私有变量（这意味着它不能在LinkedList实例外部被访问和更改，只有通过linkedList实例才可以）。
//但是，如果我们需要在类的外部循环访问列表，就需要提供一种获取类的第一个元素的方法。
function getHead(){
    return this.head;
}
```
###4.2 双向链表

双向链表与单向链表的区别在于，在单向链表中，一个节点只有链向下一个节点的链接，而在双向链表中，链接是双向的：一个链向下一个元素，另一个链向前一个元素。如下图所示： 

![双向链表](https://img-blog.csdn.net/20180808100516290?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIwOTAxMzk3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

**双向链表代码实现：**

```js
function Node(element){
    this.element = element;
    this.next = null;
    this.prev = null;
}
function DoublyLinkedList(){
    let length = 0;
    let head = null;
    let tail = null;  //新增的，保存对列表最后一项的引用
    //方法
    this.append = append;  //向链表尾部添加元素
    this.insert = insert;  //向链表特定位置插入元素
    this.remove = remove;  //移除元素
    this.removeAt = removeAt ;  //移除特定位置的元素
    this.indexOf = indexOf;  //返回元素在链表中的索引。没有该元素则返回-1。
    this.isEmpty = isEmpty;   //判断链表是否为空
    this.size = size;  //返回链表包含元素个数
    this.toString = toString;   //由于链表项使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值。
    this.getHead = getHead;  //获取表头
}
//DoublyLinkedList的验证
let list = new DoublyLinkedList();
list.append(15);
list.append(10);
list.insert(1,44);
console.log(list.size());   //3
list.removeAt(1);
list.remove(10);
console.log(list.size());    //1
console.log(list.indexOf(15));  //0
list.removeAt(0);
console.log(list.isEmpty());    //true

//1、向链表尾部添加元素
function append(element){
    let node = new Node(element);
    let current;
    if(this.head == null){   //空链表,只需要把head和tail都指向这个新节点
        this.head = node;
        this.tail = node;
    }else{
        current = this.tail;  //获取最后一项
        current.next = node;  //将新节点赋给最后一个元素的next指针，建立连接
        node.prev = current;  //还有前驱节点
        this.tail = node;  //更新对最后一个节点的引用   
    }
    length++;   //更新链表长度
}

//2、向链表特定位置插入元素
function insert(position, element){
    //检查越界值
    if(position < 0 || position > length){
        return false;
    }
    let node = new Node(element);
    let current = this.head, index = 0, previous;
    if(position == 0){  //在第一个位置添加
        if(!this.head){   //空列表情况
            this.head = node;
            this.tail = node;   
        }else{
            node.next = current;
            current.prev = node;
            this.head = node;
        }
    }else if(position == length){
        current = this.tail;
        current.next = node;
        node.prev = current;
        this.tail = node;   
    }else{
        while((index++) < position){
            previous = current;
            current = current.next;
        }
        node.next = current;
        current.prev = node;
        previous.next = node;
        node.prev = previous;
    }
    length++;
    return true;
}

//3、移除元素，第一种是根据元素的值移除元素；第二种是从特定位置移除一个元素，现在我们看看第一种。第二种移除方法见于indexOf方法之后。
function removeAt(position){
    if(position < 0 || position >= length){
        return null;
    }
    let current = this.head;
    let previous, index = 0;
    if(position === 0){   //删除第一个
        this.head = current.next;
        if(length === 1){
            this.tail = null;
        }else{
            this.head.prev = null;
        }
    }else if(position === length-1){      //删除最后一个
        current = this.tail;
        previous = current.prev;
        previous.next = null;
        this.tail = previous;
    }else{
        while((index++) < position){
            previous = current;
            current = current.next;
        }
        previous.next = current.next;
        current.next.prev = previous;
    }
    length--;
    return current.element;   //返回被删除元素的值
}

//4、toString方法，会把LinkedList对象转换成一个字符串
function toString(){
    let current = this.head;
    let str = '';
    while(current){
        str += current.element;
        current = current.next;
    }
    return str;
}

//5、indexOf方法
function indexOf(element){
    let current = this.head;
    let index = 0;
    while(current){
        if(current.element == element){
            return index;
        }
        current = current.next;
        index++;
    }
    return -1;
}
//6、remove方法（可以依靠indexOf方法和removeAt方法实现）
function remove(element){
    let index = this.indexOf(element);
    return this.removeAt(index);
}

//7、isEmpty方法
function isEmpty(){
    return length === 0;
}
//8、size方法
function size(){
    return length;
}
//9、getHead方法
function getHead(){
    return this.head;
}
```

###4.3 循环链表 

循环链表可以像单向链表一样，只有单向引用，也可以像双向链表一样有双向引用。循环链表和链表之间唯一的区别在于，最后一个元素指向下一个元素的指针不是引用null，而是指向第一个元素。如下图所示： 

![循环链表](https://img-blog.csdn.net/20180808110011990?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIwOTAxMzk3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![循环链表2](https://img-blog.csdn.net/20180808110020948?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIwOTAxMzk3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

循环链表方法与单向链表、双向链表类似。

##5. 集合

集合是由一组无序且唯一的项组成。这项数据结构使用了有限集合的数学概念。没有元素的集合是空集。

###5.1 创建集合: (实现Set类)

```js

function Set(){
    let items = {};//创建一个空对象，也可以是数组，不过javascript对象不允许一个键指向两个不同的属性，保证了集合里的元素都是唯一的
    //方法
    //1.has方法，如果在集合中返回true，否则返回false
    //hasOwnProperty：只会检测实例属性，如果使用（value in item），就会检测原型属性加上实例属性
    this.has = fucntion(value){
        return items.hasOwnProperty(value);
    }
    //2.add方法，向集合添加一个新的项
    this.add = function(){
        if(!this.has(value)){
            items[value] = value;//将值存为键名，方便于查找
            return true;
        }
        return false;//添加重复成员返回false
    }
    //3.remove方法,从集合中移除一个元素
    this.remove = function(){
        if(this.has(value)){
            delete items[value];
            return true;
        }
        return false;
    }
    //4.clear方法，移除集合中所有元素
    this.clear = function(){
        items = {};
    }
    //5.size方法,返回集合中有多少元素
    this.size = function(){
        let count = 0;
        for(let prop in items){
            if(items.hasOwnProperty(prop)){
                count++;
            }
        }
        return count;
    }
    //6.values方法，遍历items的所有属性，把他们添加到一个数组并返回
    this.values = function(){
        let keys = [];
        for(let key in items){
            keys.push(key)
        }
        return keys;
    }
}
//使用Set类
let set = new Set();
set.add(1);
console.log(set.values()); //输出["1"]
console.log(set.has(1)); //输出true
console.log(set.size()); //输出1
set.add(2);
console.log(set.values()); //输出["1", "2"]
console.log(set.has(2)); //true
console.log(set.size()); //2
set.remove(1);
console.log(set.values()); //输出["2"]
set.remove(2);
console.log(set.values()); //输出[]
```

###5.2 集合操作： 
对集合可以进行如下操作： 
* 并集：对于给定的两个集合，返回一个包含两个集合中所有元素的新集合。 
* 交集：对于给定的两个集合，返回一个包含两个集合中共有元素的新集合。 
* 差集：对于给定的两个集合，返回一个包含所有存在于第一个集合且不存在于第二个集 
合的元素的新集合。 
* 子集：验证一个给定集合是否是另一集合的子集。

各方法代码实现如下：
```js
//并集方法：union
this.union = function(otherSet){
    let unionSet = new Set();   //用于存放并集中的值
    let values = this.values();
    for(let i=0; i<values.length; i++){
        unionSet.add(values[i]);
    }
    values = otherSet.values();
    for(let i=0; i<values.length; i++){
        unionSet.add(values[i]);   //add函数会去重
    }
    return unionSet;
};

//交集方法：intersection
this.intersection = function(otherSet){
    let intersection = new Set();
    let values = this.values();
    for(let i=0; i<values.length; i++){
        if( otherSet.has(values[i]) ){
            intersection.add(values[i]);
        }
    }
    return intersection;
};

//差集方法：difference
this.difference = function(otherSet){
    let differenceSet = new Set();
    let values = this.values();
    for(let i=0; i<values.length; i++){
        if( !otherSet.has(values[i]) ){
            differenceSet.add(values[i]);
        }
    }
    return differenceSet;
};

//子集方法：subset
this.subset = function(otherSet){
    if(this.size() > otherSet.size()){
        return false;
    }
    let values = this.values();
    for(let i=0; i<values.length; i++){
        if( !otherSet.has(values[i]) ){
            return false;
        }
    }
    return true;
};

//将各函数置于Set函数中，测试下列代码：
let setA = new Set();
setA.add(1);
setA.add(2);
setA.add(3);
let setB = new Set();
setB.add(3);
setB.add(4);
setB.add(5);
let unionAB = setA.union(setB);
console.log(unionAB.values());    //["1", "2", "3", "4", "5"]
let intersectionAB = setA.intersection(setB);
console.log(intersectionAB .values());    //["3"]
let differenceAB = setA.difference(setB);
console.log(differenceAB.values());    //["1", "2"]
let setC = new Set();
setC.add(1);
console.log(setA.subset(setB));    //false
console.log(setC.subset(setA));    //true
```