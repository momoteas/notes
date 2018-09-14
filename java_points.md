## Java Points

#### 枚举

* [枚举详解][https://blog.csdn.net/javazejian/article/details/71333103]

* 向Enum类中添加方法与自定义结构函数

  * 重新定义一个日期枚举类，带有desc成员变量描述该日期的对于中文描述，同时定义一个getDesc方法，返回中文描述内容，自定义私有构造函数，在声明枚举实例时传入对应的中文描述，代码如下：

  * ```
    package com.zejian.enumdemo;
    
    /**
     * Created by zejian on 2017/5/8.
     * Blog : http://blog.csdn.net/javazejian [原文地址,请尊重原创]
     */
    public enum Day2 {
        MONDAY("星期一"),
        TUESDAY("星期二"),
        WEDNESDAY("星期三"),
        THURSDAY("星期四"),
        FRIDAY("星期五"),
        SATURDAY("星期六"),
        SUNDAY("星期日");//记住要用分号结束
    
        private String desc;//中文描述
    
        /**
         * 私有构造,防止被外部调用
         * @param desc
         */
        private Day2(String desc){
            this.desc=desc;
        }
    
        /**
         * 定义方法,返回描述,跟常规类的定义没区别
         * @return
         */
        public String getDesc(){
            return desc;
        }
    
        public static void main(String[] args){
            for (Day2 day:Day2.values()) {
                System.out.println("name:"+day.name()+
                        ",desc:"+day.getDesc());
            }
        }
    
        /**
         输出结果:
         name:MONDAY,desc:星期一
         name:TUESDAY,desc:星期二
         name:WEDNESDAY,desc:星期三
         name:THURSDAY,desc:星期四
         name:FRIDAY,desc:星期五
         name:SATURDAY,desc:星期六
         name:SUNDAY,desc:星期日
         */
    }
    ```

  * 从上述代码可知，在enum类中确实可以像定义常规类一样声明变量或者成员方法。但是我们必须注意到，如果打算在enum类中定义方法，务必在声明完枚举实例后使用分号分开，倘若在枚举实例前定义任何方法，编译器都将会报错，无法编译通过，同时即使自定义了构造函数且enum的定义结束，我们也永远无法手动调用构造函数创建枚举实例，毕竟这事只能由编译器执行。