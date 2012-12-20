  
#java学习笔记

###1.别名机制的演示：

<code>
	public class number
  
{

  	float i;
   	static void f(number j)
	{	
	j.i=3.1f
	}

	public static void main(String[] args)
{

	number n=new number();
 	n.i=1f;
	System.out.println("1:n.i:"+n.i);
	f(n);
	System.out.println("2:n.i:"+n.i);
}

}


//output:
	
	1.n.i:1f
	2:n.i:3.1f
</code>
调用f()方法时，并未在方法的作用域内复制其参数number的一个副本，实际上传递的是一个引用。

###2.==与！=操作符和equals()的使用：
<code>

class dog{

	String name;
	dog(String s){name=s;}
	
}


	public class equaltion
{

	public static void main(String[] args)
  {

	Integer n1=new Integer(5);
	Integer n2=new Integer(5);
	System.out.println(n1==n2); 
	System.out.println(n1!=n2);  
	System.out.println("n1.equals(n2)");  

	Dog d1=new Dog("jack");
	Dog d2=new Dog("jack");
	System.out.println(d1.equals(d2));

}

}/output:
 
	false
	true
	true
	false

</code>

对于系统中的类，==的默认行为是比较两个对象的引用是否相同，而非对象内容是否相同，如果要比较内容是否相同，应该用equals()方法。（**如果是基本类型int,char等，则可用==，！=直接比较内容。
	**）

对于用户自定义的类，其equals()方法的默认行为是比较引用是否相等，要使其比较内容，需在类中重新覆盖该方法。

###3.抛硬币模拟实验：
<code>
	public class coin{
	
	private static int count=0;
	public static void simulation()
{
	

	Random rand=new Random(47);
	boolean flag=false;
    for(int i=1;i<100;i++)
{   
   
	 flag=rand.nextBoolean();
    if(flag) count++;
}

	System.out.println("抛出正面的次数为："+count);
}
	
	public static void main(String[] args)
{

	simulation();
}

}	 //output:
	55
</code>

利用随机数类Random产生随机boolean型的变量。Random中常用的方法：

<code>
	nextInt(n) 	产生[0.n]的随机整数。
	
nextBoolean()  产生均匀的布尔值

nextLong()  随机long值

nextFlota和nextDouble() 产生[0.0f,1.0f]和[0.0d,1.0d]的随机数值。
</code>

###5.类的初始化
<code>
	public class initlize

{

	char ch;
	String s;
  	int a=5;
  	float t=1.0f;
	initlize(float t){this.t=t;}
  	 public void print()
 {

	System.out.println("ch="+ch);
    System.out.println("s="+s);
	System.out.println("a="+a);	
	System.out.println("t="+t);
}
	public static void main(String[] args)
{

	initlize  init=new initlize(5.0f);
    init.print();
}

}
</code>
//结果:

	ch=0
	s=null
	a=5
	t=5.0
初始化顺序：默认初始化，指定初始化，构造器初始化。
    

###枚举类型enum
<code>
	 enum Day

{ Monday,Tuesday,Wednesday,Thursday,Friday }

	public class Workday

{
	
	static Day day=Day.Monday;
 	public static void main(String[] args)
{
	
	System.out.println(day);
}

}
//结果：Monday

enum 关键字用于产生枚举类型。
	




