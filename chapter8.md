# view 畫面

這一單元很簡單
就是在說明畫面如何產生

##放html檔的位置

laravel靜態頁面都是放在

resource資料夾中的views當中

##新建mypage.php

在views底下新建一個 mypage.php

```html
<!DOCTYPE html>
<html>
<head>
	<title>我的頁面</title>
</head>
<body>
<h1>HI~歡迎來到我的頁面</h1>
</body>
</html>
```
接著到 route.php

添加

```php
Route::get('mypage', function () {
    return view('mypage');
});
```
打開 http://localhost:8000/mypage

可以看到

**HI~歡迎來到我的頁面**

就是mypage.php當中的

```html
<h1>HI~歡迎來到我的頁面</h1>
```


 ##添加參數
 
 這時我們修改路由
 加入一個array
 


```php
Route::get('mypage', function () {
 
$data = array('var1' => '京城五','var2' => '王力宏','var3' => '周杰魂' );

    return view('mypage',$data);
});
```
然後將mypage.php也修改一下

```php
<!DOCTYPE html>
<html>
<head>
    <title>我的頁面</title>
</head>
<body>
<h1>HI~歡迎來到我的頁面</h1>
<p><?php echo $var1; ?></p>
<p><?php echo $var2; ?></p>
<p><?php echo $var3; ?></p>


</body>
</html>
```

可以看到


**HI~歡迎來到我的頁面**

京城五

王力宏

周杰魂



