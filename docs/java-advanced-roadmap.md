# نقشه راه Java Advanced

برای کسی که Java Core را دارد: نحو، OOP، Collections، exception، generics مقدماتی، فایل، و lambda / Stream مقدماتی.

نسخهٔ هدف: **Java 21**. این نقشه از شکاف‌های مدرن زبان شروع می‌شود و به JVM می‌رسد. Spring، وب، Android و فریم‌ورک در آن نیست. مطالب نقشهٔ Core اینجا تکرار نمی‌شود.

چیزی که در Java 21 هنوز preview است، در همان بند با همین وضعیت آمده و API پایدار ۲۱ حساب نمی‌شود.

---

## فاز ۱ — قابلیت‌های مدرن زبان

**هدف:** نوع و شاخه‌بندی را با ابزار پایدار Java 21 مدل کنی، نه با سلسله‌مراتب شلخته.

**موضوع‌ها**

- [ ] `record`: canonical constructor، compact constructor، محدودیت فیلد
- [ ] `sealed` class و `sealed` interface، `permits`، `non-sealed`، `final`
- [ ] exhaustiveness در `switch` روی نوع `sealed`
- [ ] `instanceof` pattern
- [ ] pattern matching برای `switch`، از جمله `null` و `when`
- [ ] record pattern
- [ ] unnamed variable: `_`
- [ ] `switch` expression در برابر `switch` statement
- [ ] text block و incidental indentation
- [ ] انتخاب بین `record`، class، و `sealed`

**باید بتوانی بسازی:** یک مدل دامنهٔ کوچک با `sealed` و `record` که `switch` روی آن exhaustive باشد.

## فاز ۲ — Generics پیشرفته

**هدف:** امضای generic را طوری بنویسی که erasure و جهت داده را خودت دیدی باشی.

**موضوع‌ها**

- [ ] type erasure و اثرش روی overload و `instanceof`
- [ ] bounded type parameter
- [ ] wildcard: `? extends` و `? super`
- [ ] PECS
- [ ] تفاوت `List<String>`، `List<?>` و capture
- [ ] heap pollution و هشدار unchecked
- [ ] انتخاب بین پارامتر نوع و wildcard
- [ ] generic و آرایه؛ چرا `new T[]` ساخته نمی‌شود
- [ ] bridge method، در حد دیدن در bytecode

**باید بتوانی بسازی:** یک API کوچک که تولیدکننده و مصرف‌کننده را با PECS جدا کرده باشد.

## فاز ۳ — برابری و Collections

**هدف:** قرارداد برابری را با انتخاب ساختار و هزینهٔ دسترسی یکی کنی.

**موضوع‌ها**

- [ ] قرارداد `equals`: reflexive، symmetric، transitive، consistent، و `null`
- [ ] `hashCode` هم‌قرارداد با `equals`
- [ ] `Comparable` و سازگاری‌اش با `equals`
- [ ] `Comparator`: `thenComparing`، ترتیب `null`
- [ ] پیچیدگی `ArrayList`، `LinkedList`، `ArrayDeque`، `HashMap`، `TreeMap`، `HashSet`، `TreeSet`
- [ ] انتخاب ساختار: دسترسی، ترتیب، یکتایی، درج در دو سر
- [ ] `List.of`، `Set.of`، `Map.of`، `copyOf`
- [ ] unmodifiable wrapper در برابر collection واقعاً immutable
- [ ] `SequencedCollection` در Java 21
- [ ] collision و ظرفیت `HashMap`، در حد مفهوم
- [ ] iterator از نوع fail-fast و `ConcurrentModificationException`

**باید بتوانی بسازی:** یک نوع دامنه با `equals` / `hashCode` / `Comparable` که در `HashSet` و `TreeSet` درست بنشیند.

## فاز ۴ — Stream، Collector و Optional

**هدف:** تجمیع را با Collector درست جمع کنی و نبودن مقدار را از `null` جدا نگه داری.

**موضوع‌ها**

- [ ] `IntStream`، `LongStream`، `DoubleStream`
- [ ] `flatMap`
- [ ] `groupingBy`، `partitioningBy`، `toMap`
- [ ] `mapping`، `collectingAndThen`، `teeing`
- [ ] Collector سفارشی، در حد چهار تابع supplier / accumulator / combiner / finisher
- [ ] short-circuit: `findFirst`، `anyMatch`، `limit`
- [ ] parallel stream: کی ترتیب و کی هزینهٔ مشترک خراب می‌شود
- [ ] side effect داخل pipeline
- [ ] `Optional`: `map`، `flatMap`، `or`، `orElse` در برابر `orElseGet`، `orElseThrow`
- [ ] `Optional` به‌عنوان نوع برگشت، نه فیلد و نه پارامتر

**باید بتوانی بسازی:** یک گزارش تجمیعی با `groupingBy` و یک Collector ترکیبی، بدون `NullPointerException` برای مقدار غایب.

## فاز ۵ — Exception و try-with-resources

**هدف:** خطای اصلی، علت، و خطای بستن منبع را از هم جدا کنی.

**موضوع‌ها**

- [ ] checked در برابر unchecked؛ مرز پرتاب در API خودت
- [ ] exception chaining و `cause`
- [ ] ترتیب `catch` و multi-catch
- [ ] try-with-resources و ترتیب `close`
- [ ] suppressed exception
- [ ] `AutoCloseable` در برابر `Closeable`
- [ ] خطای `close` که exception اصلی را نپوشاند
- [ ] استفاده نکردن از exception برای کنترل جریان عادی
- [ ] `Scanner` روی `System.in` را نبند

**باید بتوانی بسازی:** یک `AutoCloseable` ساختگی که هم خطای کار و هم خطای `close` را با `cause` و suppressed نشان بدهد.

## فاز ۶ — I/O و NIO.2

**هدف:** متن و بایت را با charset و بافر مشخص جابه‌جا کنی، نه با پیش‌فرض پنهان.

**موضوع‌ها**

- [ ] `Path`، `Files`، `walk`، بازدید پوشه
- [ ] charset صریح، UTF-8، و خواندن با charset غلط
- [ ] buffering: `BufferedReader` و `BufferedWriter`؛ کی لازم است
- [ ] `ByteBuffer`: `flip`، `clear`، `compact`
- [ ] `FileChannel` برای خواندن و نوشتن بلوکی
- [ ] `StandardOpenOption`
- [ ] جریان متنی در برابر جریان باینری
- [ ] attribute فایل و symbolic link، در حد تشخیص

**باید بتوانی بسازی:** کپی یک فایل باینری با channel و buffer، و خواندن یک متن با charset اعلام‌شده.

## فاز ۷ — Concurrency و Java Memory Model

**هدف:** visibility، atomicity، و مدل اجرای Java 21 را از هم جدا ببینی.

**موضوع‌ها**

- [ ] Java Memory Model و happens-before
- [ ] visibility در برابر atomicity
- [ ] `volatile`: چه را تضمین می‌کند و حد آن
- [ ] `synchronized` و monitor
- [ ] `Lock`، `ReentrantLock`، `tryLock`
- [ ] `Condition`، در حد جای `wait` / `notify`
- [ ] `ConcurrentHashMap`، `CopyOnWriteArrayList`، `BlockingQueue`
- [ ] کلاس‌های atomic
- [ ] `Executor`، سیاست استخر، `shutdown` در برابر `shutdownNow`، `Future`
- [ ] `CompletableFuture`، در حد ترکیب چند کار
- [ ] virtual thread در Java 21، و pin شدن روی `synchronized`
- [ ] structured concurrency: در Java 21 هنوز preview است؛ API پایدار ۲۱ نیست
- [ ] deadlock، در حد تشخیص از روی thread dump

**باید بتوانی بسازی:** یک کار موازی با virtual thread و یک وضعیت مشترک که visibility آن با `volatile` یا lock درست شده باشد.

## فاز ۸ — Reflection، Annotation و Method Handle

**هدف:** متادیتا و صدا زدن غیرمستقیم را فقط جایی به کار ببری که API معمولی کافی نیست.

**موضوع‌ها**

- [ ] کی reflection لازم است و کی لازم نیست
- [ ] `Class`، `Method`، `Field`
- [ ] `setAccessible` و محدودیت ماژول
- [ ] retention: `SOURCE`، `CLASS`، `RUNTIME`
- [ ] خواندن annotation در runtime
- [ ] `MethodHandle`: `Lookup`، `findVirtual`، `invoke`
- [ ] `VarHandle`، در حد دسترسی اتمی و شفاف به فیلد
- [ ] هزینه و شکنندگی نسبت به صدا زدن معمولی

**باید بتوانی بسازی:** یک annotation با retention مناسب که روی متد خوانده شود و همان متد یک بار با `MethodHandle` صدا زده شود.

## فاز ۹ — Module و مرز classpath

**هدف:** مرز بستهٔ کد را بفهمی و classpath را با module path عوضی نگیری.

**موضوع‌ها**

- [ ] `module-info.java`
- [ ] `exports` و `requires`
- [ ] classpath در برابر module path
- [ ] unnamed module
- [ ] automatic module
- [ ] `opens` و `opens ... to` برای reflection
- [ ] چه برنامه‌ای هنوز بدون ماژول درست است
- [ ] اثر ماژول روی `setAccessible`

**باید بتوانی بسازی:** یک برنامهٔ دوماژوله که فقط API را export کند و دسترسی بیرون به داخل ماژول را رد کند.

## فاز ۱۰ — JVM

**هدف:** از bytecode تا GC و پروفایل، بدانی چه چیزی را نگاه کنی و چه چیزی را حدس نزنی.

**موضوع‌ها**

- [ ] class loading: bootstrap، platform، application class loader
- [ ] linking: verification، preparation، resolution، در حد نام
- [ ] خواندن bytecode با `javap`: `invokevirtual`، `invokespecial`، `getfield`، `ldc`
- [ ] stack frame در برابر heap؛ ارجاع روی stack، شیء روی heap
- [ ] GC در Java 21: Serial، Parallel، G1 به‌عنوان پیش‌فرض، ZGC وقتی تأخیر مهم است
- [ ] stop-the-world، در حد مفهوم
- [ ] allocation rate و کی GC مسئلهٔ برنامه است
- [ ] JIT به‌صورت مفهومی: C1، C2، warmup، deoptimization
- [ ] classpath و تداخل نسخهٔ کلاس
- [ ] چه چیزی را در پروفایل نگاه کنی: CPU، allocation، lock، thread dump، GC log
- [ ] `jcmd` و JFR، در حد انتخاب منبع مشاهده نه دستورهای حفظی

**باید بتوانی بسازی:** با `javap` مسیر یک فراخوانی را بخوانی و از روی thread dump یا GC log بگویی وقت یا حافظه کجا می‌رود.

---

## فهرست فازها

1. قابلیت‌های مدرن زبان
2. Generics پیشرفته
3. برابری و Collections
4. Stream، Collector و Optional
5. Exception و try-with-resources
6. I/O و NIO.2
7. Concurrency و Java Memory Model
8. Reflection، Annotation و Method Handle
9. Module و مرز classpath
10. JVM
