<div dir="rtl" align="right">

# پاسخ فاز ۵ — Exception و try-with-resources

## ۱

`open` اصلی است. `close` در `getSuppressed()` همان استثناست. try-with-resources خطای بستن را جای خطای بدنه نمی‌گذارد.

## ۲

استثنای `close`. پرتاب در `finally` استثنای بدنه را جایگزین می‌کند، مگر خودت نگه‌اش داری.

## ۳

`NoSuchFileException` زیر `IOException` است و `catch` اول آن را قبلاً برداشته. شاخهٔ دوم مرده است.

## ۴

دو نوع در multi-catch نباید نسبت والد و فرزند داشته باشند. `FileNotFoundException` خودش `IOException` است.

## ۵

اول `inner`، بعد `outer`. بستن وارونهٔ ترتیب اعلام است.

## ۶

`AutoCloseable`. `Closeable` برای I/O است و `close` آن فقط `IOException` پرتاب می‌کند.

## ۷

```java
throw new IllegalStateException("باز نشد", new IOException("قفل"));
```

آرگومان دوم `cause` است.

</div>
