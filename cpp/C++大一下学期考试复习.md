# C++ 大一下学期编程考试复习指南

## 〇、输入输出与字符串处理专题（难点突破）

### 1. cin 的行为：遇空格/换行停止

```cpp
int n;
cin >> n;   // 读整数，跳过前导空格和换行

string s;
cin >> s;   // 读一个"单词"，遇空格/换行就停！
// 输入 "hello world" → s 只得到 "hello"

char c;
cin >> c;   // 读一个非空白字符（自动跳过空格和换行）
```

### 2. 读取整行：getline

```cpp
#include <string>

string line;
getline(cin, line);  // 读一整行，包括空格，遇换行停止
// 输入 "hello world cpp" → line = "hello world cpp"
```

### 3. ⚠️ 最经典的坑：cin >> n 和 getline 混用

```cpp
int n;
cin >> n;           // 输入 "3" 然后按回车
// 此时缓冲区里还剩一个 '\n'！

string line;
getline(cin, line); // 直接读到空字符串！因为 '\n' 还在缓冲区里

// ✅ 解决方法：在 cin >> n 之后加一行
cin >> n;
cin.ignore();       // 吃掉缓冲区里的换行符
getline(cin, line); // 现在能正常读了
```

**记住口诀：`cin >>` 之后接 `getline`，必须加 `cin.ignore()`**

### 4. 各种输入场景速查

**场景一：已知个数 n，然后读 n 个数**
```cpp
int n;
cin >> n;
for (int i = 0; i < n; i++) {
    int x;
    cin >> x; // cin >> 会自动跳过空格和换行，不用管格式
}
```

**场景二：读到文件末尾（EOF）为止**
```cpp
// 写法一
int x;
while (cin >> x) {
    // 处理 x
}

// 写法二（C风格）
int x;
while (scanf("%d", &x) != EOF) {
    // 处理 x
}
```

**场景三：每行读一个字符串，共 n 行**
```cpp
int n;
cin >> n;
cin.ignore(); // ← 关键！
for (int i = 0; i < n; i++) {
    string line;
    getline(cin, line);
}
```

**场景四：读入带空格的一整行，行数未知**
```cpp
string line;
while (getline(cin, line)) {
    if (line.empty()) break; // 空行结束，按题目要求改
    // 处理 line
}
```

**场景五：一行有多个数据，用空格分隔**
```cpp
// 方法一：stringstream 拆分
#include <sstream>
string line;
getline(cin, line);
stringstream ss(line);
int x;
while (ss >> x) {
    // 每个数字都能读到
}

// 方法二：直接 cin >> 连续读（因为 >> 自动跳空格）
int a, b, c;
cin >> a >> b >> c;
```

**场景六：用逗号/其他符号分隔的数据**
```cpp
// 例：输入 "12,34,56" 用逗号分隔
#include <sstream>
#include <string>

string line;
cin >> line; // 或者 getline(cin, line)
stringstream ss(line);
string token;
while (getline(ss, token, ',')) { // 按逗号分割
    int num = stoi(token);
    cout << num << endl; // 12, 34, 56
}
```

**场景七：读入字符矩阵**
```cpp
int n, m;
cin >> n >> m;
char grid[100][100];
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        cin >> grid[i][j]; // 每个字符之间用空格分隔
    }
}

// 如果字符之间没有空格（每行是连续字符串）：
for (int i = 0; i < n; i++) {
    string row;
    cin >> row; // 读一整行字符串
    for (int j = 0; j < m; j++) {
        grid[i][j] = row[j];
    }
}
```

### 5. 输出格式控制

```cpp
#include <iomanip> // 格式控制头文件

// 保留小数位数
cout << fixed << setprecision(2) << 3.14159 << endl; // 3.14

// 设置宽度（右对齐）
cout << setw(5) << 42 << endl;    // "   42"
cout << setw(5) << left << 42;    // "42   "（左对齐）

// 补零
cout << setfill('0') << setw(4) << 7 << endl; // "0007"

// 输出不带空格的数组
for (int i = 0; i < n; i++) {
    cout << arr[i];
    if (i < n - 1) cout << " "; // 最后一个不加空格
}
cout << endl;

// 输出每行一个
for (int i = 0; i < n; i++) {
    cout << arr[i] << endl;
}
```

### 6. scanf / printf（C 风格，有时候更快更方便）

```cpp
#include <cstdio>

// scanf 格式符
int a; double b; char c; char s[100];
scanf("%d", &a);       // 读整数
scanf("%lf", &b);      // 读 double（注意是 lf 不是 f）
scanf("%c", &c);       // 读字符（会读空格和换行！）
scanf("%s", s);        // 读字符串（遇空格停）
scanf("%d,%d", &a, &b); // 读 "3,5" 这种逗号分隔的

// printf 格式符
printf("%d\n", a);           // 整数
printf("%f\n", b);           // 浮点数默认6位
printf("%.2f\n", b);         // 保留2位小数
printf("%05d\n", 42);        // "00042" 补零宽度5
printf("%-10d|\n", 42);      // "42        |" 左对齐宽度10
printf("%lld\n", (long long)1e18); // long long 用 %lld
```

### 7. 字符串处理的常见套路

**① 遍历字符串的每个字符**
```cpp
string s = "hello";
// 方法一：下标
for (int i = 0; i < s.length(); i++) {
    cout << s[i] << " ";
}
// 方法二：范围 for
for (char c : s) {
    cout << c << " ";
}
```

**② 逐字符读取输入（含空格）**
```cpp
char c;
while (cin.get(c)) { // 能读到空格、换行等所有字符
    if (c == '\n') break;
    // 处理 c
}
```

**③ 字符串中找所有某个子串的位置**
```cpp
string s = "abcabcabc";
string target = "abc";
size_t pos = 0;
while ((pos = s.find(target, pos)) != string::npos) {
    cout << "找到位置: " << pos << endl;
    pos++; // 从下一个位置继续找
}
```

**④ 按分隔符拆分字符串（通用模板）**
```cpp
#include <sstream>

// 按任意单字符分隔
vector<string> split(string s, char delim) {
    vector<string> tokens;
    stringstream ss(s);
    string token;
    while (getline(ss, token, delim)) {
        tokens.push_back(token);
    }
    return tokens;
}

// 使用：split("one,two,three", ',') → {"one", "two", "three"}
```

**⑤ 把字符串里的一段替换掉**
```cpp
string s = "hello world";
s.replace(6, 5, "cpp"); // 从位置 6 开始替换 5 个字符为 "cpp"
// s = "hello cpp"
```

**⑥ 字符串 ↔ 字符数组互转**
```cpp
// string → char[]
string s = "hello";
char arr[100];
strcpy(arr, s.c_str()); // c_str() 返回 const char*

// char[] → string
char arr[] = "world";
string s2(arr); // 直接构造
```

### 8. 输入输出速查表

```
┌────────────────────────────┬────────────────────────────────────┐
│          需求              │            写法                     │
├────────────────────────────┼────────────────────────────────────┤
│ 读一个整数                 │ cin >> n;                           │
│ 读一个单词（不含空格）      │ cin >> s;                           │
│ 读一整行（含空格）          │ getline(cin, s);                    │
│ cin后接getline             │ cin >> n; cin.ignore(); getline...  │
│ 读到EOF为止                │ while (cin >> x) { }               │
│ 读到特定值停止             │ while (cin >> x && x != 0) { }     │
│ 按逗号分割一行             │ getline(ss, token, ',')            │
│ 保留2位小数输出             │ cout << fixed << setprecision(2)   │
│ 补零输出                   │ printf("%04d", n);                  │
│ 读单个字符（含空格）        │ cin.get(c);                         │
│ 读单个字符（跳过空格）      │ cin >> c;                           │
└────────────────────────────┴────────────────────────────────────┘
```

---

## 一、基础语法必考

### 1. 输入输出
```cpp
#include <iostream>
using namespace std;
cin >> n;
cout << result << endl;
```

### 2. 数据类型与强制转换
- `int`, `double`, `char`, `string`, `bool`
- 强制转换：`(int)3.7` 或 `static_cast<int>(3.7)`

### 3. 控制结构
- `if / else if / else`
- `switch-case`
- `for`, `while`, `do-while`

### 4. 数组与字符串
- 一维数组、二维数组
- `string` 类：`length()`, `substr()`, `find()`, `append()`, `+` 拼接
- 字符数组与 `<cstring>`：`strlen()`, `strcpy()`, `strcmp()`, `strcat()`

---

## 二、函数与递归（高频考点）

### 1. 函数重载与默认参数
```cpp
int add(int a, int b, int c = 0);
```

### 2. 值传递 vs 引用传递
```cpp
void swap(int &a, int &b);
```

### 3. 递归（几乎必考）
- **阶乘**
```cpp
int fact(int n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);
}
```
- **斐波那契数列**
```cpp
int fib(int n) {
    if (n <= 2) return 1;
    return fib(n - 1) + fib(n - 2);
}
```
- **汉诺塔**
```cpp
void hanoi(int n, char A, char B, char C) {
    if (n == 1) { cout << A << "->" << C << endl; return; }
    hanoi(n - 1, A, C, B);
    cout << A << "->" << C << endl;
    hanoi(n - 1, B, A, C);
}
```

---

## 三、指针与引用

### 1. 基本操作
```cpp
int a = 10;
int *p = &a;
cout << *p; // 10
```

### 2. 指针与数组
```cpp
int arr[5] = {1,2,3,4,5};
int *p = arr;
cout << *(p + 2); // 3
```

### 3. 动态内存
```cpp
int *p = new int(10);
int *arr = new int[n];
delete p;
delete[] arr;
```

### 4. 引用
```cpp
int &ref = a;
ref = 20; // a 也变成 20
```

---

## 四、结构体与类（面向对象，重点）

### 1. 结构体
```cpp
struct Student {
    string name;
    int score;
};
```

### 2. 类的定义
```cpp
class Circle {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    double area() { return 3.14159 * radius * radius; }
    double getRadius() { return radius; }
    void setRadius(double r) { radius = r; }
};
```

### 3. 构造函数与析构函数
- 默认构造、带参构造、拷贝构造
- 初始化列表：`Circle(double r) : radius(r) {}`

### 4. this 指针
```cpp
void setRadius(double radius) {
    this->radius = radius;
}
```

### 5. 友元函数
```cpp
friend void print(Circle c);
```

### 6. 运算符重载
```cpp
Complex operator+(const Complex &other) {
    return Complex(real + other.real, imag + other.imag);
}
```

### 7. 继承与多态
```cpp
class Animal {
public:
    virtual void speak() { cout << "..." << endl; }
};
class Dog : public Animal {
public:
    void speak() override { cout << "汪汪" << endl; }
};
```

---

## 五、必考算法模板

### 1. 排序算法

**冒泡排序**（最常考）
```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - 1 - i; j++)
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
}
```

**选择排序**
```cpp
void selectSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[minIdx]) minIdx = j;
        swap(arr[i], arr[minIdx]);
    }
}
```

**插入排序**
```cpp
void insertSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i], j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### 2. 查找算法

**二分查找**（必须会手写）
```cpp
int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

**线性查找**
```cpp
int search(int arr[], int n, int target) {
    for (int i = 0; i < n; i++)
        if (arr[i] == target) return i;
    return -1;
}
```

### 3. 素数判断与筛法

**判断素数**
```cpp
bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return false;
    return true;
}
```

**埃氏筛**
```cpp
void sieve(int n) {
    vector<bool> prime(n + 1, true);
    for (int i = 2; i * i <= n; i++)
        if (prime[i])
            for (int j = i * i; j <= n; j += i)
                prime[j] = false;
}
```

### 4. 最大公约数与最小公倍数
```cpp
int gcd(int a, int b) {
    return b == 0 ? a : gcd(b, a % b);
}
int lcm(int a, int b) {
    return a / gcd(a, b) * b;
}
```

### 5. string 常用操作大全

```cpp
#include <string>
using namespace std;

string s = "hello";
string s2(5, 'a');    // "aaaaa"
string s3(s, 1, 3);   // 从 s[1] 取 3 个字符 → "ell"

// 拼接
s = s + " world";     // "hello world"
s.append("!");        // "hello world!"
s.push_back('x');     // 末尾加一个字符
s.pop_back();         // 删除末尾字符

// 查找
s.find("world");      // 返回起始下标 6，找不到返回 string::npos
s.rfind("l");         // 从后往前找
s.find_first_of("aeiou");   // 找第一个元音字母的位置
s.find_first_not_of("aeiou");

// 截取子串
s.substr(6);          // 从下标 6 到末尾 → "world!"
s.substr(6, 5);       // 从下标 6 取 5 个字符 → "world"

// 插入与删除
s.insert(5, " dear"); // 在下标 5 处插入
s.erase(5, 5);        // 从下标 5 删 5 个字符
s.erase(s.begin());   // 删第一个字符
s.erase(s.end() - 1); // 删最后一个字符

// 替换
s.replace(0, 5, "HELLO"); // 前 5 个字符替换为 "HELLO"

// 比较
s.compare("hello");   // 0=相等, >0=s更大, <0=s更小

// 大小与容量
s.length(); s.size(); // 长度
s.empty();            // 是否为空
s.clear();            // 清空

// 遍历
for (int i = 0; i < s.length(); i++) cout << s[i];
for (char c : s) cout << c;

// 数字 ↔ 字符串转换
int num = stoi("123");       // string → int
long lnum = stol("123456");  // string → long
double d = stod("3.14");     // string → double
string s_num = to_string(42); // int → string
```

### 6. cstring（C 风格字符串函数，考试常考）

```cpp
#include <cstring>

char s1[100] = "hello";
char s2[100] = "world";

strlen(s1);              // 5（不含 '\0'）
strcpy(s1, s2);          // s1 变成 "world"
strncpy(s1, s2, 3);      // 只复制前 3 个字符
strcat(s1, s2);          // s1 后面拼上 s2
strncat(s1, s2, 3);      // 只拼前 3 个
strcmp(s1, s2);          // 0 相等, >0 s1>s2, <0 s1<s2
strncmp(s1, s2, 3);      // 只比较前 3 个
strchr(s1, 'l');         // 第一个 'l' 的指针
strrchr(s1, 'l');        // 最后一个 'l' 的指针
strstr(s1, "ell");       // 子串首次出现的指针
memset(s1, 'a', 5);      // 前 5 个字节设为 'a'
```

### 7. 单个字符处理（\<cctype\>）

```cpp
#include <cctype>
// 返回非零=true, 0=false
isalpha('A');    // 是否字母
isdigit('5');    // 是否数字
isalnum('a');    // 是否字母或数字
isupper('A');    // 是否大写
islower('a');    // 是否小写
isspace(' ');    // 是否空白（空格/tab/换行）
ispunct(',');    // 是否标点符号
toupper('a');    // 'A'（返回转换后的字符，不改变原字符）
tolower('A');    // 'a'
```

### 8. 字符串高频考题

**① 统计各类字符个数**
```cpp
void countChars(string s) {
    int letters = 0, digits = 0, spaces = 0, others = 0;
    for (char c : s) {
        if (isalpha(c)) letters++;
        else if (isdigit(c)) digits++;
        else if (isspace(c)) spaces++;
        else others++;
    }
    cout << "字母:" << letters << " 数字:" << digits
         << " 空格:" << spaces << " 其他:" << others << endl;
}
```

**② 字符串反转**
```cpp
// 方法一：双指针
string reverseStr(string s) {
    int i = 0, j = s.length() - 1;
    while (i < j) swap(s[i++], s[j--]);
    return s;
}
// 方法二：STL
string reverseStr2(string s) {
    reverse(s.begin(), s.end());
    return s;
}
```

**③ 判断回文串**
```cpp
bool isPalindrome(string s) {
    int i = 0, j = s.length() - 1;
    while (i < j) {
        if (s[i] != s[j]) return false;
        i++; j--;
    }
    return true;
}
```

**④ 凯撒密码加密/解密**
```cpp
string caesarEncrypt(string s, int shift) {
    for (char &c : s) {
        if (isupper(c))
            c = (c - 'A' + shift) % 26 + 'A';
        else if (islower(c))
            c = (c - 'a' + shift) % 26 + 'a';
    }
    return s;
}
string caesarDecrypt(string s, int shift) {
    return caesarEncrypt(s, 26 - shift);
}
```

**⑤ 字符串分割（按空格拆分单词）**
```cpp
#include <sstream>
void splitWords(string s) {
    string word;
    stringstream ss(s);
    while (ss >> word) {
        cout << word << endl;
    }
}
```

**⑥ 删除所有指定字符**
```cpp
string removeChar(string s, char ch) {
    string result;
    for (char c : s)
        if (c != ch) result += c;
    return result;
}
```

**⑦ 单词首字母大写**
```cpp
void capitalizeFirst(string &s) {
    bool newWord = true;
    for (char &c : s) {
        if (isalpha(c) && newWord) {
            c = toupper(c);
            newWord = false;
        } else if (isspace(c)) {
            newWord = true;
        }
    }
}
```

**⑧ 找最长单词**
```cpp
#include <sstream>
string longestWord(string s) {
    string word, longest;
    stringstream ss(s);
    while (ss >> word) {
        if (word.length() > longest.length())
            longest = word;
    }
    return longest;
}
```

### 9. 矩阵运算

**矩阵转置**
```cpp
void transpose(int a[][100], int n) {
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            swap(a[i][j], a[j][i]);
}
```

**矩阵乘法**
```cpp
void matMul(int A[][100], int B[][100], int C[][100], int n) {
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            C[i][j] = 0;
            for (int k = 0; k < n; k++)
                C[i][j] += A[i][k] * B[k][j];
        }
}
```

**对角线求和**
```cpp
void diagonalSum(int a[][100], int n) {
    int mainSum = 0, antiSum = 0;
    for (int i = 0; i < n; i++) {
        mainSum += a[i][i];           // 主对角线
        antiSum += a[i][n - 1 - i];   // 副对角线
    }
    cout << "主:" << mainSum << " 副:" << antiSum << endl;
}
```

**蛇形矩阵**
```cpp
void snakeMatrix(int n) {
    int a[100][100], num = 1;
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0)
            for (int j = 0; j < n; j++) a[i][j] = num++;
        else
            for (int j = n - 1; j >= 0; j--) a[i][j] = num++;
    }
}
```

### 10. 数组经典题型

**① 找最大/最小值及下标**
```cpp
void findMinMax(int arr[], int n) {
    int minIdx = 0, maxIdx = 0;
    for (int i = 1; i < n; i++) {
        if (arr[i] < arr[minIdx]) minIdx = i;
        if (arr[i] > arr[maxIdx]) maxIdx = i;
    }
    cout << "最小值:" << arr[minIdx] << " 下标:" << minIdx << endl;
    cout << "最大值:" << arr[maxIdx] << " 下标:" << maxIdx << endl;
}
```

**② 数组逆序**
```cpp
void reverseArr(int arr[], int n) {
    for (int i = 0; i < n / 2; i++)
        swap(arr[i], arr[n - 1 - i]);
}
```

**③ 删除指定位置元素**
```cpp
int removeAt(int arr[], int n, int pos) {
    for (int i = pos; i < n - 1; i++)
        arr[i] = arr[i + 1];
    return n - 1;
}
```

**④ 在指定位置插入元素**
```cpp
int insertAt(int arr[], int n, int pos, int val) {
    for (int i = n; i > pos; i--)
        arr[i] = arr[i - 1];
    arr[pos] = val;
    return n + 1;
}
```

**⑤ 有序数组去重**
```cpp
int uniqueArr(int arr[], int n) {
    int j = 0;
    for (int i = 1; i < n; i++)
        if (arr[i] != arr[j]) arr[++j] = arr[i];
    return j + 1;
}
```

**⑥ 两个有序数组合并**
```cpp
void mergeArr(int a[], int n, int b[], int m, int c[]) {
    int i = 0, j = 0, k = 0;
    while (i < n && j < m) {
        if (a[i] <= b[j]) c[k++] = a[i++];
        else c[k++] = b[j++];
    }
    while (i < n) c[k++] = a[i++];
    while (j < m) c[k++] = b[j++];
}
```

### 11. 数字拆分与数学题

**① 各位数字拆分**
```cpp
void splitDigits(int n) {
    if (n == 0) { cout << 0; return; }
    while (n > 0) {
        cout << n % 10 << " ";
        n /= 10;
    }
}
```

**② 水仙花数**
```cpp
bool isNarcissistic(int n) {
    int sum = 0, temp = n;
    while (temp > 0) {
        int d = temp % 10;
        sum += d * d * d;
        temp /= 10;
    }
    return sum == n;
}
// 三位水仙花数：153, 370, 371, 407
```

**③ 完数判断**
```cpp
bool isPerfect(int n) {
    int sum = 1;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            if (i != n / i) sum += n / i;
        }
    }
    return sum == n && n != 1;
}
// 6 = 1+2+3, 28 = 1+2+4+7+14
```

**④ 数字反转**
```cpp
int reverseNum(int n) {
    int rev = 0;
    while (n > 0) {
        rev = rev * 10 + n % 10;
        n /= 10;
    }
    return rev;
}
```

### 12. 算法常用技巧

**① 前缀和**
```cpp
void prefixSum(int arr[], int n) {
    int sum[1000];
    sum[0] = arr[0];
    for (int i = 1; i < n; i++)
        sum[i] = sum[i - 1] + arr[i];
    // [l, r] 区间和 = sum[r] - sum[l - 1]
}
```

**② STL sort 自定义排序**
```cpp
#include <algorithm>

sort(arr, arr + n, greater<int>()); // 降序

struct Student { string name; int score; };
bool cmp(Student a, Student b) {
    return a.score > b.score; // 按分数降序
}
sort(stu, stu + n, cmp);
```

**③ vector 常用操作**
```cpp
#include <vector>

vector<int> v = {3, 1, 4, 1, 5};

v.push_back(9);      // 末尾添加
v.pop_back();        // 删除末尾
v.size();            // 大小
v.empty();           // 是否为空
v.clear();           // 清空
v.front(); v.back(); // 首尾元素

sort(v.begin(), v.end());
reverse(v.begin(), v.end());
v.erase(v.begin() + 2);        // 删除第 3 个元素
v.insert(v.begin() + 1, 99);   // 第 2 个位置插入 99

// 去重
sort(v.begin(), v.end());
v.erase(unique(v.begin(), v.end()), v.end());
```

---

## 六、STL 常用容器（看教学进度）

```cpp
#include <vector>
vector<int> v;     v.push_back(), v.size(), v[i]

#include <map>
map<string, int> m; m["key"] = value;

#include <set>
set<int> s;         s.insert(), s.count()

#include <algorithm>
sort(arr, arr + n);
reverse(arr, arr + n);
```

---

## 七、文件操作（部分学校考）

```cpp
#include <fstream>
ofstream out("output.txt");
out << "hello" << endl;
out.close();

ifstream in("input.txt");
int x;
while (in >> x) { /* 处理 */ }
in.close();
```

---

## 八、应试技巧

1. **先看清楚题目要求**，注意输入输出格式
2. **先写框架再填逻辑**：先写 `main` 函数框架，再逐个实现
3. **边界条件**：注意 n=0、n=1、空字符串等特殊情况
4. **变量初始化**：声明变量时一定要初始化，尤其是累加器、计数器
5. **数组越界**：循环条件仔细检查
6. **分步调试**：不会做就先 cout 中间结果
7. **时间分配**：先做有把握的题，难题最后攻克

---

> 加油！把上面的模板多写几遍，手写一遍加深记忆。
