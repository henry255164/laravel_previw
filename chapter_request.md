# 番外篇: Request 請求


資料來自於: Laravel 5.2 官網 [HTTP 請求篇](https://laravel.tw/docs/5.2/requests)


##引用Request實例

```php
use Illuminate\Http\Request;
```

以上就是引用實例，可以直接添加在 Route.php 當中使用。





引用有多種不同的呼叫方式

##基礎的取值


```php
public function update(Request $request, $id){
  $name = $request->input('name');
}

```
