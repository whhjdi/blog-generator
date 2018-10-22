---
title: learn-webpack4（二）
date: 2018-10-21 12:44:06
tags: [webpack]
---
# 多页面解决方案
对于webpack4提取公共代码需要用到optimization.splitChunks配置
## 提取公共代码
pageA和pageB俩个入口文件，都引入了subPageA,subPageB和lodash。
俩个sub文件又都引入了module.js
具体代码看demo

## webpack配置

```json
{
  "name": "webpack4",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack --config webpack.config.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.15.1",
    "webpack-cli": "^3.1.2"
  },
  "dependencies": {
    "lodash": "^4.17.11"
  },
  "description": ""
}
```
```javascript
const webpack = require("webpack");
const path = require("path");

module.exports = {
  // 多页面应用
  entry: {
    pageA: "./src/pageA.js",
    pageB: "./src/pageB.js"
  },
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "[name].bundle.js",
    chunkFilename: "[name].chunk.js"
  },
  optimization: {
    splitChunks: {
      cacheGroups: {
        // 注意: priority属性设置，使第三方库先被打包提取
        // 其次: 打包业务中公共代码
        common: {
          name: "common",
          chunks: "all",
          minSize: 1,
          priority: 0
        },
        // 首先: 打包node_modules中的文件
        vendor: {
          name: "vendor",
          test: /[\\/]node_modules[\\/]/,
          chunks: "all",
          priority: 10
        }
      }
    }
  }
};
```
npm start打包之后，在dist目录生成了4个文件，然后在html中引入
```javascript
  <script src="./dist/common.chunk.js"></script>
  <script src="./dist/vendor.chunk.js"></script>
  <script src="./dist/pageA.bundle.js"></script>
  <script src="./dist/pageB.bundle.js"></script>
```