# for与enhanced-for

Java5 引入了一种主要用于数组的增强型 for 循环。

```java
for(声明语句 : 表达式)
{
   //代码句子
}
```

**声明语句：**声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。

**表达式：**表达式是要访问的数组名，或者是返回值为数组的方法

以遍历数组为例区分for与enhanced-for：

```java
int[] arr = new int[]{0,1,2,3,4,5,6};
//for
for(i = 0;i < arr.length;i++){
    System.out.print(arr[i] + " ");
}
//enhanced-for
for(int x : arr){
    System.out.print(x + " ");
}

```

