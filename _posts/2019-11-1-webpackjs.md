---
	layout:     post                  #不要管他
title:      webpack     #标题
subtitle:   webpack.js              #别名,简介,标题下面的那一行字
date:       2019-11-1            #发表时间
author:     Zhaolai                    #作者
header-img: img/post-bg-rwd.jpg   #背景图片
catalog: true                     #导航目录,不要管他
original: true                    #是否原创申明
tags:                             #标签,可以有多个
    - webpack.js
    - 前端
    - Js安装
---

## 安装

```js
"devDependencies": {
    "webpack": "^4.41.2"
}
```

## webpack.config.js配置

#### entry入口

单一入口

```js
const config = {
  entry: './path/to/my/entry/file.js'
};
// 就是下面对象语法的简写
const config = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
module.exports = config;
```

传入数组就会创建多个主入口

```js
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

#### output输出

只能有一个输出的配置

```js
const config = {
  output: {
      // 文件名, 可以使用占位符'[name].js'代表多入口文件
    filename: 'bundle.js',
    // 文件路径,  __dirname + '/dist'使用拼接方式
    path: '/home/proj/public/assets'
  }
};

module.exports = config;
```

#### mode模式

```js
module.exports = {
  // 'development'
  mode: 'production'
};
```

#### loader转换

安装对应的解释器

```cli
// css
npm install --save-dev css-loader
// TypeScript
npm install --save-dev ts-loader
```

使用

```js
module: {
    rules: [{
        // css文件
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
    }, {
        // 图片
        test: /\.(png|svg|jpg|gif)$/,
        use: ['file-loader']
    }, {
        // 字体文件
        test: /\.(woff|woff2|jpg|gif)$/,
        use: ['file-loader']
    }, {
        // 常量
        test: /\.(csv|tsv)$/,
        use: ['csv-loader']
    }, {
        // 常量
        test: /\.xml$/,
        use: ['xml-loader']
    }]
}
```

#### plugins插件

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
const webpack = require('webpack'); //访问内置的插件

const config = {
    plugins: [
        // 清清除多余文件
        new CleanWebpackPlugin(),
        // 更改html的连接
        new HtmlWebpackPlugin({
            title: "Webpack App"
        }),
        // 热替换
        new webpack.NamedModulesPlugin(),
        new webpack.HotModuleReplacementPlugin(),
        // 防止加载重复
        new webpack.optimize.SplitChunksPlugin({
            name: 'common'
        })
    ]
};

module.exports = config;
```

DevServer服务器

```js
const config = {   
    devServer: {
        // 路径
        contentBase: './dist',
        // 热替换
        hot: true
    },
};
```

## package.json配置

#### script操作

```json
{  
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        // 打包
        "build": "webpack",
        // 开启服务器
        "start": "webpack-dev-server --open"
    },
}
```

#### sideEffects

有影响的文件, 防止压缩时被删除

```json
{  
    "sideEffects": [
        "*.css",
        "./src/some-side-effectful-file.js"
    ],
}
```

