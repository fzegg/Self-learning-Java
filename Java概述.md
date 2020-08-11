# 语言特点：跨平台性

同一个Java程序在不同操作系统中的不同JVM运行



# 核心机制：Java虚拟机、垃圾收集机制

## Java虚拟机：

- JVM是一个虚拟的计算机
- 不同平台有不同虚拟机，只能在有JVM的平台上运行
- 屏蔽了底层运行平台的差别，**“一次编译，到处运行”**
- 运行过程：用户->字节码文件（Java程序）->JVM->操作系统->硬件

## 垃圾回收：

- C/C++中由程序员回收无用内存

- 垃圾回收在Java程序运行过程中自动进行，程序员无法控制或干预

- 依然会出现**内存泄漏**与**内存溢出**

  

# JVM、JDK、JRE

- #### JDK(Java Development Kit     Java开发工具包)：

提供给开发人员使用，包括了Java开发工具（编译工具javac.exe、打包工具jar.exe等）和JRE

- #### JRE(Java Runtime Enviroment     Java运行环境)

包括JVM和Java程序需要的核心类库（Java SE标准类库），要运行一个开发好的Java程序只需要安装JRE

- #### 使用JDK开发工具完成的Java程序交给JRE运行