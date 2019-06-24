# 指针强化，字符串
## 数组元素输出的问题
对于字符可以一次性输出数组中的字符，但是对于数值类型的数组，只能利用for循环逐个输出,原因是字符串后有“\0”结束标识  
```
char a[] = "abcd";       // 定义一个字符类型的数组，并进行初始化
int b[]={2, 3, 4, 1, 9}  // 定义一个int型的数组，并进行初始化;  
int i;
printf("%s", a);         // 一次性输出整个字符数组中的所有字符
for(i=0; i<5; i++)       // 利用for循环对int数组中的数字进行逐个输出
    printf("%d ", b[i]);
```
## 指针易错点
1 写内存时，一定要确保内存可写  
```
char *buf = "fwejiofgh";//文字常量区，内存不可改
buf[2] = '1';//err

char buf2[] = "dehoiefho";//可改
buf[3] = '3';//ok
```
分析上述代码，因为指针buf指向全局区的内存常量区，是不可改的因此会出错，而buf2是将全局区的字符串拷贝到栈区，可以进行修改  
2 指针变量的大小  
即sizeof(指针)在32位系统下占4个字节，在64位系统下占8个字节  
不同类型的指针，例如int，char是指针所指向的内存空间的类型和大小，与指针本身的大小无关  
3 不允许向NULL和非法地址拷贝内存  
```
char *p = NULL;
strcpy(p,"111");//err
```
4 指针可以不断的改变指向  
## 指针存在的最大意义：间接赋值
下列程序，如果想通过形参改变实参的值，必须地址传递  
```
int get1()
{
  a = 10;
  return a；
}

void get2(int a)
{
  a = 22;
}

void get2(int *p)
{
  *p = 33;
}

int main(void)
{
  int b = get1();//输出b为10
  
  get2(b);//输出b依然为10
  
  //如果想通过形参改变实参的值，必须地址传递  
  get3(&b);
  
  return 0;
}
```
