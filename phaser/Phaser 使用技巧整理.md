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



## 設定重力

```javascript
object.body.setAllowGravity(false);
object.body.setAllowGravity(true);
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
