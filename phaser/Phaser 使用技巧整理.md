# Phaser 使用技巧整理

專案 載浮載沉

版本 phaser3.55.2.js



## 資源

[phaser3官網 example](https://labs.phaser.io/index.html)



## 待閱讀

[Move Objects According To The Mouse Position With Phaser 3](https://steemit.com/utopian-io/@onepice/move-objects-according-to-the-mouse-position-with-phaser-3)

[how-to-create-sprite-sheets-for-phaser3](https://www.codeandweb.com/texturepacker/tutorials/how-to-create-sprite-sheets-for-phaser3)



## 圖層順序

```javascript
obj.setDepth(2);
```



## 圖片縮放

```javascript
obj.setScale(.2,.2)
```



## 設定container 包物件

![image-20210813124658109](https://i.imgur.com/7UGOlow.png)

```javascript
function preload ()
{
    this.load.image('buttonBG', 'assets/sprites/button-bg.png');
    this.load.image('buttonText', 'assets/sprites/button-text.png');
}

function create ()
{
    var bg = this.add.image(0, 0, 'buttonBG');
    var text = this.add.image(0, 0, 'buttonText');

    var container = this.add.container(400, 300, [ bg, text ]);

    container.setSize(bg.width, bg.height);
}
```

[reference](https://labs.phaser.io/edit.html?src=src/game%20objects/container/draggable%20container.js)



## 設定sprite切換



![img](https://i.imgur.com/c2ehBab.png)

```javascript
function preload ()
{
    this.load.spritesheet('aliens', 'assets/sprites/bsquadron-enemies.png', { frameWidth: 192, frameHeight: 160 });
}

function create ()
{
    var alien = this.add.sprite(400, 300, 'aliens', 0).setInteractive();

    alien.on('pointerover', function () {

        this.setFrame(3);

    });

    alien.on('pointerout', function () {

        this.setFrame(0);

    });
}
```

[reference](https://labs.phaser.io/edit.html?src=src/input%5Cgame%20object%5Csprite%20example.js)





## 世界座標中心

![Phaser 3 Center Text In Middle Of Screen](https://i.imgur.com/l0Y7ybi.jpg)

```javascript
const screenCenterX = this.cameras.main.worldView.x + this.cameras.main.width / 2;
const screenCenterY = this.cameras.main.worldView.y + this.cameras.main.height / 2;
const loadingText = this.add.text(screenCenterX, screenCenterY, 'Loading: 0%').setOrigin(0.5);
```



```js
// 測試大量圖檔
for (let i = 0; i < 200; i++) {
    this.load.image('bg' + i, 'assets/undersea.jpg')
}

// 創建 text
let percentText = this.add.text(this.cameras.main.width / 2, this.cameras.main.height / 2, '', {
    font: '52px Open Sans',
    fill: '#ffffff'
}).setOrigin(0.5, 0.5)

// 偵聽處理檔案
this.load.on('progress', value => {
    percentText.setText(parseInt(value * 100) + '%')
})

// 偵聽載入檔案結束
this.load.on('complete', () => {
    percentText.destroy()		// 載入完，把它從畫面上清除
})
```





[reference](https://www.stephengarside.co.uk/blog/phaser-3-center-text-in-middle-of-screen/)



## 設定可拖曳

```javascript
cube.setInteractive();
self.input.setDraggable(cube);
```

> 必須先設定互動，才能使用draggable 功能





## 物件與物件之間 overlap

```javascript
create()
{
    self.RectangleToRectangle = Phaser.Geom.Intersects.RectangleToRectangle;
	self.GetBounds = Phaser.Display.Bounds.GetBounds;
}

update() {

	this.GetBounds(this.cube04, this.rect1);
	this.GetBounds(this.rect_water, this.rect2);

	if (this.RectangleToRectangle(this.rect1, this.rect2)) {
        
        
    }
    
    
}
```

[reference](https://phaser.io/examples/v3/category/geom/intersects)



## 設定游標

```javascript
this.systems.game.input.setCursor({ cursor: 'grabbing' });
this.systems.game.input.resetCursor({ cursor: 'true' });
```



## 設定物件透明度

```javascript
object.alpha = 0.5;
object.clearAlpha();
```



## 設定物件顯示or隱藏

```javascript
object.visible = true;
```



## 設定動畫

![image-20210813133125039](https://i.imgur.com/iDgRMpU.png)

```javascript
//回到原本水位位置
self.tweens.add({
    targets: [self.rect_water, self.rect_water_ruler],
    y: self.gSetting.water.y,
    ease: 'Power2',
    duration: 500,
    onComplete: self.onCompleteHandler,
});

onCompleteHandler = (tween, targets, myImage) => {
    //console.log('onCompleteHandler');

    tween.parent.killTweensOf(self.rect_water);
    tween.parent.killTweensOf(self.rect_water_ruler);
}

//增加水位
self.tweens.add({

    targets: [self.rect_water, self.rect_water_ruler],
    y: self.add_water_height(self, 50),
    ease: 'Power2',
    duration: 500,
    onComplete: self.onCompleteHandler,
});

add_water_height = (self, add_h) => {
    return self.gSetting.water.y - add_h;
}

```



## 創建重力物件

```js
scene.create = function() {
    // 把物件賦予重力
    let ground = this.add.sprite(180, 400, 'tile')
    this.physics.add.existing(ground)

    // 直接創建重力物件
    let ground2 = this.physics.add.sprite(180, 200, 'tile')
}
```



## 設定重力

```javascript
object.body.setAllowGravity(false);
object.body.setAllowGravity(true);
```



## 不受重力碰撞影響而變更位置

```js
ground.body.immovable = true
```



## 設定碰撞

```javascript
//讓兩個物件產生碰撞
this.physics.add.collider(ground, ground2);

//設定碰撞事件
self.physics.add.collider(cube, self.weigh, weight_event, null, self);
self.physics.add.collider(cube, self.box_down_side, boxDownSide_event, null, self);
```





## 切換場景
![image-20210813133839704](https://i.imgur.com/SBNmFo3.png)

`index.js`

```javascript
import MainScene from './Scenes/MainScene.js';
import StartScene from './Scenes/StartScene.js';

var config = {
    type: Phaser.AUTO,
    scale: {
        mode: Phaser.Scale.FIT,        
        autoCenter: Phaser.Scale.CENTER_BOTH,
        width: 1500,
        height: 700
    },    
    physics: {
        default: 'arcade',
        arcade: {
            gravity: { y: 800 },         
        }
    },
    scene: [StartScene,MainScene]
};
var game = new Phaser.Game(config);

```



`StartScene.js`

```javascript
create() {
    btnStart.on('pointerover', function () {
        this.scene.sys.game.input.setCursor({ cursor: 'pointer' });      
    });

    btnStart.on('pointerout', function () {
        this.scene.sys.game.input.resetCursor({ cursor: 'true' });
    });
    btnStart.on('pointerdown', function () {            
        self.scene.start('MainScene');
    });
}
```



## 放大鏡效果



![img](https://i.imgur.com/JGJ28cg.jpg)

![img](https://i.imgur.com/X8PLFhx.png)

![img](https://i.imgur.com/ESxkX97.png)

![image-20210813140836787](https://i.imgur.com/9vtpHfd.png)

```javascript
class Example extends Phaser.Scene
{
    constructor ()
    {
        super();
    }

    preload ()
    {
        this.load.image('pic', 'assets/pics/sword-art-online.jpg');
        this.load.image('magnify-out', 'assets/sprites/magnify-glass-outside.png');
        this.load.image('magnify-in', 'assets/sprites/magnify-glass-inside.png');
    }

    create ()
    {
        this.add.image(400, 300, 'pic').setTint(0x2d2d2d);

        //  The scale creates a slight magnification effect
        const pic = this.add.image(400, 300, 'pic').setScale(1.05);

        const lense = this.make.sprite({
            x: 400,
            y: 300,
            key: 'magnify-in',
            add: false
        });

        pic.mask = new Phaser.Display.Masks.BitmapMask(this, lense);

        const magnify = this.add.image(400, 300, 'magnify-out');

        this.input.on('pointermove', function (pointer) {

            lense.x = pointer.x;
            lense.y = pointer.y;

            magnify.x = pointer.x;
            magnify.y = pointer.y;

        });
    }
}

const config = {
    type: Phaser.WEBGL,
    parent: 'phaser-example',
    width: 800,
    height: 600,
    scene: [ Example ]
};

const game = new Phaser.Game(config);

```



[reference](https://labs.phaser.io/edit.html?src=src/display/masks/magnify%20glass.js&v=3.55.2)





## 相機效果



```js
scene.gameOver = function() {
    // 500 ms 相機 shake 效果
    this.cameras.main.shake(500)					
    
    // 偵聽 shake 動畫結束
    this.cameras.main.on('camerashakecomplete', () => {
        // 500 ms 相機 fade 效果
        this.cameras.main.fade(500)				
    })
    
    // 偵聽 fade out 動畫結束
    this.cameras.main.on('camerafadeoutcomplete', () => {	
        // 遊戲重新
        this.scene.restart()						
    })
}
```



## 設定動畫

```js
scene.create = function() {
    // 把 man 物件的 origin 設在中間正下方，並設為可互動
    this.man = this.add.sprite(50, 310, 'man', 0).setOrigin(0.5, 1).setInteractive()

    // 對於 man 增加 tweens 動畫
    this.man.scaleTween = this.tweens.add({
        targets: this.man,
        scaleX: 1.2,
        scaleY: 1.2,
        duration: 1000
    })
}


```

上面一開始載入完時，就會自動執行動畫，所以可以多添加 paused: true

```js
this.man.scaleTween = this.tweens.add({
    targets: this.man,
    scaleX: 1.2,
    scaleY: 1.2,
    duration: 1000,
    paused: true
})
```



```js
this.man.on('pointerdown', () => {
    this.man.scaleTween.restart()
})
```

