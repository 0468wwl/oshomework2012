  
#java学习笔记
##  第三章
1.别名机制的演示：
<code>

public class number
  
{
   float i;
   		 
	static void f(number j){
  
	j.i=3.1f
}

	public static void main(String[] args)

{	number n=new number();
 
	n.i=1f;

	System.out.println("1:n.i:"+n.i);

	f(n);

	System.out.println("2:n.i:"+n.i);
}


//output:


	1.n.i:1f

	2:n.i:3.1f
</code>
调用f()方法时，并未在方法的作用域内复制其参数number的一个副本，实际上传递的是一个引用。



