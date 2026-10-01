بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 43 — Threat Intel Feeds

## Goal

الصفحة دي بتجاوب على سؤال مهم، وهو:

ازاي الـ TIP هتجيب Threat Intel؟ وكمان ازاي أعرف إن الـ Feed اللي باخده منها مفيد ولا لأ؟

---

# أولًا: يعني إيه Threat Intelligence Feed؟

الـ Threat Feed هو مصدر بيبعتلي Threat Information بشكل مستمر، وأحيانًا بشكل Automated.

يعني بدل ما الـ Analyst كل يوم يدور يدويًا على:

* Malicious IPs
* Malicious Domains
* Malicious URLs
* Malware Hashes

الـ Feed ممكن يوصّلهم تلقائيًا.

**الصورة:**

```text
Threat Feed
     ↓
Indicators / Threat Information
     ↓
     TIP
     ↓
SIEM / SOAR / IDS / EDR
     ↓
SOC Analyst
```

فـ الـ Feed يعتبر مصدر Input للـ TIP.

---

# 🎯 Goal of Threat Feeds

**Automated, Relevant, Up-to-date**

## 1️⃣ Automated

يعني زي ما قلنا إن المعلومات توصلي بشكل Automatically بدل ما أنا أجمعها يدويًا بنفسي.

مثلًا:

```text
Feed
 ↓
New malicious IP
 ↓
TIP
 ↓
SIEM
```

بدل:

```text
Analyst
 ↓
Search Google
 ↓
Copy IP
 ↓
Paste into TIP
```

## 2️⃣ Relevant

ودي من أهم الكلمات في الصفحة.

مش معنى إن الـ Feed عنده:

```text
1,000,000 malicious IPs
```

إنه مفيد لك تلقائيًا.

السؤال:

**هل الـ Threats دي Relevant لبيئتي؟**

مثال:

لو شركتي في قطاع Financial Services، ممكن يكون عندي اهتمام أكبر بـ:

* Banking malware
* Credential theft
* Phishing
* Financial fraud infrastructure

بينما Feed مليان Indicators لا علاقة لها بالـ Threats اللي بواجهها ممكن يسبب Noise.

فـ:

> More indicators ≠ Better intelligence

## 3️⃣ Up-to-date

هنا بيقول إن الـ Threat Intel عندي لازم يكون دايمًا متحدث.

طب ليه؟

عشان الـ Attacker Infrastructure دايمًا بتتغير.

مثلًا:

```text
Day 1:
evil.com → malicious

Day 30:
evil.com → dead

Day 40:
attacker uses newdomain.com
```

لو الـ Threat Intel متحدثش، كده أنا هستخدم معلومات ملهاش قيمة أو لازمة.

---

# 1️⃣ Open-source and Closed-source Threat Feeds

**Utilize access to closed and open-source threat feeds**

هنا بيقول إنه عادي أستخدم Open Source أو Closed Source.

## Open-source

معلومات متاحة للعامة.

مثلًا:

* Public Threat Feeds
* Security Researchers
* Open Communities
* Public Reports

## Closed-source

مصادر مش متاحة للجميع، وممكن تحتاج:

* Subscription
* Membership
* Commercial Service
* Industry Sharing Group

زي بعض الـ Commercial Intelligence Feeds.

الفكرة مش:

```text
Open-source = سيئ
Closed-source = أفضل
```

لأ.

لازم يكون التقييم بتاعي بناءً على جودة وملاءمة المصدر بالنسبة للبيئة بتاعتي.

---

# 2️⃣ Categorize Based on Their Contents

هنا هو بيقول إن مش كل الـ Feeds لازم تكون نفس النوع من المعلومات.

Feed ممكن يكون:

```text
IP Feed
```

Feed تاني:

```text
Domain Feed
```

Feed تالت:

```text
Malware Hash Feed
```

أو Feed يقدم:

```text
IP
Domain
URL
Hash
Malware
Threat Actor
Campaign
TTP
```

فلازم أعرف:

**الـ Feed ده بيقدم إيه بالضبط؟**

مثلًا:

```text
Feed A
→ IPs only

Feed B
→ URLs + Domains

Feed C
→ Malware hashes

Feed D
→ Full CTI + context
```

وده بيرجعنا للصفحة بتاعة **TIP Requirements**.

لو أنا محتاجة:

* Malware Configuration
* Campaigns
* Threat Actors
* TTPs

فـ Feed مجرد:

```text
IP + Hash
```

مش هيغطي احتياجاتي.

---

# 3️⃣ Don't Just Take, Share!

هنا بيقول إنه من الأفضل ماكونش دايمًا مستهلكة للـ Threat Intel، لازم أشارك المعلومات المفيدة اللي بكتشفها.

يعني الـ Flow مش:

```text
External Feed
      ↓
Your Organization
```

فقط.

لكن:

```text
Organization A
      ↓
Shares intelligence
      ↓
Community
      ↓
Organization B / C / D
```

وأنا كمان لو اكتشفت:

* New malicious IP
* New phishing domain
* New malware hash
* New attacker infrastructure

ممكن أشارك المعلومة مع الـ Relevant Community.

وده سبب مهم لوجود:

**ISACs (هنتكلم عنه فيما بعد).**

---

# طيب ييجي دلوقتي سؤال مهم جدًا: إزاي أقيس الـ Feed Effectiveness؟

الكتاب مش بيقول:

"جيب Feed وخلاص".

لأ، لازم أسأل:

**هل الـ Feed ده فعلًا مفيد للـ SOC Team؟**

وفيه أسئلة محددة جدًا.

## 1. "When an alert goes off based on feed X, how often is it a true positive?"

يعني:

لو عندي Feed اسمه:

```text
Feed X
```

والـ SIEM عمل Alert لأن Indicator جاي من الـ Feed ده ظهر عندي.

السؤال:

**كام مرة الـ Alert ده طلع True Positive فعلًا؟**

مثال:

Feed X تسبب في:

```text
100 Alerts
```

بعد التحقيق:

```text
20 True Positive
80 False Positive
```

يبقى عندي مؤشر على جودة الـ Feed من ناحية **Alert Usefulness / Precision**.

لكن لازم أخلي بالي: إحنا مش بنقول إن النسبة دي وحدها تحسم جودة الـ Feed، لأن الـ Context والـ Detection Design والـ Environment بيفرقوا.

## 2. "How quickly does data hit the feed?"

دي اسمها عمليًا:

**Speed / Timeliness**

يعني:

لو Researchers اكتشفوا Threat الساعة:

```text
10:00 AM
```

الـ Feed وصله الساعة:

```text
10:10 AM
```

ده سريع.

لكن لو وصله:

```text
Next week
```

فممكن تكون قيمة الـ Feed أقل في الـ Use Cases اللي محتاجة Detection سريع.

### ليه السرعة مهمة؟

خلينا مثلًا نتخيل:

```text
Attacker infrastructure discovered
          ↓
Threat feed
          ↓
Your SIEM / IDS
```

كل ما الـ Information توصل أسرع، كل ما هقدر أضيفيها للـ Detection أسرع.

وده ممكن يساعدني إني أكتشف الـ Activity المرتبطة بالـ Indicator.

## 3. Accuracy vs Completeness

الكتاب بيسألك:

هل أنا بفضل Feed فيه أي حاجة ممكن تكون Dangerous؟

ولا:

Feed فيه فقط الأشياء اللي متأكدين 100% إنها Malicious؟

فيه Trade-off هنا.

### 🟥 Accuracy

يعني الـ Feed يكون دقيق جدًا.

مثلًا يقول:

```text
1.2.3.4 → Malicious
```

فغالبًا يكون فعلًا Malicious.

ده يقلل:

* False Positives

### 🟦 Completeness

يعني الـ Feed يحاول يكون واسع وشامل ويحتوي على أكبر قدر ممكن من الأشياء المشبوهة / الخطرة.

لكن هنا ممكن يدخل:

* Potentially Malicious
* Suspicious
* Not Fully Confirmed

وبالتالي ممكن تزيد الـ False Positives.

---

## طب ليه الكتاب بيقول إن Accuracy مش دايمًا الأفضل؟

تخيلي عندي Feed شديد الحذر.

بيقول:

```text
Only include indicators
when 100% confirmed malicious
```

فممكن تحصل:

```text
True malicious IOC
      ↓
Not yet confirmed
      ↓
NOT included
```

الـ SOC عندك مش هيعمل Alert عليه.

وده اسمه:

**False Negative**

يعني Threat موجود، لكن Detection ماحصلش.

وده كمثال عليه الحاجات اللي بتكون Zero-Day.

---

# False Positive vs False Negative

خلينا نربطهم بالـ Feed:

## False Positive

الـ Feed قال:

```text
Malicious
```

لكن في الحقيقة:

```text
Benign
```

فتحصلي Alert بدون Threat حقيقي.

## False Negative

الـ Feed ماحطش Indicator لأنه مش Confirmed، بينما هو فعلًا Malicious.

فالـ Attack ممكن يعدي بدون Alert.

إذن عندك Trade-off:

```text
          More cautious
               ↓
      Fewer False Positives
               ↑
      But potentially more
        False Negatives


          More inclusive
               ↓
      More potential coverage
               ↑
      But potentially more
        False Positives
```

مفيش اختيار واحد صحيح لكل Organization.

وده بالضبط اللي الكتاب بيقوله:

> There's no right answer here.

لكن لازم أعرف فلسفة الجهة اللي بتنتج الـ Feed.

---

# يعني إيه "Philosophy of the group"؟

دي جملة الكتاب ذكرها وأكد عليها.

لازم أعرف:

هل الـ Feed Provider:

### Conservative؟

يعني:

"مش هنضيف Indicator إلا لما نكون متأكدين جدًا".

ولا:

### More Inclusive؟

يعني:

"هنضيف أي Indicator ممكن يكون Dangerous، والـ SOC هو اللي يحقق".

الاتنين لهم آثار مختلفة.

---

# مثال

## Feed A

```text
100 indicators
95 confirmed malicious
```

دقيق جدًا، لكن ممكن يكون مش شامل.

## Feed B

```text
1000 indicators
```

فيهم:

```text
600 confirmed
400 suspicious
```

أوسع، لكن ممكن يسبب Alerts أكتر وتحقيقات أكتر.

فأنا كـ SOC لازم أعرف:

**إيه الـ Methodology اللي الـ Feed Provider بيستخدمها؟**
