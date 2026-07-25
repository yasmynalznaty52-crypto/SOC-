<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

# 🎯 Goals of SEC450 (Day 03)

</div>
عموماً، الـ **Blue Team** الناجح مش بس شخص بيعرف يستخدم **Tools**، لكن لازم يكون خليط من:

> **Tools + Data + Analysis + Process + Mindset**

---

# 1) Tools 🛠️

### ➜ Security Information and Event Management (SIEM)

وده "حرفيًا" قلب الـ **SOC**، وبيجمع الـ **Logs** من أماكن مختلفة.

### ➜ Threat Intelligence Platforms

منصات بتوفر معلومات عن التهديدات والمهاجمين.

### ➜ Incident Management

إدارة الحوادث الأمنية من بداية اكتشافها لحد ما يتم احتواؤها وإغلاقها.

---

# 2) Data 📊

إزاي أتعامل مع البيانات اللي الـ **SOC** بيطلعها، زي:

1. Network Logs
2. Endpoint Logs
3. Application Logs

---

# 3) Triage 🚦

أحدد الأولويات بسرعة وبشكل صحيح.

يعني أنا عندي **Alerts** كتيرة، لكن مش كلها بنفس الخطورة.

لازم أعرف أبدأ بأنهي **Alert** الأول.

---

# 4) Analysis 🔍

إزاي أعمل تحليل قوي لكل الـ **Alerts**.

يعني مش أول ما يظهر الـ **Alert** أقفله وخلاص، لكن لازم أسأل:

- إيه اللي حصل؟
- بدأ منين؟
- مين عمله؟
- هل في أجهزة تانية اتصابت؟

---

# 5) Automation 🤖

**When and What to Automate to Make Your Life Easier**

يعني أخلي الكمبيوتر يعمل الشغل المتكرر بدل ما أعمله يدوي كل مرة.

---

# 6) Mindset 🧠

طريقة التفكير.

وأبني عقلية الـ **Blue Teamer** في التعامل مع الهجمات والتحقيق فيها.

---

# 7) Continuous Improvement 📈

يعني التحسين المستمر.

لازم أسأل نفسي دايمًا:

- ليه فاتنا الـ **Alert** ده؟
- ليه خد وقت طويل؟
- إيه اللي ممكن نطوره المرة الجاية؟

---

# 🛑 Notes

- الهدف النهائي من **SEC450** هو إنه يجهزك للعمل كعضو في فريق الـ **Blue Team**.

- أفضل **Blue Teamer** هو اللي فاهم الواقع الصح، ومش معتمد على الأدوات بس.

- الـ **SOC** مش موجود علشان الأمان وبس، لكنه موجود كمان علشان يساعد الشركة تكمل شغلها، ومايخليش المشكلة الأمنية تكون سبب في توقف الـ **Business**.

- دور الـ **SOC** هو تقليل الـ **Impact** الناتج عن الحوادث الأمنية، مش إنه يمنع كل الهجمات بنسبة 100%.

<div align="center">

# 📖 SOC Overview

## Section: Components of Security Operations

</div>

سبق شرحهم قبل كده:

- **People**
- **Process**
- **Technology**

---

# Understanding Your Mission – Four Core Questions

> **Cyber defense is difficult. Where do we even start?**

ناس كتير بتبدأ غلط، مثلًا تقول: هنشتري **Splunk** أو **EDR**.

لكن الكتاب بيقول لأ، لازم تبدأ بالإجابة على 4 أسئلة أساسية.

---

# 1) What Are We Trying to Protect? 🛡️

أنا بحمي إيه؟

ناس كتير بتجاوب وتقول "الشركة"، لكن ده جواب عام.

الإجابة الصح تكون مثلًا:

- بيانات العملاء (Customer Data)
- Domain Controller
- Database
- البريد الإلكتروني (Email)
- Servers
- Source Code

وطبعًا الحاجات دي بتختلف من شركة للتانية.

---

# 2) What Are the Threats? 🎯

مين ممكن يهاجمنا؟

هل هو:

- شخص من داخل الشركة؟
- Attacker من خارج الشركة؟

وإيه نوع الـ **Attack**؟

- APT
- Phishing
- Malware

لازم أعرف طبيعة شبكتي، وأعرف مين ممكن يهاجمها.

وده هو دور الـ **Threat Intelligence**.

---

# 3) How Do We Detect Them? 🔍

يعني لو الهجوم حصل، هعرف منين؟

وده يدخل فيه:

- Detection Rules
- Logs
- IDS
- IPS
- EDR
- SIEM

---

# 4) How Will You Respond? 🚨

يعني اكتشفت الهجوم، هنعمل إيه؟

هل عندي خطة واضحة للاستجابة؟

مثلًا لو الهجوم **Ransomware**، فالاستجابة تكون:

- عزل الجهاز.
- قفل الحساب.
- منع الـ IP.
- استرجاع الـ Backup.

وده كله جزء من الـ **Incident Response**.

---

> 💡 **Note**

**The better and more detailed you answer these questions, the better off you are.**

---

# Finding the Organization's Risk Appetite

**(معرفة إزاي الشركة بتستعد للمخاطر)**

---

# Aligning the SOC with the Organization

**(مواءمة مركز العمليات الأمنية مع احتياجات الشركة)**

قبل ما ندخل في الجزء ده، نسأل سؤال.

لو أنا عملت **SOC**، وفيه:

- SIEM
- EDR
- Threat Hunting
- Threat Intelligence

لكن الشركة مش محتاجة كل ده، أو أولوياتها مختلفة...

يبقى إحنا ضيعنا:

- فلوس.
- وقت.
- موظفين.

وده ضد الهدف الأساسي، لأن الـ **SOC** لازم يخدم الـ **Business**، مش العكس.

---

# 1) A Charter, Approved by Management

لازم يكون عندي **SOC Charter**.

طيب يعني إيه **Charter**؟

هي وثيقة رسمية بتحدد:

- مهمة الفريق.
- صلاحياته.
- مسؤولياته.

ومن غيرها، كل واحد هيشتغل بالطريقة اللي هو شايفها.

---

## ليه لازم الإدارة توافق عليها؟

علشان لما الـ **SOC** يعمل إجراء معين، محدش يقول:

> "مين قالك تعمل كده؟"

---

## الـ Charter بتحتوي على إيه؟

### Constituency Served

مين الجهة اللي الـ **SOC** بيخدمها.

---

### Services to Be Delivered

إيه الخدمات اللي هيقدمها الـ **SOC**.

---

### Scope of Work

ودي من أهم النقاط.

علشان أعرف:

- إيه اللي داخل مسؤوليتي.
- وإيه اللي خارج مسؤوليتي.

---

### High-Level Mission Statement

زي الجملة اللي شرحناها قبل كده:

> **Reduce the probability of material impact to the organization.**

---

### Goals

الأهداف المطلوبة، ولازم تكون قابلة للقياس (**Measurable**).

---

### Organizational Structure

هيكل الفريق.

```text
SOC Manager
      │
      ▼
     L3
      │
      ▼
     L2
      │
      ▼
     L1
      │
      ▼
Threat Hunter
```

بحيث كل واحد يعرف:

- بيرفع لمين.
- ومين مسؤول عن إيه.

---

### Concept of Operations (CONOPS)

طريقة تشغيل الـ **Blue Team**.

مثلًا:

- هل الـ SOC شغال 24/7؟
- مين بيسلم الـ Incident؟
- ومين بيستلمها بعده؟

---

# Steering Committee

**(لجنة توجيهية أو لجنة إشراف)**

ودي عبارة عن اجتماع دوري بيحضره الإدارة، مثل:

- IT Manager
- Business Owner

والهدف منه التأكد إن الـ **SOC** ماشي في الاتجاه الصحيح.

---

## وظيفتها

### 1) Enumerates Risk Concerns

تحديد أهم المخاطر اللي الـ **Business** قلقان منها.

---

### 2) Aligns SOC Capabilities with Business Needs

التأكد إن إمكانيات الـ **SOC** بتخدم احتياجات الشركة.

---

### 3) Ensuring That Communication Lines Stay Open

التأكد إن قنوات التواصل بين كل الأطراف تفضل مفتوحة باستمرار.

---

## 📌 Note

الهدف في النهاية إن الـ **SOC** يلبي احتياجات الـ **Business**، ويركز موارده على المخاطر ذات التأثير الأكبر على الشركة.
