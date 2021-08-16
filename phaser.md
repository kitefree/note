# Phaser 教學

## Phaser 是什麼

- 一個快速、免費、開源的H5遊戲框架
- 支持WEBGL和Canvas兩種渲染方式，並支持桌面和移動web瀏覽器
- 甚至可以使用第三方工具編譯打包成ios、android和桌面app
- phaser CE 與 phaser3



## Phaser 可以做什麼

- 2d遊戲開發
- 推廣活動



## Phaser 特色

![image-20210618124036875](https://i.imgur.com/CbcIrlz.png)

## Game

### Game的創建

![image-20210618124206803](https://i.imgur.com/xYE0xEB.png)



```javascript
new Game({
	width:375,
    height:667,
    renderer:Phaser.AUTO,
    parent:"",
    transparent:false,
    antialias:true,
    physicsConfig:null
})
```



### Game工作原理

![image-20210618131753257](https://i.imgur.com/WSS023c.png)



### Game中的子系統

1. 資源加載系統
2. 場景系統
3. 物理引擎
4. 聲音系統
5. 輸入系統
6. 粒子系統





## 常見遊戲元素

- 視覺
  - 圖片
  - 聲音

遊戲渲染方式

- 可以通過DOM實現

- CANVAS

  中小型都可以

- WEBGL

  性能大約是CANVAS 3到5倍，可以使用到GPU，3D性

- 文字

- 事件

  

## 遊戲中的資源

1. 圖片與圖片集
2. 聲音
3. 字體
4. 視頻



### 圖片

```javascript
game.load.image('logo','logo.png')
```

![](http://i.imgur.com/FgfF8SD.png)

### 圖片集

1維

```javascript
game.load.spritesheet('sheetImg','s37x45.png',37,45,18)
```

變數名,路徑,寬,高,圖片數量



2維

```javascript
game.load.atlasXML('xmlimg','/xml.png','/data.xml')
game.load.atlasXML('jsonimg','/json.png','/data.json')
```

![image-20210618132120289](https://i.imgur.com/VI8GfBn.png)

### 字體

```javascript
game.load.bitmapFont('cedFont','/cedFont.png','/cedFont.xml')
```

### 聲音

```javascript
game.load.audio('cedmusic','/music.mp3')
```

### 視頻

```javascript
game.load.video('cedvideo','/video.mp4')
```



## 遊戲資源加載原理

![image-20210618133243059](https://i.imgur.com/7ygJbj4.png)



### 遊戲中資源加載回調事件

| 事件名稱             | 說明         |
| -------------------- | ------------ |
| onFileStart          |              |
| onFileError          |              |
| onFileComplete       |              |
| onLoadStart          |              |
| onBeforeLoadComplete | 只會執行一次 |
| onLoadComplete       | 只會執行一次 |



```javascript
preload() {
    //加载资源
    game.load.image("logo", "/assets/images/logo.png");
    game.load.image("bgload", "/assets/images/bgload.jpg");
    game.load.spritesheet("s37x45", "/assets/learn/s37x45.png", 37, 45, 18);
    game.load.atlasXML('xmlImg', '/assets/learn/xml.png', '/assets/learn/data.xml');
    game.load.atlas('jsonImg', '/assets/learn/json.png', '/assets/learn/data.json');
    game.load.audio('cedAudio', '/assets/learn/cedAudio.mp3');
    game.load.bitmapFont('cedFont', '/assets/learn/cedFont.png', '/assets/learn/cedFont.xml');

    //设置并行下载个数
    game.load.maxParallelDownloads = 1;

    game.load.onFileStart.add((progress, key, url) => {
        console.log("ced--onFileStart--" + progress + "--" + key + "--" + url)
    }, this);
    game.load.onFileError.add((key, file) => {
        console.log("ced--onFileError--" + key + "--" + JSON.stringify(file))
    }, this);
    game.load.onFileComplete.add((progress, key, success, totalLoad, total) => {
        console.log("ced--onFileComplete--" + progress + "--" + key + "--" + success + "--" + total)
    }, this);

    game.load.onLoadStart.add(() => {
        console.log("ced--onLoadStart--")
    }, this);
    game.load.onBeforeLoadComplete.add(() => {
        console.log("ced--onBeforeLoadComplete--")
    }, this);
    game.load.onLoadComplete.add(() => {
        console.log("ced--onLoadComplete--")
    }, this);
}
```



## 顯示對象

| 類型 |          |
| :--- | -------- |
| 圖片 | Image    |
| 精靈 | Sprite   |
| 文本 | Text     |
| 圖形 | Graphics |

### image

![image-20210618134347670](https://i.imgur.com/WpD4B5f.png)



#### 1. 坐標

```javascript
var cedImage = game.add.image(0,0,"s37x45",1);
cedImage.position.set(game.world.centerX,30);
```



#### 2. 大小

```javascript
cedImage.width = 200;
cedImage.height = 200;
```



#### 3. 縮放

```javascript
cedImage.scale.set(2,2);
```



#### 4. 錨點

```javascript
cedImage.anchor.set(0.3,0.3);
```

![img](https://i.imgur.com/G5nt7XB.png)

0,0 

圖片的左上角

1,1

圖片的右下角

0.5,0.5

圖片的中心，也是比較常見的設法

#### 5. 旋轉

```javascript
cedImage.rotation  = 200
```



#### 6. 透明度

```javascript
cedImage.alpha = 0.5
```



#### 7. 遮照

```javascript
var gmask = game.add.graphics(130,130);
gmask.beginFill(0xffffff,1);
gmask.drawRect(0,0,50,50);
gmask.endFill();
cedImage.mask=gmask;
```



#### 8. 事件

```javascript
cedImage.inputEnabled = true;
cedImage.events.onInputDown.add(function(){
	console.log("in down")
},this);

cedImage.events.onInputUp.add(function(){
	console.log("in up")
},this);
```



### Sprite

image 的功能在sprite 都有，差在多了2個功能`動畫` `物理引擎`

#### 何時該使用sprite ? image?

不需要動畫的時候還是用image，在效能上使用資源較少

```javascript
var cedImage = game.add.sprite(0,0,"s37x45",1);
```

### Text

```javascript
var text = game.add.text(30, 125, "hello world webpack",
{
    fill: '#fff',
    fontWeight: 100,
    fontSize: '20px',
    backgroundColor: "red",
    wordWrap: true,
    wordWrapWidth: 20,
    align: 'right',
    stroke: '#00000',
    strokeThickness: 3
});
```



### Graphics

![image-20210618141053352](https://i.imgur.com/zCdLgvY.png)



```javascript
var graphics = game.add.graphics(150, 200)

/**常用api
 *
 *
 * lineStyle(width, color, alpha);描边样式
 *
 * beginFill(color, alpha);填充样式
 * endFill();
 *
 * moveTo(x, y) 移动画笔到
 * lineTo(x, y) 直线
 *
 * drawCircle(x, y, diameter);圆形
 * drawEllipse(x, x, halfWidth, halfHeight)椭圆
 * arc(x, y, radius) 弧形
 *
 * drawRect(x, y, width, height)矩形
 * drawPolygon(path)多边形，参数是多边形顶点的数组
 * */
graphics.moveTo(0, 0);
graphics.lineStyle(2, 0xffffff, 1);
graphics.lineTo(200, 0)

//描边样式
graphics.lineStyle(2, 0x000000, 1)
//填充样式
graphics.beginFill(0xffffff, 1);
graphics.drawCircle(0, 30, 60);

//描边样式
graphics.lineStyle(2, 0xffffff, 1)
//填充样式
graphics.endFill();
graphics.beginFill(0x000000, 1);
graphics.drawRect(0, 60, 100, 80)
graphics.endFill();
```



### 顯示對象容器

![image-20210618141147334](https://i.imgur.com/8W7ZNnZ.png)

容器的好處，分組修改對象



#### 相關操作

```javascript
//组
var group = game.add.group();

//组中添加元素
var gi1= game.add.image(0,0,"jsonImg",21,group)
var gi2= game.make.image(100,0,"jsonImg",2);
group.add(gi2);

var gs1 = group.create(0, 300, "jsonImg", 3);
var gs2 = group.create(100, 300, "jsonImg", 22);

//调节顺序
group.bringToTop(gs1);
group.swap(gs1, gs2);

//删除存在的对象
group.remove(gs1, true);

//整體調整 透明
group.alpha = 0.5;
//整體調整 坐標
group.y = 100;
//添加子组
var groupChild = game.add.group(group);
groupChild.x = 100;
groupChild.y = 400;
var gc2 = groupChild.create(0, 0, "jsonImg", 2);
```

#### 常用顯示對象容器

- Text
- Image
- Sprite
- Group

#### 世界坐標、組坐標

當group 被加到world底下，那它的坐標自然就是世界坐標

group1下加了一個group2，那group2的坐標就是對應於group1底下的組坐標。而這個group2的世界坐標相當於group1世界坐標加上group2組坐標



## 渲染對象列表

![image-20210618164310716](https://i.imgur.com/HWzmTLP.png)

根容器 Stage

Game 遍歷所有元素

先渲染的就在圖層的最下面，後渲染的就會覆蓋在上一層



#### stage是什麼

- 顯示對象容器
- 是有大小和顯示效果的



#### world是什麼

- 顯示對象容器
- 是有大小，而且任意大小



#### 圖解渲染

![image-20210618164432662](https://i.imgur.com/UWeLdnZ.png)



![image-20210618164441634](https://i.imgur.com/2R7Y8a4.png)



![image-20210618164450650](https://i.imgur.com/QecFqZ7.png)



![image-20210618164458787](https://i.imgur.com/N4omwoN.png)



#### 世界很大，移動畫布問題

如果每一次都要移動world 去到stage、canvas，那計算坐標肯定會瘋掉

![image-20210618164515547](https://i.imgur.com/Et3Id9K.png)



![image-20210618164537230](https://i.imgur.com/lAXlVZc.png)



#### 使用camera

使用camera的概念去移動攝影機

![image-20210618164556971](https://i.imgur.com/NOS3aNV.png)



```javascript
//设置背景颜色
game.stage.backgroundColor = "#a8d4bf";

// 设置世界的大小
game.world.setBounds(0, 0, 1500, 667);

//创建两个图片
var gi1 = game.add.image(0, 0, "jsonImg", 21)
var gi2 = game.add.image(380, 0, "jsonImg", 21)


//移动摄像机
game.camera.x = 50;
```



## State

### state創建方式

共3種寫法

```javascript
var state1={
	preload:function(){},
	create:function(){},
	update:function(){},
	render:function(){},    
}
```

```javascript
var state2= function(){
	this.preload(){}
	this.create(){}
	this.update(){}
	this.render(){}
}
```

```javascript
state3 class extends Phaser.State{
	preload(){}
	create(){}
	update(){}
	render(){}
}
```



### state使用方式

```javascript
//添加state
game.state.add("state1",state1)

//啟動
//start(key,clearWorld,clearCache,param)
/* 參數說明
clearWorld default true
clearcache default false
param 傳遞參數給另一個state
*/
game.state.start("state1")
```





### state使用與原理

phaser 只有一個world

一個遊戲會有很多頁面，可以使用state來達成多頁面功能，

在unity 來說，就是多Scenes

將state 加入到state 管理器中



### state參數傳遞



`BootState.js`

```javascript
    create(){
        var text = game.add.text(game.world.centerX,25,"open preload",{fill:'#fff'});
        text.anchor.set(0.5);
        text.inputEnabled = true;
        text.events.onInputDown.add(function(){
            console.log("onInputDown");
            this.state.start("PreLoadState",true,false,"boot_test");
        },this);

    }
```



`PreLoadState.js`

```javascript
    init(p){        
        console.log("init p:",p);    
    }
```





### state生命週期與工作原理

子系統的update會調用state的update

shutdown 是state 的生命週期的最後一個，通常來destory物件，比方說destory 監視器物件

![image-20210618171944146](https://i.imgur.com/TgTqpLp.png)



## 動畫



動畫分類

補間動畫

幀動畫



### 補間動畫

- 創建方式

  ```javascript
  var tween = game.add.tween(displayObject)
  tween.to(properties,duration,ease,autoStart,delay,repeat,yoyo)
  tween.from(properties,duration,ease,autoStart,delay,repeat,yoyo)
  ```

  在屬性的部分也可以多設定縮放、透明度等等功能

   動畫也有事件的類型

  `tween.onStart`

  `tween.onLoop`

  `tween.onComplete`

- 代碼示例

    `preload`
    
    ```javascript
    preload () {
      game.load.atlas('jsonImg', '/assets/images/json.png', '/assets/images/data.json')
    }
    ```
    `create()`
    
    ```javascript
    create(){
        // 補間動畫
        // tween.to(properties,duration,ease,autoStart,delay,repeat,yoyo)
        // tween.from(properties,duration,ease,autoStart,delay,repeat,yoyo)
        // var img = game.add.image(100, 100, 'jsonImg', 21)    
        // var tween = game.add.tween(img)
    
        tween.onStart.add(function () {
          console.log('tween onStart')
        }, this)
        tween.onLoop.add(function () {
          console.log('tween onLoop')
        }, this)
    
        tween.onComplete.add(function () {
          console.log('oAnim onComplete')
        }, this)
    }
    ```
    
    

### 幀動畫

只有sprite 類型才能有幀動畫

- 創建方式

  ```javascript
  var s = game.add.sprite(x,y,"圖片集")
  s.anamitions.add(name,[,frames],[,frameRate],[,loop],[,userNumericIndex])
  s.anamitions.play("name",[,frameRate],[,loop])
  s.anamitions.stop("name")
  ```

  

- 代碼示例

  `preload()`

  ```javascript
  preload () {
  	game.load.atlasXML('octopus', '/assets/images/octopus.png', '/assets/images/octopus.xml')
  }
  ```

  `create()`

  ```javascript
    create () {
  	// 幀動畫
      var octopus = game.add.sprite(100, 200, 'octopus')
      var oAnim = octopus.animations.add('swim', null, 60, false)
  
      oAnim.onStart.add(function () {
        console.log('oAnim onStart')
      }, this)
      oAnim.onLoop.add(function () {
        console.log('oAnim onLoop')
      }, this)
  
      oAnim.onComplete.add(function () {
        console.log('oAnim onComplete')
      }, this)
  
      octopus.animations.play('swim', 30, true)
    }
  ```

  
