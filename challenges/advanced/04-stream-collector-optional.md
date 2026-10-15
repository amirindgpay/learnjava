<div dir="rtl" align="right">

# چالش‌های فاز ۴ — Stream، Collector و Optional

جواب این فایل جای دیگری است.

## ۱

`load()` چند بار صدا زده می‌شود؟ `found` از قبل مقدار دارد.

```java
String label = found.orElse(load());
String other = found.orElseGet(this::load);
```

## ۲

`map` که خودش `Stream` برمی‌گرداند چه نوعی می‌سازد، و کدام عمل آن را صاف می‌کند؟

## ۳

`Collectors.toMap` بدون تابع ادغام، و دو عنصر با یک کلید. نتیجه چیست؟

## ۴

باگ را پیدا کن. Stream موازی است و هر دو نخ به یک `ArrayList` بیرون از pipeline `add` می‌کنند.

## ۵

`partitioningBy` روی یک لیست که هیچ عنصرش شرط را ندارد. map چند کلید دارد؟

## ۶

`Optional` را نوع فیلد یک `record` کرده‌ای تا «نبودن» را نشان بدهی. این انتخاب با نقش `Optional` می‌خواند یا نه؟

## ۷

یک `groupingBy` روی `Order::city` بنویس که پایین‌دستش با `teeing` هم `counting` را داشته باشد هم `summingLong(Order::amount)`. تابع آخر را فقط با نوع نتیجه‌اش توصیف کن.

</div>
