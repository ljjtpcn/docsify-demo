## JFrame
?> `JFrame`，窗口。`JFrame` 是一个可以独立显示的组件，一个窗口通常包含有标题、图标、操作按钮(关闭、最小化、最大化)，还可以为窗口添加菜单栏、工具栏等。一个进程中可以创建多个窗口，并可在适当时候进行显示、隐藏 或 销毁。

### 案例
```java
public class MyDemo {
    public static void main(String[] args) {
        // 第一个窗口,构造方法参数为窗口标题
        JFrame frame = new JFrame("第一个窗口");

        //设置标题方法
        frame.setTitle("hello");

        // 当关闭窗口时, 退出整个程序
        frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);

        // 调整窗口大小
        frame.setSize(500, 300);

        //显示窗口
        frame.setVisible(true);
    }
}
```
!> 当创建一个 JFrame 类的实例化对象后，其他组件并不能够直接放到容器上面，需要将组件添加至内容窗格，而不是直接添加至 `JFrame` 对象。示例代码：`frame.setContentPane(panel);`

效果如下:
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112062331106.png)
---

## JPanel and JButton
?> `JPanel` 是一种中间层容器，它能容纳组件并将组件组合在一起，但它本身必须添加到其他容器中使用。</br>`JButton`表示一个按钮控件。



```java
public static void main(String[] args) {

        //创建面板对象
        JPanel panel1 = new JPanel();

        //将面板添加进窗口
        frame.setContentPane(panel1);

        //创建按钮控件并添加进面板panel1
        JButton button1 = new JButton("测试按钮");
        panel1.add(button1);
        
        //显示窗口
        frame.setVisible(true);
    }
```
效果如下:
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112062346998.png)
---


## JLabel
?> 标签控件, 用于显示文本。
```java
public static void main(String[] args) {

        //创建并添加标签文本控件
        root.add(new JLabel("twopair.cn"));

        //显示窗口
        frame.setVisible(true);
    }
```
效果如下:
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112070004443.png)
---


## 监听
动作事件监听器是 `Swing` 中比较常用的事件监听器，很多组件的动作都会使用它监听，像按钮被里击、列表框中选择一项等。与动作事件监听器有关的信息如下。

事件名称：`ActionEvent`。

事件监听接口: `ActionListener`。

事件相关方法：`addActionListener()` 添加监听，`removeActionListener()` 删除监听。

涉及事件源：`JButton`、`JList`、`JTextField` 等。

### 案例1
下面以按钮的单击事件为例来说明动作单击事件监听器的应用。在此案例中当按钮被点击时将显示当前时间。
```java
public class MyFrame extends JFrame {
    JLabel label = new JLabel("点击test刷新");

    public MyFrame(String name) {
        super(name);

        //创建根容器
        JPanel root = new JPanel();
        this.setContentPane(root);

        JButton button = new JButton("test");
        root.add(button);
        root.add(label);
        button.addActionListener((e) -> {
            System.out.println("按钮被点击了!!");
            test();
        });

    }

    private void test() {
        DateFormat dateFormat = new SimpleDateFormat("dd-MM-yy:HH:mm:ss");
        Date date = new Date();
        String dateStr = dateFormat.format(date);
//        System.out.println(dateStr);
        label.setText(dateStr);
    }
}

//测试类
public class MyDemo {
    public static void main(String[] args) {
        JFrame frame = new MyFrame("监听");
        frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
        frame.setSize(500, 300);
        frame.setVisible(true);
    }
```
效果如下:
![](https://hexoljj.oss-cn-shenzhen.aliyuncs.com/img/202112070922959.png)
---

## JTextField
?> 单行文本框。

`Swing` 中使用 `JTextField` 类实现一个单行文本框，它允许用户输入单行的文本信息。该类的常用构造方法如下。
`JTextField()`：创建一个默认的文本框。
`JTextField(String text)`：创建一个指定初始化文本信息的文本框。
`JTextField(int columns)`：创建一个指定列数的文本框。
`JTextField(String text,int columns)`：创建一个既指定初始化文本信息，又指定列数的文本框。