<div dir="rtl" align="right">

# پاسخ فاز ۲ — Generics پیشرفته

## ۱

بعد از erasure هر دو `print(List)` هستند. overload روی آرگومان نوعی که پاک می‌شود مجاز نیست.

## ۲

کامپایلر رد می‌کند، چون نوع عنصر در زمان اجرا نیست. چک قانونی `instanceof List` یا `instanceof List<?>` است و نوع عنصر را ثابت نمی‌کند.

## ۳

`nums.add(3)`. تولیدکنندهٔ `? extends` را نمی‌شود پر کرد. `get` به‌صورت `Number` مجاز است.

## ۴

`Integer` را می‌توانی `add` کنی. `get` فقط `Object` می‌دهد، چون نوع واقعی شاید والد `Integer` باشد.

## ۵

موقع `names.get(0)`، نه موقع `add`. لیست خام هشدار را دور می‌زند و `ClassCastException` را به خواندن موکول می‌کند.

## ۶

آرایه نوع اجزا را در اجرا نگه می‌دارد و `T` پاک شده. کامپایلر آرایه‌ای نمی‌سازد که نتواند store آن را چک کند.

## ۷

```java
static <T> void transfer(List<? extends T> from, List<? super T> to)
```

مبدأ `extends` است و مقصد `super`.

</div>
