<div dir="rtl" align="right">

# چالش‌های فاز ۱ — محیط و اولین برنامه

جواب این فایل جای دیگری است. هر مورد را خودت تمام کن.

## ۱

فایل را با نام `Main.java` ذخیره کرده‌ای و داخلش این است. `javac Main.java` چه می‌گوید؟

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("سلام");
    }
}
```

## ۲

`javac Hello.java` سالم تمام شده. این فرمان را می‌زنی:

```bash
java Hello.class
```

چه می‌شود و دنبال چه نامی می‌گردد؟

## ۳

خروجی چیست؟

```java
int x = 1; // x = 2;
System.out.println(x);
```

## ۴

فقط همین را زده‌ای، نه `javac` را. برنامه چاپ می‌کند یا نه، و آیا کنار منبع فایل `.class` می‌ماند؟

```bash
java Hello.java
```

`Hello.java` همان class عمومی `Hello` با یک `main` است و package ندارد.

## ۵

باگ را پیدا کن. برنامه قرار است دو خط چاپ کند.

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("یک")
        System.out.println("دو");
    }
}
```

شمارهٔ خطی که `javac` نشان می‌دهد مال کدام جمله است؟

## ۶

کدام کار را اول انجام می‌دهی اگر `java -version` عدد ۲۱ بدهد و `javac -version` عدد ۱۷؟

## ۷

دو فرمان را بنویس که `Hello.java` را در همین پوشه کامپایل کنند و بعد class را اجرا کنند. بگو کدام فایل تازه کنار منبع ظاهر می‌شود.

</div>
