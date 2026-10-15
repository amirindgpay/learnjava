<div dir="rtl" align="right">

# پاسخ فاز ۹ — Lambda و Stream

## ۱

همان `sara` و `ali`، و از خود زنجیره چیزی چاپ نمی‌شود. عمل پایانی نیست، پس pipeline اجرا نمی‌شود و منبع را هم عوض نمی‌کند.

## ۲

`UnsupportedOperationException`. `toList` در Java 16 به بعد لیست غیرقابل‌تغییر می‌دهد.

## ۳

`NoSuchElementException`. میانگین لیست خالی تهی است. قبل از `getAsDouble` باید `isPresent` را ببینی.

## ۴

نتیجهٔ جدا. `sorted` روی Stream ترتیب منبع `List` را عوض نمی‌کند.

## ۵

صدا زدن متد روی `null`. `orElse` اگر تهی باشد جایگزین را برمی‌گرداند و اینجا به `null` دست نمی‌زند.

## ۶

`for`. یک پیمایش ساده با حلقه روشن‌تر است. Stream را برای زنجیرهٔ فیلتر و تبدیل نگه دار.

## ۷

```java
names.stream()
    .filter(name -> name.length() > 4)
    .sorted()
    .toList();
```

جای `filter` می‌توانی `name -> name.length() > 4` را همین‌طور بگذاری. method reference این شرط را کوتاه‌تر نمی‌کند.

</div>
