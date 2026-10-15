<div dir="rtl" align="right">

# چالش‌های فاز ۱۰ — فایل: I/O و NIO.2

جواب این فایل جای دیگری است.

## ۱

`notes.txt` کنار فایل `.java` است. برنامه را از پوشهٔ والد اجرا می‌کنی. `Path.of("notes.txt")` کدام فایل را می‌بیند؟

## ۲

`Files.writeString` را دو بار روی یک مسیر صدا می‌زنی، بار دوم با متن کوتاه‌تر. محتوای فایل کدام است؟

## ۳

باگ را پیدا کن. شاخهٔ «فایل پیدا نشد» هرگز اجرا نمی‌شود. این کد کامپایل هم نمی‌شود.

```java
try {
    Files.readString(path);
} catch (IOException e) {
    System.out.println(e.getMessage());
} catch (NoSuchFileException e) {
    System.out.println("فایل پیدا نشد");
}
```

## ۴

کدام فراخوانی را باید در try-with-resources بگذاری: `Files.readString` یا `Files.list`؟ چرا آن یکی را خود متد می‌بندد؟

## ۵

فایل نیست. برنامه stack trace چاپ می‌کند. به‌جای آن چه نوع exception را جدا می‌گیری و چه جمله‌ای چاپ می‌کنی؟

## ۶

یک خط `scores.csv` این است: `nima,x`. بقیهٔ خط‌ها عدد درست دارند. برنامه باید بایستد یا همان خط را گزارش کند و ادامه بدهد؟

## ۷

بلوک try-with-resources را بنویس که `Files.list(Path.of("."))` را ببندد و فقط نام‌هایی را که به `.txt` ختم می‌شوند چاپ کند.

</div>
