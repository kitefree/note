





# 软件测试之Jmeter接口测试、压力测试、数据库、项目实战从入门到精通全集【柠檬班】



https://www.bilibili.com/video/BV1st411Y7QW?from=search&seid=17892575272997093771

https://cloud.tencent.com/developer/inventory/1923

https://www.bilibili.com/video/BV1st411Y7QW?p=30&spm_id_from=pageDriver

https://blog.miniasp.com/post/2012/10/18/How-to-do-Web-Load-Test

## JMeter 之HTTP請求詳解 request



請求地址

請求方法

請求正文：請求參數

HTTP協議/版本



x-Requested-With:告訴服務器這個是一個ajax請求





## Jmeter 之HTTP 請求詳解 response



響應狀態碼

響應頭

響應報文

 

常見響應頭：

location:告訴瀏覽器跳到哪裡

content-length:告訴瀏覽器回送數據的長度

content-type:告訴瀏覽器回送數據的類型





## HTTP 請求常見狀態碼

2開頭(請求成功)表示成功處理了請求的狀態代碼

3開頭(請求被重定向)表示要完成請求，需要進一步操作。通常，這些狀態代碼用來重定向

4開頭(請求錯誤)這些狀態代碼表示請求可能出錯，妨礙了服務器的處理。

5開頭(服務器錯誤)這些狀態代碼表示服務器在嚐試處理請求時發生內部錯誤。這些錯誤可能是服務器本身的錯誤，而不是請求出錯。



## JMETER 工作介面介紹

- 邏輯控制器
  - 吞吐量控制器



- 監聽器
  - 用於請求之後





## 發送get請求

添加線程組



![image-20210724161137954](https://i.imgur.com/DUHNuzM.png)

協議預設為http，可以不填，如果是https，請填上

服務器名稱請只填domain name ，不要包含http

路徑該有斜槓就請補上

參數 請注意空格問題



## 發送post請求

沒什麼重點可以寫



## 請求參數的類型

parameters 頁籤 與body data 頁籤 在切頁之前，請記得都先清空。只能有一個頁籤有資料



body data 通常拿來填寫json、xml 格式

![image-20210724162918704](https://i.imgur.com/eYzwiCa.png)

## 請求默認值



http 要求預設值

![image-20210725181021439](https://i.imgur.com/hXhRgVU.png)

可以讓每一個請求的內容重複使用這個設定

如果在那個單一請求上填寫了值，那就會直接覆蓋那個預設值





## 結果樹

無重點



## cssjquer_tester使用

![image-20210725185803893](https://i.imgur.com/4oNod5C.png)



td[class=explaintarget]
div[class=nav clearfix].a
input[name=q]





## 結果樹html應用

![image-20210725190226282](https://i.imgur.com/v5h2nxK.png)





## 結果樹JSON模式使用

$.reason

$.result.id

$.result['yangli']

![image-20210725190852842](https://i.imgur.com/BvkGM2E.png)

http://testingpai.com/article/1594713060451



## 結果樹document使用

![image-20210725191331577](https://i.imgur.com/EueJvOC.png)

## 結果樹 RegexpTester使用

![image-20210725191656050](https://i.imgur.com/R74SOcY.png)

正常表達式



## 結果樹XPATH TESTER





![image-20210725192840262](https://i.imgur.com/sIQyeYq.png)



![image-20210725192622978](https://i.imgur.com/W3bHcsO.png)

![image-20210725192643803](https://i.imgur.com/dRqVtpS.png)





## http 訊息管理頭

![image-20210725193547583](https://i.imgur.com/jicOwRK.png)

`http要求管理員` 可以拖拉到個別的`HTTP請求` ，會只有那個請求生效這個`HTTP要求管理員`的設定





## 斷言(驗證)

![image-20210725203644297](https://i.imgur.com/EIyjc2Q.png)



![image-20210725203701647](https://i.imgur.com/fElVyG5.png)



## 斷言XPath Assertion

一般還是用斷言比較多，比較少用XPATH



## 結合fidder

![image-20210725205641634](https://i.imgur.com/PIPeG0w.png)



填上127.0.0.1 port 8888



![image-20210725205949203](https://i.imgur.com/2JHWKxQ.png)





## 自定義變量

執行緒群組>新增>設定元素>使用者自訂變數

引用變量方式`${}`

![image-20210725210759488](https://i.imgur.com/cVVDZZg.png)

![image-20210725210812719](https://i.imgur.com/iEdOail.png)





## 請求參數化TXT



![image-20210725214116549](https://i.imgur.com/XfrSBMF.png)



![image-20210726132557700](https://i.imgur.com/w8Ygs6Y.png)

## 請求參數化CSV

新增>設定元素>CSV資料設定

同TXT概念，只是用CSV格式，EXCEL預覽模式編輯



## 參數化函數助手_CSVRead

![image-20210726134127399](E:\壓力測試\软件测试之Jmeter接口测试、压力测试、数据库、项目实战从入门到精通全集【柠檬班】.assets\image-20210726134127399.png)

![image-20210726134200185](E:\壓力測試\软件测试之Jmeter接口测试、压力测试、数据库、项目实战从入门到精通全集【柠檬班】.assets\image-20210726134200185.png)

 

## 函數助手randomstring

![image-20210726134609049](E:\壓力測試\软件测试之Jmeter接口测试、压力测试、数据库、项目实战从入门到精通全集【柠檬班】.assets\image-20210726134609049.png)



## 正則表達式

後置處理器>正規表示剖析器

加在request 底下

debug sampler 可以看正規表示取到的結果

接著可以再把取到的結果塞到下一個request

![image-20210726175009464](https://i.imgur.com/70wsBIa.png)



## 正則表達式獲取多組

![image-20210727131539906](https://i.imgur.com/QPM1EfR.png)

匹配數字 -1 代表全取

P28





## foreach循環控制器

![image-20210727163427158](https://i.imgur.com/p6RZXyl.png)





![image-20210727163444760](https://i.imgur.com/UlYW9c3.png)



## 場景設計

### 哪些業務需要做壓力測試？

比較常用業務場景(OR 功能模塊)

比方說瀏覽網頁業務量少，充值的網頁業務量特別多。就針對充值的網頁業務量進行測試

單業務場景/或者多業務場景

項目要求做的業務場景



### 壓測試的併發數是多？

有預期的數值？一次性達到？有上次性能測試的結果值？ 100 200 300 按時間的逐步增加 ，參照上次的性能測試的結果 200

無預期的數值？ 只有考參的在線用戶數？ 2:8 原則 --->可以用在線用戶數的20%作為參考去測試。 

1000個用戶  200 個併發  



### 關注哪些參數？

#### 響應時間  

1 3 5 / 2 5 8 參考值

比方說 1 秒可以接受 

1~3秒還可以接受

5 秒以上不能接受

2 5 8 也是這個概念



#### TPS

越高越好 會有極限值 枓據這個結果 去做進一步的併發數/腳本的調整 

#### 錯誤率

越低越好 99.99%  如果你做的是銀行業務 必須是 100%正確率/ 有對應的容錯機制/處理機制

#### CPU 和內存 隊列 磁盤 的使用情況

CPU 最好不要超過80%

內存最好要保留20%空閒

磁盤 讀寫操作頻率不要過高過快



### 目標項目的場景設計

登入-投資-登出

核心業務是：投資

全發用戶：目標100(因為是測試環境)



