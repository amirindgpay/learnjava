<div dir="rtl" align="right">

# چالش‌های فاز ۷ — Exception و Generics

جواب این فایل جای دیگری است.

## ۱

کاربر به‌جای عدد کلمه تایپ کرده، `InputMismatchException` را گرفته‌ای و دوباره `nextInt` می‌زنی. چرا حلقه تمام نمی‌شود؟

## ۲

این متد کامپایل می‌شود؟ `InvalidAgeException` زیرکلاس `Exception` است و زیر `RuntimeException` نیست.

```java
static int parseAge(String text) throws InvalidAgeException {
    throw new InvalidAgeException(text);
}
```

اگر `throws` را برداری چه می‌شود؟

## ۳

خروجی چیست؟

```java
static int pick() {
    try {
        return 1;
    } finally {
        return 2;
    }
}
```

## ۴

باگ را پیدا کن. پیام فقط می‌گوید خطا، و مقدار بد سن در آن نیست.

```java
throw new InvalidAgeException("خطا");
```

سن خوانده‌شده `-4` بوده.

## ۵

بستن این `Scanner` چه چیز دیگری را هم می‌بندد؟

```java
Scanner scanner = new Scanner(System.in);
scanner.close();
```

## ۶

خروجی یا خطا چیست؟

```java
Integer boxed = null;
int n = boxed;
```

## ۷

یک `Box<String>` و یک `Box<Integer>` از همان class. آیا دو فایل class جدا ساخته می‌شود؟ یک جمله بگو `put` کردن عدد در جعبهٔ رشته در کدام مرحله رد می‌شود، کامپایل یا اجرا.

</div>
