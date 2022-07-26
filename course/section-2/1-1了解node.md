# 第一章 第一节 了解node.js

## 什么是node.js

node.js是一个后端开发工具，可以让js代码脱离浏览器，直接在计算机上运行。

### 安装

打开网站https://nodejs.org/zh-cn/，安装长期维护版或最新尝鲜版即可，注意win7系统可安装的最新版本为13.14.0，可以在这里查看以往的版本https://nodejs.org/zh-cn/download/releases/

安装时，一路点next即可，注意在`Tools For Native Modules`栏目中将勾打上，安装完毕后会自动打开`powershell`安装相应内容，安装内容还是挺多的，稍微等一会，不要擅自关闭

### 检查安装是否成功

win+r键打开运行窗口，输入cmd或powershell，输入node，回车即可。如果安装成功，会输出安装的node版本

## npm

在node安装时，会自动安装npm这个包管理器

### 初始化npm项目

打开一个文件夹，注意文件夹名称不能包含中文，按下shift加右键，在此处打开powershell，输入`npm init -y`即可。当然也可以输入`npm init`，然后可以自定义项目属性

### npm项目结构

npm项目包括两部分：package.json和node_modules

对于package.json，包含所有的项目属性、脚本、依赖包等，同时也会有package-lock.json，包含所有包的详细安装信息。依赖包又分为项目依赖及开发依赖两部分，其中项目依赖是用户在使用时一定会用到的包，开发依赖是在开发时必须用到的包，用户使用时不会用到，一般是转译工具及本地服务器等

对于node_modules，是所有包的源码存放地，包括类型部分和源码部分，一般不需要动

### npm install

这是npm的最常用的命令，可以安装指定npm包。例如`npm install less`，就可以在项目中安装less依赖包，之后写样式就可以直接用less代替css了。对于从别人那里下载的项目，可以使用`npm install`安装所有在package.json或package-loc.json中的依赖包

#### -g -S -D

-g是将依赖包安装至全局，例如`npm install -g nrm`，就可以把nrm安装至全局，使用nrm

-S是--save的简写，可以将依赖包安装至项目依赖

-D是--save-dev的简写，可以把依赖包安装至开发依赖。一般情况下，在不明确指明-S或-D时，依赖包会安装至项目依赖

#### 安装指定版本

使用`npm install <pkg>@x.y.z`，例如`npm install pixijs-legacy@6.0.0`即为安装pixijs-legacy的6.0.0版本

使用`npm install <pkg>@latest`安装最新版本

使用`npm install <pkg>@type`安装类型标注文件，部分包会没有类型标注文件

##### nrm

这里插一下nrm的用法，nrm是一个很好用的管理器，可以设置npm镜像位置。由于npm的默认镜像位置在美国，所以速度比较慢。因此，淘宝建立了一个在国内的npm镜像网站，每过15分钟同步一次。在nrm中设置的方法为`nrm use taobao`

#### npm run

这是npm中第二常用的命令，可以运行package.json中的脚本。

我们打开一个项目中的package.json，如下列代码

```json
{
  "name": "12",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

我们会看到scripts一项，这里就是可以运行的所有代码，运行时会在powershell中运行。例如我们输入`npm run test`，就会运行脚本中的test脚本。

#### npm常用命令参考

- `npm install`：缩写`npm i`，安装依赖包
- `npm unistall`：卸载某个依赖包
- `npm update`：更新所有或指定依赖包
- `npm test`：等于`npm run test`
- `npm init`：初始化npm项目
- `npm help`：显示帮助信息
- `npm login`：登入npm账户
- `npm logout`：退出npm账户
- `npm publish`：发布npm包
- `npm unpublish`：撤销发布

### 使用npm建立vite+vue3项目

使用`npm init vite@latest`，然后安装指示安装即可。由于powershell的背景是蓝的，所以有的选项可能看不清，甚至看不见，例如vue3+ts就看不见（悲），所以建议用cmd，用vscode也可以，使用快捷键ctrl+j可以快速呼出终端。

## pnpm

使用`npm i -g pnpm`即可安装

### 基础使用

常用命令有以下内容

- `pnpm install`：缩写`pnpm i`，等价于`npm i`，注意不带后面的包名
- `pnpm add <pkg>`：等价于`npm i <pkg>`，用于安装指定依赖包
- `pnpm update`：缩写`pnpm up`，等价于`npm update`
- `pnpm remove`：缩写`pnpm rm`，或写成`pnpm unistall`，等价于`npm unistall`
- `pnpm <script>`：也可写作`pnpm run`或`pnpm run-script`,等价于`npm run`
- `pnpm test`：等价于`npm test`
- `pnpm init`：等价于`npm init`

### 使用pnpm建立vite+vue3项目

使用`pnpm create vite`命令