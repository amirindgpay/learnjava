<div dir="rtl" align="right">

# چالش‌های فاز ۸ — Reflection، Annotation و Method Handle

جواب این فایل جای دیگری است.

## ۱

annotation روی متد هست و `getAnnotation` مقدار `null` می‌دهد. محتمل‌ترین `Retention` غلط کدام است، `SOURCE`، `CLASS`، یا `RUNTIME`؟

## ۲

`setAccessible(true)` روی فیلد private یک ماژول دیگر، در حالی که بسته `open` نشده. چه exceptionی می‌آید؟

## ۳

متد هدف `IllegalArgumentException` پرتاب می‌کند و تو با `Method.invoke` صدا می‌زنی. آن را مستقیم می‌بینی یا پیچیده در نوع دیگری؟

## ۴

`MethodHandles.lookup()` را داخل class دیگری می‌سازی و می‌خواهی متد private کلاس هدف را `findVirtual` کنی. چرا اختیار کافی نیست؟

## ۵

نام متد را همین حالا در منبع می‌دانی و هیچ افزونه‌ای در کار نیست. reflection را انتخاب می‌کنی یا صدا زدن معمولی را؟ یک دلیل هزینه.

## ۶

`invokeExact` را با آرگومان `int` صدا می‌زنی در حالی که `MethodType` پارامتر `Integer` خواسته. چه نوع خطایی می‌آید؟

## ۷

حداقل retention و target را برای annotationی بنویس که در runtime از روی متد خوانده شود. بدنهٔ annotation یک `String value()` دارد. لازم نیست کلاس نمونه را بنویسی.

</div>
