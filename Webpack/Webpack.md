# Webpack

 

## 建立package.json 指令

```
npm init
```



## 安裝webpack 指令

```
npm install webpack webpack-cli --save
npm install webpack webpack-cli --save-dev
```



## 建立`src資料夾` `dist資料夾`

### src

#### helper.js

```js
export default{
    fn1(){
        console.log('this is helper fn')
    }
}
```

#### main.js

```js
import helper from './helper'

helper.fn1()
```



### dist

#### index.html

```html
<script src="main.bundle.js"></script>
```





## 建立webpack.config.js

```javascript
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.bundle.js'
  }
};
```



## 修改package.json檔

### 加入 `build` 設定

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
```



## 開始build

```
npm build
```



## 支援打包css

### 安裝指令

```
npm install style-loader --save
```

### 加入 style.css

```css
body{
    background-color: green;
}
```

### 修改main.js

```js
import helper from './helper'
import './style.css'
helper.fn1()
```



### 修改webpack

```json
module.exports = {
  ...
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
    ],
  },  
};
```



### 執行build

我們會發現在css的相關語法已經轉成js打包在main.bundle.js 裡面

參考：[npm css loader](https://www.npmjs.com/package/css-loader)





## 支援打包scss

### 安裝指令

```
npm install sass-loader sass webpack --save-dev
```

### 加入 all.scss

```scss
$body-color: red;

body {
  background-color: $body-color;
}
```



修改webpack.js

```js
  module: {
    rules: [
      {
		...
      },
      {
        test: /\.s[ac]ss$/i,
        use: [
          // Creates `style` nodes from JS strings
          "style-loader",
          // Translates CSS into CommonJS
          "css-loader",
          // Compiles Sass to CSS
          "sass-loader",
        ],
      },      
    ],
  },  
```



如果要找image ,  一樣的概念尋找 image loader 關鍵字進行安裝



## webpack dev server 安裝

```
npm install webpack-dev-server --save
```



### 修改webpack.config.js

```js
module.exports = {
  mode: 'development',
  ...
  ...
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    compress: true,
    port: 9000,
  },     
}
```



### 修改package.json

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack server --open",
    "build": "webpack"
  }
```



## mode差異

mode:'development'

未壓縮

mode:'production'

壓縮過



執行指令

```
npm start
```





## html-webpack-plugin

### 安裝指令

```
 npm install --save-dev html-webpack-plugin
```



### 修改webpack.config.js

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  ... 
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.[hash].bundle.js'
  },
  plugins: [new HtmlWebpackPlugin()],
}
```



我們可以透過這個插件，在dist資料夾底下自動產生index.html ，並且配上hash方法，讓每次js名稱都有所不同，避免每次佈署時的緩存問題



### 樣版功能

修改webpack.config.js

```js
  plugins: [new HtmlWebpackPlugin({
    template:'./src/base.html'
  })],
```



新增base.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kite</title>
</head>
<body>
    <header>kite blog</header>
</body>
</html>
```



npm run build 產生的index.html 會依照這份樣版進行複製產生，並加入index.bundle.js 



## MiniCssExtractPlugin



修改webpack.config.js

```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
	...
    plugins: [new HtmlWebpackPlugin({
        template:'./src/base.html'
    }),
    
    new MiniCssExtractPlugin({
    filename:'main.[hash].css'
    })
              
    ...    
    module: {
        rules: [
          {
            test: /\.css$/i,
            use: [MiniCssExtractPlugin.loader, "css-loader"],
          },
          {
            test: /\.s[ac]ss$/i,
            use: [
              // Creates `style` nodes from JS strings
              MiniCssExtractPlugin.loader,
              // Translates CSS into CommonJS
              "css-loader",
              // Compiles Sass to CSS
              "sass-loader",
            ],
          },      
        ],
    },   
    
}
```



透過這個外掛，可以讓css獨立打包成一個檔出來，不會轉譯成以js寫出的css





接續看

https://youtu.be/uP6KTupfyIw?t=4204



## 參考網站

[npm trends](https://www.npmtrends.com/)







為什麼要webpack

轉譯套件成js、html、css

壓縮

用套件工具輕鬆達到不同瀏覽器的前綴語法
