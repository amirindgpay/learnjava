<div dir="rtl" align="right">

# چالش‌های فاز ۷ — Concurrency و Java Memory Model

جواب این فایل جای دیگری است.

## ۱

`count` از نوع `volatile int` است و چند نخ `count++` می‌کنند. atomicity برقرار است؟ visibility چطور؟

## ۲

یک نخ فیلدهای معمولی را پر می‌کند و آخر `ready` از نوع `volatile` را `true` می‌کند. نخ دیگر اول `ready` را `true` می‌بیند. نوشتن‌های قبل از آن را هم می‌بیند؟ نام رابطه چیست؟

## ۳

در Java 21 یک virtual thread داخل `synchronized` روی سوکت بلوکه می‌شود. به carrier چه می‌شود؟ `ReentrantLock` همین pin را دارد؟

## ۴

`StructuredTaskScope` را در کد Java 21 بدون preview صدا می‌زنی. چرا این API پایدار ۲۱ نیست؟

## ۵

فرق `shutdown` و `shutdownNow` را در یک جمله بگو: کارِ در حال اجرا و صفِ شروع‌نشده.

## ۶

باگ را پیدا کن. استخر دو نخی است. هر task منتظر `Future` یک task دیگر است که هنوز وارد استخر نشده، چون هر دو جا پر است.

## ۷

در thread dump دو نخ `BLOCKED` هستند. هر کدام `waiting to lock` مانیتوری است که دیگری `locked` کرده. نام این وضعیت چیست؟

</div>
