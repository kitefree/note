





# 软件测试之Jmeter接口测试、压力测试、数据库、项目实战从入门到精通全集【柠檬班】





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

