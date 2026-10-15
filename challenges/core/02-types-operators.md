<div dir="rtl" align="right">

# چالش‌های فاز ۲ — نوع، متغیر و عملگر

جواب این فایل جای دیگری است.

## ۱

هر سه چاپ چه عددی است؟

```java
System.out.println(5 / 2);
System.out.println(5 / 2.0);
System.out.println((double) (5 / 2));
```

## ۲

خروجی چیست؟

```java
System.out.println(-3 / 2);
System.out.println(2_000_000_000 * 2);
```

متغیر دوم در محدودهٔ `int` نمی‌ماند. خطا می‌آید یا یک عدد دیگر؟

## ۳

خروجی دو خط چیست؟

```java
String a = "exit";
String b = new String("exit");
System.out.println(a == b);
System.out.println(a.equals(b));
```

## ۴

باگ را پیدا کن. میانگین دو نمرهٔ صحیح باید جزء اعشاری داشته باشد.

```java
int first = 1;
int second = 2;
double mean = (double) (first / second);
```

## ۵

این برنامه عدد ۱۲ و بعد کلمهٔ `hello` را در ورودی دارد. خط دوم چه چاپ می‌کند؟

```java
Scanner scanner = new Scanner("12\nhello");
int n = scanner.nextInt();
String line = scanner.nextLine();
System.out.println(n);
System.out.println("[" + line + "]");
```

## ۶

کدام را برای مقایسهٔ ورودی کاربر با متن `خروج` انتخاب می‌کنی، و چرا آن یکی غلط است: `==` یا `equals`؟

## ۷

عبارت را طوری بنویس که `passed / total` وقتی هر دو `int` هستند حاصل اعشاری بدهد. تبدیل را کجا می‌گذاری؟

## ۸

خروجی چیست؟

```java
System.out.println('A' + 1);
```

</div>
