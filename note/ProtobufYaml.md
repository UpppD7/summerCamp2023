# Protobuf&Yaml

## Protobuf ##

**1.proto文件示例** 

```
// import "other_protos.proto"; // 如果需要引用其它的protobuf文件，可以使用import语句。` 

syntax = "proto3"; // 指定protobuf遵循的语法格式是proto2还是proto3。在本教程和之后的开发中，我们都使用proto3语法格式。  
package student; // 包名声明。如在本例中，proto文件生成的类都会被放在namespace student中，这一举措的意义在于防止命名冲突 

enum Sex // 自定义枚举类型
{
    MALE = 0;
    FEMALE = 1;
}`

message Course // protobuf中，使用message定义数据结构，类似于C中的结构体
{
    int32 credit = 1;
    string name = 2;
}

message StudentInfo
{
    // 变量声明格式 <限定修饰符> <数据类型> <变量名>=id
    int32 age = 1;
    string name = 2;
    Sex sex = 3;
    repeated Course courses = 4; // repeated表示重复（数组），本例也表明message可以嵌套message
}
```

一个常见的约定是，我们会将经常使用的字段编号为1-15，不常用的字段编号为16以上的数字，因为1-15的编号编码仅需要1 byte，这样可以减小字节流的体积。



**2.repeated** 

repeated 关键字可以定义重复多次的信息（即数组），其顺序是有序的。

示例：哨兵按顺序到各点巡逻



**3.命名法** 

- message、enum采用大驼峰命名法，如 message StudentInfo 。

- 字段采用下划线分割法，且全部小写，如 string student_name 。

- 枚举值采用下划线分割法，且全部大写，如 FIRST_VALUE 。

  

**4.使用proto文件进行序列化和反序列化** （了解，编译后会自动生成proto文件）

`protoc --help # 查看使用方法
protoc test.proto --cpp_out=. # 在当前目录下生成.cpp文件和.h文件` 

使用 `--cpp_out` 选项，会生成 `<protobuf_name>.pb.h` 文件和 `<protobuf_name>.pb.cc` 文件。生成的文件中会将proto文件中定义的message转换为对应的类，供C++程序使用。

想要成功生成可执行文件，*需要链接protobuf的静态库和动态库* 。在Linux系统上应用使用到protobuf的C++工程，最好的方法是使用CMake。



**5.prototxt文件** （可读性强，便于调参）

`inline bool ReadProtoFromTextFile(const char *file_name, T *proto)` 从prototxt文件中读取参数的函数

**6.Proto2与Proto3的区别**

二者不兼容，详询[proto3和proto2的区别](https://blog.csdn.net/ymzhu385/article/details/122307593)

# Yaml

## ***关键是缩进***

- 缩进**只能用空格**，不能用TAB字符
- 缩进的**空格数量不重要**，但是**同一层级的元素左侧必须对齐**
- 用**#**表示注释，且仅支持单行注释
- 一个文件中可以包含多个文件的内容
  - 用“---”表示一份内容的开始
  - 用“...”表示一份内容的结束（非必需）





## 数据结构与类型

### 对象

`key: value` 使用“**冒号+空格**”来分开**键**与**值**



```yaml
key:
  child-key1: value1
  child-key2: value2 
```

支持多层嵌套（**用缩进表示层级关系**）



```yaml
key: { child-key1: value1, child-key2: value2 }
```

支持**流式风格**的语法



```yaml
?
  - keypart1
  - keypart2
:
  - value1
  - value2
```

使用**问号“?”**声明一个复杂对象，允许你使用多个词汇（数组）来组成键



## 数组

以**区块格式（Block Format）（即“破折号+空格”）**开头的数据

```yaml
values:
  - value1
  - value2
  - value3
```



**内联格式（Inline Format）**（用方括号包裹，逗号加空格分隔，类似 JSON）

```yaml
values: [value1, value2, value3]
```



**多维数组**（用缩进表示层级关系）

```yaml
values:
  -
    - value1
    - value2
  -
    - value3
    - value4
```





## 字符串

一般不需要用引号包裹，但如果字符串中**使用了反斜杠“\”开头的转义字符就必须使用引号包裹**

```yaml
strings:
  - Hello without quote # 不用引号包裹
  - Hello
   world # 拆成多行后会自动在中间添加空格
  - 'Hello with single quotes' # 单引号包裹
  - "Hello with double quotes" # 双引号包裹
  - "I am fine. \u263A" # 使用双引号包裹时支持 Unicode 编码
  - "\x0d\x0a is \r\n" # 使用双引号包裹时还支持 Hex 编码
  - 'He said: "Hello!"' # 单双引号支持嵌套"
```



**保留换行**

使用**竖线符“ | ”**来表示该语法，每行的缩进和行尾空白都会被去掉，而额外的缩进会被保留

```yaml
lines: |
  我是第一行
  我是第二行
    我是吴彦祖
      我是第四行
  我是第五行
```

**折叠换行**

使用**右尖括号“ > ”**来表示该语法，只有空白行才会被识别为换行，原来的换行符都会被转换成空格

```yaml
lines: >
  我是第一行
  我也是第一行
  我仍是第一行
  我依旧是第一行

  我是第二行
  这么巧我也是第二行
```



## 空（Null）

null”、“Null”和“~”都是空，不指定值默认也是空



## 类型转换

YAML 支持使用**严格类型标签“!!”**（双感叹号+目标类型）来强制转换类型

```yaml
!!float '666' # !! 为严格类型标签
'666' # 其实双引号也算是类型转换符
!!str 666 # 整数转为字符串
!!str 666.66 # 浮点数转为字符串
!!str true # 布尔值转为字符串
!!str yes # 布尔值转为字符串
```



## 数据重用与合并

由**锚点标签“&”**和**引用标签“\*”**组成的语法，利用这套语法可以快速引用相同的一些数据

```yaml
a: &anchor # 设置锚点
  one: 1
  two: 2
  three: 3
b: *anchor # 引用锚点
```

配合**合并标签“<<”**使用可以与任意数据进行合并（相当于c++中的继承）

```yaml
human: &base # 添加名为 base 的锚点
    body: 1
    hair: 999
singer:
    <<: *base # 引用 base 锚点，实例化时会自动展开
    skill: sing # 添加额外的属性
programer:
    <<: *base # 引用 base 锚点，实例化时会自动展开
    hair: 6 # 覆写 base 中的属性
    skill: code # 添加额外的属性
```
