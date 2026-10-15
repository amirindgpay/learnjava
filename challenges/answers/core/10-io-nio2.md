<div dir="rtl" align="right">

# پاسخ فاز ۱۰ — فایل: I/O و NIO.2

## ۱

فایل کنار پوشه‌ای که `java` را از آن زده‌ای، نه کنار `.java`. مسیر نسبی به پوشهٔ اجرا بسته است، پس این اجرا `notes.txt` منبع را نمی‌بیند.

## ۲

متن بار دوم. `writeString` فایل را از نو می‌نویسد، نه اینکه به ته آن اضافه کند.

## ۳

`NoSuchFileException` خودش زیر `IOException` است. `catch` دوم مرده است و کامپایلر ردش می‌کند. شاخهٔ خاص باید اول بیاید.

## ۴

`Files.list`. Stream پوشه را باز نگه می‌دارد. `readString` فایل را خودش می‌بندد.

## ۵

`NoSuchFileException`، و چاپ `فایل پیدا نشد` به‌جای stack trace.

## ۶

ادامه بدهد. یک خط خراب دلیل توقف بقیهٔ فایل نیست. همان خط را با شماره‌اش گزارش کن.

## ۷

```java
try (Stream<Path> paths = Files.list(Path.of("."))) {
    paths.filter(path -> path.toString().endsWith(".txt"))
        .forEach(System.out::println);
}
```

</div>
