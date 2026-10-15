<div dir="rtl" align="right">

# پاسخ فاز ۸ — Reflection، Annotation و Method Handle

## ۱

`CLASS` یا `SOURCE`. هر دو را reflection در runtime نمی‌بیند. برای `getAnnotation` باید `RUNTIME` باشد. `CLASS` در فایل class هست و باز هم `null` می‌دهد.

## ۲

`InaccessibleObjectException`. ماژول بدون `opens` چک دسترسی را حتی بعد از `setAccessible(true)` برنمی‌دارد.

## ۳

پیچیده در `InvocationTargetException`. استثنای خود متد `getCause` آن است.

## ۴

`lookup` اختیار همان کلاسی را دارد که آن خط در آن نوشته شده. private کلاس دیگر از آن lookup دیده نمی‌شود.

## ۵

صدا زدن معمولی. reflection اسم را رشته می‌کند، inline نمی‌شود، و با عوض شدن نام در کامپایل نمی‌شکند.

## ۶

`WrongMethodTypeException`. `invokeExact` نوع آرگومان را دقیق می‌خواهد. `int` با `Integer` یکی نیست.

## ۷

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface Label {
    String value();
}
```

</div>
