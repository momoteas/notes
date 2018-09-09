









## Object Driven

* starting on: Sept. 9, 2018

----

###  Listener and Call back 

* [java监听器实现与原理][http://www.cnblogs.com/againn/p/9512013.html]

* 监听器，字面上的理解就是监听观察某个事件（程序）的发生情况，当被监听的事件真的发生了的时候，事件发生者（事件源） 就会给注册该事件的监听者（监听器）发送消息，告诉监听者某些信息，同时监听者也可以获得一份事件对象，根据这个对象可以获得相关属性和执行相关操作。

  监听器模型涉及以下三个对象，模型图如下：

  （1）事件：用户对组件的一个操作，或者说程序执行某个方法，称之为一个事件，如机器人程序执行工作。
  （2）事件源：发生事件的组件就是事件源，也就是被监听的对象，如机器人可以工作，可以跳舞，那么就可以把机器人看做是一个事件源。
  （3）事件监听器（处理器）：监听并负责处理事件的方法，如监听机器人工作情况，在机器人工作前后做出相应的动作，或者获取机器人的状态信息。

* ![](https://images2018.cnblogs.com/blog/1118635/201808/1118635-20180821160439733-1857455760.png)

* 执行顺序如下：

  1、给事件源注册监听器。
  2、组件接受外部作用，也就是事件被触发。
  3、组件产生一个相应的事件对象，并把此对象传递给与之关联的事件处理器。
  4、事件处理器启动，并执行相关的代码来处理该事件。

   

  监听器模式：事件源注册监听器之后，当事件源触发事件，监听器就可以回调事件对象的方法；更形象地说，监听者模式是基于：注册-回调的事件/消息通知处理模式，就是被监控者将消息通知给所有监控者。 

  1、注册监听器：事件源.setListener。
  2、回调：事件源实现onListener。

* 下面是一个模仿监听器的demo，需求：实现机器人工作和跳舞，在机器人开始工作和跳舞之前输出相关提示。

  首先创建一个事件源Robot：

  ```
  package com.ssm.listener.robotListener;
  
  /**
   * 事件源：机器人
   */
  public class Robot {
  
      private RobotListener listener;
  
      /**
       * 注册机器人监听器
       * @param listener
       */
      public void registerListener(RobotListener listener){
       this.listener  = listener;
      }
  
      /**
       * 工作
       */
      public void working(){
          if(listener!=null){
              Even even = new Even(this);
              this.listener.working(even);
          }
          System.out.println("机器人开始工作......");
      }
  
      /**
       * 跳舞
       */
      public void dancing(){
          if(listener!=null){
              Even even = new Even(this);
              this.listener.dancing(even);
          }
          System.out.println("机器人开始跳舞......");
      }
  
  
  }
  ```

* 创建时间对象Even：

  ```
  package com.ssm.listener.robotListener;
  
  /**
   * 事件对象
   */
  public class Even {
  
      private Robot robot;
  
      public Even(){
          super();
      }
      public Even(Robot robot){
          super();
          this.robot = robot;
      }
  
  
      public Robot getRobot() {
          return robot;
      }
  
      public void setRobot(Robot robot) {
          this.robot = robot;
      }
  }
  ```

* 创建时间监听器接口RobotListener：

  ```
  package com.ssm.listener.robotListener;
  
  /**
   * 事件监听器
   */
  public interface RobotListener {
  
      public void working(Even even);
      public void dancing(Even even);
  }
  ```

* 实现事件监听器MyRobotListener：

  ```
  package com.ssm.listener.robotListener;
  
  public class MyRobotListener implements  RobotListener{
      @Override
      public void working(Even even) {
          Robot robot = even.getRobot();
          System.out.println("机器人工作提示：请看管好的你机器人，防止它偷懒！");
      }
  
      @Override
      public void dancing(Even even) {
          Robot robot = even.getRobot();
          System.out.println("机器人跳舞提示：机器人跳舞动作优美，请不要走神哦！");
      }
  }
  ```

* 事件监听器测试类

  ```
  package com.ssm.listener.robotListener;
  
  public class TestListener {
  
      public static void main(String[] args) {
          Robot robot = new Robot();
          robot.registerListener(new MyRobotListener());
          robot.working();
          robot.dancing();
      }
  }
  ```



----

