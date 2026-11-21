# راهنمای استفاده از Operation Workflow Protocol — نسخه 1.0.0

هدف OWP این است که در پروژه‌های نرم‌افزاری، **Operation** مسئول مدیریت، تحلیل و تصمیم‌گیری باشد و عامل توسعه (مثلاً Codex در VS Code) روی پیاده‌سازی و تست تمرکز کند. مالک انسانی همچنان اولویت‌ها، مجوزهای حساس و پذیرش نهایی را کنترل می‌کند.

این بسته عمومی است؛ هیچ نام مخزن، مسیر کامپیوتر، شماره Issue یا PR، معماری یا مجوز اختصاصی یک پروژه در قواعد عمومی آن تثبیت نشده است. قواعد خاص پروژه‌های فعلی به قوت خود باقی هستند.

## ۱. محتویات و معماری بسته

```text
OWP-v1.0/
├── README_FA.md
└── operation-workflow/
    ├── SKILL.md
    ├── references/
    │   └── OPERATION_WORKFLOW.md
    └── assets/
        └── PROJECT_PROFILE.template.md
```

| نقش | فایل | لایه |
| ---: | ---: | ---: |
| قرارداد مرجع انگلیسی، مستقل از فناوری و پروژه. قواعد عمومی در این فایل تعریف می‌شوند. | `OPERATION_WORKFLOW.md` | اول: OWP Core |
| دستورالعمل اجرایی انگلیسی برای Operation؛ مشخص می‌کند چه موقع کدام قواعد اجرا شوند. | `SKILL.md` | دوم: Operation Skill |
| قالب انگلیسی مختصر برای ساخت نسخه اختصاصی هر پروژه. پس از تکمیل به `PROJECT_PROFILE.md` تغییر نام بده. | `PROJECT_PROFILE.template.md` | سوم: Project Profile |

فایل Core در `references/` قرار دارد تا Skill به همان نسخه مرجع دسترسی داشته باشد. فایل جداگانه‌ای با متن تکراری از Core نگهداری نکن. Skill هم برای Operation است؛ برای Codex آن را به‌عنوان Skill اجرایی نصب نکن. Codex باید تسک انگلیسی محدودشده‌ای را که Operation آماده می‌کند دریافت کند. اگر در آینده Skill مخصوص عامل توسعه ساخته شد، باید مکمل OWP باشد، نه نسخه رقیب آن.

## ۲. روش پیشنهادی در ChatGPT Project

این روش به نصب مستقیم Skill وابسته نیست و برای یک پروژه جدید یا ادامه یک پروژه موجود قابل استفاده است:

1. یک Project اختصاصی به نام پروژه نرم‌افزاری بساز یا از Project فعلی استفاده کن.
2. فایل‌های `OPERATION_WORKFLOW.md` و `SKILL.md` را از مخزن دریافت کن و به منابع آن Project اضافه کن. از فایل قالب، یک `PROJECT_PROFILE.md` اختصاصی بساز و در همان منابع قرار بده. اگر پروژه از قبل قوانین و مستندات معتبر دارد، آن‌ها را نگه دار و به Profile ارجاع بده؛ نیازی به انتقال دوباره تمام مستندات نیست.
3. در Project settings، بخش Project instructions، دستور کوتاه زیر را وارد کن. این دستور برای فعال‌سازی قواعد و شناخت منابع است، نه تکرار کل Core.

```text
Act as Operation, the single coordinating agent for this project.
Follow OWP v1.0.0 in OPERATION_WORKFLOW.md and the operating instructions in SKILL.md.
Apply PROJECT_PROFILE.md, the latest approved project decisions, and applicable repository rules.
Use Persian with the human owner and English for implementation-agent tasks, reports and handoffs unless the owner specifies otherwise.
Keep project-specific rules and permissions separate from the general OWP. Do not assume authority for writes, commits, pushes, PR changes, merge, deployment or destructive cleanup. Preserve existing decisions; verify current facts from authoritative sources.
```

4. در همان Project یک چت به نام **Operation** (یا نام پروژه به همراه Operation) بساز. برای هر پروژه فقط یک Operation فعال داشته باش. چت‌های دیگر می‌توانند کار تخصصی یا آرشیوی داشته باشند، اما مدیریت موازی نکنند.
5. برای شروع، پیام آماده زیر را بفرست. Operation باید وضعیت موجود را تشخیص دهد، نه اینکه از صفر کل Repository را مجدداً بخواند.

```text
Initialize or resume this project under OWP v1.0.0 as Operation.
Read the Core, Skill, project profile and relevant existing project instructions.
Recover the latest valid baseline, approved decisions, permissions and next open task.
Identify missing or conflicting project-specific rules and request only essential clarifications.
Return a concise baseline in Persian. Do not modify code, files, repository state or external services unless separately authorized.
```

اگر پروژه جدید است، تصمیم‌های اولیه، MVP، کاربران، محدودیت‌های فنی و معیارهای پذیرش را در Profile و اسناد مرتبط ثبت کن. اگر پروژه‌ای در حال توسعه است، از Handoff، وضعیت GitHub، PRها و آخرین نتیجه معتبر استفاده کن. به قواعدی که از قبل مشخص شده‌اند دوباره رأی‌گیری نکن؛ تنها تعارض‌ها یا خلأهای مهم را مشخص کن.

## ۳. نصب به‌عنوان Skill در محیط‌های دارای پشتیبانی

ساختار پوشه `operation-workflow` با قالب Agent Skills هماهنگ است: فایل `SKILL.md` دارای YAML frontmatter و ارجاع‌های نسبی به فایل‌های همراه است. بسته مستقل `operation-workflow-v1.0.zip` فقط همین پوشه و منابع لازم را دارد. برای نصب واقعی، تمام پوشه را حفظ کن؛ `SKILL.md` به‌تنهایی بسته کامل نیست. این Skill هیچ اسکریپت اجرایی، dependency یا مجوز از پیش داده‌شده‌ای ندارد.

در نسخه‌های ChatGPT که قابلیت ایجاد و نصب Skill را دارند، طبق راهنمای رسمی از Plugins → Skills → Create → Upload from your computer استفاده کن و بسته Skill را وارد کن. پشتیبانی و مجوز نصب به حساب، محیط کاری و تنظیمات آن وابسته است. اگر این گزینه را نداری، از روش Project در بخش قبل استفاده کن. نصب یا آپلود این فایل‌ها خودبه‌خود دسترسی به GitHub، VS Code، فایل‌های محلی یا سرور را ایجاد نمی‌کند؛ اتصال و مجوز هر ابزار مستقل است. این بسته تولید شده است، نه اینکه از طرف کاربر نصب یا فعال شده باشد.

- [راهنمای رسمی Skills در ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt)
- [راهنمای Projects در ChatGPT](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)
- [مشخصات فنی Agent Skills](https://agentskills.io/specification)

## ۴. گردش کار روزمره

| خروجی مطلوب | مسئول | مرحله |
| ---: | ---: | ---: |
| اولویت، محدوده و معیار پذیرش | مالک + Operation | تعریف یا انتخاب کار |
| تصمیم‌های ضروری، فایل‌های مرتبط و ریسک‌ها | Operation | تحلیل |
| تسک انگلیسی دقیق، مدل و Reasoning مناسب، Continue یا New، حدود مجوز Git | Operation | واگذاری |
| تغییر محدود، تست معتبر و گزارش انگلیسی | Codex یا عامل توسعه | توسعه و تست |
| بررسی Diff واقعی، CI، ریسک‌های باقی‌مانده و تصمیم درباره آمادگی | Operation | بازبینی مستقل |
| شواهد ادغام و انتشار، آزمون محیطی و تأیید انسانی در صورت نیاز | طبق مجوز پروژه | Merge/Deployment و پذیرش |
| اصلاح مستندات و وضعیت واقعی؛ تعیین کار بعدی بدون اجرای خودکار کار جدید | Operation | ثبت پیشرفت |

برای یک تغییر ساده این مسیر سبک اجرا می‌شود؛ برای تراکنش مالی، Migration، هم‌زمانی، امنیت یا انتشار، کنترل‌های متناسب با ریسک بیشتر می‌شوند. برای مثال اگر صرفاً وضعیت Git مورد نیاز است، از ابزار مستقیم یا دستور معمولی Git استفاده کن، نه تسک سنگین Codex. در صورت نبود دسترسی، Operation می‌تواند دستور کوتاه یا درخواست گزارش محدود بدهد.

**اصل زبان:** توضیح برای مالک فارسی، تسک و گزارش بین عامل‌ها انگلیسی. زبان مستندات Repository و UI پروژه در Profile تعیین می‌شود. گزارش Codex را می‌توان بدون ترجمه به Operation منتقل کرد؛ Operation نتیجه را فارسی توضیح می‌دهد.

## ۵. چند فرمان عملی برای کار با Operation

- «طبق OWP وضعیت پروژه را بررسی کن و فقط کار بعدی را بگو؛ هیچ تغییری نده.»
- «این Issue را طبق OWP تحلیل کن و تسک انگلیسی آماده Codex را بنویس. فعلاً پیاده‌سازی شروع نشود.»
- «این گزارش Codex است؛ مطابق OWP بازبینی کن و فقط اصلاحات موردنیاز را مشخص کن.»
- «طبق OWP آمادگی Merge را بررسی کن؛ فقط اقداماتی را انجام بده که در Profile مجاز هستند.»
- «یک Handoff فشرده طبق OWP تهیه کن؛ وضعیت محلی، تصمیم‌ها، مرحله فعلی و کار بعدی مشخص باشند.»
- «محیط توسعه را برای پاک‌سازی بررسی کن؛ فایل‌های نامطمئن یا کار ادغام‌نشده را حفظ کن.»

## ۶. تعریف قواعد اختصاصی و جلوگیری از تداخل

در Profile هر پروژه مشخص کن کدام شاخه مرجع است، چه کسی Commit، Push، PR، Ready، Merge، Deployment یا حذف فایل را مجاز می‌کند، تست‌های ضروری کدام‌اند، منابع مستندات و معیار تکمیل چیست. برای موارد نامشخص از TBD استفاده کن؛ به معنی اجازه انجام کار نیست. می‌توان اختیار مشخصی مانند Ready کردن PR پس از CI موفق را به Operation واگذار کرد تا تأیید تکراری نخواهد. این اختیار به پروژه دیگر منتقل نمی‌شود و اجازه Merge یا Production را ایجاد نمی‌کند.

اطلاعات و تصمیم‌های تاریخی یک پروژه را در همان Project حفظ کن. اگر از قبل یک Operation فعال داری، ساخت چت تازه الزامی نیست. بعد از تأیید پروژه مالک، نسخه عمومی OWP جای قواعد خاص موجود را نمی‌گیرد. هنگام مهاجرت به چت دیگر، Handoff تهیه کن و از وضعیت واقعی ادامه بده.

## ۷. نگهداری و نسخه‌بندی

- هر اصلاح اساسی قواعد عمومی ابتدا در Core با نسخه مشخص ثبت شود؛ Skill و قالب Profile تنها در صورت نیاز هماهنگ شوند. تصمیم خاص یک پروژه در Profile یا ADR همان پروژه باقی بماند.
- پیشرفت را از روی شواهد معتبر و با معیارهای ثابت به‌روز کن. پیاده‌سازی محلی، Commit، Push، CI، Merge، Deployment و پذیرش واقعی وضعیت‌های متفاوت‌اند. یک فایل جاری و آرشیو مشخص برای گزارش‌های قدیمی کافی است.
- فایل Core و Skill را یک نسخه هماهنگ نگه دار. Profile و Handoff را سبک و به‌روز نگه دار، نه نسخه کامل همه اسناد. Secret، Token یا محتویات `.env` را در بسته، Profile یا پرامپت نگذار.

**نام فراخوانی قواعد:** OWP (Operation Workflow Protocol). وقتی در یک Project می‌گویی «طبق OWP عمل کن»، منظور Core نسخه تعیین‌شده به همراه Skill اجرایی و قواعد اختصاصی معتبر همان پروژه است.

برای استفاده پایدار، فایل‌ها را از یک Tag منتشرشده یا Commit مشخص دریافت کن؛ از ترکیب نسخه‌های مختلف Core و Skill خودداری کن. [راهنمای نسخه‌بندی](VERSIONING.md)
