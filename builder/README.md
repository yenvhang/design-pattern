## Builder Pattern
  优点:
  > 1. 链式调用写起来很舒服的哇
  > 2. 避免构造方法太多，或者构造参数太多导致调用构造方法时传入错误的参数。
  > 3. 可以对参数强加约束。 如下 Student 的 name属性不能为空。
  > 4. 不使用new对象后再调setter方法，避免了对象被创建好了但成员属性未完全设置好导致的状态不一致。
## example
```java
public class Student {
    //required field
    private String name;

    //optional
    private int sex;
    private String school;
    private int age;
    private String profession;

    private Student(Builder builder){
        this.name =builder.name;
        this.sex=builder.sex;
        this.school=builder.school;
        this.age=builder.age;
        this.profession=builder.profession;
    }

    public String getName() {
        return name;
    }

    public int getSex() {
        return sex;
    }

    public String getSchool() {
        return school;
    }

    public int getAge() {
        return age;
    }

    public String getProfession() {
        return profession;
    }

    public static class Builder{
        //required field
        private String name;

        //optional
        private String school;
        private int age;
        private String profession;
        private int sex;

        public Builder(String name) {
            this.name = name;
        }

        public Builder age(int age){
            this.age=age;
            return this;
        }
        public Builder school(String school){
            this.school=school;
            return this;
        }
        public Builder profession(String profession){
            this.profession=  profession;
            return this;
        }
        private Builder sex(int sex){
            this.sex =sex;
            return this;
        }
        public Student build(){
            return new Student(this);
        }
    }
//for example
    public static void main(String[] args) {
        Student student =new Builder("ye")
                .age(24)
                .sex(0)
                .profession("java developer")
                .school("qdu")
                .build();
        System.out.println(student);
    }
}
```
## 插件推荐
自动生成Builder的插件

<https://plugins.jetbrains.com/plugin/7354-innerbuilder>

![Image text](https://github.com/yenvhang/design-pattern/tree/master/builder/builder.gif)