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



執行指令

```
npm start
```



## 參考網站

[npm trends](https://www.npmtrends.com/)



