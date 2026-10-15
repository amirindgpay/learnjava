<div dir="rtl" align="right">

# چالش‌های فاز ۸ — Collections

جواب این فایل جای دیگری است.

## ۱

`equals` فقط `id` را می‌بیند و `hashCode` را ننوشته‌ای. دو `Student` با یک شماره و دو نام را در `HashSet` می‌ریزی. `size` چند است؟

## ۲

کلید در map نیست. چه چاپ می‌شود، و رفتار درست چیست؟

```java
Map<String, String> phoneBook = new HashMap<>();
System.out.println(phoneBook.get("nobody"));
```

## ۳

همان سه نام، یکی تکراری، یک بار در `ArrayList` و یک بار در `HashSet`. اندازهٔ هر کدام؟

`"ماست"`، `"نان"`، `"ماست"`.

## ۴

برای دفترچهٔ تلفن که با نام پیدا می‌کنی، `ArrayList` جفت‌ها را انتخاب می‌کنی یا `HashMap` را؟ یک دلیل.

## ۵

باگ را پیدا کن.

```java
List<String> items = new ArrayList<>();
items.add("نان");
items.add("ماست");
for (String item : items) {
    if (item.equals("نان")) {
        items.remove(item);
    }
}
```

## ۶

`TreeSet` و `HashSet` هر دو یکتایی می‌دهند. کدام را فقط وقتی برمی‌داری که ترتیب مرتب‌شده را هم بخواهی؟

## ۷

`hashCode` این class را با `Objects.hash` فقط روی `id` بنویس. `equals` از قبل فقط `id` را مقایسه می‌کند.

</div>
