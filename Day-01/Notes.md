<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ
</div>

---
# Day 01 - Welcome to Blue Team Fundamentals

## Section 1: Welcome to Blue Team

### 1) People 🧠
**Mindset, Mental Model, Career Progression, Burnout**

أول حاجة هنتكلم عنها هي الشخص نفسه وطريقة تفكيره.

يعني مثلًا لو حصل إن شخص دخل على موقع أو System في الشركة، طريقة التفكير بتختلف حسب خبرة الشخص:

```


                 طريقة التفكير

        ┌───────────────────────────┐
        │                           │
        ▼                           ▼

   شخص مبتدئ                 SOC Analyst

   - هيشوف الـ Alert          - هو دخل منين؟
   - ويقفله وخلاص             - ليه عمل كده؟
   - مش هيشغل دماغه           - هو لسه موجود؟
                              - إيه الأجهزة اللي اتأثرت؟
                              - هل دي بداية Malware؟
```

يعني الـ SOC Analyst بيفكر كمحقق، مش مجرد شخص بيقفل Alerts.

---

## 🧠 Mental Model

معناها إن بدل ما كل Alert أتعامل معاها من الصفر، لازم يكون عندي طريقة ثابتة أمشي عليها.

الـ Workflow يكون:

```
Alert
  ↓
Validate
  ↓
Investigate
  ↓
Scope
  ↓
Contain
  ↓
Remediate
  ↓
Lessons Learned
```

---

## 🔥 Burnout

الـ SOC من أكثر المجالات اللي فيها ضغط بسبب:

- Alerts طول اليوم.
- Night shifts.
- كمية كبيرة من الـ Logs.
- ضغط من الإدارة.

عشان كده مهم يكون عند الـ SOC Analyst طريقة تفكير وتنظيم تساعده يكمل في المجال.

---

# 2) Process ⚙️

طريقة الشغل أهم من الأدوات.

يعني الهدف مش إني أعرف أستخدم Tool وخلاص، لكن أعرف أحقق في الـ Alerts والـ Logs وأفهم:

- هل ده Malware؟
- هل حد بيعمل Scan على الشبكة؟
- هل ده Reconnaissance؟

---

## 🔎 Investigation Theory

بدل ما أخمن، لازم يكون عندي خطوات للتحقيق.

مثلاً:

- تحليل الـ Logs.
- مراجعة الـ RAM.
- جمع الأدلة.
- فهم الأحداث اللي حصلت.

---

## 🚦 Triage

دي من أهم الحاجات في شغل الـ SOC.

معناها ترتيب أولويات الـ Alerts حسب الخطورة.

```
Critical
   ↓
High
   ↓
Medium
   ↓
Low
```

---

## Key Takeaways

- الـ SOC Analyst لازم يفكر كمحقق.
- الـ Mental Model يساعدني أمشي بطريقة ثابتة في التحقيق.
- الـ Process أهم من الأدوات.
- الـ Triage يساعدني أحدد الأولويات
# Day 01 - Welcome to Blue Team Fundamentals

## Data Flow 🔄

يعني البيانات ماشية إزاي في الـ System أو الشبكة.

مثال على Data Flow:

```
User
  ↓
Windows
  ↓
Event Log
  ↓
Sysmon
  ↓
SIEM
  ↓
Alert
  ↓
SOC Analyst
```

الفكرة إن الـ SOC Analyst لازم يفهم رحلة البيانات من أول ما تحصل Event لحد ما تتحول إلى Alert يتم التحقيق فيها.

---

# 3) Technology 💻

ده الجزء التقني، وبيشمل الحاجات اللي الـ SOC Analyst لازم يكون فاهمها.

---

## 🌐 Network Monitoring

يعني مراقبة حركة الشبكة باستخدام أدوات مثل:

- Wireshark
- IDS (Intrusion Detection System)
- Firewall Logs

الهدف هو اكتشاف أي نشاط غير طبيعي داخل الشبكة.

---

## 🖥️ Host Monitoring

ده مراقبة الـ Endpoint أو الجهاز نفسه.

مثال:

- Windows Event Logs
- System Activities
- Processes Running on the Device

---

## 🔗 Understanding Protocols

لازم يكون عند الـ SOC Analyst فهم للبروتوكولات الأساسية مثل:

- HTTP
- HTTPS
- FTP
- DNS
- TCP/IP

لأن فهم البروتوكولات يساعد في تحليل الـ Logs واكتشاف الهجمات.

---

## 🚨 Spotting Attacks

يعني أعرف أميز علامات الهجوم.

مثال:

- وجود عدد كبير من الـ Commands الغريبة.
- Failed Logins كثيرة.
- Encoded PowerShell Commands.
- DNS Tunneling.

الهدف هو معرفة هل النشاط طبيعي أم يشير إلى Attack.

---

## 🐍 Scripting and Automation

بدل ما أعمل نفس المهمة 100 مرة يدويًا، أستخدم Scripts لأتمتة الشغل.

مثال:

- كتابة Script بلغة Python.
- تحليل Logs بشكل أسرع.
- تنفيذ Tasks متكررة تلقائيًا.

---

# Strategic, Operational and Tactical Levels 🎯

دي مستويات التفكير داخل الـ SOC أو مجال الـ Cyber Security بشكل عام.

---

## 1) Tactical Level (تكنيكي) 🔧

ده المستوى الفني اليومي.

يشمل:

- تحليل الـ Logs.
- مراجعة الـ Alerts.
- التحقيق في الحوادث.
- عمل Containment للجهاز المصاب وفصله عن الشبكة.

---

## 2) Operational Level (تشغيلي) ⚙️

ده مستوى إدارة العمليات.

يشمل:

- توزيع الـ Tasks.
- تنظيم الـ Shifts.
- متابعة أداء الفريق.
- التأكد من سير العمل بشكل صحيح.

---

## 3) Strategic Level (استراتيجي) 🏢

ده مستوى الإدارة العليا مثل:

- CEO
- Security Management

يركز على القرارات الكبيرة مثل:

- كيف نقلل المخاطر؟
- هل نحتاج فريق Threat Hunting؟
- هل نحتاج شراء أدوات حماية جديدة؟

مثال:

شراء EDR  
(**Endpoint Detection and Response**)

وهو نوع من برامج الحماية التي يتم تثبيتها على أجهزة الموظفين لمراقبة واكتشاف الأنشطة المشبوهة.

مثال:
- Windows Defender

---

## Key Takeaways 💡

- فهم Data Flow مهم لمعرفة مصدر الـ Alert.
- الـ SOC Analyst يحتاج معرفة بالـ Network والـ Host Monitoring.
- فهم البروتوكولات يساعد في التحقيق.
- Automation يوفر الوقت ويقلل العمل اليدوي.
- مستويات Tactical, Operational, Strategic توضح اختلاف أدوار الأشخاص داخل الأمن السيبراني

# Why Are We Being Attacked? 🎯

السؤال ده معناه **"ليه أصلاً حد ممكن يهاجمنا؟"**  
مش "إزاي الهكر هاجمنا؟"

لأن معرفة الهدف من الهجوم بتساعدني أتوقع نوع الهجوم وأستعد له.

---

# 1) Why are so many cyber attacks happening in the first place?

ليه الـ **Cyber Attacks** بقت كثيرة جدًا؟

الإجابة هي إن مش كل الـ **Attackers** عندهم نفس الأهداف.

في دوافع مختلفة للهجمات مثل:

- 💰 Financial Gain (السرقة المالية)
- 📂 Data Theft (سرقة البيانات)
- 🕵️ Espionage (التجسس)
- 📉 Reputation Damage (تخريب السمعة)
- ⭐ Fame (البحث عن الشهرة)

كل هدف من دول له نوع مختلف من الهجمات.

---

# Securing Strategy 🛡️

قبل ما أشتري أدوات حماية مثل:

- Firewall (FW)
- EDR (Endpoint Detection and Response)
- SIEM

لازم أسأل نفسي:

> أنا بحمي الـ System من مين؟

يعني لازم أفهم الـ Threats اللي ممكن تستهدفني قبل ما أحدد الأدوات المناسبة.

---

## Example:

لو شركة فيها:

### 🏦 Financial Transactions

فممكن تكون هدف لهجمات هدفها:

- سرقة الأموال.
- الاحتيال المالي.

لكن لو شركة تعمل في:

### 🔬 Research & Development

أو لديها:

- Research Data
- Patents

فقد تكون هدفًا لهجمات هدفها:

- التجسس.
- سرقة المعلومات.
- سرقة الملكية الفكرية.

---

# Budget Planning 💰

لكي أنفق الميزانية بطريقة منطقية، يجب أن أعرف:

1. مين ممكن يهاجمني؟
2. ليه هيهاجمني؟
3. هيستخدم إيه في الهجوم؟

---

# Threat Intelligence 🧠

هو جمع وتحليل المعلومات عن:

- المهاجمين.
- أساليب الهجوم.
- التهديدات الحالية.

وذلك لمساعدتي على الاستعداد قبل حدوث الهجوم.

Threat Intelligence لا يعني فقط معرفة أن هناك Hacker، ولكن معرفة:

### Who?
مين المهاجم؟

### Who is being targeted?
مين الضحايا المستهدفين وما هي أهداف الهجوم؟

### What?
ما الأدوات أو الأساليب التي يستخدمها؟

### When?
متى تحدث الهجمات؟

### What type of victims are targeted?
ما نوع الضحايا الذين يستهدفهم دائمًا؟

---

## Example:

لو شركة تعمل في قطاع البنوك، وعرفت من خلال Threat Intelligence أن هناك Malware منتشر يستهدف المؤسسات المالية.

ستقوم الشركة بـ:

- زيادة الاحتياطات الأمنية.
- تحسين الحماية.
- عمل Backups.
- مراقبة الأنشطة المشبوهة.

وهذا هو دور الـ Threat Intelligence.

---

## 💡 Note

Most cyber attacks are financially motivated.

Example:

- Ransomware attacks 💰

حيث يكون الهدف الأساسي غالبًا هو الحصول على المال

# Types of Attack Motivations 🎯

أحيانًا يكون الهدف من الهجوم إن دولة أو شركة أو جهة معينة تحصل على معلومات أو تحقق هدف معين.

---

## 🕵️ Espionage (التجسس)

يعني سرقة معلومات سرية أو حساسة مثل:

- أسرار تجارية (Trade Secrets)
- خطط عسكرية (Military Plans)
- براءات اختراع (Patents)

الهدف غالبًا يكون الحصول على معلومات تساعد جهة معينة في تحقيق ميزة أو مصلحة.

---

## 🧠 APT (Advanced Persistent Threat)

الـ APT معناها:

**Advanced Persistent Threat**

وهي مجموعة من الـ Attackers تكون:

- محترفة جدًا.
- لديها موارد وإمكانيات كبيرة.
- غالبًا تكون مدعومة من دولة (State-sponsored) أو منظمة.

تتميز بأنها لا تعمل بشكل سريع فقط، ولكن قد تظل داخل النظام:

- شهور.
- أو حتى سنوات.

وهدفها غالبًا يكون التجسس أو سرقة معلومات مهمة.

---

## ⚠️ Zero-day

الـ **Zero-day Vulnerability** هي ثغرة:

- الشركة المصنعة لم تكتشفها بعد.
- لا يوجد لها Patch أو تحديث أمني حتى الآن.
- يستغلها الـ Attacker قبل أن يتم إصلاحها.

تعتبر خطيرة لأن الدفاع ضدها يكون أصعب بسبب عدم وجود حل جاهز.

---

## Other Attack Motivations 🔥

ليست كل الهجمات هدفها المال أو التجسس.

هناك دوافع أخرى مثل:

- Revenge (الانتقام)
- Entertainment (التسلية)
- Fame (الشهرة)

---

## Key Takeaway 💡

فهم دوافع الـ Attackers يساعد الـ SOC Analyst على توقع نوع التهديد والاستعداد له بشكل أفضل.
