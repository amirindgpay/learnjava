<div dir="rtl" align="right">

# فاز ۵ — Exception و try-with-resources

این درسنامه برای Java 21 است. سه چیز را از هم جدا کن: خطایی که کار اصلی شکست، علتِ زیر آن، و خطایی که موقع بستن منبع پیش می‌آید. اگر این‌ها را یکی کنی، علت واقعی گم می‌شود.

## چرا این‌طور کار می‌کند

checked exception زیر `Exception` است و زیر `RuntimeException` نیست. صدازننده باید آن را `catch` کند یا در امضا `throws` کند. unchecked یعنی `RuntimeException` و زیرکلاس‌هایش، و همچنین `Error`. مرز را در API خودت این‌طور بگذار: اگر صدازننده می‌تواند کار معقولی بکند، checked یا یک نتیجهٔ صریح بده. اگر قرارداد متد شکسته (آرگومان غلط، وضعیت غیرممکن)، unchecked. پرتاب کردن checked برای هر پیشامد کوچک، امضا را شلوغ می‌کند و کسی آن را خالی `catch` می‌کند.

chaining یعنی exception تازه، exception قبلی را به‌عنوان `cause` نگه می‌دارد. سازندهٔ دو آرگومانی یا `initCause` همین کار را می‌کند. `getCause` علت را برمی‌گرداند. پیام لایهٔ بالا می‌گوید این لایه چه می‌کرده، و cause می‌گوید زیرش چه شکسته. علت را قورت نده و یک exception تازه بدون cause نساز.

ترتیب `catch` از خاص به عام است. اگر اول `catch (Exception e)` باشد، شاخهٔ خاص‌تر مرده است و کامپایلر زیرکلاس بعدی را رد می‌کند. multi-catch یعنی `catch (A | B e)` برای نوع‌هایی که هیچ‌کدام زیر دیگری نیست. پارامتر این شاخه effectively final است.

try-with-resources هر چیزی را که `AutoCloseable` باشد، بعد از تمام شدن بدنه می‌بندد. اگر چند منبع اعلام کرده باشی، `close` به ترتیب وارونهٔ اعلام است: آخری اول بسته می‌شود، چون اغلب به قبلی وابسته است.

اگر بدنه exception پرتاب کند و `close` هم پرتاب کند، exception بدنه اصلی می‌ماند و exception بستن در `getSuppressed()` می‌نشیند. این همان دلیلی است که بستن دستی داخل `finally` خطرناک است: exception دوم، exception اول را جایگزین می‌کند مگر خودت نگه‌اش داری. try-with-resources این جایگزینی را نمی‌کند.

`AutoCloseable.close` می‌تواند `Exception` پرتاب کند. `Closeable` مخصوص I/O است، `AutoCloseable` را گسترش می‌دهد، و `close` آن فقط `IOException` پرتاب می‌کند. برای منبعی که I/O نیست، `AutoCloseable` کافی است. `Closeable` را فقط وقتی پیاده کن که واقعاً جریان بایتی یا متنی است.

جریان عادی برنامه را با exception هدایت نکن. تمام شدن حلقه، «پیدا نشد» قابل‌انتظار، و انتخاب شاخه، `return` و `if` و `Optional` هستند. exception برای شکستن قرارداد و شکست منبع است. ساخت stack trace ارزان نیست و خواننده را گول می‌زند که یک خرابی واقعی دیده.

`Scanner` را اگر روی `System.in` ساخته‌ای نبند. `close` آن، `System.in` را هم می‌بندد و بقیهٔ برنامه دیگر از ورودی استاندارد نمی‌خواند.

## قاعده

علت را در `cause` نگه دار. بستن را به try-with-resources بسپار تا خطای `close` روی خطای اصلی ننشیند. در `catch` اول نوع خاص‌تر را بگذار. منبع را برای کنترل جریان پرتاب نکن، و ورودی استاندارد را نبند.

## مثال

کار شکسته‌است و یک علت I/O دارد. بستن هم شکسته‌است. در try-with-resources خطای `open` اصلی است و خطای `close` suppressed آن است:

```java
final class Door implements AutoCloseable {
    void open() {
        throw new IllegalStateException("باز نشد", new java.io.IOException("قفل"));
    }

    @Override
    public void close() {
        throw new IllegalStateException("بسته نشد");
    }
}

static void use() {
    try (Door door = new Door()) {
        door.open();
    }
}
```

اگر فقط بخواهی دو شکست هم‌خانواده را یک‌جور ببینی، و هیچ‌کدام والد دیگری نباشد:

```java
try {
    read();
} catch (java.io.EOFException | java.nio.channels.ClosedChannelException e) {
    throw new IllegalStateException("خواندن قطع شد", e);
}
```

## اشتباه رایج

در `finally` خودت `close` را صدا زدن و exception آن را رها کردن. اگر بدنه هم exception داشته باشد، خطای بستن جایش را می‌گیرد و `cause` اصلی در stack trace نیست.

## تمام است وقتی

یک `AutoCloseable` کوچک بنویسی که هم خطای کار (با `cause`) و هم خطای `close` را نشان بدهد، و خطای `close` را suppressed خطای اصلی ببینی.

</div>
