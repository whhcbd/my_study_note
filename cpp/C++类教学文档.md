# C++ 类教学文档

## 目录
1. [类的基本概念](#类的基本概念)
2. [类的定义与使用](#类的定义与使用)
3. [构造函数与析构函数](#构造函数与析构函数)
4. [访问控制](#访问控制)
5. [类的成员函数](#类的成员函数)
6. [类模板](#类模板)
7. [类的继承](#类的继承)
8. [多态性](#多态性)
9. [综合示例](#综合示例)

---

## 类的基本概念

**类**是C++中面向对象编程的核心概念，它是一种用户自定义的数据类型，封装了数据和操作这些数据的函数。

### 类的特点
- **封装性**：将数据和操作数据的方法组合在一起
- **抽象性**：隐藏实现细节，只暴露必要的接口
- **继承性**：可以从已有类派生新类
- **多态性**：同一操作作用于不同对象产生不同结果

### 对象与类
- **类**：是对象的模板或蓝图
- **对象**：是根据类创建的具体实例

---

## 类的定义与使用

### 基本语法

```cpp
class 类名 {
    访问控制符:
        成员变量;
        成员函数;
};
```

### 示例：定义一个简单的类

```cpp
#include <iostream>
using namespace std;

class Student {
public:
    string name;
    int age;
    double score;

    void display() {
        cout << "姓名: " << name << endl;
        cout << "年龄: " << age << endl;
        cout << "分数: " << score << endl;
    }
};

int main() {
    Student s1;
    s1.name = "张三";
    s1.age = 20;
    s1.score = 95.5;
    
    s1.display();
    
    return 0;
}
```

---

## 构造函数与析构函数

### 构造函数
构造函数在对象创建时自动调用，用于初始化对象。

```cpp
class Rectangle {
private:
    double width;
    double height;

public:
    默认构造函数
    Rectangle() {
        width = 0;
        height = 0;
        cout << "默认构造函数被调用" << endl;
    }

    带参数的构造函数
    Rectangle(double w, double h) {
        width = w;
        height = h;
        cout << "带参数构造函数被调用" << endl;
    }

    double getArea() {
        return width * height;
    }
};
```

### 析构函数
析构函数在对象销毁时自动调用，用于清理资源。

```cpp
class DynamicArray {
private:
    int* data;
    int size;

public:
    DynamicArray(int s) {
        size = s;
        data = new int[size];
        cout << "构造函数：分配内存" << endl;
    }

    ~DynamicArray() {
        delete[] data;
        cout << "析构函数：释放内存" << endl;
    }
};
```

### 构造函数的多种形式

```cpp
class Point {
private:
    int x, y;

public:
    默认构造函数
    Point() : x(0), y(0) {}

    带参数的构造函数
    Point(int a, int b) : x(a), y(b) {}

    拷贝构造函数
    Point(const Point& p) : x(p.x), y(p.y) {
        cout << "拷贝构造函数被调用" << endl;
    }

    void display() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};
```

---

## 访问控制

C++提供了三种访问控制符：

### public（公有）
- 可以在类的外部访问
- 通常用于成员函数

### private（私有）
- 只能在类内部访问
- 默认访问级别
- 通常用于成员变量

### protected（保护）
- 可以在类内部和派生类中访问
- 用于继承中的成员

```cpp
class BankAccount {
private:
    string accountNumber;
    double balance;

protected:
    string ownerName;

public:
    BankAccount(string num, string name, double bal) {
        accountNumber = num;
        ownerName = name;
        balance = bal;
    }

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

    double getBalance() {
        return balance;
    }
};
```

---

## 类的成员函数

### 内联成员函数
在类内部定义的函数默认为内联函数。

```cpp
class Circle {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}

    内联函数
    double getRadius() {
        return radius;
    }

    double getArea() {
        return 3.14159 * radius * radius;
    }
};
```

### 外部定义的成员函数
在类外定义成员函数需要使用作用域解析符 `::`。

```cpp
class Rectangle {
private:
    double width;
    double height;

public:
    Rectangle(double w, double h);
    double getArea();
    double getPerimeter();
};

外部定义构造函数
Rectangle::Rectangle(double w, double h) {
    width = w;
    height = h;
}

外部定义成员函数
double Rectangle::getArea() {
    return width * height;
}

double Rectangle::getPerimeter() {
    return 2 * (width + height);
}
```

### 静态成员
静态成员属于类而不是对象。

```cpp
class Counter {
private:
    static int count;

public:
    Counter() {
        count++;
    }

    ~Counter() {
        count--;
    }

    static int getCount() {
        return count;
    }
};

初始化静态成员
int Counter::count = 0;

int main() {
    Counter c1, c2, c3;
    cout << "对象数量: " << Counter::getCount() << endl;
    return 0;
}
```

### const成员函数
const成员函数不修改对象的成员变量。

```cpp
class Date {
private:
    int day, month, year;

public:
    Date(int d, int m, int y) : day(d), month(m), year(y) {}

    const成员函数
    void display() const {
        cout << day << "/" << month << "/" << year << endl;
    }

    int getYear() const {
        return year;
    }
};
```

---

## 类模板

类模板允许我们创建通用类，可以处理不同类型的数据。

### 基本语法

```cpp
template <typename T>
class 类名 {
    // 类定义
};
```

### 简单的类模板示例

```cpp
template <typename T>
class Box {
private:
    T value;

public:
    Box(T v) : value(v) {}

    void setValue(T v) {
        value = v;
    }

    T getValue() {
        return value;
    }

    void display() {
        cout << "Box contains: " << value << endl;
    }
};

int main() {
    Box<int> intBox(42);
    Box<double> doubleBox(3.14);
    Box<string> stringBox("Hello");

    intBox.display();
    doubleBox.display();
    stringBox.display();

    return 0;
}
```

### 多个类型参数的类模板

```cpp
template <typename T1, typename T2>
class Pair {
private:
    T1 first;
    T2 second;

public:
    Pair(T1 f, T2 s) : first(f), second(s) {}

    void display() {
        cout << "First: " << first << ", Second: " << second << endl;
    }

    T1 getFirst() { return first; }
    T2 getSecond() { return second; }
};

int main() {
    Pair<int, string> p1(1, "Apple");
    Pair<string, double> p2("Price", 99.99);

    p1.display();
    p2.display();

    return 0;
}
```

### 类模板实现栈

```cpp
#include <iostream>
using namespace std;

template <typename T>
class Stack {
private:
    T* data;
    int top;
    int capacity;

public:
    Stack(int size = 10) {
        capacity = size;
        data = new T[capacity];
        top = -1;
    }

    ~Stack() {
        delete[] data;
    }

    void push(T value) {
        if (top < capacity - 1) {
            data[++top] = value;
        } else {
            cout << "栈已满！" << endl;
        }
    }

    T pop() {
        if (top >= 0) {
            return data[top--];
        } else {
            cout << "栈为空！" << endl;
            return T();
        }
    }

    bool isEmpty() {
        return top == -1;
    }

    void display() {
        cout << "栈内容: ";
        for (int i = 0; i <= top; i++) {
            cout << data[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    Stack<int> intStack(5);
    intStack.push(10);
    intStack.push(20);
    intStack.push(30);
    intStack.display();

    cout << "弹出: " << intStack.pop() << endl;
    intStack.display();

    Stack<string> stringStack(3);
    stringStack.push("Hello");
    stringStack.push("World");
    stringStack.display();

    return 0;
}
```

---

## 类的继承

### 什么是继承？

**继承**是面向对象编程中一个非常重要的概念。用一个生活中的例子来理解：

想象一下，你想创建一个"学生"类和一个"老师"类。这两个类都有一些共同的特点：
- 都有姓名
- 都有年龄
- 都可以说话

如果没有继承，你需要在每个类中都重复写这些相同的代码。但是如果用继承，你可以先创建一个"人类"作为基类，然后让"学生类"和"老师类"都继承自"人类"，这样它们就自动拥有了人类的共同属性。

### 生活中的继承例子

```
人类（基类）
    ├── 学生类（派生类）
    ├── 老师类（派生类）
    └── 工人类（派生类）
```

每个派生类都有自己的特点，但都继承了人类的基本属性。

### 第一个继承示例

让我们从最简单的例子开始：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
public:
    string name;
    int age;

    void sayHello() {
        cout << "你好，我是 " << name << endl;
    }
};

class Student : public Person {
public:
    string studentID;
    double score;

    void study() {
        cout << name << " 正在学习..." << endl;
    }
};

int main() {
    Student s1;
    
    s1.name = "张三";
    s1.age = 18;
    s1.studentID = "2024001";
    s1.score = 95.5;
    
    s1.sayHello();
    s1.study();
    cout << "成绩: " << s1.score << endl;
    
    return 0;
}
```

**运行结果：**
```
你好，我是 张三
张三 正在学习...
成绩: 95.5
```

### 代码详细解释

#### 1. 基类定义
```cpp
class Person {
public:
    string name;
    int age;

    void sayHello() {
        cout << "你好，我是 " << name << endl;
    }
};
```
- `Person` 是基类（父类）
- 包含了两个成员变量：`name` 和 `age`
- 包含了一个成员函数：`sayHello()`

#### 2. 派生类定义
```cpp
class Student : public Person {
public:
    string studentID;
    double score;

    void study() {
        cout << name << " 正在学习..." << endl;
    }
};
```
- `Student` 是派生类（子类）
- `: public Person` 表示 `Student` 公有继承自 `Person`
- 派生类新增了两个成员变量：`studentID` 和 `score`
- 派生类新增了一个成员函数：`study()`
- 在 `study()` 函数中可以直接使用 `name`，因为它是从基类继承来的

#### 3. 继承的基本语法
```cpp
class 派生类名 : public 基类名 {
    // 派生类的成员
};
```

### 继承的三个关键概念

#### 1. 基类和派生类
- **基类**：被继承的类，也称为父类
- **派生类**：继承其他类的类，也称为子类

#### 2. 访问控制符 `public`
- `public` 继承是最常用的继承方式
- 表示派生类可以访问基类的公有成员

#### 3. 继承的内容
- 派生类继承了基类的所有公有成员变量和公有成员函数
- 派生类可以添加自己的新成员

### 更完整的例子：多种派生类

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
public:
    string name;
    int age;

    Person(string n, int a) {
        name = n;
        age = a;
        cout << "Person 构造函数被调用" << endl;
    }

    void sayHello() {
        cout << "你好，我是 " << name << "，今年 " << age << " 岁" << endl;
    }

    void eat() {
        cout << name << " 正在吃饭" << endl;
    }

    void sleep() {
        cout << name << " 正在睡觉" << endl;
    }
};

class Student : public Person {
public:
    string studentID;
    double score;

    Student(string n, int a, string id, double s) 
        : Person(n, a) {
        studentID = id;
        score = s;
        cout << "Student 构造函数被调用" << endl;
    }

    void study() {
        cout << name << " 正在学习，成绩: " << score << endl;
    }

    void takeExam() {
        cout << name << " 正在参加考试" << endl;
    }
};

class Teacher : public Person {
public:
    string subject;
    int yearsOfExperience;

    Teacher(string n, int a, string sub, int years) 
        : Person(n, a) {
        subject = sub;
        yearsOfExperience = years;
        cout << "Teacher 构造函数被调用" << endl;
    }

    void teach() {
        cout << name << " 正在教授 " << subject << endl;
    }

    void gradePapers() {
        cout << name << " 正在批改试卷" << endl;
    }
};

int main() {
    cout << "=== 创建学生 ===" << endl;
    Student student("张三", 18, "2024001", 95.5);
    
    cout << "\n=== 学生信息 ===" << endl;
    student.sayHello();
    student.study();
    student.eat();
    student.takeExam();

    cout << "\n=== 创建老师 ===" << endl;
    Teacher teacher("李老师", 35, "数学", 10);
    
    cout << "\n=== 老师信息 ===" << endl;
    teacher.sayHello();
    teacher.teach();
    teacher.sleep();
    teacher.gradePapers();

    return 0;
}
```

**运行结果：**
```
=== 创建学生 ===
Person 构造函数被调用
Student 构造函数被调用

=== 学生信息 ===
你好，我是 张三，今年 18 岁
张三 正在学习，成绩: 95.5
张三 正在吃饭
张三 正在参加考试

=== 创建老师 ===
Person 构造函数被调用
Teacher 构造函数被调用

=== 老师信息 ===
你好，我是 李老师，今年 35 岁
李老师 正在教授 数学
李老师 正在睡觉
李老师 正在批改试卷
```

### 构造函数的调用顺序

从这个例子中可以看到构造函数的调用顺序：

1. **先调用基类的构造函数**：`Person` 的构造函数
2. **再调用派生类的构造函数**：`Student` 或 `Teacher` 的构造函数

```cpp
Student(string n, int a, string id, double s) 
    : Person(n, a) {  // 先调用基类构造函数
    studentID = id;
    score = s;
    cout << "Student 构造函数被调用" << endl;
}
```

### protected 访问控制

之前我们学习了 `public` 和 `private` 访问控制符。现在学习 `protected`：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
protected:  // protected 成员
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}

    void display() {
        cout << "姓名: " << name << ", 年龄: " << age << endl;
    }
};

class Student : public Person {
public:
    string studentID;

    Student(string n, int a, string id) : Person(n, a), studentID(id) {}

    void displayWithID() {
        cout << "学号: " << studentID << endl;
        cout << "姓名: " << name << endl;  // 可以访问 protected 成员
        cout << "年龄: " << age << endl;
    }
};

int main() {
    Student s("王五", 20, "2024002");
    s.displayWithID();
    
    return 0;
}
```

### 三种访问控制符的对比

| 访问控制符 | 基类内部 | 派生类内部 | 类外部 |
|-----------|---------|-----------|--------|
| `public` | ✓ | ✓ | ✓ |
| `protected` | ✓ | ✓ | ✗ |
| `private` | ✓ | ✗ | ✗ |

### 访问控制的继承示例

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    int publicVar = 1;

protected:
    int protectedVar = 2;

private:
    int privateVar = 3;
};

class Derived : public Base {
public:
    void showAccess() {
        cout << "在派生类中访问:" << endl;
        cout << "publicVar = " << publicVar << endl;
        cout << "protectedVar = " << protectedVar << endl;
        cout << "不能访问 privateVar" << endl;
    }
};

int main() {
    Derived d;
    d.showAccess();
    
    cout << "\n在main函数中访问:" << endl;
    cout << "publicVar = " << d.publicVar << endl;
    cout << "不能访问 protectedVar 和 privateVar" << endl;
    
    return 0;
}
```

### 为什么要用继承？

#### 优点：
1. **代码复用**：不需要重复写相同的代码
2. **层次清晰**：代码结构更清晰，易于理解
3. **易于维护**：修改基类代码，所有派生类都会受益
4. **扩展性强**：可以轻松添加新的派生类

#### 什么时候使用继承：
- 当多个类有共同的属性和方法时
- 当需要创建"是一种"关系时（学生**是**人，老师**是**人）
- 当需要复用代码时

### 实际应用：交通工具系统

```cpp
#include <iostream>
#include <string>
using namespace std;

class Vehicle {
protected:
    string brand;
    int year;

public:
    Vehicle(string b, int y) : brand(b), year(y) {}

    void start() {
        cout << brand << " 正在启动..." << endl;
    }

    void stop() {
        cout << brand << " 正在停止..." << endl;
    }

    void displayInfo() {
        cout << "品牌: " << brand << ", 年份: " << year << endl;
    }
};

class Car : public Vehicle {
private:
    int numberOfDoors;

public:
    Car(string b, int y, int doors) 
        : Vehicle(b, y), numberOfDoors(doors) {}

    void honk() {
        cout << brand << " 喇叭响了！" << endl;
    }

    void displayCarInfo() {
        displayInfo();
        cout << "车门数: " << numberOfDoors << endl;
    }
};

class Motorcycle : public Vehicle {
private:
    bool hasSidecar;

public:
    Motorcycle(string b, int y, bool sidecar) 
        : Vehicle(b, y), hasSidecar(sidecar) {}

    void wheelie() {
        cout << brand << " 正在做特技！" << endl;
    }

    void displayMotorcycleInfo() {
        displayInfo();
        cout << "有边车: " << (hasSidecar ? "是" : "否") << endl;
    }
};

int main() {
    Car car("丰田", 2023, 4);
    Motorcycle bike("本田", 2022, false);

    cout << "=== 汽车信息 ===" << endl;
    car.displayCarInfo();
    car.start();
    car.honk();
    car.stop();

    cout << "\n=== 摩托车信息 ===" << endl;
    bike.displayMotorcycleInfo();
    bike.start();
    bike.wheelie();
    bike.stop();

    return 0;
}
```

### 多层继承

继承可以是多层级的：

```
Vehicle（交通工具）
    ├── Car（汽车）
    │   └── SportsCar（跑车）
    └── Motorcycle（摩托车）
```

```cpp
class SportsCar : public Car {
public:
    int maxSpeed;

    SportsCar(string b, int y, int doors, int speed) 
        : Car(b, y, doors), maxSpeed(speed) {}

    void race() {
        cout << brand << " 正在比赛，最高速度: " << maxSpeed << " km/h" << endl;
    }
};

int main() {
    SportsCar ferrari("法拉利", 2024, 2, 350);
    ferrari.start();
    ferrari.race();
    ferrari.stop();
    
    return 0;
}
```

### 继承的注意事项

1. **不要过度使用继承**：能用组合解决的问题就不要用继承
2. **保持基类简单**：基类应该包含最基本的属性和方法
3. **注意构造函数调用**：派生类构造函数要正确调用基类构造函数
4. **合理使用访问控制符**：保护基类的内部数据

### 练习建议

1. 创建一个 `Shape`（形状）基类，派生出 `Circle`（圆形）和 `Rectangle`（矩形）类
2. 创建一个 `Account`（账户）基类，派生出 `SavingsAccount`（储蓄账户）和 `CheckingAccount`（支票账户）类
3. 尝试多层继承，创建更复杂的类层次结构

---

## 多态性

多态性允许使用统一的接口处理不同类型的对象。

### 虚函数

```cpp
class Shape {
public:
    virtual void draw() {
        cout << "绘制形状" << endl;
    }

    virtual double area() {
        return 0;
    }

    virtual ~Shape() {}
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}

    void draw() override {
        cout << "绘制圆形，半径: " << radius << endl;
    }

    double area() override {
        return 3.14159 * radius * radius;
    }
};

class Rectangle : public Shape {
private:
    double width, height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}

    void draw() override {
        cout << "绘制矩形，宽: " << width << ", 高: " << height << endl;
    }

    double area() override {
        return width * height;
    }
};
```

### 纯虚函数与抽象类

```cpp
包含纯虚函数的类称为抽象类
class AbstractShape {
public:
    纯虚函数
    virtual void draw() = 0;
    virtual double area() = 0;

    virtual ~AbstractShape() {}
};

class Triangle : public AbstractShape {
private:
    double base, height;

public:
    Triangle(double b, double h) : base(b), height(h) {}

    void draw() override {
        cout << "绘制三角形" << endl;
    }

    double area() override {
        return 0.5 * base * height;
    }
};
```

### 多态示例

```cpp
void processShape(Shape* shape) {
    shape->draw();
    cout << "面积: " << shape->area() << endl;
}

int main() {
    Circle circle(5.0);
    Rectangle rect(4.0, 6.0);
    Triangle tri(3.0, 4.0);

    多态调用
    Shape* shapes[3];
    shapes[0] = &circle;
    shapes[1] = &rect;
    shapes[2] = &tri;

    for (int i = 0; i < 3; i++) {
        shapes[i]->draw();
        cout << "面积: " << shapes[i]->area() << endl;
    }

    return 0;
}
```

---

## 综合示例

### 学生成绩管理系统

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

基类：人员
class Person {
protected:
    string name;
    int age;
    string id;

public:
    Person(string n, int a, string i) : name(n), age(a), id(i) {}

    virtual void display() {
        cout << "姓名: " << name << ", 年龄: " << age << ", ID: " << id << endl;
    }

    virtual ~Person() {}
};

学生类
class Student : public Person {
private:
    string major;
    vector<double> grades;

public:
    Student(string n, int a, string i, string m) 
        : Person(n, a, i), major(m) {}

    void addGrade(double grade) {
        grades.push_back(grade);
    }

    double getAverage() {
        if (grades.empty()) return 0;
        double sum = 0;
        for (double g : grades) {
            sum += g;
        }
        return sum / grades.size();
    }

    void display() override {
        cout << "=== 学生信息 ===" << endl;
        Person::display();
        cout << "专业: " << major << endl;
        cout << "平均成绩: " << getAverage() << endl;
    }
};

教师类
class Teacher : public Person {
private:
    string department;
    vector<string> courses;

public:
    Teacher(string n, int a, string i, string d) 
        : Person(n, a, i), department(d) {}

    void addCourse(string course) {
        courses.push_back(course);
    }

    void display() override {
        cout << "=== 教师信息 ===" << endl;
        Person::display();
        cout << "部门: " << department << endl;
        cout << "教授课程: ";
        for (const string& c : courses) {
            cout << c << " ";
        }
        cout << endl;
    }
};

课程模板类
template <typename T>
class Course {
private:
    string courseName;
    vector<T> students;

public:
    Course(string name) : courseName(name) {}

    void addStudent(T student) {
        students.push_back(student);
    }

    void displayAllStudents() {
        cout << "\n=== " << courseName << " 课程学生列表 ===" << endl;
        for (auto& s : students) {
            s.display();
            cout << endl;
        }
    }
};

int main() {
    创建学生对象
    Student s1("张三", 20, "S001", "计算机科学");
    Student s2("李四", 19, "S002", "软件工程");
    Student s3("王五", 21, "S003", "计算机科学");

    添加成绩
    s1.addGrade(90.5);
    s1.addGrade(85.0);
    s1.addGrade(92.0);

    s2.addGrade(88.0);
    s2.addGrade(91.5);

    s3.addGrade(95.0);
    s3.addGrade(93.5);
    s3.addGrade(96.0);

    创建教师对象
    Teacher t1("赵老师", 45, "T001", "计算机系");
    t1.addCourse("数据结构");
    t1.addCourse("算法设计");

    创建课程
    Course<Student> dataStructures("数据结构");
    dataStructures.addStudent(s1);
    dataStructures.addStudent(s2);
    dataStructures.addStudent(s3);

    使用多态
    vector<Person*> people;
    people.push_back(&s1);
    people.push_back(&s2);
    people.push_back(&s3);
    people.push_back(&t1);

    cout << "=== 所有人员信息 ===" << endl;
    for (auto p : people) {
        p->display();
        cout << endl;
    }

    显示课程学生
    dataStructures.displayAllStudents();

    return 0;
}
```

---

## 学习建议

### 循序渐进
1. 先掌握类的基本定义和使用
2. 理解构造函数和析构函数
3. 学习访问控制的概念
4. 掌握成员函数的定义
5. 深入理解类模板
6. 学习继承的概念和用法
7. 掌握多态性的应用

### 实践练习
- 从简单的类开始练习
- 逐步增加复杂度
- 多写代码，多调试
- 理解面向对象的设计思想

### 注意事项
- 注意构造函数和析构函数的调用时机
- 理解不同访问控制的区别
- 掌握虚函数在多态中的作用
- 注意类模板的实例化过程
- 理解继承中的访问权限变化

希望这份文档能帮助您理解C++中类的相关概念和用法！
