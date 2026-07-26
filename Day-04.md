<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

# 📖 Day 04 - Risk Appetite & Business Alignment

</div>

---

# Finding the Organization's Risk Appetite

**تحديد شهية المؤسسة للمخاطر.**

مقدار المخاطرة التي تقبل المؤسسة تحملها لتحقيق أهدافها.

أو بمعنى تاني:

الشركة مستعدة تتحمل مخاطر قد إيه مقابل إنها تحقق شغلها.

---

## Remember to Consider the Big Picture

معناها إنك كـ **SOC Analyst** مش هتبص للأمن بس، لكن هتبص للصورة كلها.

يعني ليه الشركة موجودة أصلاً؟

> **Organizations don't exist to be secure.**

الشركات مش اتعملت علشان تبقى Secure.

يعني مثلًا:

أمازون اتعملت علشان تبيع المنتجات، مش علشان الأمان.

الأمان وسيلة تساعد الشركة تحقق هدفها، لكنه مش الهدف نفسه.

---

# Where Is Security on the Priority List?

الترتيب بيختلف من شركة للتانية.

### Military / Government

الـ **Security** هنا رقم واحد.

لأن اختراق واحد ممكن يسبب:

- تسريب أسرار دولة.
- تهديد الأمن القومي.

وده يعتبر **Low Risk Appetite**.

---

### New Startup

شركة لسه بتحاول تنجح.

لو صرفت كل ميزانيتها على الـ **Security**، ممكن أصلًا الشركة متكملش.

عشان كده غالبًا بيكون عندها:

**High Risk Appetite.**

---

```text
No Security
      │
      ▼
Reasonable Security
      │
      ▼
Tight Security
```

كل شركة واقفة في مكان مختلف حسب:

- طبيعة شغلها.
- الميزانية.
- حجم المخاطر.

---

> 💡 **Note**

أول سؤال لازم أسأله:

> **Does your organization have a Risk Appetite Statement?**

---

> 💡 **Note**

الـ **Risk Appetite** بيتغير مع الوقت، حسب:

- الإدارة.
- الأولويات.
- طبيعة العمل.

---

## Steering Committee

تفهم أولويات الإدارة.

```text
Management Priorities
          │
          ▼
Risk Appetite
          │
          ▼
Build the Right SOC
```

---

# Meeting the Risk Appetite

## 1) What Is the Worst That Could Happen?

أول سؤال لازم أسأله.

لأن تصميم الـ **SOC** بيختلف من شركة للتانية.

---

## 2) What Type of Work Does Your Organization Do?

الشركة شغالة في إيه؟

وده مهم لأن نوع النشاط هو اللي بيحدد نوع الحماية المطلوبة.

---

## 3) How Critical Is the Success of the Security Team?

قد إيه نجاح الـ **Blue Team** مهم؟

وده مرتبط بالإجابتين اللي قبل كده.

---

# إزاي أختار الـ Security Controls الصح؟

أنواع الشركات غالبًا بتنقسم لنوعين.

---

## 1) Highly Critical

شركة متستحملش الاختراقات.

وغالبًا بنستخدم:

### 1. Application Control

يعني مش أي برنامج يشتغل على الأجهزة.

---

### 2. EDR / XDR

حلول متقدمة لمراقبة الأجهزة واكتشاف والاستجابة للهجمات.

---

### 3. Zero Trust

**Never Trust, Always Verify.**

يعني متثقش في أي مستخدم أو جهاز تلقائيًا.

حتى لو موظف داخل الشركة، كل طلب لازم يتم التحقق منه.

---

### 4. Strict Email Policies

سياسات صارمة للإيميل.

مثلًا:

- فحص الرسائل.
- منع الملفات الخطيرة.
- منع الروابط المشبوهة.

ودي تعتبر **Security Controls** قوية.

---

## 2) Less Critical

الشركة ممكن تتقبل بعض المخاطر.

فمش محتاجة كل التعقيد ده.

وغالبًا تستخدم أدوات أساسية مثل:

- Microsoft Defender

---

> 💡 **Note**

هدفي كـ **Blue Teamer** هو:

> **Find ways to increase security as much as possible without hindering the business.**

يعني أرفع مستوى الحماية من غير ما أعطل شغل الشركة.

---

## Applying All Appropriate Invisible Security

كل إجراءات الحماية اللي المستخدم مش بيحس بيها.

---

## Make Smart Choices When It Comes to Visible Security

لو في إجراءات حماية هيشوفها المستخدم (مثل تغيير كلمات المرور أو استخدام MFA)، لازم أطبقها بطريقة متوازنة من غير ما أعطل شغل الناس.

---

# Risk Appetite Meets Reality

لحد دلوقتي كنا بنقول إن لازم:

1. أعرف الـ **Risk Appetite**.
2. أحط **Security Controls** مناسبة.
3. أبني الـ **Security**.

طيب...

هل ده سهل في الواقع؟

الإجابة: لأ.

لأن الواقع مليان **Constraints**.

---

## Example

تخيل إنك شغال في شركة.

وفي جهاز مسؤول عن تشغيل جزء مهم من خط الإنتاج.

ولو الجهاز وقف...

يبقى ده **Critical Asset**.

---

## Problem 1 — Vendor-Built PC

الجهاز ده مش الشركة هي اللي جمعته.

شركة تانية هي اللي صنعته وسلمته جاهز.

---

## Problem 2 — Qualified Build & Locked Down

الجهاز تم اختباره واعتماده للعمل.

وأي تعديل عليه ممكن:

- يكسر النظام.
- أو يلغي الاعتماد.

يعني مينفعش أنزل:

- EDR
- Antivirus

---

## Problem 3 — No Security Software

مش قادر أنزل:

- Antivirus
- Firewall

على الجهاز.

---

## Problem 4 — Requires FTP

الجهاز محتاج يستخدم **FTP**.

وده بروتوكول قديم، وبياناته غير مشفرة.

---

## Problem 5 — Web Status Page

الجهاز عليه صفحة ويب.

المهندسين بيدخلوا عليها علشان يشوفوا حالة خط الإنتاج.

لكن الـ **Web Server** نفسه ممكن يكون قديم وفيه ثغرات.

---

## Problem 6 — Legacy Windows

الجهاز ممكن يكون شغال بإصدار قديم من **Windows**.

ومبقاش بيوصله:

- Security Updates.
- أو دعم أمني.

---

# How Do You Secure This Machine?

متقولش:

> نغير الجهاز.

لأن ده غالبًا مش حل عملي.

---

الحل هو استخدام:

## Compensating Controls

يعني حلول أمنية تعوض عدم قدرتك على تطبيق الحماية التقليدية.

بدل ما أحمي الجهاز نفسه...

أحمي اللي حواليه.

مثلًا:

- Network Firewall
- غلق الـ Ports غير المستخدمة.
- مراقبة الترافيك.
- Web Application Firewall (WAF) إذا كان مناسبًا للخدمة المقدمة.

---

## الخلاصة

طالما النظام مستقر...

فدوري هو:

**أقلل المخاطر لأقصى درجة ممكنة.**

---

# Risk Acceptance

بعد كل المحاولات دي...

ممكن الشركة تقرر إنها هتكمل بالنظام كما هو.

وده اسمه:

**Risk Acceptance**

يعني الشركة:

- عارفة إن في خطر.
- عارفة تأثيره.
- لكنها قررت تتقبله.

---

الكتاب بيأكد إن:

> **No system is 100% secure.**

مفيش نظام آمن بنسبة 100%.

---

وبرضه بيأكد إن:

> **Cybersecurity is one piece of a complex business pie.**

الأمن السيبراني مجرد جزء من منظومة البزنس.

---

إنت كـ **Security Engineer** أو **SOC Analyst** هتميل إنك تمنع الاختراق.

لكن الإدارة بتفكر في:

- استمرارية العمل.
- الإنتاج.
- الأرباح.
- التكلفة.

---

```text
Business Success

        │

        ▼

Security • Cost • Speed • Profit
```

---

## الخلاصة

**Risk Acceptance** معناها:

- نقلل الخطر قدر الإمكان.
- ونتقبل الجزء المتبقي من الخطر.

لكن قرار قبول المخاطر (**Risk Acceptance**) هو قرار الإدارة (**Management**) وليس قرار فريق الأمن.

ودورك كـ **SOC Analyst** هو توضيح المخاطر وتأثيرها، وليس اتخاذ القرار.
