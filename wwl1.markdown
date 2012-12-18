  
#java学习笔记
##  第三章
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

	public static void main()
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




