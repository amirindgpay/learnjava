<div dir="rtl" align="right">

# فاز ۹ — Module و مرز classpath

این درسنامه برای Java 21 است. ماژول یک مرز کامپایل و اجرا دور بسته است. classpath آن مرز را ندارد. این دو را به‌جای هم نگیر.

## چرا این‌طور کار می‌کند

`module-info.java` ریشهٔ ماژول است و نام ماژول را اعلام می‌کند، نه نام کلاس را. `exports` یک بسته را برای ماژول‌های دیگر قابلِ استفاده می‌کند. نوع public داخل بستهٔ export‌نشده را از بیرون نه import می‌کنی و نه new. `exports com.example.api to com.example.app` همان بسته را فقط به یک ماژول می‌دهد. `requires` می‌گوید این ماژول کدام ماژول را می‌خواند. بدون `requires`، حتی بستهٔ export‌شده نامرئی است. `java.base` را لازم نیست requires کنی.

مسیر را از مرز جدا کن. classpath یعنی فهرست JAR و پوشه‌ای که کلاس از آن بار می‌شود، بدون `module-info`. همهٔ آنچه روی classpath است یک unnamed module است. آن ماژول نام ندارد، پس هیچ ماژول نام‌دار نمی‌تواند `requires` آن باشد. خودش می‌تواند بسته‌های export‌شدهٔ ماژول‌های روی module path را بخواند.

module path جای JARهایی است که یا `module-info` دارند، یا به‌صورت automatic module دیده می‌شوند. JAR بدون `module-info` روی module path یک automatic module است: نامش از نام فایل JAR درمی‌آید، همهٔ بسته‌هایش export می‌شوند، و همهٔ ماژول‌های دیگر را می‌خواند، از جمله unnamed module. این پل مهاجرت است، نه مرز سخت. اگر همان JAR را به‌اشتباه روی classpath بگذاری، automatic module نمی‌شود. unnamed module می‌شود.

`exports` دسترسی زبان به نوع public است، در زمان کامپایل و اجرا. reflection به عضو private یا به عضو یک بستهٔ export‌نشده را باز نمی‌کند. برای آن `opens` لازم است. `opens com.example.internal` به هر ماژولی اجازهٔ reflection عمیق می‌دهد. `opens com.example.internal to com.example.tool` فقط به همان ماژول. بدون `opens`، `setAccessible(true)` از ماژول دیگر `InaccessibleObjectException` می‌دهد. فاز reflection همین‌جا به ماژول وصل می‌شود: دسترسی را با پرچم JVM باز نکن. اگر ابزار واقعاً باید داخل را ببیند، بسته را آگاهانه `opens` کن.

برنامهٔ کوچک این مسیر هنوز بدون ماژول درست است. `javac` و `java` با classpath برای چند پوشه کافی‌اند. ماژول را وقتی بیاور که می‌خواهی یک بسته واقعاً از بیرون نامرئی بماند، یا نمی‌خواهی دو JAR تصادفاً داخل هم را ببینند. برنامهٔ دوماژوله یعنی یک ماژول فقط API را export می‌کند و ماژول برنامه `requires` آن است. کلاس داخلی در بسته‌ای می‌ماند که در `exports` نیست. تلاش برنامه برای import آن کلاس باید در کامپایل رد شود، نه اینکه در runtime با یک if پنهان شود.

## قاعده

چیزی را که بیرون نباید ببیند export نکن. چیزی را که فقط یک ابزار باید با reflection ببیند، `opens ... to` همان ابزار کن، نه `opens` بی‌مقصد. JAR ماژول‌دار را روی module path بگذار. اگر برنامه یک `module-info` ندارد، classpath برای همین کار کافی است و لازم نیست مصنوعی ماژول بسازی.

## مثال

مرز را همین دو فایل می‌سازند. بستهٔ `com.example.internal` در هیچ `exports` نیست:

```java
module com.example.api {
    exports com.example.api;
}
```

```java
module com.example.app {
    requires com.example.api;
}
```

از کد `com.example.app`، نوع public داخل `com.example.api` دیده می‌شود. نوع داخل `com.example.internal` دیده نمی‌شود، حتی اگر public باشد. reflection به فیلد private همان API هم بدون `opens` از ماژول دیگر رد نمی‌شود.

## اشتباه رایج

گذاشتن JAR دارای `module-info` روی classpath، و انتظار مرز ماژول. آن کد داخل unnamed module بار می‌شود، `exports` دیگر مرز اجرا نیست، و بستهٔ «داخلی» دوباره در دسترس بقیهٔ classpath است.

## تمام است وقتی

یک برنامهٔ دوماژوله بنویسی که فقط بستهٔ API را export کند و استفاده از بستهٔ داخلی را در کامپایل رد کند.

</div>
