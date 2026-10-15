<div dir="rtl" align="right">

# فاز ۱ — قابلیت‌های مدرن زبان

این درسنامه برای Java 21 است. هدفش این است که شکل‌های یک دامنه را با ابزار پایدار زبان ببندی، نه با سلسله‌مراتب باز و `if`های پراکنده.

## چرا این‌طور کار می‌کند

`record` داده‌ای است که هویتش همان فیلدهایش است. کامپایلر از روی componentها canonical constructor، `equals`، `hashCode` و `toString` را می‌سازد. فیلدها `private final` هستند و خود `record` هم `final` است. اگر موقع ساخت قانون داری، compact constructor همان canonical constructor است بدون تکرار فهرست پارامتر: بدنش پارامترها را وارسی یا نرمال می‌کند و بعد کامپایلر همان پارامترها را به فیلدها نسبت می‌دهد. داخل compact constructor خودت به فیلد مقدار نمی‌دهی.

`sealed` مجموعهٔ زیرنوع را می‌بندد. `permits` فهرست مجاز است. هر زیرنوع باید `final`، `sealed` یا `non-sealed` باشد. `record` از قبل `final` است، پس می‌تواند زیر یک `sealed` بنشیند. `non-sealed` یعنی از آن نقطه سلسله‌مراتب دوباره باز است و exhaustiveness دیگر تا ته درخت تضمین نمی‌شود.

چون مجموعه بسته است، `switch` روی آن نوع می‌تواند exhaustive باشد: کامپایلر همهٔ شاخه‌ها را می‌شناسد و `default` لازم نیست. زیرنوع جدید همان `switch`ها را از کامپایل می‌اندازد. این همان چیزی است که class معمولی با زیرکلاس‌های باز به تو نمی‌دهد.

`switch` expression مقدار برمی‌گرداند و باید exhaustive باشد. `switch` statement می‌تواند فقط بعضی حالت‌ها را پوشش بدهد و لازم نیست مقداری تولید کند. شکل فلش (`->`) به case بعدی نشت نمی‌کند. شکل دونقطه‌ای کلاسیک نشت می‌کند، مگر خودت `break` یا `yield` بگذاری.

pattern matching یعنی چک نوع و معرفی متغیر در یک جا. `instanceof` pattern برای یک شاخه کافی است: `value instanceof String text`. در `switch`، pattern روی نوع `sealed` همان exhaustiveness را می‌سازد. record pattern فیلدهای `record` را در همان case باز می‌کند، تا لازم نباشد بعد از تطبیق دوباره `left()` و `right()` را صدا بزنی.

`case null` جدا از `default` است. بدون آن، مقدار `null` در `switch` هنوز `NullPointerException` می‌دهد. `when` شرط اضافه روی همان pattern است؛ اگر برقرار نباشد تطبیق به case بعدی می‌رود.

text block با `"""` یک رشتهٔ چندخطی است. incidental indentation یعنی کمترین تورفتگی مشترکِ خط‌های محتوا حذف می‌شود، و جای `"""` پایانی این تورفتگی را تعیین می‌کند. تورفتگی‌ای که برای قشنگی کد گذاشته‌ای داخل رشته نمی‌ماند.

`_` به‌عنوان unnamed variable در Java 21 هنوز preview است و فقط با `--enable-preview` روشن می‌شود. API پایدار ۲۱ نیست. تا وقتی پایدار نشده، برای مقداری که دور می‌ریزی یک نام واقعی بگذار.

انتخاب را این‌طور ببند: هویت همان فیلدها و بدون تغییر، `record`. هویت جدا از مقدار، یا وضعیتِ قابلِ عوض شدن، class معمولی. تعداد شکل‌ها بسته و `switch` باید جا افتادن یک شکل را در زمان کامپایل بگوید، `sealed`.

## قاعده

زیرنوع `sealed` را نیمه‌باز نگذار. یا `final` / `record` است، یا دوباره `sealed`، یا آگاهانه `non-sealed`. روی نوع بسته `switch` expression بنویس و `default` نگذار. `record` را جایی برنگزین که شیء باید بعد از ساخت عوض شود.

## مثال

مدل بسته. این `switch` بدون `default` کامپایل می‌شود، چون `permits` فقط همین دو `record` است:

```java
sealed interface Expr permits Const, Add {}

record Const(int value) implements Expr {}

record Add(Expr left, Expr right) implements Expr {}

static int eval(Expr expr) {
    return switch (expr) {
        case Const(int value) -> value;
        case Add(Expr left, Expr right) -> eval(left) + eval(right);
    };
}
```

compact constructor پارامتر را رد می‌کند، نه فیلد را. `switch` دوم `null` را از عدد جدا می‌کند و `when` را جلوتر از pattern کلی می‌گذارد:

```java
record Range(int from, int to) {
    public Range {
        if (from > to) {
            throw new IllegalArgumentException("from > to");
        }
    }
}

static String sign(Integer n) {
    return switch (n) {
        case null -> "خالی";
        case Integer i when i < 0 -> "منفی";
        case Integer i -> "نامنفی";
    };
}
```

## اشتباه رایج

گذاشتن `default` روی `switch` یک نوع `sealed`. امروز کامپایل می‌شود، ولی زیرنوع بعدی بی‌صدا داخل `default` می‌افتد و exhaustiveness از بین می‌رود.

## تمام است وقتی

یک مدل دامنهٔ کوچک با `sealed` و `record` بنویسی که `switch` روی آن بدون `default` کامپایل شود.

</div>
