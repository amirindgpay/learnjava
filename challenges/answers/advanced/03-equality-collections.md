<div dir="rtl" align="right">

# پاسخ فاز ۳ — برابری و Collections

## ۱

`HashSet` اندازهٔ ۲ و `TreeSet` اندازهٔ ۱. برابری `record` هر دو فیلد را می‌بیند، ولی `compareTo` فقط `id` را صفر می‌کند. درخت همان را تکراری حساب می‌کند.

## ۲

دو عضو. سطل از `hashCode` والد می‌آید و نوبت به `equals` برای یکی کردن نمی‌رسد.

## ۳

`[a, b]`. پوشش unmodifiable نمای زنده است. تغییر لیست پشتی از راه دیگر، نما را هم عوض می‌کند.

## ۴

`NullPointerException` همان لحظهٔ ساخت. `ArrayList` مقدار `null` را می‌پذیرد. `List.of` نه، و بعداً هم تغییر نمی‌کند.

## ۵

`HashSet` ترتیب ندارد و `SequencedCollection` نیست. برای ترتیب درج `LinkedHashSet` را بگیر.

## ۶

iterator این لیست fail-fast است. حذف در طول `for-each` ساختار را عوض می‌کند و `ConcurrentModificationException` می‌دهد.

## ۷

`ArrayDeque`. دو سر amortized O(1) است و `null` نمی‌گیرد. `LinkedList` برای این صف هزینه و پیچیدگی اضافه دارد.

</div>
