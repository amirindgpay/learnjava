<div dir="rtl" align="right">

# چالش‌های فاز ۵ — کلاس و شیء

جواب این فایل جای دیگری است.

## ۱

خروجی دو خط چیست؟

```java
class Counter {
    int value;

    void increment() {
        value = value + 1;
    }
}
```

```java
Counter a = new Counter();
Counter b = a;
a.increment();
System.out.println(a.value);
System.out.println(b.value);
```

## ۲

اگر `value` را `static` کنی، دو بار `new` و یک `increment` روی فقط یکی از آن‌ها، دیگری را هم عوض می‌کند؟ چرا؟

## ۳

باگ را پیدا کن. موجودی بعد از سازنده هنوز صفر است.

```java
class BankAccount {
    private int balance;

    BankAccount(int balance) {
        balance = balance;
    }
}
```

## ۴

از داخل پوشهٔ `bank` این را می‌زنی و خطا می‌گیری. فرمان درست، از کدام پوشه، چیست؟

```bash
java BankAccount
```

خط اول فایل `package bank;` است و class عمومی `BankAccount` است.

## ۵

`Book` متد `toString` دارد که یک خط فارسی برمی‌گرداند. این چاپ همان خط را می‌آورد یا نام class را؟

```java
System.out.println(book);
```

## ۶

کدام یک کامپایل نمی‌شود: خواندن `balance` از `main` یک class دیگر، یا خواندنش از متد خود `BankAccount`؟ فیلد `private` است.

## ۷

یک سازنده بنویس که پارامتر `balance` را در فیلد همنام بگذارد. از `this` کجا استفاده می‌کنی؟

</div>
