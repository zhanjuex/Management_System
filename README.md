# 学生选课信息管理系统管理端

> author: zhanjue
>
> 源代码（vs编译，devc++会报错：auto无法声明） 
>
> 最近更新:2021-10-26
>
> 如果本仓库对您有帮助，希望能给个Star~
>
> 转载请注明来源，谢谢。





* [项目功能](#项目功能)
* [主要模块](#主要模块)
* [类的说明](#类的说明)
* [项目运用课程知识汇总](#项目运用课程知识汇总)
* [项目缺陷](#项目缺陷)






## 一、项目功能：

1. 实现课程信息打印、查询、录入、删除、修改功能。

2. 实现学生信息打印、查询、录入、删除、修改功能。

3. 课程信息、学生信息交互，实现选课管理端根据学生已有学分进行选课。（包括帮助学生选课或删除学生已选课）

4. 管理端系统设置。仿真加密系统，实现密码防护、修改密码、注销功能。其中密码防护功能实现用户多次输入密码错误，系统将进入休眠状态，等待一段时间后用户才能重新输入密码，防止用户恶意登录。

5. 菜单功能选择，保证用户正常使用系统。

6. 各菜单界面交互，提升系统流畅度，用户使用效率及营造良好用户体验环境。
7. vector容器动态储存信息。

 

## 二、主要模块：

1. 课程信息管理

2. 学生信息管理

3. 管理端系统登录保护、修改密码、注销

 


## 三、类的说明：

基类：

（一）信息类

包含：编号（number）、名称（name）、构造函数。

class info//信息类

{

protected:

    long number;//编号
    
    string name;//名称

public:

    info() {}
    
    info(long num, string name) :number(num), name(name) {}

};

派生类：

（二）课程类：（继承编号、名称）

包含：友元类（学生类）、课程学分、授课老师、拷贝构造函数及各种功能实现函数，并创建课程类动态数组。

class course: public info//课程类

{

protected:

    int credit;//学分
    
    string teachername;//授课教师

public:

    course(){}
    
    course(long num, string name, int cre, string tea) : info(num, name)
    
    {
    
       credit = cre;
    
       teachername = tea;
    
    }
    
    static void print();//输出数据
    
    static void get();//获取数据
    
    static void add();//增加数据
    
    static void del();//删除数据
    
    static void edit();//修改数据
    
    static int ishave(long si);//查询是否有该课程
    
    friend class student;

};vector<course> c;

 

（三）学生类：（继承编号、名称）

包含：**课程数组**、性别、年级、本学期需修学分、构造函数、各种功能实现函数、并创建学生类动态数组。

class student: public info//学生类

{

protected:

    string sex;//性别
    
    string grade;//年级
    
    long scredit;//本学期需修学分

public:

    **vector<course> havec;//****查询学生选课信息**
    
    student(){}
    
    student(long num, string name, string se, string gra, long scr) : info(num, name)
    
    {
    
       sex = se;
    
       grade = gra;
    
       scredit = scr;
    
    }
    
    static void print();//输出数据
    
    static void get();//获取数据
    
    static void add();//增加数据
    
    static void del();//删除数据
    
    static void edit();//修改数据
    
    static int ishave(long si);//查询是否有该学生
    
    static void addcourse();// 为学生添加课程
    
    static void delcourse();//为学生删除课程
    
    static int ishavec(long si);//查询该学生是否有该课程

};vector<student> s;

 

## 四、项目运用课程知识汇总

类指针、继承、访问控制、拷贝构造函数、引用、静态成员函数、动态数组（STL容器）、友元类、组合类。

（本来想用虚函数和多态，但是成员函数没必要实例化使用，而静态成员函数和虚函数不能共同使用，就放弃了。）

 

## 五、项目缺陷：

1.  忽略了课程编号可能为001，0002等，应把基类编号改成string型，后面构造函数、功能函数等都需要修改。

2. 查询，删除，修改功能只实现编号操作，没有实现其他关键词操作。
3. 没有实现排序操作。为学生添加选课后，选课信息由时间顺序排列，未实现编号升降序。
4. 系统设计之初未考虑周全，导致某些功能中的循环嵌套有重复（如为学生添加选课信息），增加时间复杂度。即项目还存在较大的优化空间，以便节省系统开销。
5. 系统存在小bug，即某些时候选择退出系统需要选择两次才能退出。
