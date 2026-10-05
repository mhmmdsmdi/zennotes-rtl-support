# ZenNotes RTL (Persian) Override | پشتیبانی فارسی و راست‌چین برای ZenNotes
🇬🇧 **English version:** [برای مشاهده‌ی توضیحات انگلیسی اینجا کلیک کنید ↓](#english)
## درباره‌ی پروژه

این یک فایل CSS برای قابلیت **Overrides** در برنامه‌ی [ZenNotes](https://github.com/) است که پشتیبانی از **متن فارسی (RTL)** را به ادیتور و پیش‌نمایش Markdown اضافه می‌کند: جهت خودکار متن، لیست‌های راست‌چین، فاصله‌گذاری مناسب و فونت **وزیرمتن (Vazirmatn)**.

## نصب و فعال‌سازی
### ۱. نصب فونت وزیرمتن (اختیاری ولی پیشنهادی)

ZenNotes آدرس‌های اینترنتی را در Overrides لود نمی‌کند، پس فونت باید روی سیستم شما نصب باشد:

1. وزیرمتن را از [github.com/rastikerdar/vazirmatn](https://github.com/rastikerdar/vazirmatn) دانلود کنید.
2. فایل‌های فونت را روی سیستم‌عامل نصب کنید.
3. ZenNotes را کامل ببندید و دوباره باز کنید.

اگر فونت نصب نباشد، همان فونت پیش‌فرض نمایش داده می‌شود و هیچ خطایی نمی‌بینید.

### ۲. اضافه کردن فایل

فایل [`rtl.css`](./rtl.css) را داخل پوشه‌ی Overrides برنامه بگذارید، یعنی همان پوشه‌ای که فایل `example.css` در آن قرار دارد.

### ۳. فعال‌سازی

1. ZenNotes را باز کنید.
2. به مسیر **Settings → Appearance → Overrides** بروید.
3. کلید `rtl.css` را روشن کنید.

اگر تغییرات اعمال نشد، یک بار آن را خاموش و روشن کنید.

## دقیقاً چه چیزی را تغییر می‌دهد؟

### جهت متن

- هر خط در ادیتور و هر پاراگراف، عنوان، آیتم لیست، نقل‌قول و سلول جدول در پیش‌نمایش، **جهت خودش را خودکار تشخیص می‌دهد** (`unicode-bidi: plaintext`). خط فارسی راست‌چین و خط انگلیسی چپ‌چین می‌شود.
- فیلدهای ورودی (مثل جستجو) هم همین رفتار را دارند.

### بلوک‌های کد

- `pre`، `code`، `kbd` و `samp` همیشه **چپ‌به‌راست** می‌مانند و از فونت مونواسپیس استفاده می‌کنند.

### لیست‌ها

- لیست‌های بولت‌دار و شماره‌دار (`ul` و `ol`) **همیشه راست‌چین** می‌شوند. نقطه و شماره سمت راست قرار می‌گیرد.
- فاصله‌ی لیست از لبه از چپ به راست منتقل می‌شود، برای لیست‌های تو در تو هم همین‌طور.
- چک‌باکس‌های `- [ ]` هم جابه‌جا می‌شوند.
- ⚠️ چون CSS نمی‌تواند زبان هر لیست را تشخیص دهد، لیست‌های انگلیسی هم راست‌چین می‌شوند.

### نقل‌قول

- خط کناری `blockquote` به سمت شروع (راست) منتقل می‌شود و از رنگ `--z-accent` تم فعلی استفاده می‌کند.

### فاصله‌ها

- ارتفاع خط (`line-height`) در ادیتور و پیش‌نمایش یکسان می‌شود.
- فاصله‌ی پاراگراف‌ها، لیست‌ها و عنوان‌ها تنظیم می‌شود تا ظاهر ادیتور و پیش‌نمایش به هم نزدیک باشد.
- دو متغیر در ابتدای بخش فاصله‌ها قابل تغییر هستند:

```css
:root[data-theme] {
  --rtl-line-height: 1.8; /* فاصله‌ی بین خطوط */
  --rtl-gap: 0.6em;       /* فاصله‌ی بین پاراگراف‌ها و لیست‌ها */
}
```

### فونت

- فقط **حروف فارسی و عربی** با وزیرمتن نمایش داده می‌شوند (با `unicode-range`). متن انگلیسی با فونت سیستم (`system-ui`) باقی می‌ماند.
- ⚠️ چون از `!important` استفاده شده، این فونت روی تنظیم فونت در **Settings → Typography** برای ادیتور و متن پیش‌نمایش غلبه می‌کند.

### چیزهایی که تغییر نمی‌کنند

- رنگ‌ها و توکن‌های تم (`--z-*`) دست نمی‌خورند.
- هیچ آدرس اینترنتی یا فایل خارجی لود نمی‌شود.
- حالت **RTL اجباری برای همه‌چیز** به‌صورت کامنت‌شده در انتهای بخش ادیتور آمده است. اگر می‌خواهید همیشه همه‌ی متن راست‌چین باشد، آن را از کامنت دربیاورید.

## محدودیت‌ها و نکات

- ZenNotes کلاس‌های ثابت و مستندی برای ادیتور و پیش‌نمایش ندارد، برای همین بیشتر قاعده‌ها **روی تگ‌های HTML** (`p`، `li`، `h1`…`h6`، `ul`، `ol` و …) نوشته شده‌اند، نه کلاس‌های دقیق برنامه.
- به همین دلیل این قاعده‌ها ممکن است روی بخش‌های دیگر رابط کاربری (مثل سایدبار) هم اثر بگذارند. اگر چیزی به‌هم ریخت، با دکمه‌ی **Developer tools** در Settings → Appearance → Overrides اسم کلاس مربوطه را پیدا کنید و قاعده را محدود کنید.
- پیشنهاد و Pull Request برای دقیق‌تر کردن انتخابگرها خوشحال‌کننده است.


---

<a name="english"></a>

## English

[⬆ فارسی](#zennotes-rtl-persian-override--پشتیبانی-فارسی-و-راست‌چین-برای-zennotes)

### About

A CSS file for the **Overrides** feature in [ZenNotes](https://github.com/) that adds **Persian (RTL) support** to the editor and the Markdown preview: automatic text direction, right-aligned lists, consistent spacing, and the **Vazirmatn** font.

### Installation

#### 1. Install the Vazirmatn font (optional but recommended)

ZenNotes does not load remote URLs in overrides, so the font must be installed on your system:

1. Download Vazirmatn from [github.com/rastikerdar/vazirmatn](https://github.com/rastikerdar/vazirmatn).
2. Install the font files on your operating system.
3. Fully quit and reopen ZenNotes.

If the font is not installed, the default font is used and nothing breaks.

#### 2. Add the file

Put [`rtl.css`](./rtl.css) in ZenNotes' overrides folder, the same folder that contains `example.css`.

#### 3. Enable it

1. Open ZenNotes.
2. Go to **Settings → Appearance → Overrides**.
3. Toggle `rtl.css` on.

If nothing changes, toggle it off and on once.

### What exactly does it change?

#### Text direction

- Every line in the editor, and every paragraph, heading, list item, blockquote and table cell in the preview, **detects its own direction automatically** (`unicode-bidi: plaintext`). Persian lines are right-aligned; English lines stay left-aligned.
- Input fields (e.g. search) behave the same way.

#### Code

- `pre`, `code`, `kbd` and `samp` always stay **left-to-right** and use a monospace font.

#### Lists

- Bullet and numbered lists (`ul` and `ol`) are **always forced to RTL**, so bullets and numbers sit on the right.
- List indentation moves from the left to the right side, including nested lists.
- Task checkboxes (`- [ ]`) are mirrored too.
- ⚠️ CSS cannot detect the language of an individual list, so English lists are right-aligned as well.

#### Blockquotes

- The `blockquote` side border moves to the start (right) side and uses the active theme's `--z-accent` color.

#### Spacing

- `line-height` is unified between the editor and the preview.
- Paragraph, list and heading margins are adjusted so the editor and preview look closer to each other.
- Two variables at the start of the spacing section are tweakable:

```css
:root[data-theme] {
  --rtl-line-height: 1.8; /* space between lines */
  --rtl-gap: 0.6em;       /* space between paragraphs and lists */
}
```

#### Font

- Only **Persian/Arabic characters** are rendered with Vazirmatn (via `unicode-range`). English text keeps the system font (`system-ui`).
- ⚠️ Because `!important` is used, this font overrides the font set in **Settings → Typography** for editor and preview text.

#### What it does not change

- Theme colors and `--z-*` tokens are untouched.
- No remote URLs or external files are loaded.
- A **force-RTL-everywhere** mode is included as a commented-out block at the end of the editor section. Uncomment it if you want all text to always be right-aligned.

### Limitations and notes

- ZenNotes does not document stable class names for the editor and preview, so most rules target **plain HTML tags** (`p`, `li`, `h1`…`h6`, `ul`, `ol`, etc.) rather than app-specific classes.
- As a result, these rules may also affect other parts of the UI (such as the sidebar). If something looks off, use the **Developer tools** button in Settings → Appearance → Overrides to find the relevant class and narrow the rule down.
- Suggestions and pull requests to make the selectors more precise are very welcome.