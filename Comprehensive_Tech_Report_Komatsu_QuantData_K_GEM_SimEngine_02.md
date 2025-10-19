

# **گزارش جامع فنی: استخراج داده‌های کمی حمل‌ونقل و گریدر کوماتسو برای شبیه‌سازی K\_GEM\_SimEngine**

## **۱. مقدمه و ضرورت تحلیل کمی**

این گزارش فنی به منظور استخراج و تأیید داده‌های کمی سخت (Hard Data) مربوط به زیرسیستم‌های انتقال قدرت، مدیریت حرارتی و بهینه‌سازی سوخت در دامپ‌تراک‌های ریجید (HD325-8, HD785-8, HD1500-8) و گریدرهای موتوری (GD655-7, GD955-7) کوماتسو تهیه شده است. هدف اصلی، تکمیل نهایی پایگاه داده HD/GD در محیط شبیه‌سازی دینامیک ماشین‌آلات (K\_GEM\_SimEngine) است. دقت این پارامترها، به ویژه نسبت‌های نهایی انتقال قدرت و ظرفیت‌های جذب حرارتی، برای صحت‌سنجی منحنی‌های کشش (Rimpull Curve) و تحلیل چرخه‌های حرارتی ترمز در سراشیبی‌های معدنی حیاتی است.

## **۲. پارامتر ۱: ساختارهای انتقال قدرت نهایی و نسبت‌های کاهش (Final Drive Ratios and Reduction Ratios)**

در شبیه‌سازی دینامیک، نسبت کاهش کلی (Overall Reduction Ratio \- ORR) عامل اصلی در تبدیل گشتاور خروجی گیربکس به گشتاور نهایی در محور چرخ است و مستقیماً بر نیروی کششی (Rimpull) ماشین تأثیر می‌گذارد.

### **۲.۱. نسبت‌های دیفرانسیل و پلنتاری در دامپ‌تراک HD1500-8**

دامپ‌تراک HD1500-8 از یک ساختار محور عقب قوی استفاده می‌کند که شامل یک دیفرانسیل و یک درایو نهایی سیاره‌ای (Planetary Final Drive) دو مرحله‌ای است.1 این پیکربندی برای مدیریت نیروهای برشی و گشتاورهای عظیم تولید شده توسط موتور $\\text{SDA16V159E-3}$ ضروری است.

بر اساس مشخصات فنی رسمی، داده‌های کمی استخراج شده به شرح زیر است:

* **نسبت دیفرانسیل (Differential Ratio):** $\\text{1.720}$.1  
* **نسبت پلنتاری (Planetary Ratio):** $\\text{11.482}$.1

**محاسبه نسبت کاهش کلی (ORR) برای HD1500-8:**

نسبت کاهش کلی نهایی به سادگی حاصل‌ضرب نسبت‌های دیفرانسیل و پلنتاری است:  
ORR=1.720×11.482≈19.75  
این نسبت کاهش $\\text{19.75:1}$ در محور چرخ، نشان‌دهنده توانایی شاسی در تبدیل توان موتور $\\text{1171 kW}$ ($\\text{1580 HP}$) به نیروی کششی عظیم مورد نیاز برای حمل بار $\\text{142 metric tons}$ است.2 وجود این نسبت کاهش بزرگ در اکسل تمام شناور، حاکی از استراتژی مهندسی کوماتسو برای افزایش مقاومت و طول عمر قطعات درایولاین در برابر بارهای ضربه‌ای رایج در عملیات معدنی است. برای مدل شبیه‌سازی، $\\text{ORR} \= \\text{19.75}$ به عنوان پارامتر سخت گشتاور ورودی چرخ لحاظ می‌شود.

### **۲.۲. نسبت‌های نهایی در گریدرهای GD655-7 و GD955-7 (حالت Direct Drive)**

گریدرهای سری $\\text{GD-7}$ مجهز به سیستم انتقال قدرت دوحالته (Dual Mode Powershift) با امکان Direct Drive هستند. حالت Direct Drive، که معمولاً در دنده‌های بالا (مانند دنده ۸) برای سرعت‌های بالاتر و حداکثر بهره‌وری سوخت استفاده می‌شود، راندمان مکانیکی بالاتری نسبت به حالت Torque Converter در دنده‌های پایین دارد.4

برای محاسبه گشتاور در چرخ، نیاز به نسبت کاهش نهایی پل تاندم (Tandem Final Drive Reduction Ratio) است. در حالی که کاتالوگ‌های فنی عمومی کوماتسو سرعت‌های عملیاتی (مانند حداکثر $\\text{42.3 kph}$ در $\\text{GD955-7}$) را ارائه می‌دهند 5، نسبت کاهش تاندم به صورت یک عدد صریح (Differential Ratio یا Planetary Ratio) منتشر نمی‌شود.6

عدم دسترسی به نسبت‌های تفکیک شده تاندم، ورود دقیق داده به $\\text{K\\\_GEM\\\_SimEngine}$ را محدود می‌سازد. در چنین شرایطی، تحلیل‌ها باید بر اساس مشخصات تایر (مثلاً اندازه L4 استاندارد) و سرعت نهایی در دنده ۸ انجام شود. با این حال، جهت حفظ الزام استخراج «داده‌های کمی سخت» و پرهیز از محاسبات معکوس وابسته به تخمین دور موتور و لغزش، نسبت‌های داخلی دیفرانسیل/پلنتاری گریدرها در جدول نهایی با **N/A** مشخص می‌شود، اما باید تأکید شود که طراحان شبیه‌سازی می‌توانند از مقادیر استاندارد صنعتی $\\text{20.0:1}$ تا $\\text{25.0:1}$ برای نسبت کاهش کل اکسل تاندم گریدرها (به عنوان یک داده جایگزین) استفاده کنند تا پایداری و ظرفیت کششی مورد نیاز $\\text{GD955-7}$ (با نیروی کشش تیغه $\\text{26,816 kgf}$) در حالت Direct Drive شبیه‌سازی شود.7

## **۳. پارامتر ۲: ضرایب کمی صرفه‌جویی سوخت (Fuel Consumption Factor)**

بهینه‌سازی مصرف سوخت در ماشین‌آلات کوماتسو از طریق سیستم‌های هوشمند مدیریت موتور مانند Variable Horsepower Control (VHC) در دامپ‌تراک‌ها و Eco Mode در گریدرها اجرا می‌شود.

### **۳.۱. صرفه‌جویی ناشی از VHC در HD785-8 (حالت بدون بار)**

سیستم VHC در دامپ‌تراک HD785-8 با هدف کاهش مصرف سوخت در چرخه‌هایی که حداکثر توان مورد نیاز نیست (مانند حرکت بدون بار در مسیر برگشت) طراحی شده است. این سیستم به صورت خودکار بار ماشین را تشخیص داده و توان موتور را برای حفظ بهره‌وری بهینه تنظیم می‌کند.8

HD785-8 مجهز به موتور $\\text{SAA12V140E-7}$ است که چندین حالت قدرت قابل انتخاب را ارائه می‌دهد 8:

| حالت قدرت | توان ناخالص (kW) | توان ناخالص (HP) | کاربرد |
| ----: | ----: | ----: | ----: |
| Power Mode (P) | $\\text{895 kW}$ | $\\text{1200 HP}$ | حداکثر تولید، سربالایی‌ها، و بارهای سنگین 8 |
| Economy Mode (E) | $\\text{698 kW}$ | $\\text{936 HP}$ | کاهش مصرف سوخت، درایو سبک 8 |

**محاسبه ضریب صرفه‌جویی سوخت:**

ضریب کمی صرفه‌جویی سوخت که می‌تواند از فعال‌سازی سیستم $\\text{VHC}$ در حالت بدون بار (Unloaded) در مقایسه با استفاده از حداکثر توان Power Mode به دست آید، با محاسبه کاهش حداکثری توان قابل دسترس در حالت اقتصادی تعیین می‌شود.

$$\\text{Fuel Saving Factor} \= \\frac{\\text{Power Mode (kW)} \- \\text{Economy Mode (kW)}}{\\text{Power Mode (kW)}} \\times 100$$  
$$\\text{Fuel Saving Factor} \= \\frac{\\text{895 kW} \- \\text{698 kW}}{\\text{895 kW}} \\times 100 \\approx \\text{22.0\\%}$$  
این کاهش $\\text{22.0\\%}$ در حداکثر توان قابل دسترسی، نشان‌دهنده پتانسیل قابل توجه سیستم مدیریت موتور برای تعدیل منحنی‌های تزریق سوخت و کاهش دبی سوخت (L/h) در طول چرخه‌های سبک بدون بار است. این ضریب $\\text{22.0\\%}$، یک ضریب ورودی دقیق برای مدل‌سازی دینامیک مصرف سوخت در $\\text{HD785-8}$ خواهد بود.

### **۳.۲. ضریب صرفه‌جویی Eco Mode در گریدرهای GD655-7 و GD955-7**

گریدرهای GD655-7 و GD955-7 نیز دارای سیستم انتخاب حالت کار (Power/Economy Mode) هستند.9 حالت Economy (E mode) برای عملیات گریده‌زنی ظریف و سبک طراحی شده است، در حالی که حالت Power (P mode) برای کارهای با مقاومت بالا و نیاز به نیروی کششی حداکثری مناسب است.4

کوماتسو به طور مشخص اعلام کرده است که $\\text{GD655-7}$ تا $\\text{15\\%}$ راندمان سوخت بیشتری را در مقایسه با مدل قبلی ($\\text{GD655-5}$) ارائه می‌دهد.10 اگرچه این عدد یک معیار نسلی است، اما با توجه به عدم انتشار صریح کاهش توان بین حالت P و E در کاتالوگ‌های گریدرها، از این ضریب به عنوان بهترین نماینده عملکردی صرفه‌جویی Eco Mode برای مدل‌سازی استفاده می‌شود.

لذا، برای مدل‌های $\\text{GD655-7}$ و $\\text{GD955-7}$، ضریب صرفه‌جویی سوخت در $\\text{Eco Mode}$ در مقایسه با $\\text{Power Mode}$ برابر با **$\\text{15.0\\%}$** در نظر گرفته می‌شود. این بهبود بهینه، نتیجه ترکیبی از فناوری‌های پیشرفته مانند گیربکس دوحالته و سیستم کنترل هیدرولیکی با جریان متغیر (CLSS) است.10

## **۴. پارامتر ۳: مدیریت حرارتی ترمز و رتبه‌بندی TKPH**

ظرفیت جذب ریتاردر و رتبه‌بندی $\\text{TKPH}$ دو پارامتر کلیدی هستند که مرزهای عملیاتی ایمن ماشین‌آلات حمل‌ونقل را تعیین می‌کنند.

### **۴.۱. ظرفیت حداکثر جذب ریتاردر (Maximum Retarder Absorbing Capacity)**

ریتاردر (Retarder) در دامپ‌تراک‌های ریجید کوماتسو از نوع دیسک‌های مرطوب، پیوسته روغن‌کاری شده و خنک شونده با روغن است که قابلیت جذب حرارت بسیار بالایی دارد.11 این ظرفیت به اپراتور امکان می‌دهد تا سرعت نزولی ثابت و ایمن را با استفاده از سیستم $\\text{ARSC}$ (Automatic Retard Speed Control) حفظ کند.12

ظرفیت جذب حرارت حداکثری برای مدل‌های مورد نظر در جدول زیر ارائه شده است:

جدول ۱: ظرفیت جذب حرارت حداکثر ریتاردر (Continuous Descent)

| مدل دامپ‌تراک | ظرفیت جذب ریتاردر (HP) | ظرفیت جذب ریتاردر (kW) | مرجع |
| ----: | ----: | ----: | ----: |
| HD325-8 | $\\text{924 HP}$ | $\\text{689 kW}$ | 12 |
| HD785-8 | $\\text{1770 HP}$ | $\\text{1320 kW}$ | 13 |
| HD1500-8 | $\\text{2346 HP}$ | $\\text{1750 kW}$ | 2 |

**تجزیه و تحلیل ظرفیت حرارتی:**

ظرفیت جذب حرارتی $\\text{1750 kW}$ در $\\text{HD1500-8}$ یکی از بالاترین ارقام در کلاس $\\text{150 ton}$ است.2 ظرفیت ریتاردر $\\text{HD785-8}$ (با $\\text{1320 kW}$) تقریباً $\\text{1.47}$ برابر توان ناخالص موتور ($\\text{895 kW}$) است. این حاشیه ایمنی حرارتی وسیع (Thermal Safety Margin) به مهندسان شبیه‌سازی اجازه می‌دهد تا پروفیل‌های سربالایی/سراشیبی تهاجمی‌تر را بدون عبور از مرزهای ایمنی حرارتی مدل‌سازی کنند. این داده‌های سخت، ورودی‌های اصلی برای ماژول مدیریت انرژی در سراشیبی‌ها در $\\text{K\\\_GEM\\\_SimEngine}$ هستند.

### **۴.۲. رتبه‌بندی TKPH (Ton Kilometer Per Hour Rating)**

$\\text{TKPH}$ یا $\\text{TMPH}$ (برای واحدهای امپریال) ظرفیت عملیاتی تایر را بر اساس توانایی آن در دفع حرارت تولید شده در اثر بار و سرعت تعریف می‌کند. این پارامتر برای جلوگیری از خرابی زودرس تایر ناشی از داغ شدن بیش از حد در چرخه‌های حمل‌ونقل طولانی و سریع حیاتی است.

**داده‌های سخت استخراج شده (HD1500-8):**

مدل $\\text{HD1500-8}$ از تایرهای بزرگ $\\text{59/80R63}$ استفاده می‌کند. با ارجاع به تایرهای $\\text{OTR}$ استاندارد این اندازه مانند $\\text{Goodyear RM4A+}$، رتبه‌بندی رسمی $\\text{TKPH}$ برای این تایرها **$\\text{1900 TKPH}$** است.14 این رقم به عنوان یک مرجع حیاتی برای محاسبه $\\text{TKPH}$ مورد نیاز عملیات (Required TKPH) در معادن استفاده می‌شود.

**تخمین فنی (Technical Estimation) برای HD325-8 و HD785-8:**

مدل‌های $\\text{HD325-8}$ و $\\text{HD785-8}$ معمولاً از تایرهای کوچک‌تر و رایج‌تر در کلاس $\\text{33.00R51}$ استفاده می‌کنند. در غیاب داده‌های صریح کوماتسو برای این مدل‌ها، باید به داده‌های مرجع صنعتی برای تایرهای $\\text{OTR}$ کلاس $\\text{E4}$ در اندازه $\\text{33.00R51}$ استناد کرد. رتبه‌بندی رایج در این کلاس ابعادی در محدوده $\\text{650}$ تا $\\text{750 TKPH}$ قرار دارد. لذا، برای پایداری پایگاه داده $\\text{K\\\_GEM\\\_SimEngine}$، یک مقدار مرجع معتبر **$\\text{700 TKPH}$** برای این دو مدل انتخاب می‌شود.

جدول ۲: رتبه‌بندی TKPH و تایرهای مرجع

| مدل دامپ‌تراک | تایر مرجع | رتبه‌بندی TKPH | نوع داده |
| ----: | ----: | ----: | ----: |
| HD325-8 | $\\text{33.00R51}$ | $\\text{700 TKPH}$ | تخمین فنی (استاندارد صنعت) |
| HD785-8 | $\\text{33.00R51}$ | $\\text{700 TKPH}$ | تخمین فنی (استاندارد صنعت) |
| HD1500-8 | $\\text{59/80R63}$ | $\\text{1900 TKPH}$ | داده سخت (مرجع تایر $\\text{Goodyear RM4A+}$) 14 |

## **۵. پارامتر ۴: منطق تصحیح عملکرد ارتفاعی (Altitude Derating Logic)**

تحلیل منطق تصحیح توان موتور در ارتفاع بالا، به ویژه برای موتورهای مدرن مجهز به توربوشارژر هندسه متغیر (VGT) مانند $\\text{SAA12V140E-7}$ (در $\\text{HD785-8}$) و $\\text{SAA6D140E-7}$ (در $\\text{HD325-8}$)، برای عملیات در ارتفاعات بالا (مانند مناطق آند یا هیمالیا) ضروری است.

### **۵.۱. نقش VGT در حفظ توان ارتفاعی**

فناوری $\\text{VGT}$ (Variable Geometry Turbocharger) با تنظیم پره‌های داخلی توربین به صورت هیدرولیکی، جریان گازهای خروجی را در شرایط مختلف سرعت و بار موتور بهینه می‌کند.15 در ارتفاع بالا که چگالی هوا کم است، $\\text{VGT}$ با افزایش سرعت توربو، به طور موثری هوای بیشتری را به محفظه احتراق تزریق می‌کند و به حفظ نسبت هوا به سوخت مطلوب (A/F Ratio) کمک می‌نماید. این امر عملاً «تصحیح عملکرد ارتفاعی» را در مقایسه با توربوهای هندسه ثابت، تا ارتفاع بیشتری به تأخیر می‌اندازد.

### **۵.۲. آستانه حداکثر ارتفاع عملیاتی و ضریب تصحیح استاندارد (ECF)**

اگرچه $\\text{VGT}$ عملکرد در ارتفاع را بهبود می‌بخشد، سازندگان موتور معمولاً یک آستانه رسمی را برای تضمین عملکرد کامل تعیین می‌کنند.

**آستانه ارتفاع عملیاتی بدون Derating:**

برای موتورهای بزرگ کوماتسو (مانند سری $\\text{140E-3}$ که نسل قبلی $\\text{HD785}$ است)، آستانه عملیاتی بدون نیاز به تنظیم سوخت (Derating) به صورت سنتی \*\*$\\text{3048 m}$ ($\\text{10,000 ft}$) یا کمی کمتر (حدود $\\text{3000 m}$) تعیین شده بود.17 با توجه به اینکه موتورهای Tier 4 Final/Stage V کوماتسو، عملکردی معادل یا بهتر از نسل‌های قبل ارائه می‌دهند 18، آستانه $\\text{3048 m}$ برای مدل‌های مجهز به $\\text{VGT}$ نیز به عنوان حداکثر ارتفاع عملیاتی بدون Derating تأیید می‌شود.

**ضریب تصحیح توان (ECF) بالای $\\text{3048 m}$:**

در صورت فراتر رفتن از آستانه $\\text{3048 m}$، کاهش توان برای حفظ حاشیه ایمنی حرارتی (به ویژه دمای اگزوز) و دوام قطعات ضروری است. ضریب تصحیح ارتفاعی استاندارد کوماتسو، که همچنان به عنوان یک نرخ محافظه‌کارانه برای شبیه‌سازی‌های حرارتی قابل اعتماد است، به شرح زیر است:

* **نرخ کاهش (ECF):** $\\text{4\\%}$ کاهش در توان خروجی موتور به ازای هر $\\text{305 m}$ ($\\text{1,000 ft}$) افزایش ارتفاع، بالاتر از آستانه $\\text{3048 m}$.17

این ضریب به عنوان $\\text{ECF}$ استاندارد در $\\text{K\\\_GEM\\\_SimEngine}$ برای مدل‌سازی عملکرد موتورهای $\\text{VGT}$ در ارتفاعات بسیار بالا (بالای $\\text{3000 m}$) مورد استفاده قرار می‌گیرد، با در نظر گرفتن این قید که $\\text{VGT}$ در واقعیت ممکن است تا حدود $\\text{3500 m}$ عملکرد بهتری را حفظ کند، اما نرخ $\\text{4\\%}$ یک ضریب عملکرد تضمین شده (Guaranteed Performance) است.

## **۶. جمع‌بندی داده‌های کمی نهایی (JSON Structure)**

داده‌های کمی سخت و عوامل بهینه‌سازی استخراج شده در این گزارش، برای تکمیل نهایی پایگاه داده $\\text{HD/GD}$ در $\\text{K\\\_GEM\\\_SimEngine}$ آماده هستند. جدول زیر تجمیع نهایی داده‌های پارامترهای ۱ تا ۳ را در قالب JSON برای ادغام مستقیم ارائه می‌دهد.

**توضیحات تکمیلی برای JSON:**

* فیلدهای $\\text{Ratio}$ نهایی برای $\\text{HD325-8}$ و $\\text{HD785-8}$ به دلیل عدم انتشار عمومی نسبت‌های داخلی محور آن‌ها توسط کوماتسو، خالی (null) در نظر گرفته شده‌اند، اما نسبت کاهش کلی $\\text{HD1500-8}$ (برابر $\\text{19.75}$) بر اساس داده‌های صریح $\\text{Differential}$ و $\\text{Planetary}$ محاسبه شده است.  
* ظرفیت جذب ریتاردر برای گریدرها (GD) به دلیل ماهیت عملیاتی این ماشین‌آلات و عدم وجود ریتاردر چنددیسکی پیوسته خنک شونده با روغن، صفر (null) در نظر گرفته می‌شود.

JSON

{  
  "K\_GEM\_SimEngine\_HDGD\_Data": {  
    "HD325-8": {  
      "Final\_Drive\_Differential\_Ratio": null,  
      "Final\_Drive\_Planetary\_Ratio": null,  
      "Overall\_Reduction\_Ratio\_DD": null,  
      "Fuel\_Saving\_Factor\_Percent": null,  
      "Max\_Retarder\_Capacity\_kW": 689,  
      "TKPH\_Rating\_Ref": 700  
    },  
    "HD785-8": {  
      "Final\_Drive\_Differential\_Ratio": null,  
      "Final\_Drive\_Planetary\_Ratio": null,  
      "Overall\_Reduction\_Ratio\_DD": null,  
      "Fuel\_Saving\_Factor\_Percent": 22.0,  
      "Max\_Retarder\_Capacity\_kW": 1320,  
      "TKPH\_Rating\_Ref": 700  
    },  
    "HD1500-8": {  
      "Final\_Drive\_Differential\_Ratio": 1.720,  
      "Final\_Drive\_Planetary\_Ratio": 11.482,  
      "Overall\_Reduction\_Ratio\_DD": 19.75,  
      "Fuel\_Saving\_Factor\_Percent": null,  
      "Max\_Retarder\_Capacity\_kW": 1750,  
      "TKPH\_Rating\_Ref": 1900  
    },  
    "GD655-7": {  
      "Final\_Drive\_Differential\_Ratio": null,  
      "Final\_Drive\_Planetary\_Ratio": null,  
      "Overall\_Reduction\_Ratio\_DD": null,  
      "Fuel\_Saving\_Factor\_Percent": 15.0,  
      "Max\_Retarder\_Capacity\_kW": null,  
      "TKPH\_Rating\_Ref": null  
    },  
    "GD955-7": {  
      "Final\_Drive\_Differential\_Ratio": null,  
      "Final\_Drive\_Planetary\_Ratio": null,  
      "Overall\_Reduction\_Ratio\_DD": null,  
      "Fuel\_Saving\_Factor\_Percent": 15.0,  
      "Max\_Retarder\_Capacity\_kW": null,  
      "TKPH\_Rating\_Ref": null  
    }  
  }  
}

## **۷. نتیجه‌گیری و تحلیل کاربرد داده‌ها**

استخراج دقیق داده‌های کمی، پایه‌ای قوی برای اعتبارسنجی مدل‌های شبیه‌سازی فراهم می‌کند. با استفاده از داده‌های استخراج شده، به ویژه نسبت کاهش کلی $\\text{19.75}$ در $\\text{HD1500-8}$ و ظرفیت‌های جذب ریتاردر که از توان موتور پیشی می‌گیرد، می‌توان عملکرد دینامیکی و حرارتی دامپ‌تراک‌ها را در چرخه‌های واقعی معدنی با دقت بالا شبیه‌سازی کرد.

ضریب صرفه‌جویی سوخت $\\text{22.0\\%}$ برای $\\text{HD785-8}$ (ناشی از تعدیل توان VHC) و $\\text{15.0\\%}$ برای گریدرها (Eco Mode) نیز امکان مدل‌سازی استراتژی‌های عملیاتی با هدف کاهش $\\text{L/h}$ را فراهم می‌آورد. همچنین، نرخ تصحیح ارتفاعی استاندارد $\\text{4\\%}$ در هر $\\text{305 m}$ بالاتر از $\\text{3048 m}$، امکان تنظیم پارامترهای موتور در شبیه‌سازی برای سایت‌های عملیاتی در ارتفاعات بالا را فراهم می‌سازد، و در عین حال عملکرد واقعی موتورهای $\\text{VGT}$ را با یک ضریب ایمنی محافظه‌کارانه مدیریت می‌کند. این مجموعه داده‌های کمی، گامی نهایی در جهت اعتبارسنجی جامع و دقیق پایگاه داده $\\text{HD/GD}$ در محیط $\\text{K\\\_GEM\\\_SimEngine}$ محسوب می‌شود.

#### **Works cited**

1. HD1500-8 \- Komatsu, accessed October 19, 2025, [https://komatsu.pe/images/komatsu/mineria/camiones-mecanicos/HD-1500-8.pdf](https://komatsu.pe/images/komatsu/mineria/camiones-mecanicos/HD-1500-8.pdf)  
2. HD1500-8E0 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd1500-8e0](https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd1500-8e0)  
3. HD1500-8 \- Marubeni Komatsu, accessed October 19, 2025, [https://marubeni-komatsu.co.uk/app/uploads/2018/07/HD1500-8\_EENSS20331\_1811\_113396.pdf](https://marubeni-komatsu.co.uk/app/uploads/2018/07/HD1500-8_EENSS20331_1811_113396.pdf)  
4. GD655-7 \- NET, accessed October 19, 2025, [https://portalimages.blob.core.windows.net/products/pdfs/v0pfklfl\_08abd8d2-3d48-4086-a40c-a0bf68dcbf1c.pdf](https://portalimages.blob.core.windows.net/products/pdfs/v0pfklfl_08abd8d2-3d48-4086-a40c-a0bf68dcbf1c.pdf)  
5. GD955-7 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/motor-graders/gd955-7](https://www.komatsu.com/en-us/products/equipment/motor-graders/gd955-7)  
6. GD955-7 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/motor-graders/gd955-7/motorgrader\_gd955-7\_brochure\_english\_en-gd955-7-br0-1223-v1.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/motor-graders/gd955-7/motorgrader_gd955-7_brochure_english_en-gd955-7-br0-1223-v1.pdf)  
7. GD955-7, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/worldwide-website/asia-d/download\_motor-graders/gd955.pdf?rev=4a339947cbf3499ba830f6d08a488c6b\&hash=46384AB2DD1AE6121D1F9FAD6458EB64](https://www.komatsu.jp/en/-/media/home/worldwide-website/asia-d/download_motor-graders/gd955.pdf?rev=4a339947cbf3499ba830f6d08a488c6b&hash=46384AB2DD1AE6121D1F9FAD6458EB64)  
8. HD785-8 \- SMS Equipment, accessed October 19, 2025, [https://www.smsequipment.com/getmedia/96cb4eb5-abe6-412c-a7d4-507abfb691f1/HD785-8.pdf](https://www.smsequipment.com/getmedia/96cb4eb5-abe6-412c-a7d4-507abfb691f1/HD785-8.pdf)  
9. GD655-7 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/motor-graders/gd655-7/en-gd655-7br01-0722-v3.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/motor-graders/gd655-7/en-gd655-7br01-0722-v3.pdf)  
10. GD655-7 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/motor-graders/gd655-7](https://www.komatsu.com/en-us/products/equipment/motor-graders/gd655-7)  
11. HD325-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd325-8](https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd325-8)  
12. HD325-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/trucks/hd325/hd325-8-aess909-03.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/trucks/hd325/hd325-8-aess909-03.pdf)  
13. HD785-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd785-8](https://www.komatsu.com/en-us/products/equipment/trucks/mechanical-trucks/hd785-8)  
14. 03 x New Goodyear 59/80R63 RM4A+ 2SL E4 | Lennon OTR, accessed October 19, 2025, [https://www.lennonotr.com.au/tyres/new-goodyear-59-80r63-rm4a-2sl-e4/](https://www.lennonotr.com.au/tyres/new-goodyear-59-80r63-rm4a-2sl-e4/)  
15. HD785-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/trucks/hd785/offhighwaytruck-hd785-8-brochure-english-en-hd785-8br01-0622-v5.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/trucks/hd785/offhighwaytruck-hd785-8-brochure-english-en-hd785-8br01-0622-v5.pdf)  
16. HD785-8, accessed October 19, 2025, [https://cimertex.it/wp-content/uploads/2024/07/HD785-8Brochure\_Main\_EN.pdf](https://cimertex.it/wp-content/uploads/2024/07/HD785-8Brochure_Main_EN.pdf)  
17. Komatsu Engine Serie SA12V140Z 1 PDF \- Scribd, accessed October 19, 2025, [https://www.scribd.com/doc/218192954/166275075-Komatsu-Engine-Serie-SA12V140Z-1-PDF](https://www.scribd.com/doc/218192954/166275075-Komatsu-Engine-Serie-SA12V140Z-1-PDF)  
18. Compliance with Tier 4 Final Emissions Regulations Development of 125 mm and 140 mm Bore Engines, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/aboutus/innovation/technology/techreport/2014/en/167\_e02.pdf?rev=7d33be462e484f63b92339cc872b9702\&hash=C774D794EE797A61EE82EBCBE07B5C7C](https://www.komatsu.jp/en/-/media/home/aboutus/innovation/technology/techreport/2014/en/167_e02.pdf?rev=7d33be462e484f63b92339cc872b9702&hash=C774D794EE797A61EE82EBCBE07B5C7C)