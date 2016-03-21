# Laravel 與他的快樂夥伴(資料夾)介紹
```
* app
 * Route、Model與Controllers等等，連結各檔案間的關係。


* bootstrap 
 * 放置預定自動加載的資料，CSS、Bootstrap...。


* config
 * 重要資訊，如:mail、推播、session、資料庫資訊。


* database
 * 存放自動生成資料庫與子資料的內容檔案。


* public
 * 管理網站進入點，.htaccess、index.php。


* resources
 * 多語系、View(html)、Sass。
 

* storage
 * cache、log...，暫時不會用到這一塊。
 

* tests
 * 測試。
 

* vendor 
 * 各種外掛

```


其他:
1. composer.json : composer 的自動加載管理文檔。
1. .env : 一開始就要設定的，更改金鑰、資料庫帳密...。

