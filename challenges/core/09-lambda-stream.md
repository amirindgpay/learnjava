<div dir="rtl" align="right">

# چالش‌های فاز ۹ — Lambda و Stream

جواب این فایل جای دیگری است.

## ۱

لیست منبع بعد از این خط چیست؟ چیزی چاپ می‌شود؟

```java
List<String> names = new ArrayList<>(List.of("sara", "ali"));
names.stream().filter(name -> name.length() > 3).map(String::toUpperCase);
System.out.println(names);
```

## ۲

خروجی لیست تازه را در `found` ریخته‌ای. `found.add("x")` چه می‌کند؟

```java
List<String> found = names.stream().filter(name -> name.length() > 3).toList();
```

## ۳

باگ را پیدا کن. لیست نمره خالی است.

```java
OptionalDouble average = scores.stream().mapToInt(n -> n).average();
System.out.println(average.getAsDouble());
```

## ۴

این زنجیره لیست اصلی را مرتب می‌کند یا یک نتیجهٔ جدا می‌سازد؟

```java
names.stream().sorted().toList();
```

## ۵

جست‌وجو `Optional` خالی برگردانده. کدام کار `NullPointerException` می‌سازد: `orElse("پیدا نشد")` یا صدا زدن متد روی `null`؟

## ۶

برای یک حلقه که فقط عنصرها را چاپ می‌کند، `for` را انتخاب می‌کنی یا Stream را؟ یک دلیل.

## ۷

عبارت lambda و method reference را بنویس که نام‌های بلندتر از ۴ حرف را نگه دارد، مرتب کند، و `toList` بگیرد. منبع `List<String>` به نام `names` است.

</div>
