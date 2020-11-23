# Collection(单列)

## List( 有序 可重复)

### ArrayList(数组结构) 查询快 增删慢

​	相对父接口增加针对索引操作的方法：

~~~java

add(T,index)
remove(index)
get(index)
set(T,index)
~~~

### LinkedList(双向链表结构)增删快 查询慢

 ~~~  
Node<E>{
E item;
Node<E> next;
Node<E> prev;
}
 ~~~

## Set(无序 不可重复 )

### HashSet

### TreeSet

##### 排序

泛型实现comparable接口

或创建对象时实例化比较器，重写比较方法

# Map(双列 无序 不可重复)

### HashMap

### TreeMap

# 泛型



