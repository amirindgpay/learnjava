<div dir="rtl" align="right">

# فاز ۸ — Reflection، Annotation و Method Handle

این درسنامه برای Java 21 است. صدا زدن معمولی، هم سریع‌تر است هم با عوض شدن نام می‌شکند در زمان کامپایل. Reflection و `MethodHandle` را فقط جایی بیاور که در زمان کامپایل هدف را نمی‌شناسی.

## چرا این‌طور کار می‌کند

اگر کلاس و متد را همین حالا می‌شناسی، آن را مستقیم صدا بزن. reflection برای وقتی است که نام یا وجود عضو در زمان اجرا معلوم می‌شود: یک ابزار، یک آزمون‌گر، یک افزونه. هزینهٔ این انتخاب این است که تغییر نام دیگر خطای کامپایل نیست، و JVM این صدا را مثل صدا زدن معمولی inline نمی‌کند.

`Class` درِ نوع است. از شیء با `getClass()`، از نام با `Class.forName`، یا از literal با `String.class`. `getMethod` متد public، از جمله به ارث رسیده، را می‌دهد. `getDeclaredMethod` متد اعلام‌شده در خود این کلاس را می‌دهد، حتی اگر private باشد، ولی به ارث رسیده را نه. `Field` همین فرق را برای فیلد دارد. `Method.invoke` آرگومان را به‌صورت `Object` می‌گیرد و exception متد را در `InvocationTargetException` می‌پیچد.

`setAccessible(true)` چک دسترسی زبان را برای آن عضو کنار می‌گذارد. ماژول این را محدود می‌کند. اگر بسته `open` نشده باشد، حتی با `setAccessible` از ماژول دیگر `InaccessibleObjectException` می‌گیری. دور زدنش با پرچم خط فرمان، شکستن مرز ماژول است، نه راه‌حل برنامه. فاز ماژول همین `opens` را جداگانه می‌گوید.

annotation به‌تنهایی در runtime هیچ کاری نمی‌کند. باید کسی آن را بخواند. retention تعیین می‌کند اثر تا کجا بماند. `SOURCE` را کامپایلر دور می‌ریزد و در class file نیست. `CLASS` در bytecode هست ولی JVM آن را پیش‌فرض بار نمی‌کند، پس reflection نمی‌بیندش. `RUNTIME` در runtime از راه `getAnnotation` خوانده می‌شود. اگر می‌خواهی روی متد بخوانی، retention باید `RUNTIME` باشد و هدفش هم `METHOD`.

`MethodHandle` یک اشارهٔ قابلِ صدا زدن به متد است، نزدیک‌تر به JVM تا `Method.invoke`. `MethodHandles.lookup()` یک `Lookup` با اختیار همان کلاسی که این خط در آن است می‌سازد. اختیار، caller-sensitive است: از کلاس دیگر، عضو private این کلاس را پیدا نمی‌کنی. `findVirtual` متد نمونه را با `MethodType` (نوع برگشت و نوع پارامترها) پیدا می‌کند. `invokeExact` نوع‌ها را دقیق می‌خواهد. `invoke` تبدیل‌های بیشتری را تحمل می‌کند و کمی کندتر و شل‌تر است. برای کد خودت `invokeExact` را وقتی نوع‌ها را می‌دانی ترجیح بده.

`VarHandle` همین ایده برای فیلد است. `findVarHandle` فیلد را به یک دسترسی شفاف وصل می‌کند: خواندن، نوشتن، و عمل atomic مثل `compareAndSet`، بدون قفل جدا اگر خود عمل atomic کافی است. از reflection برای فیلدی که زیاد خوانده و نوشته می‌شود ارزان‌تر و دقیق‌تر است، و هنوز از دسترسی مستقیم به فیلد شکننده‌تر است.

شکنندگی مشترک است. اسم به‌صورت `String` است، پس refactor آن را دنبال نمی‌کند. دسترسی غیرقانونی امروز ممکن است با بستن ماژول فردا بشکند. اگر در ساعت این متد را میلیون بار صدا می‌زنی، صدا زدن معمولی یا یک interface که خودت طراحی کرده‌ای ارزان‌تر و روشن‌تر است.

## قاعده

متد را مستقیم صدا بزن، مگر هدف در زمان کامپایل معلوم نباشد. annotationی که می‌خواهی در runtime بخوانی `RetentionPolicy.RUNTIME` است. برای یک صدا زدن غیرمستقیم که نوعش را می‌دانی، `MethodHandle` را به `Method.invoke` ترجیح بده. `setAccessible` را راهِ عبور از ماژول حساب نکن.

## مثال

annotation با retention درست، و خواندن آن از روی متد:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface Label {
    String value();
}

class Sample {
    @Label("سلام")
    String hello() {
        return "سلام";
    }
}
```

همان متد، یک بار، با `MethodHandle`. `lookup` باید جایی باشد که اجازهٔ دیدن `hello` را دارد:

```java
MethodHandles.Lookup lookup = MethodHandles.lookup();
MethodHandle handle = lookup.findVirtual(
        Sample.class, "hello", MethodType.methodType(String.class));
String text = (String) handle.invokeExact(new Sample());
```

## اشتباه رایج

`@Retention(RetentionPolicy.CLASS)` یا فراموش کردن retention، و بعد `getAnnotation` که `null` برمی‌گرداند. annotation روی متد هست، ولی به runtime نرسیده.

## تمام است وقتی

یک annotation با `RUNTIME` بنویسی، آن را از روی یک متد بخوانی، و همان متد را یک بار با `MethodHandle` صدا بزنی.

</div>
