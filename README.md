# ZDB - پایگاه داده Key-Value سبک بر پایه SQLite

## با امنیت SQLite3 و به راحتی داده های پایتون !

ZDB یک دیتابیس **Key-Value ساده و سبک** با استفاده از SQLite است.  
این کتابخانه امکاناتی مثل **ذخیره‌سازی خودکار، صف تغییرات (queue)، کش داخلی، عملیات اتمیک و پشتیبانی از مدل‌ها** را فراهم می‌کند تا ذخیره‌سازی محلی سریع و راحت باشد، بدون نیاز به دیتابیس کامل.

![icon](https://zdb.parssource.ir/icon.ico)

---

### **ZDB** » **Z**ereOne **D**ata **B**ase

## ویژگی‌ها / Features

- رابط کاربری ساده Key-Value (`db[key] = value`)  
- پشتیبانی از انواع داده‌ها: `int`, `str`, `float`, `list`, `dict` و ساختارهای تو در تو  
- **Proxy types**: `ZValue`, `ZList`, `ZDict` برای track خودکار تغییرات و ذخیره‌سازی  
- ذخیره خودکار و **صف تغییرات** برای عملکرد بهتر  
- **کش داخلی** برای افزایش سرعت خواندن داده‌ها  
- پشتیبانی از **backup** دستی یا دوره‌ای  
- عملیات اتمیک (`increment`, `append_if_not_exists`)  
- مدیریت تراکنش‌ها (`with db.transaction():`)  
- پشتیبانی اختیاری از **Model** با type hints و multi-table  
- پشتیبانی از namespace برای چند جدول در یک دیتابیس  
- رمزگذاری اختیاری با SQLCipher  
- نسخه سینک (sync) کامل، نسخه async جداگانه

---

## نصب / Installation

نسخه سینک ZDB با کتابخانه‌های داخلی پایتون کار می‌کند:  
`sqlite3`, `json`, `threading`, `os`, `shutil` و غیره.  

```bash
pip install zDataBase
```

## بارگذاری دیتابیس

```python
from zDataBase import DataBase

db = DataBase("users") # بارگذاری دیتابیس 
```

### ورودی های کلاس DataBase »
<li>name_db = str نام دیتابیس</li>
<li>auto_save = True سیو شدن خودکار دیتابیس بعد از هر تغییر</li>
<li>use_queue = True قرار گرفتن تغییرات در صف</li>
<li>queue_interval = 0.5 ذخیره شدن دیتابیس از x ثانیه</li>
<li>max_batch = 500 حداکثر تغییرات در یک صف</li>
<li>backup = str | None نوع بک آپ » always(بعد از هر تغییر) یا interval(هر backup_interval ثانیه یک بار)</li>
<li>backup_interval = 60 مقدار ایستادن برای هر سیو بک آپ</li>
<li>use_sqlcipher = False استفاده از رمزنگاری</li>
<li>cipher_key = None رمز رمزنگاری</li>
<li>cache_enabled = True کش دیتابیس</li>
<li>cache_max_items = 10000 حداکثر آیتمی که کش نگه میدارد</li>


## تنظیم مقدار

```python
db["name"] = "mohammad"
db["profile"] = {"age":17,"skills":["python","fast_rub"]}
db["numbers"] = [1,2,3]
db["numbers"].append(4)

db.save() # سیو)در صورتی که اتو سیو فعال نباید نیاز است)
db.close() # بستن دیتابیس برای آزاد شدن منابع 
```
<hr>

## ساخت مدل

```python
from zDataBase import DataBase, Model

class UserModel(Model): # مدل 
    age: int
    name: str
    last_name: str

users = DataBase("users") # دیتابیس 

users.register_model(UserModel) # ثبت مدل برای دیتابیس

user = UserModel() # ساخت یک شی برای مدل 
user.age = 20 # تنظیم مقدار سن در شی 
user.name = "My Name" # تنظیم مقدار نام در شی 
user.last_name = "My Last Name" # تنظیم مقدار نام خانوادگی در شی 

users.model_save(user, key="user123") # ذخیره شی در دیتابیس با کلید user123

users.close() # بستن دیتابیس برای آزادس سازی منابع
```

## سایر متود ها

<li>save() - ذخیره دیتابیس به صورت دستی</li>
<li>register_model(model_cls: Type[Model])</li>
<li>model_save(model_obj: Model,key:str) ذخیره با شی</li>
<li>model_get(model_cls: Type[Model],key:str) گرفتن مقدار از مدل</li>
<li>keys() - گرفتن تمامی کلید ها</li>
<li>items() - گرفتن تمام آیتم ها</li>
<li>close() - بستن دیتابیس برای آزاد شدن منابع</li>
<li>drop() - حذف کامل دیتابیس(بدون راه بازگشت بجز بک آپ)</li>
<li>clear() - پاکسازی دیتابیس</li>
<li>get(key,defult=None) - گرفتن مقدار از دیتابیس</li>

# [GitHub | گیت هاب](https://GitHub.com/OandONE/ZDB)

# [PyPI](https://pypi.org/project/zDataBase)

# Seyyed Mohamad Hosein Moosavi Raja(01)
