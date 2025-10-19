

# **گزارش فنی جامع: استخراج داده‌های کمی ناوگان بیل‌های هیدرولیک کوماتسو (PC800 تا PC3000) برای مدل‌سازی دینامیک معدن**

این گزارش فنی، داده‌های کمی لازم برای مدل‌سازی دقیق دینامیک بارگیری، بهینه‌سازی زمان چرخه (Cycle Time) و محاسبه راندمان مصرف سوخت (Liters/Ton) را در بیل‌های هیدرولیک معدنی منتخب کوماتسو (PC800-8، PC1250-11، PC2000-11 و PC3000-8/11) ارائه می‌دهد. در مدل‌سازی عملیات معدنی، تنها ظرفیت اسمی ماشین‌آلات کفایت نمی‌کند؛ بلکه درک دقیق از فشارهای هیدرولیک، نرخ جریان پمپ، نحوه تعامل ماشین با مواد مختلف (Bucket Fill Factor) و نرخ مصرف سوخت ساعتی در حالت‌های عملیاتی متفاوت، جهت تعیین هزینه عملیاتی بر تن، ضروری است.

---

## **۱. تحلیل دینامیک ورودی و نیروهای حفاری**

عملکرد یک بیل هیدرولیک در عملیات معدنی به طور مستقیم به توان ورودی موتور و تبدیل آن به نیروی حفاری و سرعت عملگرها توسط سیستم هیدرولیک بستگی دارد. کوماتسو در طراحی بیل‌های سایز بزرگ خود از سیستم‌های کنترل یکپارچه استفاده می‌کند تا توازن بهینه بین توان مکانیکی و هیدرولیک برقرار شود.

### **۱.۱. فلسفه کنترل سیستم‌های هیدرولیک**

مدل‌های بزرگ کوماتسو، به ویژه سری \-11، مجهز به سیستم‌های هیدرولیک پیشرفته‌ای هستند که جریان پمپ را با بار مورد نیاز عملگرها (Load) تنظیم می‌کنند تا از اتلاف انرژی جلوگیری شده و عملکرد چندمنظوره (Multifunction Performance) بهبود یابد.1 مدل‌های جدیدتر، مانند PC2000-11، از منطق کنترل پمپ-موتور کارآمدتر استفاده می‌کنند که منجر به زمان چرخه سریع‌تر و عملکرد بهتر در حین انجام چندین حرکت همزمان می‌شود.3

در نسل‌های جدید (P+ Mode)، تمرکز کوماتسو بر مدیریت کل توان (Total Power Management) است؛ به این معنی که توان موتور (Net Horsepower) در PC2000-11 تا ۹ درصد افزایش یافته است.3 این افزایش توان در کنار سیستم هیدرولیک کارآمد، به بیل اجازه می‌دهد تا بهره‌وری (تولید) را در حالت Power Plus تا ۱۲ درصد نسبت به مدل‌های قبلی افزایش دهد.4 این افزایش بهره‌وری مستقیماً از طریق کاهش زمان چرخه محقق می‌شود.

### **۱.۲. مشخصات کمی سیستم هیدرولیک برای مدل‌سازی بار (Q3)**

محاسبه توان هیدرولیک مورد نیاز در فاز حفاری و لیفت، ورودی اصلی برای مدل‌سازی بار بر روی موتور است. این توان با حاصل‌ضرب دبی پمپ ($\\text{L/min}$) در فشار سیستم ($\\text{MPa}$) تعیین می‌شود.

در مدل‌های PC800-8، حداکثر فشار در مدار تجهیزات (Implement) برابر با $31.4 \\text{ MPa}$ است. این مدل‌ها همچنین دارای حالت **Heavy Lift** هستند که با افزایش فشار تا $34.3 \\text{ MPa}$ (۳۵۰ بار یا $4,980 \\text{ psi}$)، نیروی بالابری را در شرایط سخت تا ۱۰ درصد افزایش می‌دهد.6 این ویژگی برای مدل‌سازی حفاری سنگین و جابجایی قطعات بزرگ سنگ حیاتی است.

در مدل PC1250-11، دبی پمپ اصلی (Implement and Travel) برابر با $2 \\times 494 \\text{ L/min}$ (مجموع $988 \\text{ L/min}$) است، به همراه یک پمپ مجزای $600 \\text{ L/min}$ برای مدار چرخش (Swing).8 فشار استاندارد مدار تجهیزات $31.4 \\text{ MPa}$ است. در حالت Heavy Lift، فشار تا $10\\%$ افزایش می‌یابد که به $34.5 \\text{ MPa}$ می‌رسد.1

یک نکته تحلیلی قابل توجه، کاهش فشار کاری در PC2000-11 در مقایسه با مدل‌های نسل قبل است. در حالی که PC2000-11 دارای دبی کلی بسیار بالایی معادل $2317 \\text{ L/min}$ برای تجهیزات، چرخش و حرکت است 5، فشار استاندارد مدار تجهیزات آن $29.4 \\text{ MPa}$ است.5 این طراحی نشان‌دهنده یک گرایش فنی در ماشین‌آلات بزرگ کوماتسو است: انتقال از تکیه بر نیروی خام (فشار بالا) به سمت **دینامیک مبتنی بر جریان** (Flow-Driven Dynamics). فشار کمتر، تنش مکانیکی و حرارتی کمتری را به اجزای هیدرولیک وارد می‌کند و دبی بسیار بالا، سرعت عملگرها و در نتیجه، زمان چرخه را به شدت کاهش می‌دهد.5

مدل PC3000-8/11 که یک بیل فوق سنگین است، دارای دبی پمپ‌های اصلی $2730 \\text{ L/min}$ و فشار کاری $31.0 \\text{ MPa}$ ($310 \\text{ bar}$) است.10

جدول ۱، مشخصات کلیدی سیستم هیدرولیک را برای مدل‌سازی توان و بار حفاری خلاصه می‌کند:

**جدول ۱: مشخصات فنی فشار کاری و دبی هیدرولیک اصلی (Q3)**

| مدل | توان موتور خالص (HP) | حداکثر دبی پمپ اصلی (L/min) | فشار کاری استاندارد (MPa) | فشار اوج (Heavy Lift) (MPa) |
| ----: | ----: | ----: | ----: | ----: |
| PC800-8 | 487 | N/A (پیستونی متغیر) | $31.4$ | $34.3$ 6 |
| PC1250-11 | $\\approx 758$ | $988$ (فقط Implement & Travel) 8 | $31.4$ | $34.5$ (تخمین $10\\%$ افزایش) |
| PC2000-11 | 1046 | $2317$ (Implement, Swing, Travel) 9 | $29.4$ 5 | $32.9$ (Travel) 5 |
| PC3000-8/11 | 1260 | $2730$ 10 | $31.0$ 10 | $31.0$ |

### **۱.۳. ضرایب پرشدن باکت (BFF) و تأثیر بافت مواد (Q1)**

ضریب پرشدن باکت ($\\eta$) یکی از حیاتی‌ترین متغیرهای ورودی برای تبدیل ظرفیت حجمی اسمی باکت به تناژ واقعی جابجا شده در هر چرخه است. این ضریب به طور مستقیم به دانسیته حجمی ماده (t/m³) و بافت آن بستگی دارد.11 کوماتسو دانسیته $1.8 \\text{ t/m}^3$ را به عنوان معیار طراحی بیل‌های معدنی خود در نظر می‌گیرد.10

در عملیات معدنی که با سنگ‌های انفجاری سروکار داریم، کیفیت انفجار (Fragmentation) تأثیر عمیقی بر BFF و در نتیجه بر راندمان بارگیری می‌گذارد.

* **سنگ با حفاری ضعیف (Poorly Blasted Rock):** در این شرایط، به دلیل ابعاد بزرگ سنگ‌ها، مقاومت بالا و مشکل در نفوذ کامل باکت، ضریب پرشدن به شدت کاهش می‌یابد و در محدوده **$60\\%$ تا $75\\%$** قرار می‌گیرد.13  
* **سنگ با حفاری مناسب (Well Blasted Rock):** بافت ریزتر و شکستگی‌های مناسب سنگ اجازه پر شدن بهتر باکت را می‌دهد و ضریب پرشدن در محدوده **$80\\%$ تا $95\\%$** قرار می‌گیرد.13

مواد آسان‌تر مانند خاک لومی مرطوب (Moist Loam) یا شن و ماسه، که تمایل به انباشتگی دارند، می‌توانند به ضرایب پرشدن بالای **$100\\%$ تا $110\\%$** دست یابند.13

**جدول ۲: ضرایب پرشدن باکت (BFF \- $\\eta$) برای مدل‌سازی تناژ خروجی**

| بافت ماده (Input Material) | ضریب پرشدن (η) (%) | مقدار (ورودی مدل‌سازی) | تأثیر بر عملیات |
| ----: | ----: | ----: | ----: |
| Well Blasted Rock (سنگ مناسب) | $80\\% \- 95\\%$ | $0.80 \- 0.95$ | حفاری سریع و پرشدن باکت در یک یا دو گذر |
| Poorly Blasted Rock (سنگ ضعیف) | $60\\% \- 75\\%$ | $0.60 \- 0.75$ | نیاز به نیروی نفوذ بالاتر (حالت P+)، افزایش زمان حفاری |
| Hard Clay (خاک رس سخت) | $85\\% \- 95\\%$ | $0.85 \- 0.95$ | چسبندگی بالا، نیازمند نیروی تخریب بالا 15 |
| Moist Loam / Sand (خاک لومی) | $100\\% \- 110\\%$ | $1.00 \- 1.10$ | پرشدن فراتر از ظرفیت اسمی (Heaped Capacity) |

یکی از پیامدهای حیاتی در مدل‌سازی، ارتباط مستقیم بین BFF و نرخ مصرف سوخت است. اگر BFF پایین باشد (مثلاً $60\\%$), بیل باید برای دستیابی به تناژ مشخص، زمان بیشتری را صرف حفاری در حالت حداکثر توان (P+) کند. این امر به طور پیوسته، هم زمان چرخه را افزایش می‌دهد و هم فشار بر سیستم هیدرولیک و موتور را بالا می‌برد، که در نهایت منجر به افزایش قابل توجه هزینه سوخت بر تن ($\\text{Liters/Ton}$) می‌شود. مدل‌سازی باید BFF را به عنوان یک متغیر کنترل‌کننده برای انتخاب حالت کاری موتور (P یا E) در فاز حفاری در نظر بگیرد.

---

## **۲. تحلیل زمان چرخه و بهینه‌سازی عملیاتی**

مدل‌سازی دقیق دینامیک بارگیری، به درک چگونگی بهینه‌سازی زمان چرخه (T\_Cycle) بستگی دارد. زمان چرخه، مجموع زمان‌های حفاری، چرخش با بار، تخلیه و بازگشت خالی است.

### **۲.۱. بهینه‌سازی زمان چرخش (Swing Time Optimization) (Q4)**

زمان چرخش (Swing Time) بزرگترین مؤلفه متغیر در چرخه بارگیری است و بهینه‌سازی آن، کلید کاهش $\\text{Liters/Ton}$ است. در طراحی معدن، تلاش می‌شود تا زاویه چرخش در کمترین حالت ممکن حفظ شود.

بر اساس قوانین مرجع در مهندسی ماشین‌آلات معدنی، بهینه‌ترین زاویه چرخش برای راندمان بالا بین $30^{\\circ}$ تا $60^{\\circ}$ است، که تقریباً **۳ درصد** بهره‌وری بیشتری نسبت به معیار $90^{\\circ}$ به همراه دارد.16 معیار $90^{\\circ}$ به عنوان استاندارد صنعتی برای اکثر مقایسه‌های راندمان سوخت در نظر گرفته می‌شود (مانند مقایسه‌های PC2000-11 با PC2000-8).4

برای مدل‌سازی دقیق چیدمان پیت (Pit Layout)، باید قاعده افزایش زمان چرخه را لحاظ کرد: هر **$10^{\\circ}$ چرخش اضافی** (فراتر از $90^{\\circ}$) تقریباً **۱ ثانیه** به زمان چرخه کلی اضافه می‌کند.17 این افزایش در زمان چرخه، در حالی که نرخ مصرف سوخت ساعتی (L/h) در حالت P+ ثابت است، مستقیماً به کاهش تناژ خروجی ساعتی و افزایش $\\text{Liters/Ton}$ منجر می‌شود.

فناوری‌های کاهش زمان غیربارور:  
کوماتسو با معرفی قابلیت‌هایی مانند Swing Priority Mode در مدل‌هایی چون PC1250-11 و PC800-8، سعی در کاهش زمان چرخه دارد. این حالت با تغییر اولویت جریان هیدرولیک، سرعت بوم در زوایای کوچک و سرعت چرخش در زوایای بزرگ را افزایش می‌دهد تا زمان کلی چرخه بهینه شود.1 همچنین، سیستم Shockless Boom Control با کاهش ارتعاش شاسی پس از توقف‌های ناگهانی، پاشش مواد را کم کرده و به حفظ محتوای باکت و ثبات سیستم کمک می‌کند.1

### **۲.۲. تأثیر حالت Power Plus (P+) بر دینامیک چرخه**

در مدل‌های سری \-11 (PC1250 و PC2000)، حالت P+ نقش حیاتی در بهینه‌سازی چرخه ایفا می‌کند. این حالت نه تنها توان موتور را افزایش می‌دهد، بلکه با کنترل هوشمند پمپ‌های هیدرولیک، سرعت و کارایی عملگرها را بهبود می‌بخشد. در PC2000-11، این بهینه‌سازی به **کاهش ۱۱ درصدی زمان چرخه** و افزایش تولید تا ۱۲ درصد منجر شده است.3

مدل‌سازی باید درک کند که در این مدل‌ها، بهبود راندمان (کاهش هزینه بر تن) بیشتر از طریق **افزایش سرعت چرخه** به دست می‌آید تا لزوماً کاهش مصرف سوخت مطلق. به عبارت دیگر، با وجود مصرف سوخت ساعتی نسبتاً بالا در حالت P+ (بخش ۳.۲)، چون تناژ جابجا شده در واحد زمان به طور قابل ملاحظه‌ای افزایش می‌یابد، معیار نهایی $\\text{Liters/Ton}$ کاهش می‌یابد. این هدف گذاری در گزارش کوماتسو مبنی بر **کاهش ۸ درصدی هزینه‌های تولید ($/ton$)** در PC2000-11 نسبت به مدل‌های قبلی، به وضوح مشهود است.3

---

## **۳. راندمان سوخت و مدیریت انرژی**

نرخ مصرف سوخت ساعتی ($\\text{L/h}$) در حالت‌های مختلف عملیاتی (Power, Economy, Lifting) مهمترین ورودی برای محاسبه هزینه‌های عملیاتی متغیر است.

### **۳.۱. معماری موتور و کارایی سوخت**

بیل‌های PC1250-11 و PC2000-11 به موتورهای پیشرفته Komatsu SAA12V140E-7 (استاندارد آلایندگی Tier 4 Final) مجهز هستند.1 این موتورها که از سیستم تزریق سوخت Heavy Duty High Pressure Common Rail (HPCR) بهره می‌برند، مصرف سوخت را در تمام دامنه کاری بهینه می‌کنند.1

مدل‌های کاری چندگانه:  
ماشین‌آلات کوماتسو دارای حالت‌های عملیاتی قابل انتخاب هستند که امکان تنظیم توان موتور، جریان پمپ و فشار سیستم را برای تطابق با بار فراهم می‌کند:

* **حالت Power Plus (P+):** حداکثر تولید و سریع‌ترین زمان چرخه. برای حفاری سنگ سخت و بارگیری با حداکثر تناژ.  
* **حالت Power (P):** تولید استاندارد. در PC2000-11، این حالت $7\\%$ راندمان سوخت بهتری نسبت به PC2000-8 P Mode دارد.4  
* **حالت Economy (E/E0):** برای کارهای سبک‌تر یا تمیزکاری سطح. مصرف سوخت را به شدت کاهش می‌دهد. در PC2000-11، مصرف سوخت در حالت E0 تا $8\\%$ الی $9\\%$ نسبت به PC2000-8 P Mode کاهش یافته است.4 مدل‌های PC800-8 دارای چهار سطح قابل انتخاب برای حالت Economy هستند (E0 تا E3).19  
* **حالت Lifting (L):** در PC1250-11 با افزایش ۱۰ درصدی فشار هیدرولیک همراه است و برای جابجایی قطعات سنگین استفاده می‌شود.1  
* **حالت Breaker (B):** جریان و دور موتور را برای عملکرد بهینه چکش هیدرولیک تنظیم می‌کند.21

### **۳.۲. تخمین نرخ مصرف سوخت ساعتی (Q2)**

نرخ‌های مطلق مصرف سوخت ($\\text{L/h}$) معمولاً به صورت عمومی منتشر نمی‌شوند و به شدت به شرایط کاری، ارتفاع، و مهارت اپراتور وابسته هستند. با این حال، می‌توان بر اساس توان موتور (HP) و استانداردهای صنعتی، نرخ‌های ساعتی تخمینی را برای هر حالت کاری استخراج کرد که به عنوان ورودی‌های پایه برای مدل‌سازی دینامیک سوخت استفاده می‌شود.

**جدول ۳: تخمین نرخ مصرف سوخت ساعتی (L/h) در حالت‌های عملیاتی (Q2)**

| مدل | توان موتور خالص (HP) | حالت Power (P/P+) (L/h) | حالت Economy (E/E0) (L/h) | حالت Lifting (L) / Breaker (B) (L/h) |
| ----: | ----: | ----: | ----: | ----: |
| PC800-8 | 487 18 | $140 \- 155$ | $115 \- 130$ | $\\approx 160$ (Heavy Lift) / $100 \- 110$ (B Mode) |
| PC1250-11 | $\\approx 758$ | $180 \- 200$ | $150 \- 170$ | $160 \- 180$ (L Mode) |
| PC2000-11 | 1046 2 | $230 \- 250$ | $195 \- 215$ | $210 \- 230$ (L Mode) |
| PC3000-8 | 1260 22 | $280 \- 310$ | $240 \- 270$ | N/A |

### **۳.۳. مدیریت مصرف سوخت در زمان‌های غیرفعال**

مدل‌سازی جامع راندمان سوخت باید زمان‌های غیرفعال (Idle Time) را که سهم قابل توجهی در مصرف سوخت شیفت کاری دارند، لحاظ کند. ویژگی **Auto Idle Shutdown (AIS)** در مدل‌هایی مانند PC1250-11 و HD785-8، موتور را پس از یک دوره از پیش تعیین شده (۵ تا ۶۰ دقیقه) به صورت خودکار خاموش می‌کند، و از هدر رفتن سوخت در زمان انتظار کامیون جلوگیری می‌نماید.23

همچنین، نمایشگرهای داخل کابین مجهز به **ECO Guidance** هستند که به اپراتور کمک می‌کنند تا در محدوده سبز عملیات کند، که این امر یک عامل **رفتاری** مهم در کاهش مصرف لحظه‌ای سوخت است.20

---

## **۴. نتیجه‌گیری و داده‌های کمی نهایی (JSON)**

بیل‌های هیدرولیک معدنی کوماتسو از PC800-8 تا PC3000-8، یک طیف عملکردی از مدیریت قدرت موتور (HP) به سمت مدیریت جریان هیدرولیک (Flow) را نشان می‌دهند. در حالی که مدل‌های بزرگتر (PC3000) بر ظرفیت حجمی بالا تکیه دارند، مدل‌های نسل جدید (PC1250-11 و PC2000-11) با استفاده از حالت‌های P+ و سیستم‌های هیدرولیک با دبی بالا، بر کاهش زمان چرخه تمرکز می‌کنند تا راندمان $\\text{Liters/Ton}$ را بهبود بخشند.

برای مدل‌ساز، درک این امر که هزینه‌های تولید در مدل‌های \-11 از طریق افزایش بهره‌وری (کاهش زمان چرخه) و نه صرفاً کاهش مصرف سوخت مطلق، کاهش می‌یابد، حیاتی است. استفاده از ضرایب BFF برای تنظیم تناژ بر اساس کیفیت انفجار و استفاده از نرخ‌های $\\text{L/h}$ تفکیک‌شده بر اساس حالت کاری (جدول ۳)، دقت مدل‌سازی دینامیک هزینه عملیاتی را به حداکثر می‌رساند.

### **۴.۱. داده‌های کمی استخراج شده برای مدل‌سازی (JSON)**

داده‌های استخراج شده برای پارامترهای ۱ تا ۳ (Q1, Q2, Q3) در قالب JSON ارائه شده است تا مستقیماً به عنوان ورودی در نرم‌افزارهای شبیه‌سازی و مدل‌سازی هزینه مورد استفاده قرار گیرد. مقادیر L/h به صورت محدوده \[حداقل، حداکثر\] تخمین زده شده‌اند.

JSON

{  
  "Komatsu\_Mining\_Shovels\_Quantitative\_Data": {  
    "PC800-8": {  
      "Engine": "SAA6D140E-5 (Tier 3)",  
      "Net\_HP": 487,  
      "Hydraulic\_System": {  
        "Max\_Pressure\_Implement\_MPa": 31.4,  
        "Max\_Pressure\_HeavyLift\_MPa": 34.3,  
        "Swing\_Pressure\_MPa": 28.4,  
        "Main\_Pump\_Flow\_L/min": "N/A (Variable capacity piston type)"  
      },  
      "Fuel\_Consumption\_L/h\_Estimates": {  
        "Power\_Mode": ,  
        "Economy\_Mode": ,  
        "Lifting\_Mode": 160,  
        "Breaker\_Mode":   
      },  
      "Bucket\_Fill\_Factor\_Reference": {  
        "Well\_Blasted\_Rock\_Min": 0.80,  
        "Poorly\_Blasted\_Rock\_Max": 0.75,  
        "Moist\_Loam\_Max": 1.10  
      }  
    },  
    "PC1250-11": {  
      "Engine": "SAA12V140E-7 (Tier 4 Final)",  
      "Net\_HP": 758,  
      "Hydraulic\_System": {  
        "Max\_Pressure\_Implement\_MPa": 31.4,  
        "Max\_Pressure\_HeavyLift\_MPa": 34.5,  
        "Main\_Pump\_Flow\_L/min": 988,  
        "Swing\_Pump\_Flow\_L/min": 600  
      },  
      "Fuel\_Consumption\_L/h\_Estimates": {  
        "Power\_Plus\_Mode": ,  
        "Economy\_Mode": ,  
        "Lifting\_Mode": ,  
        "Breaker\_Mode": "N/A"  
      },  
      "Bucket\_Fill\_Factor\_Reference": {  
        "Well\_Blasted\_Rock\_Min": 0.80,  
        "Poorly\_Blasted\_Rock\_Max": 0.75,  
        "Moist\_Loam\_Max": 1.10  
      }  
    },  
    "PC2000-11": {  
      "Engine": "SAA12V140E-7 (Tier 4 Final)",  
      "Net\_HP": 1046,  
      "Hydraulic\_System": {  
        "Max\_Pressure\_Implement\_MPa": 29.4,  
        "Max\_Pressure\_Travel\_MPa": 32.9,  
        "Main\_Pump\_Flow\_L/min": 2317  
      },  
      "Fuel\_Consumption\_L/h\_Estimates": {  
        "Power\_Plus\_Mode": ,  
        "Economy\_Mode": ,  
        "Lifting\_Mode": ,  
        "Breaker\_Mode": "N/A"  
      },  
      "Bucket\_Fill\_Factor\_Reference": {  
        "Well\_Blasted\_Rock\_Min": 0.80,  
        "Poorly\_Blasted\_Rock\_Max": 0.75,  
        "Moist\_Loam\_Max": 1.10  
      }  
    },  
    "PC3000-8": {  
      "Engine": "SSA12V159",  
      "Net\_HP": 1260,  
      "Hydraulic\_System": {  
        "Max\_Pressure\_Implement\_MPa": 31.0,  
        "Max\_Pressure\_Bar": 310,  
        "Main\_Pump\_Flow\_L/min": 2730  
      },  
      "Fuel\_Consumption\_L/h\_Estimates": {  
        "Power\_Mode": ,  
        "Economy\_Mode": ,  
        "Lifting\_Mode": "N/A",  
        "Breaker\_Mode": "N/A"  
      },  
      "Bucket\_Fill\_Factor\_Reference": {  
        "Well\_Blasted\_Rock\_Min": 0.80,  
        "Poorly\_Blasted\_Rock\_Max": 0.75,  
        "Moist\_Loam\_Max": 1.10  
      }  
    }  
  }  
}

#### **Works cited**

1. PC1250LC-11 PC1250SP-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc1250/pc1250-11-aess861-02.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc1250/pc1250-11-aess861-02.pdf)  
2. PC2000-11 \- SMS Equipment, accessed October 19, 2025, [https://www.smsequipment.com/getmedia/b680d16a-beac-4156-8760-70d225a1ff93/PC2000-11.pdf](https://www.smsequipment.com/getmedia/b680d16a-beac-4156-8760-70d225a1ff93/PC2000-11.pdf)  
3. PC2000-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/excavators/surface-mining-excavators/pc2000-11](https://www.komatsu.com/en-us/products/equipment/excavators/surface-mining-excavators/pc2000-11)  
4. PC2000-11R, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/worldwide-website/asia\_b/awajo/cen00912-01.pdf?rev=516db1a270bf472784cec61a01c4aa4c\&hash=C774FD8277C0AE87B606104D3C33864E](https://www.komatsu.jp/en/-/media/home/worldwide-website/asia_b/awajo/cen00912-01.pdf?rev=516db1a270bf472784cec61a01c4aa4c&hash=C774FD8277C0AE87B606104D3C33864E)  
5. PC2000-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc2000lc/pc2000-11-aess933-01.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc2000lc/pc2000-11-aess933-01.pdf)  
6. PC800LC-8 \- General Equipment & Supplies, Inc., accessed October 19, 2025, [https://www.genequip.com/assets/Uploads/PC800LC-8-MH.pdf](https://www.genequip.com/assets/Uploads/PC800LC-8-MH.pdf)  
7. PC800LC-8 \- Anderson Equipment Company, accessed October 19, 2025, [https://www.andersonequip.com/web/files/MfrModelDocs/KAC-PC800LC-8-broc.pdf](https://www.andersonequip.com/web/files/MfrModelDocs/KAC-PC800LC-8-broc.pdf)  
8. PC1250LC-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/excavators/large-excavators/pc1250lc-11](https://www.komatsu.com/en-us/products/equipment/excavators/large-excavators/pc1250lc-11)  
9. PC2000-11R \- AWS, accessed October 19, 2025, [https://webklat.s3.amazonaws.com/wp-content/uploads/2024/05/13191642/Catalogo-Excavadora-Hidraulica-PC2000-11R-ing-digital.pdf](https://webklat.s3.amazonaws.com/wp-content/uploads/2024/05/13191642/Catalogo-Excavadora-Hidraulica-PC2000-11R-ing-digital.pdf)  
10. PC3000-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/excavators/surface-mining-excavators/pc3000-11](https://www.komatsu.com/en-us/products/equipment/excavators/surface-mining-excavators/pc3000-11)  
11. Excavator Bucket Size Chart: How To Choose the Right Type | BigRentz, accessed October 19, 2025, [https://www.bigrentz.com/blog/excavator-bucket-size-chart](https://www.bigrentz.com/blog/excavator-bucket-size-chart)  
12. Material Density Tables to Help Estimate Earthwork Volumes | Cat | Caterpillar, accessed October 19, 2025, [https://www.cat.com/en\_US/articles/ci-articles/earthwork-volumes-reference-tables.html](https://www.cat.com/en_US/articles/ci-articles/earthwork-volumes-reference-tables.html)  
13. Bucket Fill Factors | Cat | Caterpillar, accessed October 19, 2025, [https://www.cat.com/en\_US/articles/ci-articles/bucket-fill-factors.html](https://www.cat.com/en_US/articles/ci-articles/bucket-fill-factors.html)  
14. Bucket Fill Factors \- Bucket Selection Chart \- B. A. Caulkett, accessed October 19, 2025, [https://bacaulkett.com/bucket-fill-factors-bucket-selection-chart/](https://bacaulkett.com/bucket-fill-factors-bucket-selection-chart/)  
15. Understanding Excavator Bucket Capacities \- Werk-Brau, accessed October 19, 2025, [https://werk-brau.com/understanding-excavator-bucket-capacities/](https://werk-brau.com/understanding-excavator-bucket-capacities/)  
16. Loading tool selection guide \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/mining-parts/loadingtoolselectionguide-brochure-english-en-ltsgbr01-0522-v3.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/mining-parts/loadingtoolselectionguide-brochure-english-en-ltsgbr01-0522-v3.pdf)  
17. Productivity, Earthmoving and OOC Komatsu | PDF | Loader (Equipment) | Soil \- Scribd, accessed October 19, 2025, [https://www.scribd.com/document/337547096/Productivity-Earthmoving-and-OOC-Komatsu](https://www.scribd.com/document/337547096/Productivity-Earthmoving-and-OOC-Komatsu)  
18. PC800/800LC-8R1 BACKHOE, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/worldwide-website/asia\_b/download\_crawlerexcavators/pc800lc-8r1.pdf?rev=24345dd0f9a547a6ad15dd9988ac9f30\&hash=F21ED85767AD54D3C8145368EE93B57E](https://www.komatsu.jp/en/-/media/home/worldwide-website/asia_b/download_crawlerexcavators/pc800lc-8r1.pdf?rev=24345dd0f9a547a6ad15dd9988ac9f30&hash=F21ED85767AD54D3C8145368EE93B57E)  
19. PC800/800SE-8 BACKHOE, accessed October 19, 2025, [https://istk.ru/upload/iblock/dc7/dc771793eeacd34b8ecc88a2da9f5d71.pdf](https://istk.ru/upload/iblock/dc7/dc771793eeacd34b8ecc88a2da9f5d71.pdf)  
20. Komatsu PC800LC-8 Excavators Specs | SMS Equipment, accessed October 19, 2025, [https://www.smsequipment.com/en-us/new-equipment/excavators/komatsu-pc800lc-8/](https://www.smsequipment.com/en-us/new-equipment/excavators/komatsu-pc800lc-8/)  
21. PC290LC-11/PC290LCi-11 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc290lc/excavator-pc290lc-290lci-11-full-brochure-english-en-pc290lc-lci-11-fb01-0222-v1.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/excavators/pc290lc/excavator-pc290lc-290lci-11-full-brochure-english-en-pc290lc-lci-11-fb01-0222-v1.pdf)  
22. Komatsu PC3000 Shovel Specs & Dimensions :: RitchieSpecs, accessed October 19, 2025, [https://www.ritchiespecs.com/model/komatsu-pc3000-shovel](https://www.ritchiespecs.com/model/komatsu-pc3000-shovel)  
23. HD785-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd785-8](https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd785-8)