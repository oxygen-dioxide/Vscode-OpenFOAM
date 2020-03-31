# Vscode-OpenFOAM

### 介绍
使用vscode进行OpenFOAM编程的配置

### 说明
- 首先搜索扩展`c/c++`安装如下的C++扩展：

![cpp](https://images.gitee.com/uploads/images/2020/0331/202955_2c084abc_6577728.png "cpp.png")

- 打开工作文件夹，即你的OpenFOAM求解器存放的文件夹，按住`shift+ctrl+p`开启命令框，输入`c/c++:conf`后选择如图的第二条命令，生成`.vscode/c_cpp_properties.json`

<img
src="https://images.gitee.com/uploads/images/2020/0331/203011_4ee99ad6_6577728.png" alt="1" title="1.png" style="zoom:67%;" />

- 打开`Make/options`，可以看到所有需要包含的头文件，以`-I`开头

![](https://images.gitee.com/uploads/images/2020/0331/203020_30aea035_6577728.png)

值得注意的是，其中的`$(LIB_SRC)`所指的地址就是OpenFOAM源代码路径。如果你不知道这个路径，终端下执行

```
src
pwd
```
打印出的内容就是`$LIB_SRC`

- 接着把完整路径放到C++配置文件的`includePath`中：

<img
src="https://images.gitee.com/uploads/images/2020/0331/203027_f031cbf3_6577728.png" alt="3" title="3.png" style="zoom:67%;" />

注意每条路径用`" "`括起来，行末加`,`（最后一行路径除外）

- 接下来还有一些小工作要做，先`wmake`求解器，你会看到下面的输出：

<img
src="https://images.gitee.com/uploads/images/2020/0331/203037_0efc8c8c_6577728.png" alt="4" title="4.png" style="zoom:67%;" />

第一个参数`g++`说明`wmake`使用g++编译器，因此将g++的路径替换`compilerPath`中的内容，不知道g++路径？终端里`which g++`得到。后面`-std = c++11 -m64 ... -ftemplate-depth-100`是`compilerArgs`，大部分是规定了编译过程错误信息输出以及优化信息，还有一些尚不明确，你可以将他们都加到`compilerArgs`里

<img
src="https://images.gitee.com/uploads/images/2020/0331/203042_115e5a24_6577728.png" alt="5" title="5.png" style="zoom:67%;" />

- 最终效果：

<img
src="https://images.gitee.com/uploads/images/2020/0331/203051_8a133d47_6577728.png" alt="6 " title="6.png" style="zoom:67%;" />

自动补全，代码提示、跳转都正常

-----

### NOTE
由于OpenFOAM”特殊“的编程风格，常在头文件中写代码段而不是类声明等常规写法，会导致报错，比如`Info`的`ambigous`错误提示，目前没有解决方法

OpenFOAM的`.C .H`后缀可能使得Vscode识别语言类型错误，可以在`.vscode`下创建`setting.json`设置类型绑定，具体方法在网上很容易找到

如果是wsl用户，可以使用wsl插件在vscode中调用bash，上述操作均在vscode连接Ubuntu后进行

<img
src="https://images.gitee.com/uploads/images/2020/0331/203004_6b3a9480_6577728.png" alt="wsl" title="wsl.png"  />

如果遇到问题请发起`issue`

----

### LICENSE

本内容基于CC-BY-4.0 协议，转载请注明出处