[toc]
# 6 GUI(图形用户界面)
## 6.1 图形界面概述
1. GUI 图形用户界面：Graphical User Interface（图形用户接口）</br>
2. CUL 命令行界面：Command line User Interface（命令行用户接口）</br>
如：Dos命令行操作。

Java为GUI提供的对象都存在java.awt 和 java.swing 两个包中。
（Java做图形化界面相对较少，得先装虚拟机。一般用C++/等，Windows内置了C++的解析器。

Awt和Swing
1. java.awt :  Abstract Window ToolKit(抽象窗口工具包)，需要调用本地系统方法实现功能。属于重量级控件。
2. javax.swing : 在AWT的基础上，建立一套图形界面系统，其中提供了更多的组件，而且完全由Java实现，增强了移植性，属于轻量级控件。

## 6.2 布局管理器
容器中的组件的排放方式，就是布局</br>
常见的布局管理器：</br>
FlowLayout (流式布局管理器)
1. 从左到右的顺序排列。
2. Panel默认的布局管理器。</br>
默认居中
BorderLayout(边界布局管理器)
1. 东，南，西，北
2. Frame默认的布局管理器</br>
GridLayout(网络布局管理器)
1. 规则的矩阵
GardLayout(卡片布局管理器)
1. 选项卡
GridBagLayout(网络包布局管理器)
1. 非规则的矩阵

创建图形化界面的步骤：
1. 创建frame窗体
2. 对窗体进行基本设置。比如大小，位置，布局
3. 定义组件
4. 将组件通过窗体的add方法添加到窗体中。
5. 让窗体显示，通过setVisible(true)
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;

public class AwtDemo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Frame f=new Frame("my awt");
		f.setSize(500, 100);//宽高
		f.setLocation(300, 200);//位置
		
		f.setLayout(new FlowLayout());//设置流式布局
		
		Button b=new Button("我是一个按钮");//系统默认有一个边界式布局，没有指定东南西北中，所以会出现居中填充,按钮超级大
		f.add(b);
		
		
		f.setVisible(true);//显示窗口
	}

}

```
## 6.3 事件监听器
1. 事件源(组件)
2. 事件(Event)
3. 监听器(Listener)
4. 事件处理(引发事件后处理方式)

事件源：就是awt包或者swing包中的那些图形界面组件

事件：每一个事件源都有自己特有的对应事件和 共性事件

监听器：将可以触发某一个事件的动作都已经封装到了监听器中。

以上三者，在Java中都已经定义好了</br>
直接获取其对象来用就可以了。

我们要做的事情是，就是对产生的动作进行处理

## 6.4 窗体事件
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class AwtDemo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Frame f=new Frame("my awt");
		f.setSize(500, 100);//宽高
		f.setLocation(300, 200);//位置
		
		f.setLayout(new FlowLayout());//设置流式布局
		
		Button b=new Button("我是一个按钮");//系统默认有一个边界式布局，没有指定东南西北中，所以会出现居中填充,按钮超级大
		f.add(b);
		
		//f.addWindowListener(new MyWin());//方法一
		f.addWindowListener(new WindowAdapter() {
			public void windowClosing(WindowEvent e) {
				//System.out.println("Window closing"+e.toString());
				System.out.println("我关");
				System.exit(0);
			}

			@Override
			public void windowActivated(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowActivated(arg0);
				System.out.println("active");
			}

			@Override
			public void windowOpened(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowOpened(arg0);
				System.out.println("我被打开了");
			}
			
		});
		
		f.setVisible(true);//显示窗口
	}
}
/*class MyWin implements WindowListener
{
	//覆盖7个方法，可以我只用到了关闭的动作
	//其他动作都没用到，可是却必须复写
	
	
}*/

//因为WindowListener的子类WindowAdapter已经实现了WindowLisnter接口
//并覆盖了其中所有的方法。那么我只要继承WindowAdapter覆盖我需要的方法即可。
//方法一
class MyWin extends WindowAdapter
{
	public void windowClosing(WindowEvent e) {
		//System.out.println("Window closing"+e.toString());
		System.exit(0);
	}
}
```
## 6.5 Action事件
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class FrameDemo01 {
	//定义该图形中所需的组件的引用
	private Frame f;
	private Button but;
	
	FrameDemo01()
	{
		init();
	}
	
	public void init()
	{
		f=new Frame("my frame");
		
		//对frame进行基本设置
		f.setBounds(300, 100, 600, 500);
		f.setLayout(new FlowLayout());
		
		but=new Button("my button");
		
		//将组件添加到frame中
		f.add(but);
		
		//加载一下窗体上的事件
		myEvent();
		
		//显示窗体
		f.setVisible(true);
		
	}
	private void myEvent() {
		f.addWindowListener(new WindowAdapter() {
			public void windowClosing(WindowEvent e) {
				System.exit(0);
			}
		});
		
		//让按钮具备退出程序的功能
		/*
		 * 按钮就是事件源
		 * button的描述中，有支持一个特有的监听addActionListener
		 */
		but.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				System.out.println("退出，按钮干的");
				System.exit(0);
			}
		});
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new FrameDemo01();
	}

}

```
## 6.6 鼠标事件
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class Demo01 {
	    private Frame f;
		private Button but;
		Demo01(){
			init();
		}
		public void init(){
			f=new Frame("my frame");
			f.setBounds(300, 100, 600, 500);
			f.setLayout(new FlowLayout());
			but=new Button("my button");
			f.add(but);
			myEvent();
			f.setVisible(true);
		}
		
		private void myEvent() {
			f.addWindowListener(new WindowAdapter() {
				public void windowClosing(WindowEvent e) {
					System.exit(0);
				}
			});
			
			but.addActionListener(new ActionListener() {

				@Override
				public void actionPerformed(ActionEvent arg0) {
					// TODO Auto-generated method stub
					System.out.println("action ok");   //注意：鼠标和键盘都可以触动按钮
				}			                           //若用鼠标，先是mouseClicked
			});
			
			but.addMouseListener(new MouseAdapter() {
				private int count=1;
				private int clickCount=1;
				public void mouseEntered(MouseEvent w) {
					System.out.println("鼠标进入该组件"+(count++));
				}
				@Override
				public void mouseClicked(MouseEvent e) {
					// TODO Auto-generated method stub
					super.mouseClicked(e);
					
					if(e.getClickCount()==2)
					System.out.println("双击动作"+count++);
				}
				
			});
		}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new Demo01();
	}

}

```
## 6.6 键盘事件
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.TextField;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class Demo01 {
	    private Frame f;
		private Button but;
		private TextField tf;
		Demo01(){
			init();
		}
		public void init(){
			f=new Frame("my frame");
			f.setBounds(300, 100, 600, 500);
			f.setLayout(new FlowLayout());
			
			//设置文本框
			tf=new TextField(20);//指定列数
			
			
			but=new Button("my button");
			
			f.add(tf);
			f.add(but);
			myEvent();
			f.setVisible(true);
		}
		
		private void myEvent() {
			f.addWindowListener(new WindowAdapter() {
				public void windowClosing(WindowEvent e) {
					System.exit(0);
				}
			});
			
			//给文本框添加键盘监听
			tf.addKeyListener(new KeyAdapter() {
				public void keyPressed(KeyEvent e) {
					
					int code=e.getKeyChar();
					if(!(code>=KeyEvent.VK_0&&code<=KeyEvent.VK_9)) {
						System.out.println(code+".....是非法的");
						e.consume();//不按照默认的，不输出
					}
				}
			})
			
			
			
			but.addActionListener(new ActionListener() {

				@Override
				public void actionPerformed(ActionEvent arg0) {
					// TODO Auto-generated method stub
					System.out.println("action ok");   //注意：鼠标和键盘都可以触动按钮
				}			                           //若用鼠标，先是mouseClicked
			});
			
			but.addMouseListener(new MouseAdapter() {
				private int count=1;
				private int clickCount=1;
				public void mouseEntered(MouseEvent w) {
					System.out.println("鼠标进入该组件"+(count++));
				}
				@Override
				public void mouseClicked(MouseEvent e) {
					// TODO Auto-generated method stub
					super.mouseClicked(e);
					
					if(e.getClickCount()==2)
					System.out.println("双击动作"+count++);
				}
				
			});
			
			//给but添加一个键盘监听器
			but.addKeyListener(new KeyAdapter() {

				@Override
				public void keyPressed(KeyEvent e) {
					// TODO Auto-generated method stub
					super.keyPressed(e);
					//System.out.println(e.getKeyChar()+"........."+e.getKeyCode());
					//打印标准的ASCLL码和键盘码
					
					//System.out.println(KeyEvent.getKeyText(e.getKeyCode())+"........."+e.getKeyCode());
					//打印件键盘名和键盘码
					
					/*if(e.getKeyCode()==27)
					if(e.getKeyCode()==KeyEvent.VK_ESCAPE)//按esc键退出
						System.exit(0);*/
					
					if(e.isControlDown()&&e.getKeyCode()==KeyEvent.VK_ESCAPE)
						System.out.println("ctrl+enter  is  run");//ctrl+enter
				}
				
			});
			
			
		}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new Demo01();
	}

}

```
## 6.7 列出指定目录
```
package GUITest;

import java.awt.Button;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.TextArea;
import java.awt.TextField;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.File;

public class MyWindows {
	private Frame f;
	private TextField tf;
	private Button but;
	private TextArea ta;
	
	MyWindows(){
		init();
	}

	public void init() {
		f=new Frame("my windows");
		f.setBounds(300, 100, 600, 500);
		f.setLayout(new FlowLayout());
		
		tf=new TextField(60);
		but=new Button("转到");
		ta=new TextArea(25,70);
		
		f.add(tf);
		f.add(but);
		f.add(ta);
		
		myEvent();
		f.setVisible(true);
	}
	private void myEvent() {
		but.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent arg0) {
				// TODO Auto-generated method stub
				String dirPath=tf.getText();
				
				File dir=new File(dirPath);
				
				if(dir.exists()&&dir.isDirectory()) {
					String []names=dir.list();
					for(String name:names)
					{
						ta.setText(name+"\r\n");
					}
				}
				/*ta.setText(text);
				//System.out.println(text);*/
				//tf.setText("");//清空
			}
		});
		
		
		f.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowClosing(arg0);
				
				System.exit(0);
			}
		});
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new MyWindows();
	}

}

```
## 6.8 对话框Dialog
```
package GUITest;

import java.awt.Button;
import java.awt.Dialog;
import java.awt.FlowLayout;
import java.awt.Frame;
import java.awt.Label;
import java.awt.TextArea;
import java.awt.TextField;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.File;

public class MyWindows {
	private Frame f;
	private TextField tf;
	private Button but;
	private TextArea ta;
	
	
	private Dialog d;
	private Label lab;
	private Button okBut;
	
	MyWindows(){
		init();
	}

	public void init() {
		f=new Frame("my windows");
		f.setBounds(300, 100, 600, 500);
		f.setLayout(new FlowLayout());
		
		tf=new TextField(60);
		but=new Button("转到");
		ta=new TextArea(25,70);
		
		d=new Dialog(f,"提示信息-self",true);
		d.setBounds(400, 200, 240, 250);
		d.setLayout(new FlowLayout());
		lab=new Label();
		okBut=new Button("确定");
		
		d.add(lab);
		d.add(okBut);
		
		f.add(tf);
		f.add(but);
		f.add(ta);
		
		myEvent();
		f.setVisible(true);
	}
	private void myEvent() {
		okBut.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				d.setVisible(false);
			}
		});
		
		d.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowClosing(arg0);
				
				d.setVisible(false);
			}
		});
		
		tf.addKeyListener(new KeyAdapter() {
			public void keyPressed(KeyEvent e) {
				if(e.getKeyCode()==KeyEvent.VK_ENTER) {
					showDir();
				}
			}
		});
	
		but.addActionListener(new ActionListener() {	
			@Override
			public void actionPerformed(ActionEvent arg0) {
				// TODO Auto-generated method stub
				showDir();
			}
		});
		
		
		f.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowClosing(arg0);
				
				System.exit(0);
			}
		});
	}
	
	private void showDir() {
		String dirPath=tf.getText();
		
		File dir=new File(dirPath);
		
		if(dir.exists()&&dir.isDirectory()) {
			String []names=dir.list();
			for(String name:names)
			{
				ta.setText(name+"\r\n");
			}
		}else {
			String info="您输入的信息："+dirPath+"是错误的，请重输";
			lab.setText(info);
			d.setVisible(true);
		}
		/*ta.setText(text);
		//System.out.println(text);*/
		//tf.setText("");//清空
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new MyWindows();
	}

}

```
## 6.9 打开文件
```
package GUITest;

import java.awt.FileDialog;
import java.awt.Frame;
import java.awt.Menu;
import java.awt.MenuBar;
import java.awt.MenuItem;
import java.awt.TextArea;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class MyMenuDemo {
	private Frame f;
	private TextArea ta;
	private MenuBar bar;
	private Menu fileMenu;
	private MenuItem openItem,saveItem,closeItem;
	
	private FileDialog openDia,saveDia;
	
	MyMenuDemo(){
		init();
	}
	
	public void init() {
		f=new Frame("记事本");
		f.setBounds(300, 100, 650, 500);
		
		bar=new MenuBar();
		ta=new TextArea();

		fileMenu=new Menu("文件");
		
		openItem=new MenuItem("打开");
		saveItem=new MenuItem("保存");
		closeItem=new MenuItem("退出");
		
		fileMenu.add(openItem);
		fileMenu.add(saveItem);
		fileMenu.add(closeItem);

		bar.add(fileMenu);
		
		f.setMenuBar(bar);
		
		
		openDia=new FileDialog(f,"打开",FileDialog.LOAD);//打开
		saveDia=new FileDialog(f,"保存",FileDialog.SAVE);//打开
		
		
		f.add(ta);
		MyEvent();
		f.setVisible(true);
	}
	
	private void MyEvent() {
		openItem.addActionListener(new ActionListener() {
			
			public void actionPerformed(ActionEvent e) {
				openDia.setVisible(true);
				String dirPath=openDia.getDirectory();
				String fileName=openDia.getFile();
				System.out.println(dirPath+"......"+fileName);
				if(dirPath==null||fileName==null)
					return;
				ta.setText("");
				File file=new File(dirPath,fileName);
				try {
					BufferedReader bufr=new BufferedReader(new FileReader(file));
					String line=null;
					
					while((line=bufr.readLine())!=null) {
						ta.append(line+"\r\n");
					}
					bufr.close();
				}catch(IOException e1) {
					throw new RuntimeException("读取失败");
				}
			}
		});
		
		closeItem.addActionListener(new ActionListener() {     //菜单关闭事件

			@Override
			public void actionPerformed(ActionEvent arg0) {
				// TODO Auto-generated method stub
				System.exit(0);
			}
			
		});
		//关闭f窗体
		f.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowClosing(arg0);
				
				System.exit(0);
			}
		});
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new MyMenuDemo();
	}

}

```
## 6.10 保存文件
```
package GUITest;

import java.awt.FileDialog;
import java.awt.Frame;
import java.awt.Menu;
import java.awt.MenuBar;
import java.awt.MenuItem;
import java.awt.TextArea;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class MyMenuDemo {
	private Frame f;
	private TextArea ta;
	private MenuBar bar;
	private Menu fileMenu;
	private MenuItem openItem,saveItem,closeItem;
	private File file;
	
	private FileDialog openDia,saveDia;
	
	MyMenuDemo(){
		init();
	}
	
	public void init() {
		f=new Frame("记事本");
		f.setBounds(300, 100, 650, 500);
		
		bar=new MenuBar();
		ta=new TextArea();

		fileMenu=new Menu("文件");
		
		openItem=new MenuItem("打开");
		saveItem=new MenuItem("保存");
		closeItem=new MenuItem("退出");
		
		fileMenu.add(openItem);
		fileMenu.add(saveItem);
		fileMenu.add(closeItem);

		bar.add(fileMenu);
		
		f.setMenuBar(bar);
		
		
		openDia=new FileDialog(f,"打开",FileDialog.LOAD);//打开
		saveDia=new FileDialog(f,"保存",FileDialog.SAVE);//打开
		
		
		f.add(ta);
		MyEvent();
		f.setVisible(true);
	}
	
	private void MyEvent() {
		saveItem.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent arg0) {
				// TODO Auto-generated method stub
				if(file==null) {
					saveDia.setVisible(true);
					String dirPath=saveDia.getDirectory();
					String fileName=saveDia.getFile();
					if(dirPath==null||fileName==null)
						return;
					file=new File(dirPath,fileName);
				
				}
				try {
					BufferedWriter bufw=new BufferedWriter(new FileWriter(file));
					
					String  text=ta.getText();
					
					bufw.write(text);
					bufw.flush();
					bufw.close();
					
				}catch(IOException e2) {
					throw new RuntimeException();
				}
			}
		});
		
		
		openItem.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				// TODO Auto-generated method stub
				openDia.setVisible(true);
				String dirPath=openDia.getDirectory();
				String fileName=openDia.getFile();
				System.out.println(dirPath+"......"+fileName);
				if(dirPath==null||fileName==null)
					return;
				ta.setText("");
				file=new File(dirPath,fileName);
				try {
					BufferedReader bufr=new BufferedReader(new FileReader(file));
					String line=null;
					
					while((line=bufr.readLine())!=null) {
						ta.append(line+"\r\n");
					}
					bufr.close();
				}catch(IOException e1) {
					throw new RuntimeException("读取失败");
				}
			}
		});
		
		closeItem.addActionListener(new ActionListener() {     //菜单关闭事件

			@Override
			public void actionPerformed(ActionEvent arg0) {
				// TODO Auto-generated method stub
				System.exit(0);
			}
			
		});
		//关闭f窗体
		f.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent arg0) {
				// TODO Auto-generated method stub
				super.windowClosing(arg0);
				
				System.exit(0);
			}
		});
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new MyMenuDemo();
	}

}

```
## 6.11 Jar包双击执行
导包：`javac -d 路径 文件名.java`
创建jar包：先填写一个主函数类，放在1.txt里面</br>
语法：`jar -cvfm my.jar 1.txt`