## Java中静态变量什么时候进行初始化?

所有被标记为静态的内容,会在类刚加载的时候就分配,而不是在对象创建的时候分配,所以说静态内容一定会在第一个对象初始化之前完成加载.

可以通过以下代码进行测试:

```java
public class Person {
    String name = test();  //这里我们用test方法的返回值作为变量的初始值，便于观察
    int age;
    String sex;
    {
        System.out.println("我是普通代码块");
    }

    Person(){
        System.out.println("我是构造方法");
    }

    String test(){
        System.out.println("我是成员变量初始化");
        return "小明";
    }

    static {
        System.out.println("我是静态代码块");
    }
    static String info = init();   //这里我们用init静态方法的返回值作为变量的初始值，便于观察

    static String init(){
        System.out.println("我是静态变量初始化");
        return "test";
    }

    public static void main(String[] args) {
        Person p1 = new Person();
    }
}
```

输出结果为:

```text
我是静态代码块
我是静态变量初始化
我是成员变量初始化
我是普通代码块
我是构造方法

```



可以看出在Java类中的执行顺序: ==静态变量按序初始化->成员变量初始化->普通代码块->构造方法==