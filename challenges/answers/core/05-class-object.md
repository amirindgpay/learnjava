<div dir="rtl" align="right">

# پاسخ فاز ۵ — کلاس و شیء

## ۱

هر دو خط `1`. `b = a` شیء دوم نمی‌سازد. هر دو نام یک `Counter` هستند.

## ۲

بله. فیلد `static` مال class است، نه مال هر شیء. یک `increment` همان تنها مقدار مشترک را زیاد می‌کند.

## ۳

`balance = balance` پارامتر را به خودش نسبت می‌دهد. فیلد را باید با `this.balance = balance` پر کنی.

## ۴

از پوشهٔ والدِ `bank`، با نام کامل: `java bank.BankAccount`. از داخل پوشه، نام class دیگر `bank.BankAccount` نیست.

## ۵

همان خط فارسی. `println` خودش `toString` را صدا می‌زند.

## ۶

خواندن از class دیگر کامپایل نمی‌شود. `private` فقط داخل خود `BankAccount` دیده می‌شود.

## ۷

```java
BankAccount(int balance) {
    this.balance = balance;
}
```

`this` فیلد را از پارامتر همنام جدا می‌کند.

</div>
