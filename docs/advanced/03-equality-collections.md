<div dir="rtl" align="right">

# فاز ۳ — برابری و Collections

این درسنامه برای Java 21 است. برابری یک قرارداد است، نه یک سلیقه. ساختاری که برای نگه داشتن شیء انتخاب می‌کنی همان قرارداد را با هزینهٔ دسترسی یکی می‌کند.

## چرا این‌طور کار می‌کند

`equals` پنج تعهد دارد. reflexive: هر شیء با خودش برابر است. symmetric: اگر `a` با `b` برابر است، `b` هم با `a` برابر است. transitive: برابری زنجیره‌ای است. consistent: تا وقتی اطلاعاتِ داخل مقایسه عوض نشده، نتیجه همان می‌ماند. `x.equals(null)` همیشه `false` است، نه `NullPointerException`.

`hashCode` با همین قرارداد جفت است. دو شیء برابر باید یک `hashCode` بدهند. دو شیء نابرابر مجازند یکی بدهند؛ این collision است، نه باگ. `HashSet` و `HashMap` اول سطل را با hash پیدا می‌کنند و بعد داخل سطل `equals` می‌گیرند. اگر `equals` را نوشتی و `hashCode` را نه، شیء برابر پیدا نمی‌شود.

`Comparable.compareTo` برای `TreeSet` و `TreeMap` معیار عضویت است، نه `equals`. اگر `compareTo` صفر بدهد و `equals` نه، آن دو شیء در `TreeSet` یکی حساب می‌شوند و در `HashSet` دو تا. سازگاری یعنی `compareTo` دقیقاً وقتی صفر باشد که `equals` برقرار است. `Comparator` جدا از نوع است: `thenComparing` ترتیب را چندکلیده می‌کند، و `nullsFirst` / `nullsLast` جای `null` را صریح می‌گوید تا مقایسه وسط راه نترکد.

هزینه را با عمل یکی کن، نه با اسم کلاس:

- `ArrayList`: خواندن با اندیس O(1)، افزودن ته amortized O(1)، درج و حذف وسط O(n).
- `LinkedList`: دسترسی با اندیس O(n). افزودن و حذف دو سر O(1). برای صف و پشته انتخاب اول نیست.
- `ArrayDeque`: دو سر amortized O(1)، بدون عنصر `null`. برای صف و پشته همین را بردار.
- `HashMap` و `HashSet`: میانگین O(1). hash بد یا سطل شلوغ، زنجیره می‌سازد. از Java 8 زنجیرهٔ بلندِ کلیدهای `Comparable` درخت می‌شود و همان سطل به O(log n) نزدیک می‌شود.
- `TreeMap` و `TreeSet`: همیشه O(log n)، به ترتیب مقایسه.

ظرفیت `HashMap` توانی از دو است و load factor پیش‌فرض ۰٫۷۵ است. گذشتن از این نسبت، جدول را بزرگ می‌کند و دوباره پخش می‌کند. collision یعنی چند کلید در یک سطل، نه خراب شدن map.

`List.of`، `Set.of`، `Map.of` و `copyOf` کلکسیون واقعاً غیرقابل‌تغییر می‌سازند: `add` و `set` همیشه پرتاب می‌کنند، `null` قبول نمی‌شود، و در `Set.of` / `Map.of` تکرار همان لحظهٔ ساخت رد می‌شود. `Collections.unmodifiableList` فقط یک پوشش است. اگر لیست پشتی عوض شود، پوشش هم عوض می‌شود. عناصر را عمیق کپی نمی‌کند.

`SequencedCollection` از Java 21 ترتیب دو سر را در خود نوع می‌آورد: `getFirst`، `getLast`، `addFirst`، `addLast` و نمای `reversed`. `List`، `Deque`، `LinkedHashSet` و انواع مرتب این را دارند. `HashSet` ندارد، چون ترتیب ندارد.

iterator ساختارهای `java.util` اغلب fail-fast است. اگر وسط پیمایش ساختار را عوض کنی (نه با خود `iterator.remove`)، `modCount` نمی‌خواند و `ConcurrentModificationException` می‌آید. این تضمین همزمانی نیست؛ یک تشخیص زود است.

## قاعده

فیلدهایی که در `equals` هستند همان‌ها در `hashCode` باشند، و `compareTo` با همان‌ها صفر بدهد. برای فهرست مرتب با تکرار `ArrayList`، برای یکتایی بدون ترتیب `HashSet`، برای کلید `HashMap`، برای ترتیب مقایسه‌ای `TreeSet`، برای دو سر `ArrayDeque`. اگر نمی‌خواهی کسی مجموعه را عوض کند، `List.of` / `copyOf` بساز، نه پوشش روی لیست زنده‌ای که هنوز جای دیگری دست می‌خورد.

## مثال

این `record` ناسازگار است. `compareTo` فقط `id` را می‌بیند، ولی `equals` و `hashCode` هر دو component را می‌بینند. دو نمونه با یک `id` و `name` متفاوت در `TreeSet` یکی می‌شوند و در `HashSet` دو تا:

```java
record Student(int id, String name) implements Comparable<Student> {
    @Override
    public int compareTo(Student other) {
        return Integer.compare(id, other.id);
    }
}
```

`record` همین `equals` و `hashCode` را از هر دو component می‌سازد. این‌جا `name` هم داخل برابری است، پس با `compareTo` که فقط `id` را می‌بیند ناسازگار است. اگر قرارداد را خودت می‌نویسی، هر سه را روی یک مجموعه فیلد ببند:

```java
final class Student implements Comparable<Student> {
    private final int id;
    private final String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object other) {
        return other instanceof Student s && id == s.id;
    }

    @Override
    public int hashCode() {
        return Integer.hashCode(id);
    }

    @Override
    public int compareTo(Student other) {
        return Integer.compare(id, other.id);
    }
}
```

## اشتباه رایج

`equals` را روی شناسه نوشتن و `hashCode` را به پیاده‌سازی `Object` سپردن. دو نمونه با یک شناسه در `HashSet` دو عضو می‌شوند، چون اول سطل‌شان فرق دارد.

## تمام است وقتی

یک نوع دامنه با `equals`، `hashCode` و `Comparable` سازگار بنویسی که در `HashSet` و `TreeSet` همان عضویت را نشان بدهد.

</div>
