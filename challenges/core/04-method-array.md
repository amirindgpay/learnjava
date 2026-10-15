<div dir="rtl" align="right">

# چالش‌های فاز ۴ — متد و آرایه

جواب این فایل جای دیگری است.

## ۱

بعد از هر فراخوانی، `x` و `scores[0]` چیست؟

```java
static void bump(int n) {
    n = n + 1;
}

static void bumpFirst(int[] scores) {
    scores[0] = scores[0] + 1;
}

static void replace(int[] scores) {
    scores = new int[] {9};
}
```

شروع: `x` برابر ۱ و `scores` برابر `{1, 2}`. هر متد را یک بار با همین‌ها صدا می‌زنی.

## ۲

چرا این جفت متد کامپایل نمی‌شود؟

```java
static int area(int side) {
    return side * side;
}

static double area(int side) {
    return side * side;
}
```

## ۳

خروجی چیست؟

```java
static double average(int a, int b, int c) {
    return (a + b + c) / 3;
}
```

صدا با ۱۰ و ۱ و ۱.

## ۴

باگ را پیدا کن. آرایهٔ خالی نباید برنامه را بیندازد.

```java
static int max(int[] scores) {
    int best = scores[0];
    for (int n : scores) {
        if (n > best) {
            best = n;
        }
    }
    return best;
}
```

## ۵

این `reverse` قرار است آرایهٔ ورودی را دست‌نخورده برگرداند. کجای اثرش به بیرون نشت می‌کند؟

```java
static int[] reverse(int[] scores) {
    for (int i = 0; i < scores.length / 2; i = i + 1) {
        int tail = scores.length - 1 - i;
        int tmp = scores[i];
        scores[i] = scores[tail];
        scores[tail] = tmp;
    }
    return scores;
}
```

## ۶

برای چاپِ هم اندیس و هم مقدار، `for` معمولی را انتخاب می‌کنی یا `for (int n : scores)` را؟ چرا؟

## ۷

یک امضای `average` دوم بنویس که به‌جای سه `int` یک `int[]` بگیرد. لازم نیست بدنه را کامل کنی. بگو این کار چه نامی دارد.

</div>
