<div dir="rtl" align="right">

# پاسخ فاز ۸ — Collections

## ۱

`2`. بدون `hashCode` سازگار، دو شیء به دو سطل می‌روند و `equals` دیگر برای یکی کردنشان به کار نمی‌آید.

## ۲

کلمهٔ `null` چاپ می‌شود. باید نبودن کلید را خودت ببینی و بنویسی `چنین نامی نیست`.

## ۳

`ArrayList` اندازهٔ ۳ دارد و `HashSet` اندازهٔ ۲. لیست تکرار را نگه می‌دارد و مجموعه نه.

## ۴

`HashMap`. پیدا کردن با نام کار کلید است، نه گشتن در فهرست جفت‌ها.

## ۵

حذف داخل `for-each` ساختار لیست را عوض می‌کند. `ArrayList` این را fail-fast می‌بیند و `ConcurrentModificationException` می‌دهد.

## ۶

`TreeSet`. `HashSet` ترتیب مرتب‌شده وعده نمی‌دهد.

## ۷

```java
@Override
public int hashCode() {
    return Objects.hash(id);
}
```

همان فیلدهای `equals` باید در `hashCode` باشند.

</div>
