<div dir="rtl" align="right">

# چالش‌های فاز ۳ — برابری و Collections

جواب این فایل جای دیگری است.

## ۱

`record Student(int id, String name)` و `compareTo` فقط روی `id`. یکی را با نام `a` و یکی را با نام `b` و `id` یکسان در `HashSet` و `TreeSet` می‌ریزی. اندازهٔ هر مجموعه؟

## ۲

`equals` را نوشتی و `hashCode` هنوز مال `Object` است. دو شیء برابر در `HashSet` چند عضو‌اند؟

## ۳

خروجی چیست؟

```java
List<String> backing = new ArrayList<>(List.of("a"));
List<String> view = Collections.unmodifiableList(backing);
backing.add("b");
System.out.println(view);
```

## ۴

`List.of("a", null)` چه می‌کند؟ با `new ArrayList<>()` که بعداً `add(null)` کند فرقش چیست؟

## ۵

`HashSet` را به `SequencedCollection` می‌گیری تا `getFirst` بزنی. چرا این انتخاب غلط است؟ به‌جایش برای ترتیب درج چه می‌گیری؟

## ۶

باگ را پیدا کن.

```java
for (String item : items) {
    items.remove(item);
}
```

`items` یک `ArrayList` است.

## ۷

برای صف دو سر که `null` نمی‌خواهی، `LinkedList` را انتخاب می‌کنی یا `ArrayDeque` را؟ یک دلیل هزینه.

</div>
