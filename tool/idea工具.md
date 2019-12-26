#### 1.基本配置

①启动页面->配置项目结构(jdk)   ②显示菜单栏:view->toolbar/tool buttons  ③项目退出:close project 退出程序:exit

#### 2.项目各种文件建立

①建立类/包/接口:   ②建立资源/测试文件夹:右键该文件夹->make directory as    ③项目运行(可运行类中右边有个三角符号)

#### 3.快捷键

常用快捷键(查看快捷键:螺丝刀图标->keymap ):

(1) ctrl+alt+:   ①+b 查看抽象方法实现   ②+空格 类名提示   ③+l 格式化代码   ④+o 优化导包

(2) ctrl+:  ①+. 代码提示   ②+h 查看类继承体系   ③+d 向下复制当前行   ④+y 删除当前行   ⑤+p显示参数信息   ⑥+o/+i 重写父类/接口方法     ⑦+d 快速打开类   ⑧+e显示最近编辑文件列表   ⑨+f12 显示当前文件结构

(3) alt+: ①+**shift**+up/down 上下移动当前行   ②+Insert 生成代码   ③+enter 生成局部变量、导包等   ④+up/down 方法间快速移动

(4) 模板代码:sout/psvm/**fori/iter(foreach)**

#### 4.web项目

(1) 创建:java Enterprise->选择服务器->勾选web类型

(2) 运行:选择tomcat运行

alt+o重写方法(带钥匙图标的)          引用路径(相对webapp路径):右键+copy relative path

(3) 热部署:①自带热部署:新增成员变量不会生效        ②jrebel插件:热部署,选择右边jrebel->复选框打勾     ③小扳手图标->plugin->选择插件安装方式

#### 5.工具配置

(1)配置maven

settings->build...->build tools ->maven

(2)框架配置文件模板

先决操作:右击项目名称，选择“Add framework support” 引入相关项目模板

​	①spring配置文件

​	Ⅰ、右键->new->xml config file    Ⅱ、引入xml相关约束,如在文件输入“<mvc:”,弹出相关提示

