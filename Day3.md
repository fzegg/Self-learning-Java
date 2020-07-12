

# 数组中涉及的常见算法

## 数组元素的赋值

- #### 杨辉三角

- #### 回行数

## 求数值型数组元素的最值、平均值和总和

## 数组的复制、反转、查找

- #### 数组的复制：

new一次就有一个新数组（不new就不开辟新地址）

```java
array2 = array1;//堆空间只有一个数组，即array2和array1使用同一地址，改动array2时array1随之改变，类比于创建快捷方式，不能称作数组的复制
```

```java
array2 = new int[array1.length];
for(i = 0;i < array2.length;i++){
	array2[i] = array1[i];
} //数组的复制
```

- #### 数组的反转：

```java
//方法一
for(i = 0;i < arr.length / 2;i++){
	String temp = arr[i];//数组元素为字符类型时
	arr[i] = arr[arr.length - i - 1];
	arr[arr.length - i - 1] = temp;
}
//方法二
for(i = 0, j = arr.length - 1;i < j;i++,j--){
	String temp = arr[i];//数组元素为字符类型时
	arr[i] = arr[j];
	arr[j] = temp;
}

```

- #### 数组的查找：

```java
//线性查找
String dest = "test";
boolean isFlag = true；
for(int i = 0;i < arr.length;i++){
    //以字符串类型为例
    if(dest.equals(arr[i])){
        System.out.println("位置为" + i)；
        isFlag = false；
        break；
    }
}
if(isFlag){
    System.out.println("没有找到")；
}

//二分法查找（更迅速）
//所要查找的数组必须有序
int dest1 =-34;
int head = 0;//初始的首索引
int end = arr1.length - 1;//初始的末索引
boolean isFlag1 = true;
while(head <= end){
    int middle = (head + end)/2;
    if(dest == arr1[middle]){
        System.out.println("位置为" + middle);
        isFlag1 = false;
        break;
    }else if(arr1[middle] > dest1){
        end = middle - 1;
    }else{
        head = middle + 1;
    }
if(isFlag1){
System.out.println("没找到")；
}
```
