<div dir="rtl" align="right">

# چالش‌های فاز ۶ — وراثت، interface و چندریختی

جواب این فایل جای دیگری است.

## ۱

کدام بدن اجرا می‌شود، بدن `Shape` یا بدن `Circle`؟

```java
Shape shape = new Circle(2);
System.out.println(shape.area());
```

`Circle` متد `area` را با `@Override` نوشته است.

## ۲

باگ طراحی را پیدا کن، حتی اگر خروجی امروز درست باشد.

```java
double total = 0;
for (Shape shape : shapes) {
    if (shape instanceof Circle c) {
        total = total + c.area();
    } else if (shape instanceof Rectangle r) {
        total = total + r.area();
    }
}
```

## ۳

`new Shape()` وقتی `Shape` کلاس `abstract` است چه نتیجهٔ کامپایلی دارد؟

## ۴

فرزند متد والد را `Area` نامیده، با حرف بزرگ، و `@Override` نگذاشته. برنامه کامپایل می‌شود. چرا مساحت والد هنوز اجرا می‌شود؟

## ۵

برای «قابل پرداخت» که نه فیلد مشترک دارد و نه کد مشترک، abstract class را انتخاب می‌کنی یا interface را؟

## ۶

دو `record Point(int x, int y)` با مختصات یکسان. `equals` چه می‌گوید، بدون اینکه خودت `equals` نوشته باشی؟

## ۷

یک جملهٔ فارسی برای هر ثابت `PENDING` و `PAID` و `SHIPPED` با `switch` فلش‌دار برگردان. لازم نیست هر سه جمله را این‌جا بنویسی. بگو اگر یک ثابت را جا بیندازی کامپایلر چه کار می‌کند.

</div>
