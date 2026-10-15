<div dir="rtl" align="right">

# چالش‌های فاز ۲ — Generics پیشرفته

جواب این فایل جای دیگری است.

## ۱

چرا این overload رد می‌شود؟

```java
void print(List<String> items) {}
void print(List<Integer> items) {}
```

## ۲

`instanceof List<String>` را روی یک `Object` می‌نویسی. خطا چیست، و نزدیک‌ترین چک قانونی کدام است؟

## ۳

کدام خط کامپایل نمی‌شود؟

```java
List<? extends Number> nums = List.of(1, 2);
nums.add(3);
Number n = nums.get(0);
```

## ۴

از `List<? super Integer>` چه نوعی را بدون cast می‌توانی `add` کنی، و `get` چه نوعی برمی‌گرداند؟

## ۵

باگ را پیدا کن. هشدار unchecked را خاموش کرده‌ای.

```java
List<String> names = new ArrayList<>();
List raw = names;
raw.add(1);
String first = names.get(0);
```

خطا کی دیده می‌شود؟

## ۶

چرا `new T[n]` داخل `<T> T[] box(int n)` ساخته نمی‌شود؟

## ۷

امضای `transfer` را بنویس که از یک لیست تولیدکننده به یک لیست مصرف‌کننده بریزد. بدنه لازم نیست.

</div>
