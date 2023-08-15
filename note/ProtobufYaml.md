# Protobuf&Yaml

## Protobuf ##

**1.proto文件示例** 

`// import "other_protos.proto"; // 如果需要引用其它的protobuf文件，可以使用import语句。` 

`syntax = "proto3"; // 指定protobuf遵循的语法格式是proto2还是proto3。在本教程和之后的开发中，我们都使用proto3语法格式。`  
`package student; // 包名声明。如在本例中，proto文件生成的类都会被放在namespace student中，这一举措的意义在于防止命名冲突 ` 

`enum Sex // 自定义枚举类型
{
    MALE = 0;
    FEMALE = 1;
}` 

`message Course // protobuf中，使用message定义数据结构，类似于C中的结构体
{
    int32 credit = 1;
    string name = 2;
}` 

`message StudentInfo
{
    // 变量声明格式 <限定修饰符> <数据类型> <变量名>=id
    int32 age = 1;
    string name = 2;
    Sex sex = 3;
    repeated Course courses = 4; // repeated表示重复（数组），本例也表明message可以嵌套message
}`  

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



## Yaml ##

简单看看





