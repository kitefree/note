# PIXI JS 超人門學習



## 基礎結構

### HTML、JS載入

![image-20210716151529109](D:\kite\PIXI JS 超人門學習.assets\image-20210716151529109.png)

### JS 基礎說明

![image-20210716151203957](D:\kite\PIXI JS 超人門學習.assets\image-20210716151203957.png)



#### 初始化設定

![image-20210716151434641](D:\kite\PIXI JS 超人門學習.assets\image-20210716151434641.png)



## pixijs container 概念說明

stage 可以想像成是一個body 元素

建議在實作內容的時候都使用container 來包裏相關物件，在移動座標的時候，會比較好管理![image-20210716151831794](D:\kite\PIXI JS 超人門學習.assets\image-20210716151831794.png)

### container 實作範例



![image-20210716152334949](D:\kite\PIXI JS 超人門學習.assets\image-20210716152334949.png)



## 滑鼠監聽實作

![image-20210716154419564](D:\kite\PIXI JS 超人門學習.assets\image-20210716154419564.png)



## container add event 實作

![image-20210716154548989](D:\kite\PIXI JS 超人門學習.assets\image-20210716154548989.png)

如果要有事件記得開啟`interactive=true` ,

而`buttonMode` 是cursor變為手指頭符號





## 遊戲循環說明

`app.ticker`

這邊可以理解成unity 的update 遊戲循環(個人的理解，還是需要爬文看一下這個套件對於ticker 的詳細說明)

![image-20210716154314683](D:\kite\PIXI JS 超人門學習.assets\image-20210716154314683.png)





## GUI 工具

### 載入`dat.gui.min.js` 套件

![image-20210716155239657](D:\kite\PIXI JS 超人門學習.assets\image-20210716155239657.png)

### `new datGuiData()`

![image-20210716155306960](D:\kite\PIXI JS 超人門學習.assets\image-20210716155306960.png)

### `set app.ticker.add()`

![image-20210716155335874](D:\kite\PIXI JS 超人門學習.assets\image-20210716155335874.png)

### 預覽結果畫面

可以即時調整相關坐標，進行調整

![image-20210716155358346](D:\kite\PIXI JS 超人門學習.assets\image-20210716155358346.png)



## FPS 偵測外掛

### 載入`Stats.min.js`

![image-20210716160004003](D:\kite\PIXI JS 超人門學習.assets\image-20210716160004003.png)



### JS 實作寫法

![image-20210716160052516](D:\kite\PIXI JS 超人門學習.assets\image-20210716160052516.png)

### 預覽結果

![image-20210716160602185](D:\kite\PIXI JS 超人門學習.assets\image-20210716160602185.png)



## 幾何圖形

### 畫圓、畫矩形

![image-20210716161720950](D:\kite\PIXI JS 超人門學習.assets\image-20210716161720950.png)



## PIXI chrome plugin 外掛

![image-20210716161524141](D:\kite\PIXI JS 超人門學習.assets\image-20210716161524141.png)

