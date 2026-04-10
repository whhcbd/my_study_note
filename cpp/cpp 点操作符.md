# C++ 点操作符（.）完全指南

## 目录

1. [什么是点操作符](#什么是点操作符)
2. [点操作符的基本用法](#点操作符的基本用法)
3. [访问成员变量](#访问成员变量)
4. [访问成员函数](#访问成员函数)
5. [点操作符 vs 箭头操作符](#点操作符-vs-箭头操作符)
6. [嵌套访问](#嵌套访问)
7. [引用中的使用](#引用中的使用)
8. [访问权限控制](#访问权限控制)
9. [常见错误和注意事项](#常见错误和注意事项)
10. [实际应用示例](#实际应用示例)

---

## 什么是点操作符

**点操作符（.）** 是 C++ 中用于访问对象成员的运算符。它就像是打开对象这个"盒子"的钥匙，让你能够看到和操作对象内部的内容。

### 简单理解

想象你有一个"学生"对象，它就像一个档案袋：

- 档案袋里有：姓名、年龄、成绩（这些是成员变量）
- 档案袋上还有操作方法：显示信息、修改成绩（这些是成员函数）

点操作符就是打开档案袋的手，让你能够：

- 看到里面的信息（访问成员变量）
- 使用档案袋上的功能（调用成员函数）

```cpp
student.name        // 查看学生的姓名
student.age         // 查看学生的年龄
student.display()   // 调用显示信息的功能
```

### 为什么叫"点"操作符

因为它在代码中就是一个小圆点 `.`，连接着对象名和成员名，就像一条链子把两者连起来。

---

## 点操作符的基本用法

### 基本语法

```cpp
对象名.成员名
```

### 工作原理

1. **左边**：一个对象（对象变量或引用）
2. **右边**：该对象的成员（成员变量或成员函数）
3. **作用**：访问对象的成员

### 最简单的例子

```cpp
#include <iostream>
#include <string>

int main() {
    std::string text = "Hello";

    std::cout << text.length() << std::endl;  // 访问 string 对象的 length() 函数
    std::cout << text.size() << std::endl;    // 访问 string 对象的 size() 函数

    return 0;
}
```

在这个例子中：

- `text` 是一个 `std::string` 对象
- `.length()` 是访问 `text` 对象的 `length()` 成员函数
- `.size()` 是访问 `text` 对象的 `size()` 成员函数

---

## 访问成员变量

### 什么是成员变量

成员变量是定义在类（或结构体）内部的变量，用来存储对象的数据。

### 定义和访问成员变量

```cpp
#include <iostream>
#include <string>

class Student {
public:
    std::string name;
    int age;
    double score;
};

int main() {
    Student s1;  // 创建一个 Student 对象

    s1.name = "张三";    // 访问并赋值
    s1.age = 20;         // 访问并赋值
    s1.score = 95.5;     // 访问并赋值

    std::cout << "姓名: " << s1.name << std::endl;
    std::cout << "年龄: " << s1.age << std::endl;
    std::cout << "成绩: " << s1.score << std::endl;

    return 0;
}
```

### 使用结构体（struct）

```cpp
#include <iostream>
#include <string>

struct Point {
    double x;
    double y;
};

int main() {
    Point p1;
    p1.x = 3.5;
    p1.y = 4.5;

    std::cout << "坐标: (" << p1.x << ", " << p1.y << ")" << std::endl;

    return 0;
}
```

### 成员变量的类型

成员变量可以是任何类型：

```cpp
class ComplexClass {
public:
    int basicInt;                    // 基本类型
    std::string text;                // 标准库类型
    Point position;                  // 自定义类型
    std::vector<int> numbers;        // 容器类型
    int* pointer;                    // 指针类型
    int array[10];                   // 数组类型
};
```

### 成员变量的初始化

```cpp
class Rectangle {
public:
    int width;
    int height;

    Rectangle(int w, int h) {
        width = w;
        height = h;
    }
};

int main() {
    Rectangle rect(5, 3);

    std::cout << "宽度: " << rect.width << std::endl;
    std::cout << "高度: " << rect.height << std::endl;

    return 0;
}
```

---

## 访问成员函数

### 什么是成员函数

成员函数是定义在类（或结构体）内部的函数，用来操作对象的数据或提供特定功能。

### 定义和调用成员函数

```cpp
#include <iostream>
#include <string>

class Student {
public:
    std::string name;
    int age;
    double score;

    void display() {
        std::cout << "姓名: " << name << std::endl;
        std::cout << "年龄: " << age << std::endl;
        std::cout << "成绩: " << score << std::endl;
    }

    void setScore(double newScore) {
        score = newScore;
    }

    double getScore() {
        return score;
    }
};

int main() {
    Student s1;
    s1.name = "李四";
    s1.age = 21;
    s1.score = 88.0;

    s1.display();              // 调用成员函数
    s1.setScore(92.5);         // 调用成员函数修改成绩
    std::cout << "新成绩: " << s1.getScore() << std::endl;

    return 0;
}
```

### 成员函数的类型

#### 1. 普通成员函数

```cpp
class Calculator {
public:
    int add(int a, int b) {
        return a + b;
    }
};

Calculator calc;
int result = calc.add(3, 5);  // result = 8
```

#### 2. const 成员函数（不修改对象）

```cpp
class Circle {
public:
    double radius;

    Circle(double r) : radius(r) {}

    double getArea() const {  // const 表示不会修改对象
        return 3.14159 * radius * radius;
    }
};

Circle c(5.0);
double area = c.getArea();  // 计算面积，不会修改 c
```

#### 3. 返回引用的成员函数

```cpp
class ArrayWrapper {
private:
    int data[5];

public:
    int& get(int index) {  // 返回引用，可以修改
        return data[index];
    }
};

ArrayWrapper arr;
arr.get(0) = 10;  // 通过返回的引用修改元素
```

### 成员函数可以做什么

成员函数可以：

- 访问和修改成员变量
- 调用其他成员函数
- 执行复杂的逻辑运算
- 返回值或引用

```cpp
class BankAccount {
public:
    double balance;

    BankAccount(double initialBalance) : balance(initialBalance) {}

    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    bool withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }

    void displayInfo() {
        std::cout << "当前余额: " << balance << std::endl;
    }
};

int main() {
    BankAccount account(1000.0);
    account.displayInfo();
    account.deposit(500.0);
    account.displayInfo();
    account.withdraw(200.0);
    account.displayInfo();

    return 0;
}
```

---

## 点操作符 vs 箭头操作符

### 箭头操作符（->）

箭头操作符 `->` 用于通过指针访问对象的成员。

### 关键区别

| 操作符 | 使用场景   | 例子          |
| ------ | ---------- | ------------- |
| `.`    | 对象或引用 | `obj.member`  |
| `->`   | 指针       | `ptr->member` |

### 完整对比示例

```cpp
#include <iostream>
#include <string>

class Person {
public:
    std::string name;
    int age;

    void introduce() {
        std::cout << "我是 " << name << ", 今年 " << age << " 岁" << std::endl;
    }
};

int main() {
    Person p1;        // 对象
    Person* ptr = &p1; // 指向对象的指针

    p1.name = "王五";     // 使用点操作符
    p1.age = 25;
    p1.introduce();      // 使用点操作符

    ptr->name = "赵六";   // 使用箭头操作符
    ptr->age = 30;
    ptr->introduce();    // 使用箭头操作符

    // 等价写法：
    (*ptr).name = "钱七";  // 解引用后使用点操作符
    (*ptr).age = 28;
    (*ptr).introduce();

    return 0;
}
```

### 为什么需要两个操作符？

```cpp
Student s;          // 对象 - 使用 .
Student* ptr = &s;  // 指针 - 使用 ->

s.name = "张三";        // 正确
ptr->name = "李四";     // 正确

// ptr.name = "王五";   // 错误！ptr 是指针，不是对象
// s->name = "赵六";    // 错误！s 是对象，不是指针
```

### 实际应用中的选择

```cpp
#include <iostream>
#include <vector>

class Widget {
public:
    int value;

    Widget(int v) : value(v) {}

    void show() {
        std::cout << "Value: " << value << std::endl;
    }
};

int main() {
    Widget w1(10);
    w1.show();           // 对象，使用 .

    std::vector<Widget*> widgets;
    widgets.push_back(new Widget(20));
    widgets.push_back(new Widget(30));

    for (auto ptr : widgets) {
        ptr->show();     // 指针，使用 ->
    }

    // 清理内存
    for (auto ptr : widgets) {
        delete ptr;
    }

    return 0;
}
```

### 记忆技巧

- 点操作符 `.` 对应对象（像是一个实体的点）
- 箭头操作符 `->` 对应指针（像是指向目标的箭头）

---

## 嵌套访问

### 什么是嵌套访问

当一个对象包含另一个对象作为成员时，需要使用多个点操作符来访问内层对象的成员。

### 基本嵌套示例

```cpp
#include <iostream>
#include <string>

class Address {
public:
    std::string city;
    std::string street;
    int number;

    Address(std::string c, std::string s, int n)
        : city(c), street(s), number(n) {}
};

class Person {
public:
    std::string name;
    Address address;  // Person 包含一个 Address 对象

    Person(std::string n, Address addr) : name(n), address(addr) {}
};

int main() {
    Address addr("北京", "长安街", 100);
    Person person("张三", addr);

    person.name = "李四";
    person.address.city = "上海";      // 嵌套访问
    person.address.street = "南京路";
    person.address.number = 200;

    std::cout << "姓名: " << person.name << std::endl;
    std::cout << "地址: " << person.address.city
              << person.address.street
              << person.address.number << "号" << std::endl;

    return 0;
}
```

### 多层嵌套

```cpp
#include <iostream>
#include <string>

class Color {
public:
    int red;
    int green;
    int blue;

    Color(int r, int g, int b) : red(r), green(g), blue(b) {}
};

class Material {
public:
    std::string type;
    Color color;

    Material(std::string t, Color c) : type(t), color(c) {}
};

class Car {
public:
    std::string brand;
    Material bodyMaterial;

    Car(std::string b, Material m) : brand(b), bodyMaterial(m) {}
};

int main() {
    Color carColor(255, 0, 0);  // 红色
    Material body("金属", carColor);
    Car myCar("特斯拉", body);

    myCar.brand = "比亚迪";
    myCar.bodyMaterial.type = "碳纤维";
    myCar.bodyMaterial.color.red = 0;      // 多层嵌套访问
    myCar.bodyMaterial.color.green = 255;  // 多层嵌套访问
    myCar.bodyMaterial.color.blue = 0;     // 多层嵌套访问

    std::cout << "品牌: " << myCar.brand << std::endl;
    std::cout << "材料: " << myCar.bodyMaterial.type << std::endl;
    std::cout << "颜色: RGB("
              << myCar.bodyMaterial.color.red << ", "
              << myCar.bodyMaterial.color.green << ", "
              << myCar.bodyMaterial.color.blue << ")" << std::endl;

    return 0;
}
```

### 嵌套成员函数调用

```cpp
#include <iostream>
#include <string>

class Engine {
public:
    void start() {
        std::cout << "引擎启动..." << std::endl;
    }

    void stop() {
        std::cout << "引擎停止..." << std::endl;
    }
};

class Car {
public:
    std::string model;
    Engine engine;

    Car(std::string m) : model(m) {}

    void drive() {
        std::cout << model << " 开始行驶..." << std::endl;
    }
};

int main() {
    Car myCar("Model 3");

    myCar.engine.start();   // 嵌套访问成员函数
    myCar.drive();
    myCar.engine.stop();    // 嵌套访问成员函数

    return 0;
}
```

### 嵌套访问的注意事项

1. **链式不能太长**：过长的链式访问影响可读性
2. **检查空指针**：如果中间有指针，需要检查是否为空
3. **访问权限**：确保每个层次的成员都是可访问的

```cpp
// 好的例子 - 清晰的嵌套
student.address.city = "北京";

// 不好的例子 - 过长的链式
company.department.team.leader.address.city = "上海";

// 改进方式 - 分解为多行
auto& leader = company.department.team.leader;
auto& address = leader.address;
address.city = "上海";
```

---

## 引用中的使用

### 引用和点操作符

引用是对象的别名，使用引用时也用点操作符。

```cpp
#include <iostream>
#include <string>

class Student {
public:
    std::string name;
    int age;

    void display() {
        std::cout << name << ", " << age << "岁" << std::endl;
    }
};

void modifyStudent(Student& s) {  // 引用参数
    s.name = "修改后的名字";
    s.age = 22;
}

int main() {
    Student s1;
    s1.name = "原始名字";
    s1.age = 20;

    Student& ref = s1;  // 引用
    ref.name = "通过引用修改";  // 使用点操作符
    ref.age = 21;

    s1.display();

    modifyStudent(s1);  // 传递引用
    s1.display();

    return 0;
}
```

### 函数返回引用

```cpp
#include <iostream>
#include <vector>

class DataContainer {
private:
    std::vector<int> data;

public:
    DataContainer() {
        data = {10, 20, 30, 40, 50};
    }

    int& get(int index) {  // 返回引用
        return data[index];
    }

    const int& get(int index) const {  // const 版本
        return data[index];
    }
};

int main() {
    DataContainer container;

    container.get(0) = 100;  // 通过返回的引用修改
    std::cout << "第一个元素: " << container.get(0) << std::endl;

    const DataContainer& constRef = container;
    std::cout << "第二个元素: " << constRef.get(1) << std::endl;
    // constRef.get(1) = 200;  // 错误！const 引用不能修改

    return 0;
}
```

### 范围 for 循环中的引用

```cpp
#include <iostream>
#include <vector>

class Item {
public:
    int value;

    Item(int v) : value(v) {}

    void doubleValue() {
        value *= 2;
    }
};

int main() {
    std::vector<Item> items = {Item(1), Item(2), Item(3), Item(4)};

    std::cout << "修改前: ";
    for (const auto& item : items) {
        std::cout << item.value << " ";
    }
    std::cout << std::endl;

    for (auto& item : items) {  // 使用引用
        item.doubleValue();     // 调用成员函数
    }

    std::cout << "修改后: ";
    for (const auto& item : items) {
        std::cout << item.value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### this 指针的使用

```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;

public:
    Person(std::string name) {
        this->name = name;  // this-> 相当于 (*this).name
    }

    void setName(std::string name) {
        this->name = name;  // 区分成员变量和参数
    }

    void display() {
        std::cout << "名字: " << this->name << std::endl;
    }

    Person& setNameAndReturn(std::string name) {
        this->name = name;
        return *this;  // 返回对象的引用
    }
};

int main() {
    Person p("张三");
    p.display();

    p.setName("李四");
    p.display();

    p.setNameAndReturn("王五").display();  // 链式调用

    return 0;
}
```

---

## 访问权限控制

### 访问修饰符

C++ 使用访问修饰符来控制对类成员的访问：

- `public`：公开访问，任何地方都可以访问
- `private`：私有访问，只有类内部可以访问
- `protected`：受保护访问，类内部和派生类可以访问

### public 成员

```cpp
#include <iostream>
#include <string>

class PublicClass {
public:
    std::string publicName;  // 公开成员变量

    void publicFunction() {  // 公开成员函数
        std::cout << "这是一个公开函数" << std::endl;
    }
};

int main() {
    PublicClass obj;

    obj.publicName = "可以访问";    // 可以访问
    obj.publicFunction();           // 可以调用

    std::cout << obj.publicName << std::endl;

    return 0;
}
```

### private 成员

```cpp
#include <iostream>
#include <string>

class PrivateClass {
private:
    std::string privateName;  // 私有成员变量

    void privateFunction() {  // 私有成员函数
        std::cout << "这是一个私有函数" << std::endl;
    }

public:
    void setName(std::string name) {
        privateName = name;  // 类内部可以访问私有成员
    }

    void display() {
        std::cout << "名字: " << privateName << std::endl;
        privateFunction();   // 类内部可以调用私有函数
    }
};

int main() {
    PrivateClass obj;

    obj.setName("通过公有函数设置");
    obj.display();

    // obj.privateName = "直接设置";    // 错误！不能直接访问私有成员
    // obj.privateFunction();           // 错误！不能直接调用私有函数

    return 0;
}
```

### protected 成员

```cpp
#include <iostream>
#include <string>

class BaseClass {
protected:
    std::string protectedName;

public:
    BaseClass() : protectedName("基类") {}
};

class DerivedClass : public BaseClass {
public:
    void showProtected() {
        std::cout << "可以访问: " << protectedName << std::endl;
        protectedName = "派生类修改";  // 派生类可以访问 protected 成员
    }
};

int main() {
    DerivedClass derived;
    derived.showProtected();

    BaseClass base;
    // base.protectedName = "尝试修改";  // 错误！外部不能访问 protected 成员

    return 0;
}
```

### 访问控制的最佳实践

```cpp
#include <iostream>
#include <string>

class BankAccount {
private:
    double balance;        // 私有数据，不能直接修改

public:
    BankAccount(double initialBalance) : balance(initialBalance) {}

    double getBalance() const {           // 公开接口
        return balance;
    }

    void deposit(double amount) {         // 公开接口
        if (amount > 0) {
            balance += amount;
        }
    }

    bool withdraw(double amount) {         // 公开接口
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            return true;
        }
        return false;
    }
};

int main() {
    BankAccount account(1000.0);

    std::cout << "余额: " << account.getBalance() << std::endl;
    account.deposit(500.0);
    std::cout << "存款后: " << account.getBalance() << std::endl;

    if (account.withdraw(300.0)) {
        std::cout << "取款成功，余额: " << account.getBalance() << std::endl;
    }

    // account.balance = 999999;  // 错误！不能直接修改私有成员

    return 0;
}
```

---

## 常见错误和注意事项

### 错误 1：对指针使用点操作符

```cpp
Student* ptr = new Student();
ptr.name = "张三";    // 错误！ptr 是指针
ptr->name = "张三";   // 正确！使用箭头操作符
```

### 错误 2：对对象使用箭头操作符

```cpp
Student s;
s->name = "李四";     // 错误！s 是对象
s.name = "李四";      // 正确！使用点操作符
```

### 错误 3：访问不存在的成员

```cpp
Student s;
s.salary = 5000;      // 错误！Student 没有 salary 成员
```

### 错误 4：访问私有成员

```cpp
class PrivateExample {
private:
    int secret;

public:
    PrivateExample() : secret(42) {}
};

int main() {
    PrivateExample obj;
    int x = obj.secret;  // 错误！secret 是私有的
    return 0;
}
```

### 错误 5：空指针访问

```cpp
Student* ptr = nullptr;
ptr->name = "张三";    // 错误！空指针会导致程序崩溃
```

**正确做法：**

```cpp
Student* ptr = nullptr;
if (ptr != nullptr) {   // 检查指针是否为空
    ptr->name = "张三";
}
```

### 错误 6：忘记包含头文件

```cpp
std::string s;          // 错误！没有包含 <string>
s.length();             // 错误！

// 正确：
#include <string>
std::string s;
s.length();             // 正确
```

### 错误 7：链式访问中的空指针

```cpp
class A {
public:
    B* ptrB;
};

class B {
public:
    int value;
};

A* ptrA = nullptr;
ptrA->ptrB->value = 10;  // 错误！ptrA 是空指针

// 正确做法：
if (ptrA != nullptr && ptrA->ptrB != nullptr) {
    ptrA->ptrB->value = 10;
}
```

### 注意事项

1. **类型匹配**：确保成员的类型与你期望的一致
2. **const 正确性**：不要在 const 对象上调用非 const 成员函数
3. **生命周期**：确保对象在使用时仍然有效
4. **初始化**：使用成员前确保已经初始化
5. **可读性**：过长的链式访问影响代码可读性

```cpp
// 良好的代码风格
class Example {
public:
    int getValue() const;
    void setValue(int);
};

Example obj;
int value = obj.getValue();
obj.setValue(42);

// 避免过长的链式访问
obj.getData().getItems().at(0).getValue().getSubValue();
```

---

## 实际应用示例

### 示例 1：学生管理系统

```cpp
#include <iostream>
#include <string>
#include <vector>

class Student {
private:
    std::string name;
    int id;
    double score;

public:
    Student(std::string n, int i, double s)
        : name(n), id(i), score(s) {}

    void display() const {
        std::cout << "学号: " << id
                  << ", 姓名: " << name
                  << ", 成绩: " << score << std::endl;
    }

    void setScore(double newScore) {
        if (newScore >= 0 && newScore <= 100) {
            score = newScore;
        }
    }

    double getScore() const {
        return score;
    }

    std::string getName() const {
        return name;
    }
};

class Course {
private:
    std::string courseName;
    std::vector<Student> students;

public:
    Course(std::string name) : courseName(name) {}

    void addStudent(const Student& student) {
        students.push_back(student);
    }

    void displayAllStudents() const {
        std::cout << "课程: " << courseName << std::endl;
        std::cout << "学生列表:" << std::endl;
        for (const auto& student : students) {
            student.display();
        }
    }

    double calculateAverage() const {
        if (students.empty()) return 0.0;

        double sum = 0;
        for (const auto& student : students) {
            sum += student.getScore();
        }
        return sum / students.size();
    }
};

int main() {
    Course mathCourse("高等数学");

    mathCourse.addStudent(Student("张三", 1001, 85.5));
    mathCourse.addStudent(Student("李四", 1002, 92.0));
    mathCourse.addStudent(Student("王五", 1003, 78.5));

    mathCourse.displayAllStudents();

    std::cout << "平均成绩: " << mathCourse.calculateAverage() << std::endl;

    return 0;
}
```

### 示例 2：游戏角色系统

```cpp
#include <iostream>
#include <string>
#include <vector>

class Weapon {
public:
    std::string name;
    int damage;
    int durability;

    Weapon(std::string n, int d, int dur)
        : name(n), damage(d), durability(dur) {}

    void use() {
        if (durability > 0) {
            durability--;
            std::cout << "使用 " << name << "，造成 " << damage << " 点伤害" << std::endl;
            if (durability == 0) {
                std::cout << name << " 已经损坏！" << std::endl;
            }
        } else {
            std::cout << name << " 已经损坏，无法使用！" << std::endl;
        }
    }

    void repair() {
        durability = 100;
        std::cout << name << " 已修复" << std::endl;
    }
};

class Character {
private:
    std::string name;
    int health;
    int maxHealth;
    Weapon* currentWeapon;

public:
    Character(std::string n, int h, Weapon* weapon = nullptr)
        : name(n), health(h), maxHealth(h), currentWeapon(weapon) {}

    void attack() {
        if (currentWeapon != nullptr) {
            currentWeapon->use();
        } else {
            std::cout << name << " 没有武器，进行徒手攻击！" << std::endl;
        }
    }

    void equipWeapon(Weapon* weapon) {
        currentWeapon = weapon;
        std::cout << name << " 装备了 " << weapon->name << std::endl;
    }

    void takeDamage(int damage) {
        health -= damage;
        if (health < 0) health = 0;
        std::cout << name << " 受到 " << damage << " 点伤害，剩余生命: " << health << std::endl;
        if (health == 0) {
            std::cout << name << " 已经倒下！" << std::endl;
        }
    }

    void heal(int amount) {
        health += amount;
        if (health > maxHealth) health = maxHealth;
        std::cout << name << " 恢复了 " << amount << " 点生命，当前生命: " << health << std::endl;
    }

    void displayStatus() const {
        std::cout << "角色状态: " << name << std::endl;
        std::cout << "生命值: " << health << "/" << maxHealth << std::endl;
        if (currentWeapon != nullptr) {
            std::cout << "当前武器: " << currentWeapon->name
                      << " (伤害: " << currentWeapon->damage
                      << ", 耐久: " << currentWeapon->durability << ")" << std::endl;
        } else {
            std::cout << "当前武器: 无" << std::endl;
        }
    }
};

int main() {
    Weapon sword("长剑", 25, 100);
    Weapon bow("弓箭", 20, 50);

    Character hero("勇者", 100, &sword);
    hero.displayStatus();

    hero.attack();
    hero.attack();
    hero.attack();

    hero.equipWeapon(&bow);
    hero.attack();
    hero.attack();

    hero.takeDamage(30);
    hero.heal(20);

    hero.displayStatus();

    return 0;
}
```

### 示例 3：简单的图形系统

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

const double PI = 3.14159265358979323846;

class Point {
public:
    double x;
    double y;

    Point(double x = 0, double y = 0) : x(x), y(y) {}

    void display() const {
        std::cout << "(" << x << ", " << y << ")";
    }

    double distanceTo(const Point& other) const {
        double dx = x - other.x;
        double dy = y - other.y;
        return std::sqrt(dx * dx + dy * dy);
    }
};

class Shape {
protected:
    Point center;

public:
    Shape(const Point& c) : center(c) {}

    virtual double area() const = 0;
    virtual double perimeter() const = 0;
    virtual void display() const {
        std::cout << "中心: ";
        center.display();
        std::cout << std::endl;
    }

    virtual ~Shape() {}
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(const Point& c, double r) : Shape(c), radius(r) {}

    double area() const override {
        return PI * radius * radius;
    }

    double perimeter() const override {
        return 2 * PI * radius;
    }

    void display() const override {
        std::cout << "圆形 - ";
        Shape::display();
        std::cout << "半径: " << radius << std::endl;
        std::cout << "面积: " << area() << std::endl;
        std::cout << "周长: " << perimeter() << std::endl;
    }
};

class Rectangle : public Shape {
private:
    double width;
    double height;

public:
    Rectangle(const Point& c, double w, double h) : Shape(c), width(w), height(h) {}

    double area() const override {
        return width * height;
    }

    double perimeter() const override {
        return 2 * (width + height);
    }

    void display() const override {
        std::cout << "矩形 - ";
        Shape::display();
        std::cout << "宽度: " << width << ", 高度: " << height << std::endl;
        std::cout << "面积: " << area() << std::endl;
        std::cout << "周长: " << perimeter() << std::endl;
    }
};

class Canvas {
private:
    std::vector<Shape*> shapes;

public:
    void addShape(Shape* shape) {
        shapes.push_back(shape);
    }

    void displayAll() const {
        std::cout << "=== 画布内容 ===" << std::endl;
        for (const auto& shape : shapes) {
            shape->display();
            std::cout << "---" << std::endl;
        }
    }

    ~Canvas() {
        for (auto shape : shapes) {
            delete shape;
        }
    }
};

int main() {
    Canvas canvas;

    canvas.addShape(new Circle(Point(0, 0), 5.0));
    canvas.addShape(new Circle(Point(10, 10), 3.0));
    canvas.addShape(new Rectangle(Point(5, 5), 4.0, 6.0));

    canvas.displayAll();

    return 0;
}
```

### 示例 4：图书管理系统

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <ctime>

class Date {
public:
    int year;
    int month;
    int day;

    Date(int y, int m, int d) : year(y), month(m), day(d) {}

    void display() const {
        std::cout << year << "-" << month << "-" << day;
    }
};

class Book {
private:
    std::string title;
    std::string author;
    std::string isbn;
    bool isAvailable;
    Date publicationDate;

public:
    Book(std::string t, std::string a, std::string i, Date pd)
        : title(t), author(a), isbn(i), isAvailable(true), publicationDate(pd) {}

    void display() const {
        std::cout << "书名: " << title << std::endl;
        std::cout << "作者: " << author << std::endl;
        std::cout << "ISBN: " << isbn << std::endl;
        std::cout << "出版日期: ";
        publicationDate.display();
        std::cout << std::endl;
        std::cout << "状态: " << (isAvailable ? "可借阅" : "已借出") << std::endl;
    }

    bool borrow() {
        if (isAvailable) {
            isAvailable = false;
            return true;
        }
        return false;
    }

    bool returnBook() {
        if (!isAvailable) {
            isAvailable = true;
            return true;
        }
        return false;
    }

    std::string getTitle() const { return title; }
    std::string getIsbn() const { return isbn; }
    bool getAvailability() const { return isAvailable; }
};

class Library {
private:
    std::vector<Book*> books;

public:
    ~Library() {
        for (auto book : books) {
            delete book;
        }
    }

    void addBook(Book* book) {
        books.push_back(book);
        std::cout << "添加书籍: " << book->getTitle() << std::endl;
    }

    Book* findBookByIsbn(const std::string& isbn) {
        for (auto book : books) {
            if (book->getIsbn() == isbn) {
                return book;
            }
        }
        return nullptr;
    }

    void borrowBook(const std::string& isbn) {
        Book* book = findBookByIsbn(isbn);
        if (book != nullptr) {
            if (book->borrow()) {
                std::cout << "成功借阅: " << book->getTitle() << std::endl;
            } else {
                std::cout << "书籍已被借出: " << book->getTitle() << std::endl;
            }
        } else {
            std::cout << "未找到ISBN为 " << isbn << " 的书籍" << std::endl;
        }
    }

    void returnBook(const std::string& isbn) {
        Book* book = findBookByIsbn(isbn);
        if (book != nullptr) {
            if (book->returnBook()) {
                std::cout << "成功归还: " << book->getTitle() << std::endl;
            } else {
                std::cout << "书籍未被借出: " << book->getTitle() << std::endl;
            }
        } else {
            std::cout << "未找到ISBN为 " << isbn << " 的书籍" << std::endl;
        }
    }

    void displayAllBooks() const {
        std::cout << "=== 图书馆藏书 ===" << std::endl;
        for (const auto& book : books) {
            book->display();
            std::cout << "---" << std::endl;
        }
    }

    void displayAvailableBooks() const {
        std::cout << "=== 可借阅书籍 ===" << std::endl;
        for (const auto& book : books) {
            if (book->getAvailability()) {
                book->display();
                std::cout << "---" << std::endl;
            }
        }
    }
};

int main() {
    Library library;

    library.addBook(new Book("C++ Primer", "Stanley B. Lippman", "978-0321714114", Date(2012, 9, 1)));
    library.addBook(new Book("Effective C++", "Scott Meyers", "978-0321334879", Date(2005, 5, 22)));
    library.addBook(new Book("The C++ Programming Language", "Bjarne Stroustrup", "978-0321563842", Date(2013, 5, 19)));

    std::cout << std::endl;
    library.displayAllBooks();

    std::cout << std::endl;
    library.borrowBook("978-0321714114");
    library.borrowBook("978-0321714114");

    std::cout << std::endl;
    library.displayAvailableBooks();

    std::cout << std::endl;
    library.returnBook("978-0321714114");

    std::cout << std::endl;
    library.displayAvailableBooks();

    return 0;
}
```

---

## 总结

点操作符（.）是 C++ 中最基础、最重要的运算符之一，掌握它需要理解：

### 核心概念

1. **基本用法**：`对象.成员` - 访问对象的成员
2. **两种情况**：访问成员变量和调用成员函数
3. **区别**：点操作符用于对象，箭头操作符用于指针

### 实践要点

1. **访问权限**：理解 public、private、protected
2. **嵌套访问**：多层对象的访问链
3. **引用使用**：引用也使用点操作符
4. **错误避免**：常见错误和注意事项

### 应用场景

1. **面向对象编程**：封装、数据和方法
2. **标准库使用**：string、vector 等
3. **实际项目**：学生管理、游戏开发、图形系统等

通过熟练使用点操作符，你可以更好地理解和使用 C++ 的面向对象特性，编写更加清晰、高效的代码。
