---

---

# 1.Conda的环境管理

## 创建环境

```sh
# 创建一个名为python34的环境，指定Python版本是3.5（不用管是3.5.x，conda会为我们自动寻找3.５.x中的最新版本）
conda create --name py35 python=3.5
```

## 激活环境

```shell
# 安装好后，使用activate激活某个环境
activate py35 # for Windows
source activate py35 # for Linux & Mac
(py35) user@user-XPS-8920:~$
 # 激活后，会发现terminal输入的地方多了py35的字样，实际上，此时系统做的事情就是把默认2.7环境从PATH中去除，再把3.4对应的命令加入PATH

(py35) user@user-XPS-8920:~$ python --version
Python 3.5.5 :: Anaconda, Inc.
# 可以得到`Python 3.5.5 :: Anaconda, Inc.`，即系统已经切换到了3.５的环境
```

## 返回主环境

```shell
# 如果想返回默认的python 2.7环境，运行
deactivate py35 # for Windows
source deactivate py35 # for Linux & Mac
```

## 删除环境

```shell
# 删除一个已有的环境
conda remove --name py35 --all
```

## 查看系统中的所有环境

用户安装的不同Python环境会放在`~/anaconda/envs`目录下。查看当前系统中已经安装了哪些环境，使用`conda info -e`。

```shell
user@user-XPS-8920:~$ conda info -e
# conda environments:
#
base                  *  /home/user/anaconda2
caffe                    /home/user/anaconda2/envs/caffe
py35                    /home/user/anaconda2/envs/py35
tf                       /home/user/anaconda2/envs/tf
```

## **Conda的包管理**

## 安装库

为当前环境安装库

```shell
# numpy
conda install numpy
# conda会从从远程搜索numpy的相关信息和依赖项目
```

## 查看已经安装的库

```shell
# 查看已经安装的packages
conda list
# 最新版的conda是从site-packages文件夹中搜索已经安装的包，可以显示出通过各种方式安装的包
```

## 查看某个环境的已安装包

```shell
# 查看某个指定环境的已安装包
conda list -n py35
```

## 搜索package的信息

```shell
# 查找package信息
conda search numpy
Loading channels: done
# Name                  Version           Build  Channel             
numpy                     1.5.1          py26_1  pkgs/free           

...

numpy                    1.15.1  py37hec00662_0  anaconda/pkgs/main  
numpy                    1.15.1  py37hec00662_0  pkgs/main
```

## 安装package到指定的环境

```shell
# 安装package
conda install -n py35 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装
```

## 更新package

```shell
# 更新package
conda update -n py35 numpy
```

## 删除package

```shell
# 删除package
conda remove -n py35 numpy
```

## 更新conda

```shell
# 更新conda，保持conda最新
conda update conda
```

## 更新anaconda

~~~shell
# 更新anaconda
conda update anaconda
 ```
### 更新Python
~~~

## 更新python

conda update python

## 假设当前环境是python 3.5, conda会将python升级为3.5.x系列的当前最新版本

## **设置国内镜像**

因为[http://Anaconda.org](http://anaconda.org/)的服务器在国外，所有有些库下载缓慢，可以使用清华Anaconda镜像源。 网站地址: [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)



## Anaconda　

镜像 Anaconda 安装包可以到 https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/ 下载。 TUNA还提供了Anaconda仓库的镜像，运行以下命令：



```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ 
conda config --set show_channel_urls yes
```



即可添加 Anaconda Python 免费仓库。

运行 `conda install numpy` 测试一下吧。

## Miniconda　镜像

Miniconda 是一个 Anaconda 的轻量级替代，默认只包含了 python 和 conda，但是可以通过 pip 和 conda 来安装所需要的包。

Miniconda 安装包可以到 https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/ 下载。





# 2.webpack项目环境的搭建和react的简单封装

首先查看node.js是不是10以上

```css
node -v
1
```

## 项目搭建

**第一步** ：新建一个文件夹 为 react-stack
**第二步**： 在文件夹里面打开命令行 输入一下的指令

```css
npm install -y  生成 package.json文件

//安装webpack 项目依赖和全局都要安装
cnpm install webpack -g
cnpm install webpack-cli -g

cnpm install webpack -D
cnpm install webpack-cli -D
12345678
```

## 创建一个配置文件 webpack.config.js

1 设置入口文件:entry选项
2 设置出口:output选项
代码如下：

```css
const path = require('path')
const webpack = require('webpack')
module.exports = {
    mode: 'production',
    // 入口:指定webpack打包或本地服务运行时的程序入口文件
    // entry: './src/main.js'
    entry: path.resolve(__dirname, './src/main.js'),
    // 出口:打包之后,打包的结果放在哪里 dist
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
  }  
12345678910111213
```

## 在package.json文件里配置打包文件

```css
"build": "webpack --config webpack.config.js",
1
```

**打包命令: webpack --config xxx.config.js**

## 使用pulgins

**1、html-webpack-plugin
它的作用是自动生成一个index.html单页面，并且把打包后.js脚本文件插入进去。**

**安装命令**

```css
  cnpm install html-webpack-plugin -D
1
```

## 在webpack.config.js 配置

```css
 // plugins:用于扩展功能
    plugins: [
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, './public/index.html'),
            title: 'react'
        }),
        new CleanWebpackPlugin(),
        // 用于热更新功能
        new webpack.NamedModulesPlugin(),
        new webpack.HotModuleReplacementPlugin()
    ],
1234567891011
```

**2、clean-webpack-plugin
它的作用是自动删除目录中的dist文件夹，无需手动操作了**

## 搭建devServer

**安装命令**

```css
cnpm install webpack-dev-server -D
cnpm install webpack-dev-server -g
12
```

## 在webpack.config.js 配置

```css
    devServer: {
        port: '8090',
        open: true,
        contentBase: path.resolve(__dirname, 'public'),
        hot: true  // 开启热更新功能
    }
123456
```

## 开启HMR热更新功能

**HMR的作用是：局部代码发生变化时，不用刷新整个页面（重新编译）即可自动更新，速度比较快。**
1.在devServer中添加 **hot：true**
2，引入webpack模块 添加插件

## 使用css和scss

**安装命令**

```css
cnpm install style-loader -D
cnpm install css-loader -D
cnpm istall sass-loader -D
cnpm install node-sass -D
1234
```

## 在webpack.config.js 配置

```css
module:{
        rules:[
            {test:/\.(css|scss)$/, use:['style-loader','css-loader','sass-loader']}

        ]
    },
123456
```

在安装node-sass的时候很容易安装不上 当你第二次安装的时候安装上了 运行的时候可能会报错，这时候你只要把node_modules的依赖包删除重新 安装这样就可以解决的

## 使用JSBabel

JS编译器，把ES6(下一代ECMAScript)转化成浏览器能够兼容的ES5代码
安装命令：

```css
cnpm install babel-loder -D
cnpm install @babel/core -D
12
```

**配置**

```css
rules: [
    {test:/\.js$/, use:['babel-loader'], exclude: /node_modules/}
]
123
```

## 使用ESLint

[ESLint地址](https://eslint.bootcss.com/docs/user-guide/getting-started)
**安装**

```css
cnpm install eslint-loader -D
cnpm install eslint -D
12
```

**配置**

```css
rules: [
{test:/\.js$/, use:['eslint-loder',], exclude:/node_modules/, enforce:'pre'}
]
123
```

[ExtractTextWebpackPlugin](https://www.webpackjs.com/plugins/extract-text-webpack-plugin/)
**注意：要求git仓库中去找**

**安装**

```css
cnpm install mini-css-extract-plugin -D
1
```

[插件地址](https://github.com/webpack-contrib/mini-css-extract-plugin)

**配置**

```css
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
rules: [
      {
        test: /\.css$/i,
        use: [MiniCssExtractPlugin.loader, 'css-loader'],
      },
    ],
1234567
```

## 新建一个.exlintrc.json的文件

```css
{
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true
        }
    },
//在rules里面可以设置禁止使用的代码
    "rules": {
    }
}
123456789101112
```

## 生产环境和开发环境的分布

**安装插件**

```css
cnom install cross-env -D
1
```

[插件地址](https://www.npmjs.com/package/cross-env)

## 在package.json里面配置cross-nev NODE_ENV=production

```css
{
  "scripts": {
    "build": "cross-env NODE_ENV=production webpack --config webpack.config.js",
    "serve": "cross-env NODE_ENV=development webpack-dev-server --config webpack.config.js",
  }
}
123456
```

**production: 生产环境
development:开发环境
根据cross-env NODE_ENV=production 来区别开发环境和生产环境**

## react组件的分装

**第一步：先安装Babel插件**
[插件的地址](https://www.babeljs.cn/docs/babel-preset-env)

```css
cnpm install @babel/preset-react -D 支持jsx语法的babel插件
cnpm install @babel/preset-env -D  支持ES6中较新的语法
12
```

**第二步：创建.baberlrc.json的文件配置**

```css
{
    "presets": [
      ["@babel/preset-react"],
      ["@babel/preset-env",{"useBuiltIns": "entry"}]
    ]
  }
123456
```

**第三步：封装组件**

```css
//引入react
import React from 'react'

//定义react的根组件
export defulat class App extends React.component{
      constructor(props){
            super(props)
           }
         render (){
            return (
             <div>
             <h1> 你好！ </h1>
             </div>
            )
          }  
}

1234567891011121314151617
```

**第四步：把封装好的组件渲染到真实的DOM上**

```css
//引入
 import React from 'react'
 import ReactDOM from 'react-dom'
 ReactDOM.render(< App  /> , document.getElementById('root'))
```
