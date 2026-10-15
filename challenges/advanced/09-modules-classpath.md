<div dir="rtl" align="right">

# چالش‌های فاز ۹ — Module و مرز classpath

جواب این فایل جای دیگری است.

## ۱

JAR دارای `module-info` را روی classpath می‌گذاری. بستهٔ export‌نشده هنوز از بقیهٔ classpath دیده می‌شود؟ چرا مرز ماژول این‌جا نیست؟

## ۲

`exports` را روی نام class نوشته‌ای نه نام بسته. این خط درست است؟

```java
exports com.example.api.Api;
```

## ۳

بسته export شده ولی `opens` نشده. کامپایل به نوع public موفق است. `setAccessible` روی فیلد private از ماژول دیگر چه می‌شود؟

## ۴

ماژول نام‌دار می‌تواند `requires` به unnamed module بدهد؟ unnamed module کدام کد است؟

## ۵

JAR بدون `module-info` را روی module path می‌گذاری. automatic module است یا بخشی از unnamed module؟ همهٔ بسته‌هایش export می‌شوند؟

## ۶

ابزار تست فقط باید به یک بستهٔ داخلی reflection کند. `opens` بی‌مقصد را انتخاب می‌کنی یا `opens ... to` همان ابزار را؟

## ۷

دو خط `module-info` بنویس: ماژول `com.example.api` فقط بستهٔ `com.example.api` را export کند، و ماژول `com.example.app` آن را `requires` کند. بستهٔ `com.example.internal` در هیچ exports نباشد.

</div>
