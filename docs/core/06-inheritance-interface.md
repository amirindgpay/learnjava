<div dir="rtl" align="right">

# فاز ۶ — وراثت، interface و چندریختی

این درسنامه برای Java 21 است. به‌جای اینکه در `main` بپرسی «این شیء واقعاً کدام class است؟»، رفتار را روی خود شیء می‌گذاری و از نوع مشترک صدا می‌زنی.

## چرا این‌طور کار می‌کند

`extends` یعنی فرزند، فیلد و متد قابل‌دیدن والد را دارد و می‌تواند متد را عوض کند. `super` یعنی همان نسخهٔ والد، معمولاً از داخل سازنده یا از داخل متدی که می‌خواهی کار والد را هم انجام بدهی. `@Override` به کامپایلر می‌گوید این متد باید دقیقاً یک متد والد را بپوشاند. اگر اسم را غلط بنویسی، به‌جای یک متد تازهٔ بی‌اثر، خطا می‌گیری.

abstract class را وقتی بخواه که چند فرزند وضعیت و کد مشترک دارند، ولی یک متد را هر کدام جور خودش باید بسازد. از خود abstract class نمی‌شود `new` کرد. متد abstract بدن ندارد. فرزند غیربستر آن را پیاده می‌کند.

interface وقتی است که فقط یک قابلیت مشترک داری، نه یک وضعیت مشترک. مثلاً «قابل پرداخت بودن»: `int pay()`. هر class که آن را `implements` کند آن متد را دارد. قانون این مسیر همین یک خط است: وضعیت و کد مشترک، abstract class. فقط قرارداد یک رفتار، interface.

چندریختی یعنی متغیر از نوع والد یا interface باشد و شیء از نوع فرزند. `Shape shape = new Circle(...)` مجاز است. `shape.area()` بدن `Circle` را اجرا می‌کند، چون شیء دایره است، نه چون متغیر را دایره نامیده‌ای. نوع متغیر فقط می‌گوید چه متدهایی را حق داری صدا بزنی.

`protected` برای عضوی است که فرزند لازم دارد و کد بیرون class نه. از `private` بازتر است و از `public` بسته‌تر.

`enum` مجموعهٔ ثابتی از وضعیت‌هاست: `PENDING`، `PAID`، `SHIPPED`. مقدار تازه‌ای در زمان اجرا به آن اضافه نمی‌کنی. `switch` فلش‌دار روی enum خوانا است، چون حالت‌ها معلوم‌اند.

`record` داده‌ای است که هویتش همان فیلدهایش است. کامپایلر سازنده، `equals`، `hashCode` و `toString` را می‌سازد. متد خودت، مثل فاصلهٔ دو نقطه، را کنار همان فیلدها می‌نویسی.

`instanceof` با الگو، از Java 16، چک و معرفی متغیر را یکی می‌کند: `if (shape instanceof Circle c)`. داخل بلوک، `c` از نوع `Circle` است و cast جدا نمی‌خواهد. این ابزار را برای وقتی نگه دار که واقعاً باید به نوع فرزند برسی. اگر در `main` برای هر شکل یک `instanceof` نوشتی، چندریختی را دور زده‌ای.

sealed class یعنی فقط classهایی که اجازه داده‌ای حق `extends` دارند. در این فاز شناختنش کافی است. برای تمام شدن فاز لازم نیست.

اگر چند class را `public` کنی، هر کدام یک فایل به همان نام می‌خواهد. ساده‌ترین کار: فقط کلاسی که `main` دارد `public` باشد.

## قاعده

متد مشترک را روی نوع والد یا interface صدا بزن. در `main` به نوع واقعی `if` نزن. abstract class را برای وضعیت مشترک بگذار و interface را برای یک قابلیت. عضوی که فقط فرزند باید ببیند `protected` است، نه `public`.

## مثال

```java
abstract class Shape {
    abstract double area();
}

class Circle extends Shape {
    private final double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}
```

```java
class Rectangle extends Shape {
    private final double width;
    private final double height;

    Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    double area() {
        return width * height;
    }
}

class Demo {
    static void printAreas() {
        Shape[] shapes = { new Circle(1), new Rectangle(2, 3) };
        for (Shape shape : shapes) {
            System.out.println(shape.area());
        }
    }
}
```

حلقه نوع واقعی را نمی‌پرسد. `Circle` همان کلاس مثال قبل است.

## اشتباه رایج

در `main` نوشتن `if (shape instanceof Circle)` و `if (shape instanceof Rectangle)` برای حساب مساحت. با فرزند سوم باید `main` را دوباره باز کنی. مساحت کار خود شکل است.

## تمام است وقتی

یک interface یا abstract class با دو پیاده‌سازی داشته باشی و متد را از روی نوع والد صدا بزنی، بدون اینکه در `main` به نوع واقعی `if` بزنی.

</div>
