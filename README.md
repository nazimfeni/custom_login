CUstom Login us developed for practice purpose only using Laravel 10

**Steps:**
Step 1: Setting Up Laravel Project
composer create-project --prefer-dist laravel/laravel custom_login
step-2: Now go to the project directory using command  
cd custom_login 
Step 3: Create and Configuring Database Connection in .env file. You have to configure according to your system
DB_DATABASE=custom_login
DB_USERNAME=root
DB_PASSWORD=root
Step 4: Now run the project
php artisan migrate

Step 5: Creating Custom Controllers
php artisan make:controller CustomAuthController

Step 6: Create Auth Blade View Files under /resources/view/auth folder

layouts.blade.php
login.blade.php
register.blade.php
dashboard.blade.php

Step 7: Create a middleware named: DisableAuthCaching  



Step 8: Creating Auth Routes
```php
<?php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\CustomAuthController;
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
*/
Route::get('/', function () {
    return view('home');
});


Route::get('dashboard', [CustomAuthController::class, 'dashboard'])->name('dashboard');
Route::get('login', [CustomAuthController::class, 'index'])->name('login');
Route::post('custom-login', [CustomAuthController::class, 'customLogin'])->name('login.custom');
Route::get('register', [CustomAuthController::class, 'registration'])->name('register');
Route::post('custom-registration', [CustomAuthController::class, 'customRegistration'])->name('register.custom');
Route::get('signout', [CustomAuthController::class, 'signOut'])->name('signout');


Route::group(['middleware' => ['web', DisableAuthCaching::class]], function () {
    Route::get('dashboard', [CustomAuthController::class, 'dashboard'])->name('dashboard');
    Route::get('login', [CustomAuthController::class, 'index'])->name('login');
    Route::post('custom-login', [CustomAuthController::class, 'customLogin'])->name('login.custom');
    Route::get('register', [CustomAuthController::class, 'registration'])->name('register');
    Route::post('custom-registration', [CustomAuthController::class, 'customRegistration'])->name('register.custom');
    Route::get('signout', [CustomAuthController::class, 'signOut'])->name('signout');
});
```



