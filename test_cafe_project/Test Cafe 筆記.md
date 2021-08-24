# Test Cafe 筆記



## 介紹

[官網](https://testcafe.io/)

1. Write tests with ease
2. Test in every browser that matters
3. Deploy without fear
   1. CI/CD-ready
   2. Concurrent test runs
   3. If something goes wrong...

 



[[Day 11] 看見 TestCafe，又簡單又完整的工具鍊](https://ithelp.ithome.com.tw/articles/10221559)


>TestCafe 是筆者用過框架裡，支援最多**作業系統** 和 **瀏覽器** 的測試框架



## 安裝



```shell
npm install -g testcafe
```



## 起手式

```javascript
import { Selector } from 'testcafe'; // 引入 testcafe 的 html element 選擇器

fixture `Getting Started` // 設定測試集名稱
    .page `http://devexpress.github.io/testcafe/example`; // 測試目標網頁

test('HelloWorld test', async t => { // 一個測試案例
    await t
        .typeText('#developer-name', 'HelloWorld') //在文字框輸入 HelloWorld
        .click('#submit-button') //按下送出按鈕
        .expect(Selector('#article-header').innerText).eql('Thank you, HelloWorld!');
        // 使用 expect 驗證 #article-header 內的文字 等於 Thank you, HelloWorld!
});
```





## 執行錯誤

執行 

```
testcafe day01.js
```

testcafe : 因為這個系統上已停用指令碼執行，所以無法載入 C:\Users\RESH\AppData\Roaming\npm\testcafe.ps1 檔案。如需詳細資訊，請參閱 about_Execution_Policies，網址為 https:/go. 
microsoft.com/fwlink/?LinkID=135170。



開啟powershell ，請使用「系統管理員身份」執行。

```powershell
Set-ExecutionPolicy RemoteSigned
```



[解決 Windows 上輸入指令出現「因為這個系統上已停用指令碼執行，所以無法載入...」的問題](https://hsiangfeng.github.io/other/20200510/1067127387/)



## 執行參數

```sh
testcafe chrome HelloWorld.js --speed 0.3
```

> 0.01 ~ 1 之間 1最快，0.01最慢



三神器 Selectors, Actions, Assertions

## 瀏覽器測試




>對於 Web 自動化測試而言，一個瀏覽器還真解決不了所有事！
>為了完成相容性測試和提高測試完整度，通常要在多的瀏覽器上測試過。



```
#啟用chrome
testcafe chrome day02.js

#啟用firefox
testcafe firefox day02.js

#啟用edge
testcafe edge day02.js

#失敗
testcafe chrome,firefox day02.js

#成功 ,本地端所有瀏覽器一起執行,但是最後沒有close,停在測試完的地方
testcafe all day02.js

#無頭模式
testcafe chrome:headless day02.js

#模擬iphone or android device
testcafe "chrome:emulation:device=iphone X" day02.js
testcafe "chrome:emulation:device=pixel 2" day02.js

#模擬器 + headless mode 
testcafe "chrome:headless:emulation:device=iphone X" day02.js
testcafe "chrome:headless:emulation:device=pixel 2" day02.js

```



真正的平行測試，將**多個測試案例** 分散到 **多個瀏覽器跑**
下例，若有 2 個測試案例，會開 2 個 Chrome 瀏覽器，各跑 1 個測試案例。

```
testcafe -c 2 chrome day02.js --speed .5
```

