# python



![image-20210713110336045](D:\kite\python爬蟲.assets\image-20210713110336045.png)



```python
str = "12345678"
print(str[:])
print(str[2:])
print(str[2:-2])
print(str[:-3])

```







```python
odds = []
for i in c:
	if i % 2 != 0:
		odds.append(i)
```







```python
odds = [
    
    i
    for i in c 
    if i % 2 != 0
    
    
]
```





```python
stocks = [
    {
        'name':'2330',
        'close':203
    },
    {
        'name':'2303',
        'close':40
    }    
]

print(
[
    stock['name']
    for stock in stocks
    if stock['close'] > 100 
]
)


```

![image-20210713111011469](D:\kite\python爬蟲.assets\image-20210713111011469.png)

```python
if 'eo' in 'hello':
    print('ok')
    
stocks = 
{
	'name':'2330',
	'close':203
}

#dictonary 比較的是key值
if 'name' in stocks:

#如果是要判斷後面的值，怎要做呢?
#values 是把這個dictonary的值當成集合進行回傳
if '283' in stocks.values():

print(stock.values())
#result 
#dict_values(['2330',283])

print(stock.keys())
#result
#dict_keys(['name','close'])

print(stock.items())
#result tuple 物件
#dict_items([('name','2330'),('close',283)])


```

![image-20210713111954572](D:\kite\python爬蟲.assets\image-20210713111954572.png)

```python
import json
s = {"name":"john"}
d = json.loads(s)
print(d['name'])

d = [
    {
        'name': 'marry'
    }
]

print(json.dumps(d))


```





```python
import urllib.parse as up 
url = 'https//24h.pchome.com.tw:8080/prod/DPAE1T-1900AHGHO'
result = up.urlparse(url)
print(result.path.split('/')[-1])
```





無痕還是可以追蹤

可以用比如finegerprint.js

在html5 的canvas 上面畫一個圖，再用uint8 算出一個數字

在同一台電腦、瀏覽器、GPU 算出來的值會是一樣的。



隱碼追蹤



pyquery like jquery 

pip chardet 字碼檢測套件



有講到在露天買PC，都會有那種主機廠商伺服器等級的退役主機，效能都不錯，價錢平民

定錨效應

花五、六年打底



不建議做爬蟲的工作太久

