  
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

enum 关键字用于产生枚举类型（枚举为整型常量）。



###7.可变参数列表
	class A{}
	public class Varargs {
	public  static void print1(Object... args) {
		for(Object obj:args)
			System.out.println("obj:"+obj);
			System.out.println();
		}
	public static void print2(Object[] args){
		for(Object obj:args)
			System.out.println("obj:"+obj);
			System.out.println();
		}
	
	public static void main(String[] args){
		print1(5,"hello",'A',2.11d,1.1f,new var());
		System.out.println();
		print1(new Object[]{5,'a',"haha",new var()});
		System.out.println();
		print2(new Object[]{10,'b',"xixi",new var()});
		/!print2(5,"hello",'A',2.11d,1.1f,new var());
	
		}
}

	//output:
	obj:5
	obj:hello
	obj:A
	obj:2.11
	obj:1.1
	obj:p1.var@c17164

	obj:5
	obj:a
	obj:haha
	obj:p1.var@1fb8ee3

	obj:10
	obj:b
	obj:xixi
	obj:p1.var@61de33

Object[]可解析为Object类型，但Object[]类型不能被解析为Object类型。

###8."工厂":

###9.向上转型。
<code>

	import static net.mindview.util.Print.*;
    enum Note{ Dou,Ran,Me,Fa,Sou;}

	class Instrument{
	public static void tune(Instrument i)

{
	
	i.play(Note.Ran);
}

	public void play(Note n)
{
	 
	print("Instrument play:"+n);	
}

}
	
	class Brass extends Instrument{

	public void play(Note n){
		print("Brass play:"+n);
	}
}
	
	class Stringed extends Instrument
{

	public static void tune(Stringed s){
		s.play(Note.Sou);
	}
	public  void play(Note n){
		print("Stringed play:"+n);
	}
}
	
	public class music {

    public static void main(String[] args){

	   Instrument horn=new Brass();
	   Instrument voiln=new Stringed();
	   Brass horn2=new Brass();
		/！Stringed horn3=new Brass();	//类型不匹配。
		Stringed voiln2=new Stringed();
       Instrument.tune(horn);
	   Instrument.tune(voiln);
	   Stringed.tune(horn);            //
	   Stringed.tune(horn2);
	   Stringed.tune(voiln2);
   }

}//结果：

	Brass play:Ran
	Stringed play:Ran
	Brass play:Ran
	Brass play:Ran
	Stringed play:Sou
Brass与Stringed继承自Instrument,向上转型为基类Instrument.在实际调用中通过公共接口tune()调用的是导出类中覆盖了的play()方法。将一个方法调用与一个方法主体关联起来叫做绑定，绑定分为前期绑定（编译时期绑定，除static,final和private方法外的所有）和后期绑定（运行时确定）。Imstrument.tune()接口展示了多态。

###10.构造器和多态
	class meal
{  
	
	meal(){
	print("meal()");  }
}
	
	class bread
{
	
	bread(){
	print("bread()");  }
}
	
	class lunch extends meal
{
	
	lunch(){
	print("lunch()");  }
}

	class chess{
		chess(){
			print("chess()");
		}
	}

	
	class goodlunch extends lunch
{

	goodlunch(){
	print("goodlunch()");   }
}

	public class sandwich extends goodlunch
{

	private bread b=new bread();
    private chess c=new chess();
	sandwich(){
	print("sandwich()");   
}


	public static void main(String[] args)
{

	sandwich sw=new sandwich();
}

}//结果：

	meal()
	lunch()
	goodlunch()
	bread()
	chess()
	sandwich()
初始化顺序：基类构造器  导出类数据成员  导出类构造器主体
           

###11.用继承进行设计
####一条通用的原则：用继承表达行为间的差异，用字段表达状态上的变化。
<code>
	
	import static net.mindview.util.Print.*;
	class Status{
	void action(int speed){
		speed=0;
		print(speed);
	}
}

//使用继承实现行为的差异。

	class Boot extends Status{
	void action(int speed){
		speed=speed+20;
		print(speed);
	}
	
}

	class ChangeSpeed extends Status{
	void action(int speed){
		speed=speed-5;
		print(speed);
	}
}

	class  Stop extends Status{
	void action(int speed){
	speed=speed-19;
	print(speed);
	}
}

//使用组合（字段）表达状态上的变化。

	class AlertStatus{

	private Status sta=new Status();
	public void changeboot(){sta=new Boot();}
	public void changespeed(){ sta=new ChangeSpeed();}
	public void changestop(){ sta=new Stop();}
		public  void play(){ sta.action(0);}
	}

	public class Startship {

	public static void main(String[] args) {
		AlertStatus sta=new AlertStatus();
		sta.play();
		sta.changeboot();
		sta.play();
		sta.changespeed();
		sta.play();
		sta.changestop();
		sta.play();
		
	}

}//output

	0
	20
	-5
	-19

###12.完全解耦
如果一个方法操作的是类而非接口，那么只能使用这个类及其子类，此方法不适用与不在此继承结构中的其它类，这样方法的复用性降低，就像下面的Apply.process()一样。

	import java.util.Arrays;
	import static net.mindview.util.Print.*;
	class Processor{
	public String name(){
		return getClass().getSimpleName();
	}
	Object process(Object input){
		return input;
	}
}

	class Upcase extends Processor{
	String process(Object input){
		return ((String)input).toUpperCase();
	}
}
	
	class Splitter extends Processor{
	String process(Object input){
		return Arrays.toString(((String)input).split(" "));
	}
}

	public class Apply {
    public static void process(Processor p,Object s){
    	print("当前调用的类型为："+p.name());
    	print(p.process(s));
    }
    public static String s="hello,java jes5!";
    public static void main(String[] args){
    	process(new Upcase(),s);
    	process(new Splitter(),s);
    	
    }
}//output
	
	当前调用的类型为：Upcase
	HELLO,JAVA JES5!
	当前调用的类型为：Splitter
	[hello,java, jes5!]
Apply.process()使用了策略设计模式（方法根据传递的对象参数不同而具体执行不同的行为）。

如果有不在Process继承结构中的某类Filters：
	
	class wareform{ }
	

	class Filters{
	public String name(){
		return getClass().getSimpleName();
	}
	public wareform process(wareform input){
		return input;
	}
}

	class Highpass extends Filters{
		double cutoff;
		Highpass(double cutoff){this.cutoff=cutoff;}
		public wareform process(wareform input){
		return input;
	}
}

//Apply.process()方法无法适用于Filters类。

如果把Processor设计成接口，让Apply.process()操作接口，并适配Filters类，让它成为Apply.process()所能接受的类型，其代码便可复用，像下面这样；
	
	interface Processor{
	String name();
	Object process(Object input);  //把Processor设计成接口。
}

 	public class FiltersAdapter implements Processor     //适配Filters类。
{           
         
		 Filters filter;
          public FiltersAdapter(Filters filter){      //使用代理。
        	  this.filter=filter;
          }
          public String name(){
        	  return filter.name();
        	  }
          public wareform process(Object input){
        	  return filter.process((wareform)input);
        	  
          }
          public static void main(String[] args){
        	  wareform w=new wareform();
        	  Apply.process(new FiltersAdapter(new Highpass(2.0)), w);   //代码复用。
          }
}

###13.适配接口
知识点：
	
	Scanner类实现了Iterator接口: class Scanner implement Iterator<String> 
	其构造器之一接受的是一个Readable接口：Scanner(Readable resource){}
    Readable接口是专为Scanner而设计的：interface  Readable{Read(CharBuff cb);}
	若想使用Scanner输入自定义的新类，只需要让该类implements Readable接口中的read()方法即可。
	Charbuff为输入源缓冲区，缓冲区空时返回-1.


	import java.nio.*;
	import java.util.*;

	class randsentence implements Readable{

	public static Random rand=new Random(47);
	public static final char[] first="寂拣面做".toCharArray();
	public static final char[] second="寞尽朝个".toCharArray();
	public static final char[] third="沙寒大幸".toCharArray();
	public static final char[] forth="洲枝海福".toCharArray();
	public static final char[] fitth="冷不春勇".toCharArray();
	public static final char[] sixth="冷肯花敢".toCharArray();
	public static final char[] seventh="，栖开的".toCharArray();
	private int count;

	public randsentence(int count){
		this.count=count;
	}
	public int read(CharBuffer cb){
		if(count--==0)  
			return -1;
		//cb.append(first[rand.nextInt(first.length)]);
		
		for(int i=0;i<4;i++){
			cb.append(first[i]);
			cb.append(second[i]);
			cb.append(third[i]);
			cb.append(forth[i]);
			cb.append(fitth[i]);
		   cb.append(sixth[i]);
		   cb.append(seventh[i]);
		  
		}
		
		return 1;
}

}
	
	public class Makepoem {
	
		public static void main(String[] args){
		Scanner s=new Scanner(new randsentence(1));
		
		System.out.println(s.next());
	}
	
	}//output
	寂寞沙洲冷冷，拣尽寒枝不肯栖面朝大海春花开做个幸福勇敢的    //程序有误，待改进。


创建一个类，它可以产生char随机序列，适配这个类，使其成为Scanner一种输入对象。
	
	import java.nio.CharBuffer;
	import java.util.*;

	class RandomChars {
		private static Random rand = new Random();
		public char next() {
		return (char)rand.nextInt(110);       //产生随机char序列。
		}
		public static void main(String[] args) {			
			RandomChars rc = new RandomChars();
		for(int i = 0; i < 10; i++)
				System.out.print(rc.next() + " ");
		}
	 }

//适配类，使其能被Scanner读取。
	
	public class AdapterRandcharSquence extends RandomChars implements Readable
{
	
	private int count;
	public AdapterRandcharSquence(int count){
		this.count = count;
	}			
	public int read(CharBuffer cb)
{

		if(count-- == 0)
			return -1;
		String result = Character.toString(next()) + " ";
		cb.append(result);
		return result.length();
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner s = new Scanner(new AdapterRandcharSquence(10));
		while(s.hasNext())
			System.out.println(s.next() + " ");
	}

}//output

	+ 
	0 
	? 
	+ 
	7 
	P 
	4 
	; 
	4 
	j 


	
	
	

	



	




