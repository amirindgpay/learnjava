<div dir="rtl" align="right">

# پاسخ فاز ۹ — Module و مرز classpath

## ۱

بله دیده می‌شود. کد classpath در unnamed module بار می‌شود و `exports` دیگر مرز اجرا نیست.

## ۲

نه. `exports` نام بسته است، نه نام کلاس. خط درست `exports com.example.api;` است.

## ۳

کامپایل نوع public برقرار می‌ماند. `setAccessible` روی عضو private از ماژول دیگر `InaccessibleObjectException` می‌دهد، چون `opens` نیست.

## ۴

نه. unnamed module نام ندارد. همان کدی است که روی classpath است، نه روی module path.

## ۵

automatic module. همهٔ بسته‌هایش export می‌شوند و این مرز سخت نیست. اگر همان JAR روی classpath باشد، unnamed module است.

## ۶

`opens ... to` همان ابزار. `opens` بی‌مقصد به هر ماژولی اجازهٔ reflection عمیق می‌دهد.

## ۷

```java
module com.example.api {
    exports com.example.api;
}
```

```java
module com.example.app {
    requires com.example.api;
}
```

نبودن `com.example.internal` در `exports` یعنی از `app` دیده نمی‌شود.

</div>
