# C++ std::string 学习笔记

## 1. 简介

`std::string` 是 C++ 标准库提供的字符串类，位于 `std` 命名空间。

头文件：

```cpp
#include <string>
```

使用：

```cpp
std::string str = "hello";
```

相比 C 风格字符串：

```cpp
char str[] = "hello";
```

优势：

- 自动管理内存
- 长度可变
- 提供丰富字符串操作函数
- 更安全

---

# 2. 创建 string

## 基本创建

```cpp
std::string str;
```

空字符串：

```
""
```

---

## 初始化

```cpp
std::string name = "Tom";
```

或：

```cpp
std::string name("Tom");
```

---

## 重复字符

```cpp
std::string str(5, 'a');
```

结果：

```
aaaaa
```

---

# 3. 基本操作

## 获取长度

```cpp
str.size();
str.length();
```

例：

```cpp
std::string s = "hello";

s.size();   // 5
```

---

## 访问字符

下标：

```cpp
str[0];
```

安全访问：

```cpp
str.at(0);
```

区别：

|方式|特点|
|-|-|
|`[]`|不检查越界|
|`at()`|检查越界|

---

# 4. 字符串拼接

## 使用 +

```cpp
std::string a="hello";
std::string b="world";

std::string c=a+b;
```

结果：

```
helloworld
```

---

## 使用 +=

```cpp
str += " world";
```

---

# 5. 字符串比较

支持：

```cpp
==
!=
>
<
>=
<=
```

例如：

```cpp
if(a == b)
{
    cout<<"相等";
}
```

比较规则：

按字典序比较。

---

# 6. 常用成员函数

## append()

追加：

```cpp
str.append("abc");
```

等价：

```cpp
str += "abc";
```

---

## insert()

插入：

```cpp
str.insert(位置, "内容");
```

例：

```cpp
str.insert(5," world");
```

---

## erase()

删除：

```cpp
str.erase(开始位置, 长度);
```

例：

```cpp
str.erase(1,2);
```

---

## replace()

替换：

```cpp
str.replace(开始位置, 长度, "新内容");
```

---

## substr()

截取子串：

```cpp
str.substr(开始位置, 长度);
```

例：

```cpp
std::string s="hello";

s.substr(1,3);
```

结果：

```
ell
```

---

## find()

查找：

```cpp
int pos = str.find("abc");
```

找不到：

```cpp
std::string::npos
```

---

# 7. 输入字符串

## cin

```cpp
std::string name;

std::cin >> name;
```

只能读取一个单词。

---

## getline()

读取整行：

```cpp
std::getline(std::cin,name);
```

可以读取空格。

---

# 8. string 与 C 字符串转换

## string → char*

```cpp
str.c_str();
```

例：

```cpp
strcmp(a.c_str(), b.c_str());
```

---

## char[] → string

```cpp
char arr[]="hello";

std::string s=arr;
```

---

# 9. 遍历 string

## 普通 for

```cpp
for(int i=0;i<str.size();i++)
{
    std::cout<<str[i];
}
```

---

## 范围 for（推荐）

```cpp
for(char c : str)
{
    std::cout<<c;
}
```

---

# 10. 常用函数速查

|函数|作用|
|-|-|
|`size()`|获取长度|
|`empty()`|判断是否为空|
|`clear()`|清空|
|`append()`|追加|
|`insert()`|插入|
|`erase()`|删除|
|`replace()`|替换|
|`substr()`|截取|
|`find()`|查找|
|`c_str()`|转 C 字符串|
|`push_back()`|添加字符|
|`pop_back()`|删除末尾字符|

---

# 11. 与 C 字符串对比

| |char[]|std::string|
|-|-|-|
|长度|固定|动态|
|内存管理|手动|自动|
|拼接|strcat|+|
|比较|strcmp|==|
|安全性|低|高|

---

# 12. 学习重点

初学阶段重点掌握：

1. 创建 `std::string`
2. `+` / `+=` 拼接
3. `size()`
4. 字符访问
5. `find()`
6. `substr()`
7. `getline()`
8. `c_str()`

现代 C++ 中：

> 字符串处理优先使用 `std::string`，除非需要兼容 C 接口，否则不推荐使用 `char[]`。