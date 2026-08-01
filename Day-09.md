<div align="center">

# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 09 - Defensible Network Concepts

</div>

## 📌 What will we learn?

In this module, we will learn about:

- What makes a network defensible.
- The types of data monitoring required for security.
- Network-based security monitoring.
- Endpoint and application monitoring.
- Cloud monitoring.
- Monitored data centralization concepts.
- Formatting different data types for centralization.

> **This module discusses one of the most fundamental questions in defensive security:**
>
> **How should a network be monitored to make it defensible?**

---

# ➜ Defensible Network

كلمة **Defensible Network** لا تعني شبكة مستحيل يتم اختراقها، لأننا اتفقنا من قبل أن:

> **Compromise Will Happen**

أي مؤسسة معرضة للاختراق مهما كانت قوية.

لذلك فالمقصود بـ **Defensible Network** هو:

> شبكة تم تصميمها وإدارتها بطريقة تجعلها قادرة على **اكتشاف الهجوم بسرعة، واحتوائه (Containment)، والاستجابة له (Response)، وتقليل تأثيره قبل أن يسبب ضررًا كبيرًا.**

يعني بدل ما يكون الهدف:

> **Prevent Every Attack**

يبقى الهدف الحقيقي هو:

> **Detect → Respond → Contain → Recover**

---

# مراحل بناء Defensible Network

الكتاب يوضح أن أي شبكة تريد أن تصبح **Defensible** يجب أن تمر بعدة مراحل، وكل مرحلة تعتمد على المرحلة التي قبلها.

---

# 1️⃣ Monitoring

أول وأهم خطوة.

السؤال هنا هو:

> **هل أنا شايف فعلاً كل اللي بيحصل داخل الشبكة؟**

بدون Monitoring لا يمكن الدفاع عن أي شبكة، لأنك ببساطة **أعمى** ولا تعرف ماذا يحدث.

لذلك يجب جمع البيانات من مصادر متعددة مثل:

- Network Traffic
- Endpoints
- Firewalls
- Routers
- IDS / IPS
- DNS
- VPN
- Web Servers

ثم يتم إرسال هذه البيانات إلى مكان مركزي، وغالبًا يكون:

> **SIEM**

الكتاب قال جملة مهمة جدًا:

> **Start monitoring first.**

أي قبل شراء أدوات جديدة أو التفكير في حلول متقدمة، ابدأ أولًا بجمع البيانات، لأن بدون البيانات لن تستطيع اكتشاف أي شيء.

---

# 2️⃣ Inventoried

بعد أن بدأت في المراقبة، اسأل نفسك:

> **أنا عندي كام جهاز أصلًا؟**

الكثير من المؤسسات تعتقد أنها تعرف جميع أجهزتها، لكن الواقع غير ذلك.

لذلك يجب وجود:

> **Asset Inventory**

أي قائمة تحتوي على جميع الأصول الموجودة داخل البيئة.

وليس مجرد عدد الأجهزة، بل معلومات مثل:

- اسم الجهاز
- IP Address
- Operating System
- Owner
- Location
- Purpose

لأن أول سؤال أثناء أي Incident سيكون:

> الجهاز ده إيه؟

ولو لم تعرف الإجابة، سيصبح التحقيق أصعب بكثير.

---

# 3️⃣ Controlled

بعد معرفة جميع الأجهزة، يأتي دور التحكم في الاتصالات داخل الشبكة.

السؤال هنا:

> **مين يقدر يكلم مين؟**

قديمًا كان كثير من الشبكات يعمل بطريقة:

> **Any-to-Any Communication**

أي أي جهاز يستطيع التواصل مع أي جهاز.

وده كان يمثل خطورة كبيرة.

أما الآن فيتم تطبيق مبدأ:

> **Least Privilege**

أي كل جهاز يتواصل فقط مع الأجهزة التي يحتاجها فعلاً.

ومن أمثلة ذلك:

### Ingress Filtering

التحكم في الترافيك الداخل إلى الشبكة.

### Egress Filtering

التحكم في الترافيك الخارج من الشبكة.

الفكرة كلها هي التحول من:

> Any-to-Any

إلى

> Only Necessary Connections

---

# 4️⃣ Claimed (Ownership)

كل جهاز داخل الشبكة يجب أن يكون له:

> **Owner**

أي شخص أو فريق مسؤول عنه.

فمثلًا لو ظهر Malware على Server معين، يجب أن أعرف:

- مين المسؤول عن السيرفر؟
- هل ينفع أعزله؟
- هل ينفع أقفله؟
- هل سيؤثر على Business؟

ولو لم يكن هناك Owner واضح، ستكون الاستجابة للحوادث أبطأ بكثير.

ولذلك يجب أيضًا أن يكون لكل Asset:

- Policies
- Procedures
- Recovery Plan

الكتاب يؤكد على نقطة مهمة جدًا:

> **Incident Response مستحيل ينجح لو معرفتش مين صاحب الجهاز.**

---

# 5️⃣ Minimized (Attack Surface)

الـ **Attack Surface** هو كل نقطة يمكن أن يستغلها المهاجم للدخول إلى الشبكة.

مثل:

- Open Ports
- Running Services
- User Accounts
- Applications
- Exposed Systems
- Misconfigurations

والمطلوب هو:

> **تقليل Attack Surface قدر الإمكان.**

مثال:

بدل وجود 50 Port مفتوح...

أفتح فقط الـ Ports المطلوبة.

كذلك:

- إزالة الخدمات غير المستخدمة.
- تطبيق Least Privilege.
- حذف الحسابات غير الضرورية.
- تعطيل البروتوكولات القديمة.
- تقليل الصلاحيات الزائدة.

كل ذلك يجعل عملية الاختراق أصعب بكثير.

---

# 6️⃣ Assessed

بعد تقليل المخاطر، يجب أن أسأل:

> **هل الدفاعات التي بنيتها تعمل فعلًا؟**

ويكون ذلك عن طريق:

- Vulnerability Assessment
- Penetration Testing
- Red Team Exercises

فنبحث عن:

- هل ما زالت توجد ثغرات؟
- هل أدوات الـ Detection تعمل؟
- هل سيتم اكتشاف المهاجم؟

الكتاب يوضح أن:

> **Assessment يجيب على سؤال: هل كل اللي عملناه جاب نتيجة فعلًا؟**

---

# 7️⃣ Current

حتى لو كانت البيئة ممتازة اليوم...

ستظهر غدًا Vulnerabilities جديدة.

لذلك يجب الاهتمام بـ:

> **Patch Management**

أي تثبيت التحديثات الأمنية لمعالجة الثغرات المعروفة.

لكن الكتاب يوضح نقطة مهمة جدًا:

**لماذا جاءت Current في النهاية؟**

لأن تحديث الأنظمة قد يسبب مشاكل أو يكسر بعض التطبيقات، خاصة في بيئات الـ Production.

لذلك يجب أولًا فهم البيئة بالكامل، ومعرفة الأصول والاعتماديات (Dependencies)، ثم تنفيذ التحديثات بطريقة مدروسة.

---

# 8️⃣ Measured (Measurement)

آخر خطوة، وهي خطوة كثير من الناس تنساها.

السؤال هنا:

> **إزاي أعرف إن الشبكة أصبحت أفضل؟**

الإجابة:

لازم أقيس.

مثلًا أقيس:

- عدد الـ Vulnerabilities قبل وبعد الإصلاح.
- Mean Time To Detect (MTTD)
- Mean Time To Respond (MTTR)
- عدد الـ Incidents.
- نسبة الـ False Positives.
- نسبة الأجهزة المحدثة.

بدون Measurement لن تعرف:

- هل تحسن مستوى الأمان؟
- هل الـ Detection أصبح أسرع؟
- هل إجراءات الـ Response أصبحت أفضل؟

وهنا تتكون دائرة التحسين المستمر:

> **Measure → Discover Weaknesses → Improve → Measure Again → Improve More**

وهي ما يسمى:

> **Feedback Loop**

---

# ترتيب المراحل مهم جدًا

الكتاب يؤكد أن ترتيب هذه المراحل ليس عشوائيًا.

فلا يمكن مثلًا أن تبدأ بعمل Patch Management بينما لا تعرف أصلًا الأجهزة الموجودة عندك.

ولا يمكن تنفيذ Incident Response بشكل جيد إذا كنت لا تعرف Owner لكل جهاز.

كل مرحلة تبني الأساس للمرحلة التالية.

---

# محور الموديول

في نهاية الجزء، يقول الكتاب:

> **Throughout this module we will focus on Monitoring.**

أي أن بقية الموديول سيركز بالكامل تقريبًا على أول مرحلة، لأنها أساس عمل الـ SOC.

كما يذكر أيضًا:

> **Understanding your data collection and monitoring system is the first part of orienting yourself in a SOC.**

أي أن أول شيء يجب أن يتعلمه محلل الـ SOC هو:

- البيانات دي بتيجي منين؟
- مين اللي بيجمعها؟
- بتتخزن فين؟
- شكلها عامل إزاي؟

ثم يقول:

> **Once you understand what data is collected, how it is collected, and where it comes from, you will intuitively know what sources you must consult to answer any given analysis question.**

أي بمجرد أن تفهم:

- **What data is collected** → ما هي البيانات التي يتم جمعها؟
- **How it is collected** → كيف يتم جمعها؟ (Logs، Agent، Packet Capture...)
- **Where it comes from** → ما هو مصدرها؟ (Firewall، Windows، DNS، EDR...)

ستعرف بشكل طبيعي:

> لو وصلك Alert أو Incident، أي Logs يجب أن تفتحها؟ ومن أين تبدأ التحقيق؟

وهنا يظهر الفرق الحقيقي بين:

### Junior Analyst

يضيع وقتًا طويلًا في البحث عن مصدر البيانات المناسب.

### Experienced Analyst

يعرف فورًا أي مصدر بيانات يحتوي على الإجابة، فيبدأ التحقيق بسرعة وكفاءة.

---

# 📝 ملخص السلايد

الفكرة الأساسية هي أن الشبكة لا تصبح **Defensible** بمجرد تركيب أدوات أمنية، بل يجب أن تمر بمجموعة من المراحل المترابطة تبدأ بـ **Monitoring** لجمع البيانات، ثم **Inventoried** لمعرفة جميع الأصول، ثم **Controlled** للتحكم في الاتصالات، ثم **Claimed (Ownership)** لتحديد المسؤول عن كل أصل، ثم **Minimized** لتقليل سطح الهجوم، ثم **Assessed** لاختبار فعالية الدفاعات، ثم **Current** للحفاظ على الأنظمة محدثة ومعالجة الثغرات، وأخيرًا **Measured** لقياس الأداء والتحسين المستمر.

هذه المراحل مجتمعة تمنح الـ **Blue Team** القدرة على اكتشاف الهجمات بسرعة، والاستجابة لها، واحتوائها، وتقليل تأثيرها، وهو الهدف الحقيقي لأي **SOC** ناجح.

> **💡 أهم رسالة في هذا الموديول:**
>
> الدفاع الحقيقي لا يبدأ بشراء أدوات جديدة، بل يبدأ بفهم بياناتك، ومعرفة مصادرها، ومراقبتها بشكل صحيح، لأنك لا تستطيع حماية شيء لا تستطيع رؤيته.
