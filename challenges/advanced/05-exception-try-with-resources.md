<div dir="rtl" align="right">

# چالش‌های فاز ۵ — Exception و try-with-resources

جواب این فایل جای دیگری است.

## ۱

بدنهٔ `try` استثنای `open` را پرتاب می‌کند و `close` استثنای `close` را. کدام اصلی است و آن یکی را از کجا می‌خوانی؟

## ۲

همان دو استثنا، ولی `close` را خودت در `finally` صدا می‌زنی و استثنای `close` را نمی‌گیری. کدام استثنا به بیرون می‌رسد؟

## ۳

چرا این `catch` کامپایل نمی‌شود؟

```java
catch (IOException e) {
    // ...
} catch (NoSuchFileException e) {
    // ...
}
```

## ۴

`catch (FileNotFoundException | IOException e)` چه اشکالی دارد؟

## ۵

دو منبع در پرانتز `try` اعلام شده‌اند: اول `outer`، بعد `inner`. ترتیب `close` چیست؟

## ۶

منبع تو جریان بایت نیست و `close`اش `Exception` می‌دهد نه فقط `IOException`. `AutoCloseable` را پیاده می‌کنی یا `Closeable` را؟

## ۷

یک `throw` بنویس که `IllegalStateException` با پیام `باز نشد` بسازد و علتش یک `IOException` با پیام `قفل` باشد.

</div>
