<div dir="rtl" align="right">

# چالش‌های فاز ۳ — شرط و حلقه

جواب این فایل جای دیگری است.

## ۱

`label` آخر چیست؟

```java
int choice = 1;
String label = "";
switch (choice) {
    case 1:
        label += "A";
    case 2:
        label += "B";
    default:
        label += "C";
}
```

## ۲

همان انتخاب با فلش. خروجی چیست، و چرا با سؤال قبل فرق دارد؟

```java
String label = switch (choice) {
    case 1 -> "A";
    case 2 -> "B";
    default -> "C";
};
```

`choice` برابر ۱ است.

## ۳

`n` در پایان چند است؟

```java
int n = 0;
do {
    n = n + 1;
} while (false);
```

## ۴

باگ را پیدا کن. قرار بوده اعداد ۱ تا ۳ چاپ شوند.

```java
int n = 1;
while (n <= 3) {
    System.out.println(n);
}
```

قبل از نوشتن حلقه، جملهٔ پایان را بگو.

## ۵

برای عدد ۱۵ این متد چه برمی‌گرداند؟ ترتیب شرط‌ها را مقصر بدان یا نه.

```java
static String fizz(int n) {
    if (n % 3 == 0) {
        return "Fizz";
    } else if (n % 5 == 0) {
        return "Buzz";
    } else if (n % 15 == 0) {
        return "FizzBuzz";
    }
    return String.valueOf(n);
}
```

## ۶

کدام اعداد چاپ می‌شوند؟

```java
for (int n = 1; n <= 5; n = n + 1) {
    if (n == 3) {
        continue;
    }
    if (n == 5) {
        break;
    }
    System.out.println(n);
}
```

## ۷

این `switch` expression کامپایل می‌شود؟ اگر نه، چه چیزی کم است؟

```java
static String name(int choice) {
    return switch (choice) {
        case 1 -> "جمع";
        case 2 -> "تفریق";
    };
}
```

## ۸

یک `for` بنویس که ۱۲، ۱۴، ۱۶ را چاپ کند و جملهٔ پایانش این باشد: تمام می‌شود وقتی عدد از ۱۶ بزرگ‌تر شود.

</div>
