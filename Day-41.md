# بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ

# Day 41 — Storing and Sharing Threat Intelligence In a Safe Way: De-fanged Indicators

الخطوة العملية دي مهمة جدًا لأي SOC Analyst خصوصًا لو يعمل Share للـ IOCs في Reports.

وهنا هو بيقول إزاي أنا هشارك الـ IOCs دي من غير ما تتحول بالغلط للينك قابل للفتح؟

وده في حد ذاته بيسمى **De-fanging**.

---

# أولًا: يعني إيه De-fanged Indicator؟

مثلًا يعني عندنا IOCs حقيقي على شكل لينك زي مثلًا:

```text
hxxp://satkas.waw.pl/rainloop/forecast
```

ده Live URL.

لو حطيتيه في:

* Slack
* Email
* Word
* Browser
* بعض الـ Threat Intelligence Platforms
* بعض أدوات الـ SOC

ممكن البرنامج يحوله تلقائيًا إلى **Clickable Link**.

وده طبعًا خطر لأن ممكن أي حد يدوس عليه بالغلط.

عشان كده بنعمل:

**De-fang**

واللي هو عبارة عن إني بعمل تغيير بسيط جدًا في شكل الـ IOC بحيث يفضل لسه مفهوم، لكن مايبقاش قابل للفتح والتشغيل بسهولة.

زي كده مثلًا:

```text
http  → hxxp

.waw.pl → .waw[.]pl
```

حاجات بسيطة جدًا لكن الـ Analyst طبعًا يقدر يفهمها بسرعة.

---

# طيب ليه مثلًا الموضوع ده مهم ليا كـ SOC Analyst؟

بسبب نفس الكلام اللي قولته، إنه لو أنا مثلًا بعمل **Incident Investigation** ولقيت عندي لينك بعتبره كـ IOC وبعته للفريق على Slack، حد ممكن يضغط عليه بالخطأ.

وده ممكن يؤدي إلى:

```text
Click
 ↓
Request to malicious server
 ↓
Malicious content
```

خصوصًا لو الـ URL بيؤدي مباشرة إلى:

* Malware
* Phishing page
* Exploit
* Payload
* C2 infrastructure

عشان كده بنعمل:

```text
hxxp://malicious-domain[.]com/payload.exe
```

فتبقى المعلومة قابلة للقراءة والمشاركة لكن مش **Live** بشكل مباشر.

---

# نفهم الأمثلة الموجودة في السلايد

عندي مثلًا:

## Example 1

```text
hxxp://satkas.waw[.]pl/rainloop/forecast
```

ده:

**URL**

وهو De-fanged باستخدام:

```text
hxxp

[.]
```

---

## Example 2

```text
vm-srv-1.gel.ulaval[.]ca
```

ده:

**Domain / Hostname**

تم تغيير:

```text
.ca
```

إلى:

```text
[.]ca
```

---

## Example 3

```text
156[.]96[.]46[.]116
```

ده:

**IPv4 Address**

بدل:

```text
156.96.46.116
```

---

## Example 4

```text
188[.]34[.]185[.]85
```

نفس الفكرة:

**IP Address → De-fanged IP**

---

# طب Details اللي جنبهم معناها إيه؟

السلايد مثلًا:

```text
Indicator
156[.]96[.]46[.]116

Details
TA Infrastructure
```

معناه إن:

```text
Indicator = 156[.]96[.]46[.]116
Context/Description = TA Infrastructure
```

وده بيرجعنا مباشرة للصفحات اللي فاتت:

**IOC مش مجرد Indicator، لازم يكون عندك Context.**

يعني مش:

```text
156[.]96[.]46[.]116
```

وخلاص.

لكن:

```text
156[.]96[.]46[.]116
↓
TA Infrastructure
```

أو:

```text
hxxp://...
↓
TrailBlazer C2
```

وده يخلي الـ IOC مفيد في التحقيق.

---

# طيب هيجي حد يسأل هل الـ De-fanging يعتبر Encryption؟

والإجابة هي إنه لا أكيد.

لأني أنا مشفرتش الـ IOCs، أنا خليته زي ما هو حرفيًا بس غيرت حاجات، بس ضفت حاجات أو غيرت حاجات بسيطة.

يعني أنا مخبيتش المعلومة.

الهدف منها إنها تفضل مفهومة للبشر بس مش Live.

يعني:

```text
De-fanging ≠ Encryption
```

```text
De-fanging ≠ Obfuscation for secrecy
```

هو أساسًا **Safety mechanism** عند مشاركة الـ IOCs.

وعادي لو احتجت الـ IOC بنفس الشكل هعمل **Re-fanging**.

---

# نربط بالـ Threat Intelligence Platform

إحنا كنا بنتكلم إن الـ TIP بيخزن:

```text
IOC
+
Context
+
Relationships
```

لكن أثناء **Sharing / Reporting** لازم ناخد بالنا إن الـ IOC ممكن يبقى dangerous لو اتعرض بشكل مباشر.

فمثلًا:

```text
TIP
 ↓
Malicious URL
 ↓
De-fang
 ↓
Report / Slack / Email
```

---

# نفهم القاعدة دي

## Common De-fanging

| Live       | De-fanged       |
| ---------- | --------------- |
| `http://`  | `hxxp://`       |
| `https://` | `hxxps://`      |
| `evil.com` | `evil[.]com`    |
| `1.2.3.4`  | `1[.]2[.]3[.]4` |

والهدف:

> **Prevent accidental clicks/connections while preserving the IOC's meaning.**

---

# 🎯 الخلاصة

الـ **De-fanged IOC** هو IOC اتغير شكله بطريقة بسيطة عشان مايبقاش **Live** أثناء التخزين أو المشاركة.

Intelligence نفسها تتحول إلى سبب في **accidental connection أو infection**.

وأهم جملة:

> **De-fanging makes malicious indicators safe to store and share without making them directly clickable/live.**
