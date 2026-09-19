# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 40 -Part2 — Threat Intelligence Platform Requirements

الصفحة دي مش بس بتقول أنا محتاجة TIP لا، وكمان أنا هحتاجه **بإمكانيات قد إيه؟**

يعني بعد ما عرفنا الـ TIP جه الوقت إني أحدد أنا عايزاه بإمكانيات قد إيه على حسب طبيعة شغله، يعني هنحدد الـ **Requirements**.

---

# أول سؤال: Indicators ولا Low-level Configuration Details؟

هنا الكتاب بيسألني هل أنا هخزن الـ Indicator وخلاص، ولا هخزن كمان تفاصيل تقنية عميقة شوية عن الـ Threats.

وده فرق مهم طبعًا لأن كل واحد ليه إمكانيات معينة.

---

# 1️⃣ لو احتياجك مجرد Indicators

معظم الـ TIPs تقدر تتعامل بسهولة مع حاجات زي:

```text
IP Address
Domain
URL
Hash
Filename
```

مثلًا:

```text
IP: 1.2.3.4

Domain: evil.com

SHA256:
abc123...

URL:
evil.com/malware.exe

Filename:
malware.exe
```

دي حاجات **standard / common indicators**.

---

# 2️⃣ Easy Bulk Entry

الكتاب بيقول إن من الـ important features:

> easy bulk entry and integration

يعني لو عندي مثلًا:

```text
10,000 IPs
5,000 domains
20,000 hashes
```

مش منطقي أدخلهم واحد واحد.

لازم الـ TIP يدعم **Bulk Import**.

مثلًا:

```text
CSV
   ↓
1000 IPs
1000 Domains
500 Hashes
   ↓
TIP
```

وكمان Integration مع tools تانية بحيث البيانات تدخل تلقائيًا.

---

# 3️⃣ لكن الموضوع بيختلف لو عندك Malware Analysis

هنا تبدأ الصفحة تسألك:

> Are you storing malware configurations?

يعني هل إنتِ بس بتخزني:

```text
Hash → abc123
```

ولا بتخزني تفاصيل **Configuration** الخاصة بالـ Malware؟

مثلًا Malware ممكن يكون عنده:

```text
C2 Server
Port
Campaign ID
Mutex
Encryption Key
Persistence
User-Agent
Bot ID
```

فهنا البيانات مش مجرد IOC واحد.

### مثال يوضح الفرق

### TIP بسيط:

```text
Malware.exe
SHA256 = abc123
```

كفاية لو هدفي tracking للـ indicator.

### لكن Malware Analyst ممكن يحتاج:

```text
Malware.exe
│
├── SHA256
├── C2 = evil.com
├── Port = 443
├── Mutex = XYZ
├── Persistence = Scheduled Task
├── Config ID = 12345
├── Campaign = Campaign-X
└── Encryption = ...
```

هنا أنا محتاجة TIP يسمح بتخزين **additional/custom information**.

---

# 4️⃣ Non-standard Fields

دي مرتبطة بالنقطة اللي فوق.

الـ TIP ممكن يكون عنده fields جاهزة:

```text
IP
Domain
Hash
URL
Filename
```

لكن أنا ممكن أحتاج field مش موجود أصلًا.

مثلًا:

```text
Malware Family
Campaign ID
Actor Infrastructure
Mutex
C2 Protocol
Victim ID
```

دي ممكن تكون **custom / non-standard fields**.

فالسؤال هنا:

> هل الـ TIP يسمحلي أضيف fields من عندي؟

لأن بعض الأنظمة مرنة أكثر من غيرها.

---

# 5️⃣ How do you want to correlate across items?

طبعًا مش كفاية إن الـ TIP بتخزن المعلومات.

أنا لازم أسأل نفسي: **أنا عايزة أربط المعلومات دي مع بعض إزاي؟**

مثلًا:

```text
Malware X
   │
   ├── Hash → abc123
   ├── C2 → evil.com
   ├── IP → 1.2.3.4
   ├── Campaign → Campaign-A
   └── TTP → T1053.005
```

أو:

```text
Threat Actor A
      │
      ├── Campaign 1
      │       └── Malware X
      │              └── evil.com
      │
      └── Campaign 2
              └── Malware Y
```

كل ما كان الـ TIP قادر يعمل **Relationships / Correlation** بشكل أفضل، كل ما قدرت أفهم الـ **Threat Picture** بشكل أفضل.

---

# 6️⃣ Is Sharing Required?

السؤال هنا:

**هل محتاجة أشارك الـ Threat Intelligence مع Organizations أو Teams أخرى؟**

مثلًا:

```text
Organization A
       ↓
Malicious IP
       ↓
Share
       ↓
Organization B
```

لو الـ Sharing جزء أساسي من شغلي، يبقى لازم أختار TIP يدعم الموضوع ده كويس.

أما لو الـ TIP للاستخدام الداخلي فقط، فـ Sharing ممكن يكون أقل أهمية.

---

# 7️⃣ What Volume of Indicators?

هنا بيتكلم عن أنا إيه **كم الـ Indicators** اللي محتاجة أخزنه عندي.

لأني في فرق كبير طبعًا بين:

```text
100 indicators
```

و:

```text
1,000,000 indicators
```

لو عندي حجم ضخم، لازم أفكر في:

```text
Storage

Search performance

Import speed

API performance

Database scalability
```

يعني مش بس:

> "هل TIP يقدر يخزن indicators؟"

لكن:

> يقدر يخزن ويبحث في العدد اللي عندي بكفاءة؟

---

# ------------------------------------------------------------------------------------------------

# 🎯 إيه اللي اتعلمناه من الصفحة دي يعني؟

الكتاب بيقول:

> قبل ما أختار TIP، أحدد الأول الـ workflow بتاعي واحتياجاتي.

اسأل نفسك:

```text
1. What am I storing?
        ↓
2. How much am I storing?
        ↓
3. Do I need custom fields?
        ↓
4. How do I correlate items?
        ↓
5. Do I need sharing?
        ↓
6. What tools must integrate with it?
```

وبعدين اختار الـ **TIP المناسب**.

---

# 💡 مثال عملي يثبت الفكرة

تخيل عندي **SOC صغير** واحتياجاتي:

```text
IP
Domain
Hash
URL
```

وعندي:

```text
10,000 indicators
```

ومحتاجة:

```text
SIEM ↔ TIP
```

بس.

فأغلب الـ **TIP solutions** ممكن تحقق احتياجاتك الأساسية.

لكن اتخيل عندي **Threat Intelligence / Malware Analysis Team** بعمل تحليل عميق:

```text
Indicators
+
Malware Configurations
+
Custom Fields
+
Threat Actors
+
Campaigns
+
Complex Relationships
+
Sharing
+
Millions of Indicators
```

هنا لازم أختار TIP أكثر **flexible/scalable** لأن الـ Requirements أعلى.

---

# ⭐ أهم فكرة في الصفحة

الكتاب مش بيقول:

> "اختاري TIP معين."

هو بيقول:

> **Don't choose the platform first. Define your requirements first.**

يعني:

```text
❌ TIP → then figure out what you need

✅ Requirements → then choose TIP
```

---

# 📝 الخلاصة اللي محتاجاها

**TIP Requirements تعتمد على:**

| Requirement       | السؤال                                             |
| ----------------- | -------------------------------------------------- |
| **Indicators**    | IPs, hashes, domains, URLs...؟                     |
| **Bulk Entry**    | عندي كمية كبيرة وعايزة أضيفها بسهولة؟              |
| **Integration**   | محتاجة SIEM/IMS/tools تتكامل معاه؟                 |
| **Custom Fields** | محتاجة أخزن تفاصيل غير الـ standard fields؟        |
| **Correlation**   | عايزة أربط indicators بـ malware/campaigns/actors؟ |
| **Sharing**       | محتاجة أشارك الـ intelligence؟                     |
| **Volume**        | هخزن كام indicator؟                                |

---

# ⭐ وأهم distinction

لو احتياجك مجرد **common IOCs** → أغلب الـ TIPs هتقدر تخدمك.

لو محتاجة **detailed malware analysis + custom fields + complex relationships + sharing + large volume** → لازم تختاري TIP بناءً على الـ **specific workflow والـ requirements** بتاعتك.

---

## 🎯 فلو ده كل احتياجي، غالبًا مش هحتاج TIP معقد جدًا.
