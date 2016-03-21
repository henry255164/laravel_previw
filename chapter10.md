# controller 控制器


前面幾章節做下來route.php變得很臃腫，這樣不是好現象，未來整理會很麻煩。
所以我們將route.php轉移到一個個不同的controller中。

##修改route.php

將 
```php
Route::get('customer/{id}', function($id){
    //這個很明顯阿!!就是抓資料庫!!
    $customer = App\Customer::find($id);
    
    echo $customer->name . "<br/>";
    echo "Orders : <br/>";
    
    //這裡是使用Model裡要使用的function名稱
    $orders = $customer->forfun;
    echo '<ul>';
    foreach ($orders as $order) {
        echo '<li>'.$order->name . "</li>";
    }
    echo '</ul>';
});
``` 
剪下(保留)程式碼，修改為

```php
Route::get('customer/{id}', 'CustomerController@customer');
```

##建立controller

還沒完，到CMD輸入``` php artisan make:controller CustomerController ```

新的 CustomerController.php 會被建置在 app->https->controllers之下

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Http\Requests;
use App\Http\Controllers\Controller;

class CustomerController extends Controller
{
  //  
}
```
加入程式碼
```php
public function customerr($id){
    //這個很明顯阿!!就是抓資料庫!!
    $customer = App\Customer::find($id);

    echo $customer->name . "<br/>";
    echo "Orders : <br/>";

    //這裡是使用Model裡要使用的function名稱
    $orders = $customer->forfun;
    echo '<ul>';
    foreach ($orders as $order) {
        echo '<li>'.$order->name . "</li>";
    }
    echo '</ul>';
```

其實就是之前保留的程式碼，我們將function命名為customerr別忘了將$id帶入

這時就可以去看網頁的樣子了。
http://localhost:8000/customer/1
保持不變。

##簡化資料庫寫法

我們可以看到當我們需要使用資料庫時的語法
`$customer = App\Customer::find($id);`

嘗試將它簡化，在前面的宣告加上
`use App\Customer as Customk`

這時就可以將原先寫法改為
`$customer = Customk::find($id);`

完整程式碼
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Http\Requests;
use App\Http\Controllers\Controller;
use App\Customer as Customk;

class CustomerController extends Controller
{
    //同一個controller可以有很多function，名稱也不同
    public function customerr($id){
    //這個很明顯阿!!就是抓資料庫!!
    $customer = Customk::find($id);
    
    echo $customer->name . "<br/>";
    echo "Orders : <br/>";
    
    //這裡是使用Model裡要使用的function名稱
    $orders = $customer->forfun;
    echo '<ul>';
    foreach ($orders as $order) {
        echo '<li>'.$order->name . "</li>";
    }
    echo '</ul>';
}
```
可以再去看一下網頁。

##將網頁判斷移到view中 (.blade.php)

進一步實現MVC架構，將
```php
    echo $customer->name . "<br/>";
    echo "Orders : <br/>";
    
    //這裡是使用Model裡要使用的function名稱
    $orders = $customer->forfun;
    echo '<ul>';
    foreach ($orders as $order) {
        echo '<li>'.$order->name . "</li>";
    }
    echo '</ul>';
```

剪下(保留)程式碼，並修改為

```php
    $customer = Customk::find($id);
    return view('customer',$array = array('customjj' => $customer ));
```

再到 resources->views 底下新增 customer.blade.php

```php
<!DOCTYPE html>
<html>
<head>
    <title>Customer</title>
</head>
<body>
    <h1>{{ $customjj->name }}</h1>

    <h3>Order: </h3>
    <ul>
    @foreach ($customjj->forfun as $order)
        <li>{{ $order->name }}</li>
    @endforeach
    </ul>
</body>
</html>
```
其實前面都教過了。如果前面都有照做的話，就可以明白這些都是再route的程式碼，被修改道不同的檔案，實現MVC管理(Model View Contorller)。







