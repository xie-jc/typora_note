#### 1修改npm的缓存目录和全局目录(如下目录为例)

①全局目录:npm config set prefix "D:\nodejs\node_global"   ②缓存目录:npm config set cache "D:\nodejs\node_cache"   ③测试全局变量:npm install express -g

#### 2安装cluster

命令:npm install cluster

#### 3配置npm环境变量和nodejs变量

①NODE_HOME=D:\nodejs\node_global\node_modules   ②path=D:\nodejs\node_global

③path=D:\nodejs

#### 4确认配置有效性

①进入node   ②输入:require('cluster')

#### 5将npm下载仓库改为国内(cnpm) 

命令:npm install -g cnpm --registry=http://registry.npm.taobao.org

