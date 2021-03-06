#### 程序包编译安装：
**testapp-VERSION-release.src.rpm --> 安装后，使用rpmbuild命令制作成二进制格式的rpm包，而后再安装**

**源程序从获取到使用的过程：**
源代码 --> 预处理 --> 编译(gcc) --> 汇编（汇编器） --> 链接（链接器） --> 执行

##### 源代码组织格式：
多文件：文件中的代码之间，很可能存在跨文件依赖关系；
C、C++项目管理器： make (configure --> Makefile.in --> makefile)
java项目管理器： maven

##### C代码编译安装三步骤：
* **./configure：**
  (1) 通过选项传递参数，指定启用特性、安装路径等；执行时会参考用户的指定以及Makefile.in文件生成makefile；
  (2) 检查依赖到的外部环境；
* **make：**
  根据makefile文件，构建应用程序；
* **make install**

##### 开发工具：
- autoconf: 生成configure脚本
- automake：生成Makefile.in

 **建议：安装前查看INSTALL，README**

#### 开源程序源代码的获取：
**官方自建站点：**
[apache.org](http://apache.org/) (ASF)
[mariadb.org](http://mariadb.org/)
...
**第三方组织代码托管站点：**
SourceForge
[Github.com](http://github.com/)
[code.google.com](http://code.google.com/)

#### c/c++编译器: gcc (GNU C Complier)
##### 编译C源代码：
>前提：提供开发工具及开发环境
>开发工具：make, gcc等
>开发环境：开发库，头文件
>glibc：标准库

>通过“包组”提供开发组件
>CentOS 6: "Development Tools", "Server Platform Development"

- **第一步：configure脚本**
  选项：指定安装位置、指定启用的特性
  --help: 获取其支持使用的选项
  **选项分类：**
  安装路径设定：
  --prefix=/PATH/TO/SOMEWHERE: 指定默认安装位置；默认为/usr/local/
  --sysconfdir=/PATH/TO/SOMEWHERE：配置文件安装位置；
  **System types:**
  Optional Features: 可选特性
  --disable-FEATURE
  --enable-FEATURE[=ARG]
  Optional Packages: 可选包
  --with-PACKAGE[=ARG]
  --without-PACKAGE

- **第二步：make**
- **第三步：make install**

##### 安装后的配置：
(1) 导出二进制程序目录至PATH环境变量中；
编辑文件`/etc/profile.d/NAME.sh`
`export PATH=/PATH/TO/BIN:$PATH`

(2) 导出库文件路径
编辑/`etc/ld.so.conf.d/NAME.conf`
添加新的库文件所在目录至此文件中；
让系统重新生成缓存：
`ldconfig [-v]`

(3) 导出头文件
基于链接的方式实现：
`ln -sv`

(4) 导出帮助手册
编辑`/etc/man.config`文件
添加一个MANPATH