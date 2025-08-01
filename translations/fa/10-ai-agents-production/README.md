<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8164484c16b1ed3287ef9dae9fc437c1",
  "translation_date": "2025-07-23T08:13:30+00:00",
  "source_file": "10-ai-agents-production/README.md",
  "language_code": "fa"
}
-->
# عوامل هوش مصنوعی در تولید: مشاهده‌پذیری و ارزیابی

با حرکت عوامل هوش مصنوعی از نمونه‌های اولیه آزمایشی به کاربردهای واقعی، توانایی درک رفتار آن‌ها، نظارت بر عملکردشان و ارزیابی سیستماتیک خروجی‌هایشان اهمیت پیدا می‌کند.

## اهداف یادگیری

پس از تکمیل این درس، شما خواهید دانست:
- مفاهیم اصلی مشاهده‌پذیری و ارزیابی عوامل
- تکنیک‌هایی برای بهبود عملکرد، هزینه‌ها و اثربخشی عوامل
- چه چیزی و چگونه عوامل هوش مصنوعی خود را به صورت سیستماتیک ارزیابی کنید
- چگونه هزینه‌ها را هنگام استقرار عوامل هوش مصنوعی در تولید کنترل کنید
- چگونه عوامل ساخته‌شده با AutoGen را ابزارگذاری کنید

هدف این است که شما را با دانش لازم برای تبدیل عوامل "جعبه سیاه" به سیستم‌های شفاف، قابل مدیریت و قابل اعتماد مجهز کنیم.

_**توجه:** استقرار عوامل هوش مصنوعی ایمن و قابل اعتماد بسیار مهم است. درس [ساخت عوامل هوش مصنوعی قابل اعتماد](./06-building-trustworthy-agents/README.md) را نیز بررسی کنید._

## ردپاها و بخش‌ها

ابزارهای مشاهده‌پذیری مانند [Langfuse](https://langfuse.com/) یا [Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry) معمولاً اجرای عوامل را به صورت ردپاها و بخش‌ها نمایش می‌دهند.

- **ردپا** نمایانگر یک وظیفه کامل عامل از ابتدا تا انتها است (مانند پاسخ به یک پرسش کاربر).
- **بخش‌ها** مراحل جداگانه درون ردپا هستند (مانند فراخوانی یک مدل زبانی یا بازیابی داده‌ها).

![درخت ردپا در Langfuse](https://langfuse.com/images/cookbook/example-autogen-evaluation/trace-tree.png)

بدون مشاهده‌پذیری، یک عامل هوش مصنوعی می‌تواند مانند یک "جعبه سیاه" به نظر برسد - حالت داخلی و استدلال آن مبهم است، که تشخیص مشکلات یا بهینه‌سازی عملکرد را دشوار می‌کند. با مشاهده‌پذیری، عوامل به "جعبه‌های شیشه‌ای" تبدیل می‌شوند، شفافیتی که برای ایجاد اعتماد و اطمینان از عملکرد صحیح آن‌ها حیاتی است.

## چرا مشاهده‌پذیری در محیط‌های تولید اهمیت دارد

انتقال عوامل هوش مصنوعی به محیط‌های تولید چالش‌ها و نیازهای جدیدی را معرفی می‌کند. مشاهده‌پذیری دیگر یک قابلیت "خوب داشتن" نیست، بلکه یک قابلیت حیاتی است:

*   **اشکال‌زدایی و تحلیل علت اصلی:** هنگامی که یک عامل شکست می‌خورد یا خروجی غیرمنتظره‌ای تولید می‌کند، ابزارهای مشاهده‌پذیری ردپاهای لازم برای شناسایی منبع خطا را فراهم می‌کنند. این امر به ویژه در عوامل پیچیده که ممکن است شامل چندین فراخوانی LLM، تعاملات ابزار و منطق شرطی باشد، اهمیت دارد.
*   **مدیریت تأخیر و هزینه:** عوامل هوش مصنوعی اغلب به LLM‌ها و سایر API‌های خارجی متکی هستند که بر اساس تعداد توکن یا فراخوانی هزینه‌بردار هستند. مشاهده‌پذیری امکان ردیابی دقیق این فراخوانی‌ها را فراهم می‌کند، که به شناسایی عملیات‌هایی که بیش از حد کند یا گران هستند کمک می‌کند. این امر به تیم‌ها اجازه می‌دهد تا درخواست‌ها را بهینه کنند، مدل‌های کارآمدتر را انتخاب کنند یا جریان‌های کاری را برای مدیریت هزینه‌های عملیاتی و اطمینان از تجربه کاربری خوب بازطراحی کنند.
*   **اعتماد، ایمنی و انطباق:** در بسیاری از کاربردها، مهم است که عوامل به صورت ایمن و اخلاقی رفتار کنند. مشاهده‌پذیری یک مسیر حسابرسی از اقدامات و تصمیمات عامل فراهم می‌کند. این مسیر می‌تواند برای شناسایی و کاهش مشکلاتی مانند تزریق درخواست، تولید محتوای مضر یا سوءمدیریت اطلاعات شخصی قابل شناسایی (PII) استفاده شود. به عنوان مثال، می‌توانید ردپاها را بررسی کنید تا بفهمید چرا یک عامل پاسخ خاصی ارائه داده یا از یک ابزار خاص استفاده کرده است.
*   **حلقه‌های بهبود مستمر:** داده‌های مشاهده‌پذیری پایه‌ای برای یک فرآیند توسعه تکراری هستند. با نظارت بر عملکرد عوامل در دنیای واقعی، تیم‌ها می‌توانند زمینه‌های بهبود را شناسایی کنند، داده‌هایی برای تنظیم دقیق مدل‌ها جمع‌آوری کنند و تأثیر تغییرات را اعتبارسنجی کنند. این امر یک حلقه بازخورد ایجاد می‌کند که بینش‌های تولیدی از ارزیابی آنلاین، آزمایش‌های آفلاین و اصلاحات را اطلاع‌رسانی می‌کند و منجر به عملکرد بهتر عوامل می‌شود.

## معیارهای کلیدی برای ردیابی

برای نظارت و درک رفتار عامل، باید طیف وسیعی از معیارها و سیگنال‌ها را ردیابی کنید. در حالی که معیارهای خاص ممکن است بسته به هدف عامل متفاوت باشند، برخی معیارها به طور جهانی مهم هستند.

در اینجا برخی از رایج‌ترین معیارهایی که ابزارهای مشاهده‌پذیری نظارت می‌کنند آورده شده است:

**تأخیر:** عامل چقدر سریع پاسخ می‌دهد؟ زمان‌های انتظار طولانی تجربه کاربری را منفی تحت تأثیر قرار می‌دهد. باید تأخیر را برای وظایف و مراحل جداگانه با ردیابی اجرای عامل اندازه‌گیری کنید. به عنوان مثال، عاملی که برای همه فراخوانی‌های مدل ۲۰ ثانیه زمان می‌برد، می‌تواند با استفاده از یک مدل سریع‌تر یا اجرای فراخوانی‌های مدل به صورت موازی تسریع شود.

**هزینه‌ها:** هزینه هر اجرای عامل چقدر است؟ عوامل هوش مصنوعی به فراخوانی‌های LLM که بر اساس تعداد توکن یا API‌های خارجی هزینه‌بردار هستند متکی هستند. استفاده مکرر از ابزار یا درخواست‌های متعدد می‌تواند به سرعت هزینه‌ها را افزایش دهد. به عنوان مثال، اگر یک عامل پنج بار یک LLM را برای بهبود کیفیت حاشیه‌ای فراخوانی کند، باید ارزیابی کنید که آیا هزینه توجیه‌پذیر است یا می‌توانید تعداد فراخوانی‌ها را کاهش دهید یا از یک مدل ارزان‌تر استفاده کنید. نظارت در زمان واقعی همچنین می‌تواند افزایش‌های غیرمنتظره را شناسایی کند (مانند اشکالاتی که باعث حلقه‌های API بیش از حد می‌شوند).

**خطاهای درخواست:** چند درخواست توسط عامل شکست خورده است؟ این می‌تواند شامل خطاهای API یا فراخوانی‌های ابزار ناموفق باشد. برای مقاوم‌تر کردن عامل خود در برابر این موارد در تولید، می‌توانید تنظیمات پشتیبان یا تلاش مجدد را انجام دهید. به عنوان مثال، اگر ارائه‌دهنده LLM A از دسترس خارج شود، به عنوان پشتیبان به LLM B تغییر دهید.

**بازخورد کاربر:** ارزیابی‌های مستقیم کاربران بینش‌های ارزشمندی ارائه می‌دهند. این می‌تواند شامل رتبه‌بندی‌های صریح (👍بالا/👎پایین، ⭐۱-۵ ستاره) یا نظرات متنی باشد. بازخورد منفی مداوم باید شما را هشدار دهد زیرا این نشانه‌ای است که عامل به درستی کار نمی‌کند.

**بازخورد ضمنی کاربر:** رفتارهای کاربران بازخورد غیرمستقیم ارائه می‌دهند حتی بدون رتبه‌بندی‌های صریح. این می‌تواند شامل بازنویسی فوری پرسش، پرسش‌های تکراری یا کلیک بر روی دکمه تلاش مجدد باشد. به عنوان مثال، اگر مشاهده کنید که کاربران مکرراً همان پرسش را می‌پرسند، این نشانه‌ای است که عامل به درستی کار نمی‌کند.

**دقت:** عامل چقدر خروجی‌های صحیح یا مطلوب تولید می‌کند؟ تعریف دقت متفاوت است (مانند صحت حل مسئله، دقت بازیابی اطلاعات، رضایت کاربر). اولین قدم تعریف موفقیت برای عامل شما است. می‌توانید دقت را از طریق بررسی‌های خودکار، امتیازات ارزیابی یا برچسب‌های تکمیل وظیفه ردیابی کنید. به عنوان مثال، علامت‌گذاری ردپاها به عنوان "موفق" یا "ناموفق".

**معیارهای ارزیابی خودکار:** همچنین می‌توانید ارزیابی‌های خودکار تنظیم کنید. به عنوان مثال، می‌توانید از یک LLM برای امتیازدهی به خروجی عامل استفاده کنید، مانند اینکه آیا مفید، دقیق یا خیر است. همچنین چندین کتابخانه متن‌باز وجود دارد که به شما کمک می‌کند جنبه‌های مختلف عامل را امتیازدهی کنید. به عنوان مثال، [RAGAS](https://docs.ragas.io/) برای عوامل RAG یا [LLM Guard](https://llm-guard.com/) برای شناسایی زبان مضر یا تزریق درخواست.

در عمل، ترکیبی از این معیارها بهترین پوشش را از سلامت عامل هوش مصنوعی ارائه می‌دهد. در [دفترچه یادداشت نمونه این فصل](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb)، نشان خواهیم داد که این معیارها در مثال‌های واقعی چگونه به نظر می‌رسند، اما ابتدا یاد خواهیم گرفت که یک جریان کاری ارزیابی معمولی چگونه به نظر می‌رسد.

## ابزارگذاری عامل خود

برای جمع‌آوری داده‌های ردیابی، باید کد خود را ابزارگذاری کنید. هدف ابزارگذاری کد عامل این است که ردپاها و معیارهایی تولید کند که توسط یک پلتفرم مشاهده‌پذیری قابل جمع‌آوری، پردازش و تجسم باشند.

**OpenTelemetry (OTel):** [OpenTelemetry](https://opentelemetry.io/) به عنوان یک استاندارد صنعتی برای مشاهده‌پذیری LLM ظهور کرده است. این ابزار مجموعه‌ای از API‌ها، SDK‌ها و ابزارها برای تولید، جمع‌آوری و صادرات داده‌های تله‌متری فراهم می‌کند.

کتابخانه‌های ابزارگذاری زیادی وجود دارند که چارچوب‌های عامل موجود را پوشش می‌دهند و صادرات بخش‌های OpenTelemetry به یک ابزار مشاهده‌پذیری را آسان می‌کنند. در زیر یک مثال از ابزارگذاری یک عامل AutoGen با کتابخانه ابزارگذاری [OpenLit](https://github.com/openlit/openlit) آورده شده است:

```python
import openlit

openlit.init(tracer = langfuse._otel_tracer, disable_batch = True)
```

[دفترچه یادداشت نمونه](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb) در این فصل نشان خواهد داد که چگونه عامل AutoGen خود را ابزارگذاری کنید.

**ایجاد دستی بخش‌ها:** در حالی که کتابخانه‌های ابزارگذاری یک خط پایه خوب ارائه می‌دهند، اغلب مواردی وجود دارد که اطلاعات دقیق‌تر یا سفارشی مورد نیاز است. می‌توانید بخش‌ها را به صورت دستی ایجاد کنید تا منطق برنامه سفارشی اضافه کنید. مهم‌تر از همه، می‌توانند بخش‌های ایجادشده به صورت خودکار یا دستی را با ویژگی‌های سفارشی (که به عنوان برچسب‌ها یا متاداده نیز شناخته می‌شوند) غنی کنند. این ویژگی‌ها می‌توانند شامل داده‌های خاص کسب‌وکار، محاسبات میانی یا هر زمینه‌ای باشند که ممکن است برای اشکال‌زدایی یا تحلیل مفید باشد، مانند `user_id`، `session_id` یا `model_version`.

مثال ایجاد ردپاها و بخش‌ها به صورت دستی با [Langfuse Python SDK](https://langfuse.com/docs/sdk/python/sdk-v3):

```python
from langfuse import get_client
 
langfuse = get_client()
 
span = langfuse.start_span(name="my-span")
 
span.end()
```

## ارزیابی عامل

مشاهده‌پذیری به ما معیارها می‌دهد، اما ارزیابی فرآیند تحلیل آن داده‌ها (و انجام آزمایش‌ها) برای تعیین عملکرد عامل هوش مصنوعی و نحوه بهبود آن است. به عبارت دیگر، پس از داشتن آن ردپاها و معیارها، چگونه از آن‌ها برای قضاوت عامل و تصمیم‌گیری استفاده می‌کنید؟

ارزیابی منظم مهم است زیرا عوامل هوش مصنوعی اغلب غیرقطعی هستند و ممکن است تکامل یابند (از طریق به‌روزرسانی‌ها یا تغییر رفتار مدل) – بدون ارزیابی، نمی‌دانید که آیا "عامل هوشمند" شما واقعاً کار خود را به خوبی انجام می‌دهد یا اینکه عملکرد آن کاهش یافته است.

دو دسته ارزیابی برای عوامل هوش مصنوعی وجود دارد: **ارزیابی آنلاین** و **ارزیابی آفلاین**. هر دو ارزشمند هستند و مکمل یکدیگرند. معمولاً با ارزیابی آفلاین شروع می‌کنیم، زیرا این حداقل گام ضروری قبل از استقرار هر عاملی است.

### ارزیابی آفلاین

![موارد مجموعه داده در Langfuse](https://langfuse.com/images/cookbook/example-autogen-evaluation/example-dataset.png)

این نوع ارزیابی شامل ارزیابی عامل در یک محیط کنترل‌شده است، معمولاً با استفاده از مجموعه داده‌های آزمایشی، نه پرسش‌های زنده کاربران. شما از مجموعه داده‌های انتخاب‌شده استفاده می‌کنید که می‌دانید خروجی مورد انتظار یا رفتار صحیح چیست و سپس عامل خود را روی آن‌ها اجرا می‌کنید.

به عنوان مثال، اگر یک عامل حل مسئله ریاضی ساخته باشید، ممکن است یک [مجموعه داده آزمایشی](https://huggingface.co/datasets/gsm8k) شامل ۱۰۰ مسئله با پاسخ‌های شناخته‌شده داشته باشید. ارزیابی آفلاین اغلب در طول توسعه انجام می‌شود (و می‌تواند بخشی از خطوط لوله CI/CD باشد) تا بهبودها را بررسی کند یا از کاهش عملکرد جلوگیری کند. مزیت این نوع ارزیابی این است که **قابل تکرار است و می‌توانید معیارهای دقت واضحی دریافت کنید زیرا حقیقت زمین دارید**. همچنین ممکن است پرسش‌های کاربران را شبیه‌سازی کنید و پاسخ‌های عامل را با پاسخ‌های ایده‌آل مقایسه کنید یا از معیارهای خودکار که قبلاً توضیح داده شد استفاده کنید.

چالش اصلی در ارزیابی آفلاین اطمینان از جامع بودن و مرتبط بودن مجموعه داده آزمایشی شما است – عامل ممکن است در یک مجموعه آزمایشی ثابت عملکرد خوبی داشته باشد اما با پرسش‌های بسیار متفاوت در تولید مواجه شود. بنابراین، باید مجموعه‌های آزمایشی را با موارد جدید و مثال‌هایی که سناریوهای دنیای واقعی را منعکس می‌کنند به‌روز نگه دارید​. ترکیبی از موارد کوچک "آزمایش دود" و مجموعه‌های ارزیابی بزرگ‌تر مفید است: مجموعه‌های کوچک برای بررسی سریع و مجموعه‌های بزرگ‌تر برای معیارهای عملکرد گسترده‌تر​.

### ارزیابی آنلاین

![نمای کلی معیارهای مشاهده‌پذیری](https://langfuse.com/images/cookbook/example-autogen-evaluation/dashboard.png)

این نوع ارزیابی به ارزیابی عامل در یک محیط زنده و واقعی اشاره دارد، یعنی در طول استفاده واقعی در تولید. ارزیابی آنلاین شامل نظارت بر عملکرد عامل در تعاملات واقعی کاربران و تحلیل نتایج به صورت مداوم است.

به عنوان مثال، ممکن است نرخ‌های موفقیت، امتیازات رضایت کاربران یا سایر معیارها را در ترافیک زنده ردیابی کنید. مزیت ارزیابی آنلاین این است که **چیزهایی را که ممکن است در یک محیط آزمایشگاهی پیش‌بینی نکنید، ثبت می‌کند** – می‌توانید تغییر مدل را در طول زمان مشاهده کنید (اگر اثربخشی عامل با تغییر الگوهای ورودی کاهش یابد) و پرسش‌ها یا موقعیت‌های غیرمنتظره‌ای را که در داده‌های آزمایشی شما نبودند، شناسایی کنید​. این نوع ارزیابی تصویر واقعی از نحوه رفتار عامل در دنیای واقعی ارائه می‌دهد.

ارزیابی آنلاین اغلب شامل جمع‌آوری بازخورد ضمنی و صریح کاربران، همان‌طور که توضیح داده شد، و احتمالاً اجرای آزمایش‌های سایه یا A/B (که در آن نسخه جدیدی از عامل به صورت موازی برای مقایسه با نسخه قدیمی اجرا می‌شود). چالش این نوع ارزیابی این است که ممکن است برچسب‌ها یا امتیازات قابل اعتماد برای تعاملات زنده دشوار باشد – ممکن است به بازخورد کاربران یا معیارهای پایین‌دستی (مانند اینکه آیا کاربر روی نتیجه کلیک کرده است) متکی باشید.

### ترکیب دو نوع ارزیابی

ارزیابی آنلاین و آفلاین متقابل نیستند؛ آن‌ها کاملاً مکمل یکدیگرند. بینش‌های حاصل از نظارت آنلاین (مانند انواع جدید پرسش‌های کاربران که عامل در آن‌ها عملکرد ضعیفی دارد) می‌توانند برای تقویت و بهبود مجموعه داده‌های آزمایشی آفلاین استفاده شوند. به طور مشابه، عواملی که در آزمایش‌های آفلاین عملکرد خوبی دارند، می‌توانند با اطمینان بیشتری مستقر شده و به صورت آنلاین نظارت شوند.

در واقع، بسیاری از تیم‌ها یک حلقه را اتخاذ می‌کنند:

_ارزیابی آفلاین -> استقرار -> نظارت آنلاین -> جمع‌آوری موارد شکست جدید -> افزودن به مجموعه داده آفلاین -> اصلاح عامل -> تکرار_.

## مشکلات رایج

هنگام استقرار عوامل هوش مصنوعی در تولید، ممکن است با چالش‌های مختلفی روبرو شوید. در اینجا برخی از مشکلات رایج و راه‌حل‌های احتمالی آن‌ها آورده شده است:

| **مشکل**    | **راه‌حل احتمالی**   |
| ------------- | ------------------ |
| عامل هوش مصنوعی وظایف را به طور مداوم انجام نمی‌دهد | - درخواست داده‌شده به عامل هوش مصنوعی را اصلاح کنید؛ اهداف را به وضوح مشخص کنید.<br>- شناسایی کنید که تقسیم وظایف به زیروظایف و مدیریت آن‌ها توسط عوامل متعدد می‌تواند کمک‌کننده باشد. |
| عامل هوش مصنوعی وارد حلقه‌های مداوم می‌شود  | - اطمینان حاصل کنید که شرایط و ضوابط خاتمه واضحی دارید تا عامل بداند چه زمانی باید فرآیند را متوقف کند.<br>- برای وظایف پیچیده که نیاز به استدلال و برنامه‌ریزی دارند، از یک مدل بزرگ‌تر که برای وظایف استدلال تخصصی شده است استفاده کنید. |
| فراخوانی‌های ابزار عامل هوش مصنوعی عملکرد خوبی ندارند   | - خروجی ابزار را خارج از سیستم عامل آزمایش و اعتبارسنجی کنید. |

- پارامترها، درخواست‌ها، و نام ابزارها را بهبود دهید.  
| سیستم چندعاملی عملکرد ثابتی ندارد | - درخواست‌های داده‌شده به هر عامل را اصلاح کنید تا مشخص و متمایز از یکدیگر باشند.<br>- یک سیستم سلسله‌مراتبی با استفاده از یک عامل "مسیر‌یابی" یا کنترل‌کننده ایجاد کنید تا تعیین کند کدام عامل مناسب است. |

بسیاری از این مشکلات را می‌توان با استفاده از ابزارهای مشاهده‌پذیری بهتر شناسایی کرد. ردگیری‌ها و معیارهایی که قبلاً بحث شد، به شناسایی دقیق محل وقوع مشکلات در جریان کاری عامل کمک می‌کنند و فرآیند رفع اشکال و بهینه‌سازی را بسیار کارآمدتر می‌سازند.

## مدیریت هزینه‌ها

در اینجا چند استراتژی برای مدیریت هزینه‌های استقرار عوامل هوش مصنوعی در محیط تولید آورده شده است:

**استفاده از مدل‌های کوچک‌تر:** مدل‌های زبان کوچک (SLM) می‌توانند در برخی موارد استفاده عاملی عملکرد خوبی داشته باشند و هزینه‌ها را به‌طور قابل‌توجهی کاهش دهند. همان‌طور که قبلاً ذکر شد، ایجاد یک سیستم ارزیابی برای تعیین و مقایسه عملکرد در مقابل مدل‌های بزرگ‌تر بهترین راه برای درک این است که یک SLM چقدر در مورد استفاده شما عملکرد خواهد داشت. استفاده از SLM‌ها را برای وظایف ساده‌تر مانند طبقه‌بندی قصد یا استخراج پارامتر در نظر بگیرید و مدل‌های بزرگ‌تر را برای استدلال پیچیده نگه دارید.

**استفاده از مدل مسیریاب:** یک استراتژی مشابه استفاده از تنوع مدل‌ها و اندازه‌ها است. شما می‌توانید از یک LLM/SLM یا تابع بدون سرور برای مسیریابی درخواست‌ها بر اساس پیچیدگی به مدل‌های مناسب استفاده کنید. این کار نه تنها هزینه‌ها را کاهش می‌دهد بلکه عملکرد مناسب برای وظایف درست را نیز تضمین می‌کند. به‌عنوان مثال، درخواست‌های ساده را به مدل‌های کوچک‌تر و سریع‌تر هدایت کنید و فقط از مدل‌های بزرگ و گران‌قیمت برای وظایف استدلال پیچیده استفاده کنید.

**ذخیره‌سازی پاسخ‌ها:** شناسایی درخواست‌ها و وظایف رایج و ارائه پاسخ‌ها قبل از عبور از سیستم عاملی شما، راه خوبی برای کاهش حجم درخواست‌های مشابه است. حتی می‌توانید یک جریان برای شناسایی میزان شباهت یک درخواست به درخواست‌های ذخیره‌شده خود با استفاده از مدل‌های هوش مصنوعی پایه‌تر پیاده‌سازی کنید. این استراتژی می‌تواند هزینه‌ها را برای سوالات متداول یا جریان‌های کاری رایج به‌طور قابل‌توجهی کاهش دهد.

## بیایید ببینیم این در عمل چگونه کار می‌کند

در [دفترچه نمونه این بخش](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb)، نمونه‌هایی از نحوه استفاده از ابزارهای مشاهده‌پذیری برای نظارت و ارزیابی عامل خود را خواهیم دید.

## درس قبلی

[الگوی طراحی فراشناخت](../09-metacognition/README.md)

## درس بعدی

[MCP](../11-mcp/README.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما تلاش می‌کنیم دقت را حفظ کنیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نادرستی‌ها باشند. سند اصلی به زبان اصلی آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حساس، توصیه می‌شود از ترجمه حرفه‌ای انسانی استفاده کنید. ما مسئولیتی در قبال سوء تفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.