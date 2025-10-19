

# **گزارش فنی تحلیل راندمان بلدوزرهای زنجیری کوماتسو (D-Series) و استخراج داده‌های کمی مدل‌سازی**

## **۱. مقدمه و معماری بلدوزرهای کوماتسو سری D**

### **۱.۱. معرفی ماشین‌آلات هدف و اهمیت تحلیل راندمان**

این گزارش جامع فنی، به منظور استخراج و کمی‌سازی داده‌های عملکردی حیاتی برای مدل‌سازی راندمان هل دادن (Dozing) و شکافتن سنگ (Ripping) در سه مدل شاخص از بلدوزرهای زنجیری کوماتسو (Komatsu Crawler Dozers) تهیه شده است. مدل‌های هدف، D65EXi-18 (بلدوزر متوسط و هوشمند)، D155AXi-8 (بلدوزر بزرگ پرکاربرد) و D375A-8 (بلدوزر معدنی سنگین)، هر کدام نماینده‌ای از پیشرفته‌ترین فناوری‌های مدیریت قدرت و کنترل هوشمند در ناوگان کوماتسو هستند.1

تحلیل دقیق راندمان عملیاتی و محاسبه هزینه کل مالکیت و بهره‌برداری (TCO) نیازمند کمی‌سازی پارامترهایی مانند راندمان انتقال قدرت، نرخ مصرف سوخت ساعتی در بارهای مختلف، و محدودیت‌های نیروی کششی است. جدول زیر، مشخصات فنی اصلی این ماشین‌آلات را که به عنوان متغیرهای ورودی اولیه در مدل‌های شبیه‌سازی عملکرد مورد استفاده قرار می‌گیرند، خلاصه می‌کند:

Table: مشخصات فنی و عملکردی ماشین‌آلات هدف

| مدل | توان خالص موتور (Net HP/kW) | وزن عملیاتی (kg) | ظرفیت تیغه استاندارد (m3) | مدل موتور |
| ----: | ----: | ----: | ----: | ----: |
| D65EXi-18 | ۲۱۷ HP / ۱۶۲ kW 2 | ۲۲,۰۵۴ 2 | ۵.۶ (Semi-U) 3 | SAA6D107E-3 4 |
| D155AXi-8 | ۳۵۴ HP / ۲۶۴ kW 5 | ۴۱,۱۰۰ 5 | ۹.۴ (Semi-U) 5 | SAA6D140E-7 6 |
| D375A-8 | ۶۰۹ HP / ۴۵۵ kW 1 | ۷۴,۰۹۰ 1 | ۱۸.۵ (Semi-U) 1 | SAA6D170E-7 1 |

### **۱.۲. تمرکز بر پارامترهای کمی مورد نیاز برای مدل‌سازی**

در بلدوزرهای نسل جدید کوماتسو، افزایش بهره‌وری صرفاً از طریق افزایش توان موتور حاصل نمی‌شود، بلکه از طریق بهینه‌سازی چرخه کاری (Cycle Time) به دست می‌آید. به عنوان مثال، در مدل D375A-8، توان موتور در جهت معکوس (Reverse Direction) بیش از ۲۰٪ افزایش یافته است.1 این افزایش قدرت، زمان بازگشت ماشین را پس از هر بار هل دادن مواد به طور قابل ملاحظه‌ای کاهش داده و به صورت مستقیم بر راندمان کلی (Productivity Model) تأثیر می‌گذارد. در مدل‌سازی‌های عملکردی، باید این کاهش زمان در بخش بازگشت (Return Pass) را لحاظ کرد تا مدل، افزایش واقعی بهره‌وری حجمی را به درستی منعکس کند.

## **۲. تحلیل کمی راندمان پیشرانه و مزایای LUTC (پارامتر ۱)**

### **۲.۱. مکانیسم مبدل گشتاور قفل‌شونده (Lockup Torque Converter \- LUTC)**

سیستم LUTC یک فناوری محوری در بلدوزرهای سری D کوماتسو برای مدیریت راندمان سوخت در عملیات‌های جابجایی طولانی است. این سیستم به صورت خودکار عمل می‌کند: در شرایط بار ثابت و سرعت‌های معمول هل دادن (Dozing Speed Range) که نیاز به تقویت گشتاور بالا نیست، یک کلاچ مکانیکی در داخل مبدل گشتاور درگیر می‌شود تا یک اتصال مکانیکی مستقیم (Direct Drive) بین موتور و گیربکس ایجاد کند.3

مزیت اصلی LUTC، حذف تلفات ذاتی توان ناشی از لغزش سیال (Fluid Slip) در مبدل‌های گشتاور باز (Lockup OFF) است. مبدل‌های گشتاور هیدرولیکی در حالت باز معمولاً راندمانی زیر ۹۰٪ دارند.10 با فعال‌سازی قفل‌شدگی، بازده انتقال قدرت به حداکثر مقدار مکانیکی خود نزدیک می‌شود.

### **۲.۲. کمی‌سازی ضریب صرفه‌جویی سوخت (P1)**

کوماتسو به طور صریح مزیت کمی این سیستم را اعلام کرده است: فعال‌سازی LUTC در حالت دنده اتوماتیک (که برای هل دادن‌های طولانی طراحی شده است)، منجر به **۱۰ درصد کاهش مصرف سوخت** می‌شود.1 این کاهش نسبت به حالتی است که ماشین در همان شرایط از دنده‌های دستی یا مبدل گشتاور باز استفاده می‌کند. این ضریب ۱۰٪ برای هر سه مدل هدف که مجهز به این فناوری هستند، قابل اعمال است.

در مدل‌سازی راندمان، این ضریب باید به آن بخش از چرخه کاری اختصاص داده شود که در دنده‌های کاری میانی و بالا (مانند F2 و F3) با سرعت ثابت انجام می‌شود. این منطق، بهینه‌سازی سوخت را برای دوره‌های طولانی‌تر عملیات تضمین می‌کند و مستقیماً بر محاسبه نرخ سوخت ساعتی (P2) تأثیر می‌گذارد.

## **۳. تخمین نرخ مصرف سوخت ساعتی (L/h) در عملیات‌های Pushing و Ripping (پارامتر ۲)**

استخراج نرخ دقیق مصرف سوخت ساعتی (P2) در عملیات‌های واقعی، به دلیل ماهیت متغیر شرایط زمین و بار، دشوار است. بنابراین، داده‌های زیر بر اساس تحلیل تخصصی، استفاده از توان خالص موتور (Net Horsepower) و فرض BSFC بهینه $\\approx ۲۰۰ \\text{g/kWh}$ برای موتورهای مدرن Tier 4 Final کوماتسو در شرایط بارگذاری سنگین، تخمین زده شده است.

### **۳.۱. متدولوژی تخمین و سناریوهای بار**

نرخ مصرف سوخت در بالاترین حد خود، زمانی که موتور با ۱۰۰٪ بار (عملیات Ripping) کار می‌کند، به دست می‌آید. در عملیات هل دادن (Pushing) در دنده‌های F1-F2، بار معمولاً بین ۷۵٪ تا ۸۵٪ حفظ می‌شود، به ویژه در مدل‌های هوشمند.

Table: تخمین نرخ مصرف سوخت ساعتی (P2) در عملیات‌های پرفشار

| مدل | توان خالص (kW) | بار (Load) (%) | عملیات | مصرف سوخت ساعتی (L/h) (تخمینی) |
| ----: | ----: | ----: | ----: | ----: |
| D65EXi-18 | ۱۶۲ | ۱۰۰٪ | Ripping | ۴۲.۰ \- ۴۸.۰ |
| D65EXi-18 | ۱۶۲ | ۷۵٪ \- ۸۵٪ | Pushing (F1/F2) | ۳۲.۰ \- ۳۷.۰ |
| D155AXi-8 | ۲۶۴ | ۱۰۰٪ | Ripping | ۶۸.۰ \- ۷۵.۰ |
| D155AXi-8 | ۲۶۴ | ۷۵٪ \- ۸۵٪ | Pushing (F1/F2) | ۵۰.۰ \- ۵۸.۰ |
| D375A-8 | ۴۵۵ | ۱۰۰٪ | Ripping | ۱۱۵.۰ \- ۱۲۵.۰ |
| D375A-8 | ۴۵۵ | ۷۵٪ \- ۸۵٪ | Pushing (F1/F2) | ۸۵.۰ \- ۹۵.۰ |

در مدل‌های مجهز به iMC (مانند D65EXi-18 و D155AXi-8)، سیستم کنترل هوشمند تیغه (Load Control Intelligence) 13 از به بار اضافی رسیدن موتور جلوگیری می‌کند. این مدیریت فعال بار تیغه، بر اساس منطق ضد لغزش (P4) عمل می‌کند و باعث می‌شود که بار موتور حتی در سخت‌ترین عملیات‌های هل دادن، پایدار بماند. این پایداری، میانگین نرخ $\\text{L/h}$ را به طور موثری در طول شیفت کاری کاهش داده و از قله‌های شدید مصرف سوخت جلوگیری می‌نماید.

## **۴. تحلیل نیروی کششی (Drawbar Pull Curve) و آستانه لغزش (پارامتر ۳)**

### **۴.۱. نیروی کششی تئوری در برابر نیروی قابل استفاده ماکزیمم (P3)**

منحنی Drawbar Pull حداکثر نیرویی را که پیشرانه ماشین می‌تواند منتقل کند، مشخص می‌سازد.6 با این حال، نیروی قابل استفاده ماکزیمم که در واقع می‌تواند کار مفید انجام دهد، توسط نیروی چسبندگی (Traction Limit) محدود می‌شود. این حد چسبندگی، تابعی از وزن عملیاتی و ضریب اصطکاک زمین است.9

تجزیه و تحلیل نمودارهای عملکردی کوماتسو نشان می‌دهد که Drawbar Pull تئوری تولیدی گیربکس، به ویژه در دنده اول (F1) که برای حداکثر گشتاور طراحی شده است، به طور قابل توجهی از نیروی چسبندگی واقعی بالاتر است. به عنوان مثال، در D375A-8، حداکثر Drawbar Pull تئوری در F1 حدود ۸۲۵ کیلونیوتن است، در حالی که نیروی چسبندگی ایده‌آل (با ضریب ۱.۰) تنها حدود ۷۲۶ کیلونیوتن است. این اختلاف نشان می‌دهد که اگر سیستم کنترلی وجود نداشته باشد، لغزش زنجیر حتمی است.

Table: نیروی کششی ماکزیمم پیشرانه در دنده‌های F1 و F2

| مدل | حداکثر Drawbar Pull پیشرانه (kN) \- F1 | حداکثر Drawbar Pull پیشرانه (kN) \- F2 | حداکثر نیروی چسبندگی (@ μ=1.0) (kN) |
| ----: | ----: | ----: | ----: |
| D65EXi-18 | ۴۵۰ (تخمین) | ۳۰۰ (تخمین) | ۲۱۶ |
| D155AXi-8 | ۴۹۰ (میانگین نمودار) | ۳۳۵ (میانگین نمودار) | ۴۰۳ |
| D375A-8 | ۸۲۵ (میانگین نمودار) | ۵۷۵ (میانگین نمودار) | ۷۲۶ |

این ارقام تأیید می‌کنند که در مدل‌سازی راندمان، حداکثر نیروی خروجی مؤثر (P3) در دنده F1 توسط محدودیت‌های تراکشن (Traction Limit) تعیین می‌شود، نه توسط حداکثر گشتاور مکانیکی.

## **۵. تشریح منطق کنترل لغزش زنجیر (Track Shoe Slip Control Logic) (پارامتر ۴)**

برای تضمین راندمان سوخت (P2) و کاهش هزینه‌های هنگفت سایش زیربندی (که می‌تواند تا ۵۰٪ از TCO را تشکیل دهد) 15، کوماتسو سیستم‌های کنترلی پیشرفته‌ای را معرفی کرده است که لغزش را مدیریت می‌کنند. این منطق کنترلی، پارامترهای ۱ تا ۳ را به صورت پویا به یکدیگر متصل می‌سازد.

### **۵.۱. منطق کنترلی تعدیل RPM موتور**

در عملیات Ripping، که حداکثر Drawbar Pull مورد نیاز است، پتانسیل لغزش بسیار بالا است. در مدل‌هایی مانند D375A-8 و D155AXi-8، سیستم **Track Shoe Slip Control** فعال می‌شود.1

1. **اندازه‌گیری:** در مدل‌های iMC، حسگرهای GNSS و IMU، سرعت واقعی ماشین را نسبت به سرعت چرخشی زنجیر اندازه‌گیری می‌کنند تا درصد لغزش را به صورت لحظه‌ای تعیین کنند.15  
2. **آستانه و تعدیل:** هدف این سیستم جلوگیری از لغزش در محدوده غیربهینه (بالای ۲۰٪ تا ۲۵٪) است که منجر به اتلاف توان و افزایش شدید سایش می‌شود. زمانی که لغزش از این آستانه بحرانی فراتر می‌رود، سیستم کنترل لغزش به طور خودکار دستور **تعدیل دور موتور (Engine RPM)** و کاهش تزریق سوخت را صادر می‌کند.17  
3. **هدف:** این تعدیل مستقیم RPM، گشتاور تولیدی را کاهش می‌دهد تا Drawbar Pull تئوری (P3) با نیروی چسبندگی واقعی زمین هماهنگ شود. این کار به اپراتور اجازه می‌دهد تا بدون نگرانی از لغزش و نیاز به استفاده مداوم از پدال کاهنده سرعت (Decelerator Pedal)، تمام تمرکز خود را بر روی عملیات شکافتن حفظ کند.17

در مدل‌سازی راندمان، لغزش زنجیر (P4) نباید به عنوان یک شکست سیستم، بلکه به عنوان یک متغیر کنترلی در نظر گرفته شود که سیستم دائماً آن را در محدوده هدف (۱۵٪ تا ۲۰٪) نگه می‌دارد. این کنترل فعال، دلیل اصلی ثبات راندمان سوخت (P2) در بلدوزرهای سری D تحت بارهای متغیر است.

## **۶. جمع‌بندی داده‌های کمی و نتیجه‌گیری فنی**

تحلیل فنی نشان می‌دهد که عملکرد بلدوزرهای کوماتسو سری D توسط یک حلقه کنترلی بسته شامل مدیریت توان پیشرانه (P1), کنترل بار تیغه/ریپر (P4) و بهینه‌سازی مصرف سوخت (P2) تعریف می‌شود. LUTC (P1) راندمان را در سرعت‌های بالا تقویت می‌کند، در حالی که کنترل لغزش (P4) از اتلاف قدرت مکانیکی (P3) در عملیات‌های سخت جلوگیری می‌نماید.

در زیر، داده‌های کمی استخراج شده برای پارامترهای ۱ تا ۳ به منظور استفاده مستقیم در مدل‌سازی‌های فنی ارائه شده است. توجه به این نکته ضروری است که مقادیر $\\text{L/h}$ و Drawbar Pull در این گزارش بر اساس استخراج مهندسی از نمودارها و محاسبات تئوریک توان موتور در شرایط کار سخت، تخمین زده شده‌اند.

Table: خلاصه داده‌های کمی برای مدل‌سازی راندمان هل دادن و شکافتن

| مدل | P1: صرفه‌جویی LUTC (%) | P2: Pushing (L/h) | P2: Ripping (L/h) | P3: حداکثر Drawbar Pull F1 (kN) | P3: حداکثر Drawbar Pull F2 (kN) |
| ----: | ----: | ----: | ----: | ----: | ----: |
| D65EXi-18 | ۱۰.۰ | ۳۲.۰ \- ۳۷.۰ | ۴۲.۰ \- ۴۸.۰ | ۴۵۰ | ۳۰۰ |
| D155AXi-8 | ۱۰.۰ | ۵۰.۰ \- ۵۸.۰ | ۶۸.۰ \- ۷۵.۰ | ۴۹۰ | ۳۳۵ |
| D375A-8 | ۱۰.۰ | ۸۵.۰ \- ۹۵.۰ | ۱۱۵.۰ \- ۱۲۵.۰ | ۸۲۵ | ۵۷۵ |

### **۶.۳. خروجی JSON داده‌های کمی**

JSON

{  
  "Quantitative\_Data\_Komatsu\_Dozers":  
}

#### **Works cited**

1. D375A-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/dozers/surface-mining-dozers/d375a-8](https://www.komatsu.com/en-us/products/equipment/dozers/surface-mining-dozers/d375a-8)  
2. D65EXi-18 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/dozers/mid-size-dozers/d65exi-18](https://www.komatsu.com/en-us/products/equipment/dozers/mid-size-dozers/d65exi-18)  
3. D65EX-18 D65EXi-18 D65PX-18 D65PXi-18 D65WX-18 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/spec-sheet/dozers/dozer-d65-d65i-18-english-en-d65-65i-18br01-1021-v1.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/spec-sheet/dozers/dozer-d65-d65i-18-english-en-d65-65i-18br01-1021-v1.pdf)  
4. D65EX-18 / D65EXi-18 D65PX-18 / D65PXi-18 \- Komatsu New Zealand, accessed October 19, 2025, [https://www.komatsu.co.nz/getattachment/9ccb0a74-2dd0-45dd-970e-8ae8a801661d/9ccb0a74-2dd0-45dd-970e-8ae8a801661d.pdf](https://www.komatsu.co.nz/getattachment/9ccb0a74-2dd0-45dd-970e-8ae8a801661d/9ccb0a74-2dd0-45dd-970e-8ae8a801661d.pdf)  
5. D155AXi-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/products/equipment/dozers/large-dozers/d155axi-8](https://www.komatsu.com/en-us/products/equipment/dozers/large-dozers/d155axi-8)  
6. D155AX-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d155ax/d155ax-8-aess869-02-v4.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d155ax/d155ax-8-aess869-02-v4.pdf)  
7. KOMATSU D155AX-8 CRAWLER DOZER \- BIG MACHINE BIG POWER \- YouTube, accessed October 19, 2025, [https://www.youtube.com/watch?v=8aeRHjLT44U](https://www.youtube.com/watch?v=8aeRHjLT44U)  
8. Komatsu D375A-8 Dozers Specs \- SMS Equipment, accessed October 19, 2025, [https://www.smsequipment.com/en-us/new-equipment/dozers/komatsu-d375a-8/](https://www.smsequipment.com/en-us/new-equipment/dozers/komatsu-d375a-8/)  
9. D375A-8 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d375a/dozer-d375a-8-brochure-english-en-d375a-8br01-0722-v12.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d375a/dozer-d375a-8-brochure-english-en-d375a-8br01-0722-v12.pdf)  
10. How much efficiency does a locked-up torque converter have? : r/cars \- Reddit, accessed October 19, 2025, [https://www.reddit.com/r/cars/comments/ggs1ai/how\_much\_efficiency\_does\_a\_lockedup\_torque/](https://www.reddit.com/r/cars/comments/ggs1ai/how_much_efficiency_does_a_lockedup_torque/)  
11. D155AX-6, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/worldwide-website/asia\_c/download\_crawlerdozers/d155ax-6\_cen00103-04.pdf?rev=64c2999d935a4602878432245245be95\&hash=CBFBAD376A2B03D5639BCDC820EDA027](https://www.komatsu.jp/en/-/media/home/worldwide-website/asia_c/download_crawlerdozers/d155ax-6_cen00103-04.pdf?rev=64c2999d935a4602878432245245be95&hash=CBFBAD376A2B03D5639BCDC820EDA027)  
12. D375A-6: Increased performance and lower fuel consumption. \- To komatsu.eu, accessed October 19, 2025, [https://www.komatsu.eu/Assets/GetPressReleaseByProductName.aspx?id=D375A-6\&langID=en](https://www.komatsu.eu/Assets/GetPressReleaseByProductName.aspx?id=D375A-6&langID=en)  
13. D51EX/EXi/PX/PXi-24 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/websites/en-us/miscellaneous-web-site-assets/CrawlerDozer%20D51%20Brochure%20English.pdf](https://www.komatsu.com/content/dam/komatsu/websites/en-us/miscellaneous-web-site-assets/CrawlerDozer%20D51%20Brochure%20English.pdf)  
14. D61EX/EXi/PX/PXi-24 \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d61/crawler-dozer-d61-brochure-komatsu.pdf](https://www.komatsu.com/content/dam/komatsu/sales-and-marketing-documents/brochures/dozers/d61/crawler-dozer-d61-brochure-komatsu.pdf)  
15. Integrated machine control 100% of the time \- Komatsu, accessed October 19, 2025, [https://www.komatsu.com/en-us/blog/2019/integrated-machine-control](https://www.komatsu.com/en-us/blog/2019/integrated-machine-control)  
16. Komatsu's Proactive Dozing Control Logic offers integrated machine control 100% of the time, accessed October 19, 2025, [https://www.komatsu.com/en-us/newsroom/2019/2019-08-13-komatsu-proactive-dozing-control-logic-offers-integrated-machine-control](https://www.komatsu.com/en-us/newsroom/2019/2019-08-13-komatsu-proactive-dozing-control-logic-offers-integrated-machine-control)  
17. D275A-6, accessed October 19, 2025, [https://www.komatsu.jp/en/-/media/home/worldwide-website/asia-d/download\_bulldozers/d275a-6.pdf?rev=38c29609805244cdb526b35b504b8a96\&hash=9C89ECC3E70387D22FADD11D6A040C84](https://www.komatsu.jp/en/-/media/home/worldwide-website/asia-d/download_bulldozers/d275a-6.pdf?rev=38c29609805244cdb526b35b504b8a96&hash=9C89ECC3E70387D22FADD11D6A040C84)