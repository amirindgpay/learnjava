<div dir="rtl" align="right">

# چالش‌های فاز ۱ — قابلیت‌های مدرن زبان

جواب این فایل جای دیگری است.

## ۱

این compact constructor کامپایل می‌شود؟

```java
record Range(int from, int to) {
    public Range {
        this.from = from;
    }
}
```

اگر نه، مقداردهی فیلد آخر کار کیست؟

## ۲

`Expr` یک `sealed` با دو `record` است و `switch` روی آن `default` دارد. فردا `record` سوم را به `permits` اضافه می‌کنی. کدام `switch`ها هنوز بی‌صدا کامپایل می‌شوند؟

## ۳

خروجی یا خطا چیست؟ `case null` نداری.

```java
static String sign(Integer n) {
    return switch (n) {
        case Integer i -> "عدد";
    };
}
```

صدا با `null`.

## ۴

چرا دومی کامپایل نمی‌شود؟

```java
return switch (n) {
    case Integer i -> "عدد";
    case Integer i when i < 0 -> "منفی";
};
```

## ۵

text block را با تورفتگی کد نوشته‌ای و `"""` پایانی هم‌ستون با `select` نیست، عقب‌تر است. آن فاصلهٔ مشترک داخل رشته می‌ماند یا حذف می‌شود؟

## ۶

در Java 21، بدون `--enable-preview`، پارامتر بی‌نام `_` را در یک lambda می‌نویسی. این API پایدار ۲۱ است؟

## ۷

بین class قابل‌تغییر، `record`، و `sealed` یکی را برای «وضعیت سفارش که بعداً از `PENDING` به `PAID` عوض می‌شود» انتخاب کن. یک دلیل.

</div>
