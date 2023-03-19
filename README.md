# PHP & Laravel

## Table of Contents
* **Basic**
    * [Installing](#安裝)
    * [Compiler](#Compiler)
    * [Variable](#Variable)
    * [Printing](#Printing)
    * [Data types](#Data-types)
    * [Function](#Function)
    * [Scope](#Scope)
        * [Local](#Local)
        * [Global](#Global)
    * [Loop](#)
    * [Generics](#)
    * [OOP](#OOp)
        * [Class](#class)
        * [Class scope](#class-scope)
          * [public](#public)
          * [private](#private)
          * [protected](#protected)
          * [static](#static)
* **Framework**
    * [Laravel](#Laravel)


## Installing
MAC OS
```bash
brew install php
```
## Compiler
```php
<?php
phpinfo()
?>    
```
可以看到php相關組態設定
![](https://i.imgur.com/Jl0unO2.jpg)

---

## Variable
php的變數使用`$`宣告
```php
<?php
    $name = "Dennis";
    echo $name;
?>
```

常數宣告，使用大寫
```php
const USER_NAME = "Dennis";
```

---

## Printing
```php
<?php
$user = "Dennis";
print_r($user);
echo $user;
?>
```
如果想要使用特殊字元做斷點
```php
<?php
$user = "Dennis";
echo ("My name is Dennis \n Hello everyone");
//My name is Dennis Software engineer
?>
```
需要加上`nl2br`函式
```php
<?php
$user = "Dennis";
echo nl2br("My name is Dennis \n Hello everyone");
/* My name is Dennis 
 * Software engineer*/
?>
```

在`echo`中輸出變數，使用`. + 變數`
```php
<?php
$user = "Dennis";
print_r($user);
echo "My name is" .$user
?>
```

在`var_dump`印出更完整的變數資料
```php
<?php
$user = "Dennis";
var_dump($user) //string(6) "Dennis"
?>
```

---

## Data Types
```php
<?php
//string
$name = "Dennis";
var_dump($name);

//number
$ROC = 1911;
$ROCYear = 88;
$Year = $ROC + $ROCYear;
var_dump($Year) //1999
    
//boolean;
$isActive= True;
var_dump($isActive) 
    
//array
$fruits = array("apple","banana","papaya","guava");
$fruits = ["apple","banana","papaya","guava"];
var_dump($fruits);
var_dump($priceOfFruit[0]);

/* 
 * 在PHP中物件的宣告方式比較特別，使用`[]`並且在陣列中宣告`key => value`
 */

$priceOfFruit = [
  "apple" => "22",
  "banana" => "22.5",
  "papaya" => "50",
  "guava" => "30"
];

$priceOfFruit = array(
  "apple" => "22",
  "banana" => "22.5",
  "papaya" => "50",
  "guava" => "30"
);

var_dump($priceOfFruit);
var_dump($priceOfFruit['apple']);

?>
```

---

## Function 
```php
<?php
  function sayHi() {
    echo "Hello world!";
  };
  sayHi();
?>
```

## Scope
### Local
由於函式內部無法存取外部變數，因此內部宣告變數也為區域變數。
```php
<?php
  $name = "Dennis";
  function myFunction(){

    echo $name; //undefined
  };
  myFunction();
?>
```

### Global
```php
<?php
  $name = "Dennis";
  function myFunction(){

    echo $name; //undefined
  };
  myFunction();
?>
```
需使用`global`存儲全域變數
```php
<?php
  $x = 10;
  function myFunction() {
    global $x;
    echo $x; //10
  };
  myFunction();
?>
```

---

## Loop
for loop
```php
<?php
for($count = 0; $count < 10 ; $count ++) {
  echo $count; //0123456789
}
?>
```
while loop
```php
<?php
$count = 10;
while($count > 0) {
  echo $count;
  $count--; 
}
?>
```

foreach

```php
<?php
$array = array("1", "2");
foreach($array as $item) {
  echo "$item.'Hello'\n";
};
```

---

## OOP
* 物件取得該屬性使用`->`

### class
* class命名為大駝峰寫法
* `new` 建立一個記憶體位置的實體
* `__construct`定義類別中的屬性

```php
<?php
class Test {
  public $title = "This is title";
  // methods and properties
}

$userOne = new Test;
```

### class scope
#### public
* 可以被實體(instance)使用
```php
<?php
class User {
  public $name;
  function __construct($name){
    $this->name = $nam
      e;
  }
  function sayHi($param) {
    $this->name = $param;
    return $this->name;
  }
}

const userOne = new User('Dennis');
var_dump(userOne->name);//string(6) "Dennis"
var_dump(userOne->sayHi('Jessica'));//string(7) "Jessica"
```

#### private
* private只允許所在類別內存取
* 並且不能被實體(instance)直接存取
```php
<?php
class Test {
  private $name = "Dennis";
  public $title = "This is for test";
  public function sayHi() {
    return $this->name;
  }
  // methods and properties
}

$test = new Test();
var_dump($test->title); //string(16) "This is for test"
var_dump($test->name); //Cannot access protected property
```

#### protected
* 允許所在類別及繼承類別存取
* 並且不能被實體(instance)存取
```php
<?php
class Test {
  protected $name = "Dennis";
  public $title = "This is for test";
  public function sayHi() {
    return $this->name;
  }
  // methods and properties
}

class Test2 extends Test {
  public function call() {
    return $this->name; 
  }
}

$test = new Test2();
var_dump($test->call()); //string(6) "Dennis"
var_dump($test->name); //Cannot access protected property
```

#### static
* 未實體化即可存取類別內的屬性及方法
* 在類別中透過`self`、`類別名`存取未實體化的屬性及方法
* 未實體化時使用類別的方法及屬性時需使用`::`
```php
<?php
class Counter{
  public static $count = 0;
  public static function increase() {
    self::$count = self::$count+1;
  }

  public static function getCount() {
    return Counter::$count;
  }
}
Counter::increase(); //1
Counter::increase(); //2
Counter::$count = 0;
var_dump(Counter::getCount());
```

static搭配實體化

```php
<?php
class Counter{
  public static $count = 0;
  public static function increase() {
    self::$count = self::$count+1;
  }

  public static function getCount() {
    return self::$count;
  }
}
Counter::increase();//1
Counter::increase();//2
$counter = new Counter();
$counter->increase();//3
var_dump(Counter::getCount());//int(3)
```

---

# Laravel
* [建立專案](#建立專案)
* [RESTful API](#RESTFUL API)
* [檔案結構](#檔案結構)
* [路由](#路由)
  * [Parameter](#Parameter)
  * [Body](#Body)
* [Request](#Request)
* [Controller](#Controller)
* [Database](#Database)


---

## 建立專案

```bash
composer create-project laravel/laravel backend
```

```bash
cd backend
```

```bash
php artisan serve
```

或是加入環境變數
```bash
composer global require laravel/installer

laravel new backend
```

---

## RESTful API
透過動詞變化達到API可以清楚辨識，並且建立易讀的遊戲規則

| 動詞 | uri |
| -------- | -------- | 
| GET     | api/user/1     |
| POST     | api/user/1    | 
| DELETE     | api/user/1     | 
| PUT     | api/user/1     | 
| PATCH     | api/user/1     | 


## 檔案結構
* [.env](#ENV)
* **app**
  * Http
    * [Controllers](#Controllers)
      * Controller.php
      * UserController.php
  * Exceptions
  * Console
  * [Models](#Models)
  * Providers
* [**routes** ](#Routes)
  * [api.php]()
  * web.php
  * channels.php
  * console.php
* **resource** 放置前端(views、css、Vue)
* database
  * [migrations](#migrationsfile)

---

## ENV
Laravel中預設資料庫為**MYSQL**這邊我們只要修改*DBUSERNAME、DBUSERPASSWORD*

![](https://i.imgur.com/qAgvSVR.png)


## Controllers
Controller能夠使檔案分層更容易閱讀

```php
php artisan make:controller ControllerName
```

```php
// \app\Http\Controllers\ServiceController

<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class ServiceController extends Controller
{

    public function testWorking() {
        $message = 'Server working';
        return $message;
    }
}
```

接著我們到 **\routes\web.php**中引入ServiceController

```php
<?php

use Illuminate\Support\Facades\Route;   
use Illuminate\Http\Request;

use App\Http\Controllers\ServiceController;// 引入ServiceContrller

Route::get('/test', [ServiceController::class,'testWorking']);
```
---


## Routes
## Models
```php
php artisan make:model Product --migraction
```
後面添加參數`--migraction`定義資料表

接著我們至`/migractions/product_table.php`

```php
public function up()
    {
      Schema::create('products', function (Blueprint $table) {
        $table->id();
        $table->string('description')->nullable();
        $table->string('name');
        $table->integer('price');
        $table->timestamps();
      });
    }
```

```php
php artisan migrate
```

![](https://i.imgur.com/e1s5PuJ.png)

這時候會問說在資料中並不存在laravel這個資料庫，是否建立它? 輸入yes

![](https://i.imgur.com/54Lg4er.png)

接著我們至db就可以看到剛剛我們需要的資料欄位正確的被建立

![](https://i.imgur.com/6B6yazo.png)

接著我們至`api.php`

```php
<?php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;
use \App\Models\Product; //引入Product

Route::get('/product',function() {
    return Product::all(); 
});

Route::get('/test',function() {
    return "Server running";
});


Route::middleware('auth:sanctum')->get('/user', function (Request $request) {
    return $request->user();
});

```
由於目前資料庫中沒資料所以回傳空陣列

![](https://i.imgur.com/7ZRLtxj.png)

接著在`api.php`添加product的post方法

```php
Route::post('/product',function() {
    return Product::create([
        "name"=>"test",
        "description"=>"for test",
        "price"=>0,
    ]);
});
```

![](https://i.imgur.com/xEWi5pY.png)

會發現回報錯誤，要求我們使用fillable變數定義該填入的資料欄位，所以至`models/product.php`
```php
class Product extends Model
{
    use HasFactory;
    public $fillable = [
        "name",
        "description",
        "price"
    ];
}
```

![](https://i.imgur.com/tgexHCc.png)


![](https://i.imgur.com/A3Lrekl.png)

我們至剛剛`api.php`中修改post/product
```php
Route::post('/product',function(Request $request) {
    return Product::create([
        "name"=>$request->name,
        "description"=>$request->description,
        "price"=>$request->name,
    ]);
});
```

![](https://i.imgur.com/wKLLKqc.png)

但是，如果有關api的東西都寫在api.php中會造成難以閱讀，於是我們可以使用Controller也就是middleware來幫助我們分離各個應用的api

```php
php artisan make:controller Product
```

![](https://i.imgur.com/emVeROX.png)

至`api.php`中修改product相關路由函式

```php
<?php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;
use \App\Http\Controllers\ProductController; //引入controller

Route::get('/product',[ProductController::class, 'getProduct']);
Route::post('/product',[ProductController::class, 'createProduct']);


Route::get('/test',function() {
    return "Server running";
});


Route::middleware('auth:sanctum')->get('/user', function (Request $request) {
    return $request->user();
});
```

接著至`ProductController.php`

```php
<?php

namespace App\Http\Controllers;
use \App\Models\Product; //引入model
use Illuminate\Http\Request;

class ProductController extends Controller
{
    public function getProduct() {
        return Product::all();
    }

    public function createProduct(Request $request) {
        return Product::create([
            "name"=>$request->name,
            "description"=>$request->description,
            "price"=>$request->price,
        ]);
    }
};

```
`createProduct`
![](https://i.imgur.com/pkKf9Pp.png)

`getProduct`
![](https://i.imgur.com/cSY3A5g.png)


---

### api.php
![](https://i.imgur.com/MQEWwJB.png)

```php
Route::get('/test',function() {
    return "Server running";
});
Route::middleware('auth:sanctum')->get('/user', function (Request $request) {
    return $request->user();
});
```


### Parameter
```php
//127.0.0.1:8000/register/Dennis

Route::get('/register/{name}', function ($name) {
    return $name; //Dennis
 });
```
若參數可有可無
```php
Route::get('/register/{name?}', function ($name=null) {
    return $name; // empty
 });
```
### Body
```php
//127.0.0.1:8000/register

/**
{
  "name": "Dennis",
  "age": 23
}
**/

Route::post('/register', function (Request $request) {
    return $request;
 });
```

---

## Request

獲取請求資料
```php
request()->input();
```
取得請求網址
```php
request()->url();
```
取得請求IP
```php
request()->ip();
```

```php
request()->getUri();
```
取得請求的query **?name=Dennis**
```php
request()->getQueryString();
```
```php
request()->header();
```
```php
request()->method();
```

---





