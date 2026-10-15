<div dir="rtl" align="right">

# پاسخ فاز ۴ — Stream، Collector و Optional

## ۱

یک بار. آرگومان `orElse` قبل از خود فراخوانی حساب می‌شود. `orElseGet` چون مقدار هست اجرا نمی‌شود.

## ۲

`Stream<Stream<...>>`. `flatMap` همان لایهٔ اضافه را برمی‌دارد. `map` برنمی‌دارد.

## ۳

`IllegalStateException`. کلید تکراری بدون تابع ادغام خطا است، نه جایگزینی خاموش.

## ۴

لیست مشترک در pipeline موازی مسابقه دارد. نتیجه گم یا خراب می‌شود. تجمیع باید با Collector باشد، نه `add` بیرونی.

## ۵

دو کلید، `true` و `false`. `partitioningBy` طرف خالی را هم در map می‌گذارد.

## ۶

نه. `Optional` نوع برگشت «شاید نباشد» است، نه فیلد. فیلد را با `null` یا یک نوع صریح مدل کن.

## ۷

```java
Collectors.groupingBy(
    Order::city,
    Collectors.teeing(
        Collectors.counting(),
        Collectors.summingLong(Order::amount),
        (count, sum) -> new long[] {count, sum}))
```

تابع آخر `Long` تعداد و `Long` جمع را به یک نتیجه، اینجا `long[]`، بدل می‌کند.

</div>
