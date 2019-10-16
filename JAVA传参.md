**JAVA程序设计语言总是按值调用**
***
例如，JAVA方法中有两类方法参数
  * 基本数据类型
  * 对象引用<br>
***
* 对于**基本数据类型**：<br>

有一个方法参数为基本数据类型的方法：
```
public static void add(int x){
  x++;
}
```
调用此方法：
```
int a = 1;
add(a);
```
在此方法中，x被初始化为a值的一个拷贝，然后x值加一，方法结束之后，参数变量x不再使用，而a的值并未发生改变！其原因就是***方法中传进去的并非a变量的地址，而是a值的拷贝***
***
* 对于**对象引用**：<br>
有一个Student类:
```
public class Student{
  private String name;
  ...
  
  public Student(String newname){
    this.name = newname;
  }
  
  public void setname(String str){
    name = str;
  }
}
```
有两个方法参数为对象引用的方法：
```
public static void setempty(Student student){
  student.setname("");
}

public static void exchange(Student student1,Student student2){
  Student temp = student1;
  student1 = student2;
  student2 = temp;
}
```
分别调用以上两个方法：
```
Student xiaoming = new Student("xiaoming");
Student xiaohong = new Student("xiaohong");
setempty(xiaoming);
exchange(xiaoming,xiaohong);
```
结果发现方法setempty实现了自己的作用设置xiaoming名字为空，而方法exchange没有成功交换xiaoming和xiaohong的对象，这是为什么呢？<br>  
首先分析第一个方法，对象引用student被初始化为xiaoming的拷贝（Student student = xiaoming），***setname方法应用于这个对象***，改变了对象的状态，所以即使方法结束，参数student不再使用，但是由于原来的对象的状态已经改变了，所以这个方法就成功改变的了对象引用xiaoming的状态（name成了空字符串）。<br>  
再分析第二个方法，由于第二个方法一样传进去的是对象（Student student1 = xiaoming,Student student2 = xiaohong），所以方法二中的改变只是***让对象引用student1由指向 xiaoming的对象 变成指向 xiaohong的对象 ，而并未使对象引用xiaoming指向xiaohong的对象***，所以方法二没能实现。<br>  
**由于两个方法传进去的都只是对象引用的对象（相当于对象引用的值）而并非其本身，所以也是按值调用并非引用调用！**
***
以上，对于JAVA中方法参数的使用情况总结：
* 一个方法不能修改基本数据类型的参数
* 一个方法可以改变一个对象参数的状态
* 一个方法不能使一个对象参数引用一个新的对象
