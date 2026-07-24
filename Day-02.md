<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

</div>
<h1 align="center">Day 02 - Dwell Time & Incident Detection</h1>
## How Long Does It Take to Realize It? ⏳

بعد ما يحصل **Cyber Attack** على الشركة وخلاص يتم اختراقها، قد إيه المدة اللي هتاخدها الشركة علشان تعرف إنها اتعرضت للاختراق؟

---

## Dwell Time 🕒

أول مصطلح هنتعرف عليه وهو **Dwell Time**.

وهو معناه الفترة الزمنية بين لحظة دخول الـ **Attacker** لأول مرة إلى النظام، ولحظة اكتشافه.

---

## Mandiant M-Trends 📊

من أشهر شركات **Incident Response** في العالم هي **Mandiant**.

والشركة بتنشر تقرير اسمه **M-Trends**، واللي بيعتمد على التحقيقات الحقيقية اللي الشركة اشتغلت عليها أثناء الاستجابة للحوادث الأمنية.

---

> 💡 **Note**

لو الشركة اكتشفت المشكلة بنفسها، فغالبًا هتكون مدة الـ **Dwell Time** قليلة.

لكن لو اللي اكتشف الاختراق كان:

- User
- Customer
- أو جهة خارجية

فده معناه إن المهاجم فضل موجود داخل النظام فترة أطول، وبالتالي هيكون الـ **Dwell Time** كبير.

---

## مدة الاكتشاف بتختلف باختلاف نوع الـ Attack

يعني مثلًا:

### 🔒 Ransomware

سرعة اكتشاف الـ **Ransomware** بتكون أكبر، لأنه بمجرد ما يصيب الجهاز بيبدأ يشفر البيانات، وبالتالي المستخدم أو الشركة بيلاحظوا المشكلة بسرعة.

أما في حالة:

### 🕵️ APT (Advanced Persistent Threat)

فالهدف الأساسي للمهاجم هو إنه يفضل موجود داخل النظام لأطول فترة ممكنة من غير ما حد يكتشفه.

علشان كده غالبًا بيكون الـ **Dwell Time** أطول.

---

## 💡 Important Note

سرعة اكتشاف الهجوم عمومًا مش دليل إن فريق الأمن ناجح.

لأن في بعض الهجمات، زي **Ransomware**، بيكون اكتشافها سريع بسبب طبيعة الهجوم نفسه، مش بالضرورة بسبب كفاءة فريق الـ **SOC**.

---

## الخلاصة عموماً 📌

### 1)

تقليل الـ **Dwell Time** حاجة كويسة، لكن مش كل انخفاض معناه إن الدفاع بقى أحسن.

---

### 2)

أهم جملة هي:

> **Some attacks are designed to be found.**

في **Attacks** زي مثلًا **Ransomware** بتعلن عن نفسها، عشان كده اكتشافها بيكون سريع، مش علشان فريق الـ **SOC** اكتشفها بدري.

---

### 3)

المقياس الحقيقي للنجاح مش بعد كام يوم اكتشفنا الهجوم، بل:

> **هل اكتشفنا الهجوم قبل ما الـ Attacker يحقق هدفه ولا لأ؟**

---

### 4)

الهدف الأول للـ **Blue Team** هو إنه يكون أسرع من الـ **Attacker** في:

- الاكتشاف (Detection).
- التحليل (Analysis).
- الاستجابة (Response).

---

# Cybersecurity Operations 🛡️

> **Protecting the Confidentiality, Integrity, and Availability of Information Systems.**

---

الحماية تبدأ من:

- التقييم الصحيح بعد الاختراق.
- مراقبة الأنظمة بشكل مستمر.
- اكتشاف أي نشاط أو سلوك غير طبيعي داخل الشركة.

---

# The First Piece of a Defensive Security Mindset 🧠

## Defensive Mindset

**Defensive Mindset** يعني عقلية المدافع، ودي بتختلف عن عقلية الـ **Pentester** أو الـ **Attacker**.

### Pentester

بيفكر:

> إزاي أدخل أو أخترق؟

### Blue Team

بيفكر:

> لو حد دخل، أكتشفه بسرعة وأقلل الضرر.

---

> 💡 **Note**

افترض إن الـ **Attacks** ممكن تحصل في أي وقت.

لكن التركيز يكون على:

- الاكتشاف السريع (Early Detection).
- الاستجابة السريعة (Rapid Response).
- تقليل الضرر (Damage Reduction).

بدلًا من الاعتماد على فكرة إن الشبكة مستحيل يتم اختراقها.

وده هو أساس شغل الـ **SOC** والـ **Blue Team**.

# What is a Security Operations Center (SOC)? 🛡️

## 1) Cyber

كل ما يتعلق بأنظمة المعلومات، مثل:

- Servers
- Cloud
- Networks

---

## 2) Security

يعني أخلي النظام يُستخدم بالطريقة اللي هو معمول عشانها بس.

---

## 3) Operations

وهي العمليات المستمرة.

---

## 4) Center

يعني نقطة تجمع، أو **Hub** أو **Nexus**.

---

> ## SOC = Blue Team

---

# 🛑 Goals

## 1) Monitoring

أراقب الشبكة أو السيرفرات أو الأجهزة، والهدف هو اكتشاف أي نشاط غريب أو مشبوه.

يعني بشكل مستمر أتابع الـ **Alerts**.

---

## 2) Threat Hunting

مفيش أي **Alerts**، لكن أنا شاكك إن في **Malware** أو نشاط مشبوه.

فأبدأ أدور بنفسي في الـ **Logs** لحد ما أوصل للدليل.

---

## 3) Incident Response

ودي الاستجابة للحوادث.

مثلاً لو في جهاز اتصاب، فريق الـ **Incident Response** يقوم بـ:

- عزل الجهاز أو الأجهزة المصابة.
- جمع الأدلة.
- توثيق الهجوم.
- استعادة الخدمة.

---

## 4) Threat Intelligence

شرحناه قبل كده.

وباختصار هو جمع وتحليل معلومات عن الـ **Attackers** والتهديدات، علشان أكون مستعد قبل ما الهجوم يحصل.

---

## 5) Digital Forensics

وده التحقيق الجنائي الرقمي.

بعد الهجوم بنبدأ نسأل:

- دخل منين؟
- استخدم إيه؟
- سرق إيه؟
- وصل لإيه؟
- فضل موجود قد إيه؟

وغالبًا بيتم باستخدام:

- Memory Analysis
- Disk Analysis
- Timeline Analysis

---

# 📊 SOC Architecture Diagram

```text
                                  ┌───────────┐
                                  │    SOC    │
                                  └─────┬─────┘
             ┌──────────────────────────┼──────────────────────────┐
             ▼                          ▼                          ▼
          People                     Process                   Technology
             │                          │                          │
     ┌───────┼───────┐          ┌───────┼───────┐          ┌───────┼───────┐
     ▼       ▼       ▼          ▼       ▼       ▼          ▼       ▼       ▼
 SOC Analysts Incident  Threat   Alerts Incident Investigation  SIEM   IDS   IPS
              Response Hunting
```

# Modern Defense Mindset (عقلية الـ Modern Blue Team)

## Modern Defense Mindset

1. افترض إن الاختراق ممكن يحصل.

2. معتمدش على المنع بس (**Detection is a must**).

3. أبحث عن المهاجم بشكل استباقي (**Threat Hunting**).

4. أركز على إيه اللي هيحصل بعد الـ **Post-Exploitation Attacks**.

5. أكتشف وأستجيب بسرعة.

6. أوزع الميزانية أو الحماية على حسب الأهمية والمخاطر.

---

## Summarizing Our Mission

$$
\Longrightarrow \text{Reduce the probability of material impact to the organization due to a cyber event.}
$$

يعني الحد أو التقليل من حدوث **تأثير جوهري** على مؤسستي نتيجة الـ **Cyber Event** اللي حصل.

أنا مقدرش أضمن إن الشركة عمرها ما هتتهكر، لكن أقدر أقلل من حدوث الـ **Attack** أو أحدّ من تأثيره.

وقولت **تأثير جوهري (Material Impact)** عشان مش كل **Incident** ليه نفس التأثير.

---

## Why Can't We Completely Prevent Attacks?

الأسباب اللي ورا إني مقدرش أمنع الاختراق بشكل كامل:

- مفيش سيستم مثالي.
- مفيش Firewall مثالي.
- مفيش SIEM يقدر يكتشف كل حاجة.

لذلك مهمتي لو حصل **Attack**:

- أقلل الـ **Impact** لأقل درجة ممكنة.
- أمنع الانتشار (**Lateral Movement**).
- أوقف تطور الأحداث.
- أراقب الـ Network والـ Endpoints بشكل جيد.

وكمان لما يحصل شيء غير طبيعي:

**Security Tools → Generate Alert → Analyst Performs Triage**

---

## Skills I Need to Learn as a Blue Team Analyst

عشان أقدر أعمل تحليل كويس، لازم أتعلم:

1. أفهم البروتوكولات.

2. أقدر أقرأ وأفهم الـ **Log Files**.

3. أعمل **High Quality Analysis**.

4. أفهم الـ **Data Flow**.

---

## Key Note

> A good defender doesn't try to build an unbreakable wall; they build a system that can detect, respond, and limit damage when the wall is eventually bypassed.
