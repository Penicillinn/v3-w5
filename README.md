### 创建项目文件夹
```
$ mkdir webpackDemo
```
### 生成初始化的package.json
```
$ npm init -y
```
### 安装webpack依赖
```
npm install webpack webpack-cli -D
```
### 在根目录新建webpack配置文件-- webpack.config.js

## 入口和出口
```
module.exports = {
  entry: './src/app.js', // 打包入口文件
  output: {
    path: path.resolve(__dirname,'dist'), // 打包好的文件放的位置
    filename: 'bundle.js' // 打包好的文件名
  },
}
```
## 插件
```
clean-webpack-plugin // 每次打包的时候都会删掉之前的dist目录

html-webpack-plugin  // 会在打包好的目录下生成一个html，并且自动将打包好的js文件引入

webpack-dev-server // npm start 的时候会在本地起一个服务器，并且把打包好的资源放到服务器上，当我们去访问本地服务的地址的时候，就相当于打开的了html文件，该文件中自动引入了打包好的并且放在了本地服务器上的js文件
```
## loader
```
// webpack 默认只会打包.js文件，如果在打包的过程中遇到了其他后缀名结尾的文件，就会报错，此时我们需要告诉webpack用什么样的loader去处理该类型的文件
```
### 修改npm脚本命令之后 运行npm run bundle 就可以正常打包了
```
  "bundle": "webpack",
  "start": "webpack serve",
```

## webpack.config.js
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');
const { VueLoaderPlugin } = require('vue-loader/dist/index'); // vue3.0

module.exports = {
  entry: './src/app.js',
  output: {
    path: path.resolve(__dirname,'dist'),
    filename: 'bundle.js'
  },
  // loader
  module: {
    rules: [
      {
        test: /\.vue$/,
        use: ['vue-loader']
      },
      {
        test: /\.css$/,
        use: ['style-loader','css-loader']
      }
    ]
  },
  // plugin
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new CleanWebpackPlugin(),
    new VueLoaderPlugin(),
  ],
  devServer: {
    port: 9990,
    proxy: {
      'api': {
        target: 'localhost:9090'
      }
    }
  }
}
```
## package.json
```
{
  "name": "vue3-demo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "bundle": "webpack",
    "start": "webpack serve"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@vue/compiler-sfc": "^3.0.5",
    "clean-webpack-plugin": "^3.0.0",
    "css-loader": "^5.0.1",
    "html-webpack-plugin": "^4.5.1",
    "style-loader": "^2.0.0",
    "vue-loader": "^16.1.2", // vue3.0
    "webpack": "^5.18.0",
    "webpack-cli": "^4.4.0",
    "webpack-dev-server": "^3.11.2"
  },
  "dependencies": {
    "vue": "^3.0.5"
  }
}

```
