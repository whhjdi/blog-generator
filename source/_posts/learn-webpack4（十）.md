---
title: learn-webpack4（十）
date: 2018-10-19 17:38:50
tags: [webpack]
---

# 自动清理dist目录（clean plugin）&& watch mode

## webpack配置

把第一个例子搬过来用.
注意webpack是倒叙的，所以把CleanWebpackPlugin，放到最后
```javascript
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const CleanWebpackPlugin = require("clean-webpack-plugin");

const path = require("path");

module.exports = {
  entry: {
    app: "./app.js"
  },
  output: {
    publicPath: __dirname + "/dist/", // js引用路径或者CDN地址
    path: path.resolve(__dirname, "dist"), // 打包文件的输出目录
    filename: "[name]-[hash:5].bundle.js",
    chunkFilename: "[name]-[hash:5].chunk.js"
  },
  plugins: [
    new HtmlWebpackPlugin({
      filename: "12.html",
      template: "./12.html",
      chunks: ["app"]
    }),
    new CleanWebpackPlugin(["dist"])
  ]
};
```

### watch mode
```bash
npx webpack --watch
<!-- 监听到变化就会重新打包 -->
npx webpack -w --progress --display-reasons --color
<!-- 显示详细的打包过程 -->
```