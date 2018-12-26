# C++ Style Guide

### 文件名定义

- 均小写,可用下划线隔开
- 功能+等级 例如:3d_base

### 命名空间定义

- 均驼峰命名
- 功能 例如:namespace My3D

### 宏定义

- 强制:每个.h必须增加判断宏定义 例如#ifndef TEST #define TEST #else #error has been defined 'TEST' #endif
- 均大写,首字母不能为_,
- 每个字段用下划线隔开
- 命名空间+功能 例如: #define MY3D_TEXUTRE_LOAD(T)

### 变量定义

- 小写字母开头,可用_隔，开能顾名思义
- 指针定义
  - 类型名后跟*,例如:char* data;错误 char *data;
  - 倡议:使用栈内存数组,全部使用new
    - 例如:char *data=new char[1024];错误: char data[1024];
  - 倡议:内存在哪里分配,在哪里释放
  - 强制:指针数组 末尾必须增加nullptrl判定边界
  - 强制:字符串数组 末尾必须以'\0'结尾
  - 倡议:struct union定义 使用typedef,并给出全部大写的类型,
    - 例如:typedef struct My3DPoint{int x,int y,int z} MY3DPOINT;
  - 强制:类名大写开头,成员变量全部小写开头,公共成员函数大写开头,私有,保护类型的成员函数,小写开头

### 函数定义

- 公共函数,全部大写开头
- 参数
  - 具有大量数据的参数,全部使用引用或者指针,禁止copy对象内存到参数栈
- 返回值
  - 凡是拥有大量数据的数据对象返回,都返回其对象指针,并且都使用new class开辟内存;
  - 例如: return new Vertex3f(1,3,4);
  - 错误:return &Vertex3f v(1,3,4);
- 重载函数定义
  - 运算符重载
    - <<,>>需要返回当前对象 例如:return *this;
    - ++,-- 返回void;
    - +,- 返回 新的对象指针;
    - 强制:每个类都重载 operator=,
  - 析构函数
    - 必须使用 virtual修饰
  - 普通函数
    - 最好使用 virtual修饰

### 类定义

- 抽象的功能函数相同作用的时候,必须写纯虚函数.
- 每个类必须重载 复制构造函数