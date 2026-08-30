# بِسۡمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ

# Day 32 - TheHive: Observable Entry

سبق و قولنا قبل كده ان ال observable ده عبارة عن حاجه مثيرة للاهتمام شوفتها اثناء مانا بعمل تحقيق زي مثلا:

* ip address
* Domaine name
* hash file
* email
* username
* host name

لكن وجودها في ال case مش معناها انه تلقائيا Malicious

طيب يجي السؤال هنا انا هعمل ايه بالحاجات دي ؟؟؟؟؟

---

# 1️⃣ بنضيف الـ Observable على مستوى الـ Case

يعني مثلا عندنا case زي كده:

```text id="2xq8ns"
Case:
Phishing Wave – Attachments
```

و اثناء التحقيق انا لقيت حاجه زي كده:

```text id="7q6yaf"
evil1.com
evil2.com
evil3.com
```

دي طبعا حاجات انا اقدر اضيفهم لل case ك observable

```text id="7a8gkz"
Case
 │
 ├── Task
 ├── Task
 │
 └── Observables
      ├── evil1.com
      ├── evil2.com
      └── evil3.com
```

---

# 2️⃣ مش لازم الـ Observable يكون Malicious

يعني مثلا اثناء التحقيق لقيت حاجه زي:

**[www.google.com](http://www.google.com)**

ده طبعا مش هعتبره ioc ده مجرد observable ظهر في البيانات اللي انا بحقق فيها

لكن ممكن Observable تاني يكون:

**evil-example.com**

وعندك دليل إنه مرتبط بالـ Attack.

ساعتها:

**Is IOC = Yes**

و في فرق طبعا بين ال observable و ال ioc ال observable دس حاجه انا لقيتها اثناء التحقيق لسه معرفش هي اصلا malicious ولا لأ او انا مش متاكد

لكن ال ioc هو اصلا عبارة عن observable عندنا سبب نحسبه انه indicator of compromise

يعني باختصار:

**كل ioc هو observable لكن مش كل observable اعتبره ioc**

و دي نقطة مهمه جدا

---

# 3️⃣ Type Dropdown

لما تضيفي Observable في TheHive، بتختاري نوعه.

مثلاً:

```text id="e7v3mp"
Type:
Domain
```

أو:

```text id="p4a9zk"
Type:
IP
```

أو:

```text id="x2b6qd"
Type:
Hash
```

أو:

```text id="h8n5rv"
Type:
URL
```

وهكذا.

TheHive عنده أنواع جاهزة، ولو محتاجة نوع إضافي ممكن تضيفيه

---

# 5️⃣ ⭐ Is IOC

دي من أهم الحاجات في السلايد.

في TheHive فيه اختيار:

**Is IOC**

ومعناه:

**هل المعلومة دي Indicator of Compromise ولا مجرد Observable؟**

مثلاً:

```text id="c7p3ls"
Observable:
evil.com

Is IOC ⭐
☑
```

يعني:

**إحنا بنعتبر evil.com IOC.**

لكن:

```text id="k5x9nm"
Observable:
google.com

Is IOC ⭐
☐
```

يعني:

**ظهر في التحقيق، لكن مش بنعتبره IOC.**

يعني باختصار هي حاجه بتكون غريبه عليا او اول مرة اشوفها فاشك فيها

---

# 6️⃣ Has Been Sighted

دي طبعا نقطة مهمه و مختلفه عن ال Is IOCs

لان انا عندي اختيار و هو **Has been sighted** و ده معناه هل انا شوفت ال observable ده قبل كده في البي~ة بتاعتنا ؟

يعني هل ظهر فعليًا في:

* Network traffic
* Logs
* Emails
* Endpoint
* DNS
* Proxy

### مثال

عندك Domain:

**evil.com**

وعندك دليل إن موظف في الشركة استلم Email فيه:

**evil.com**

إذن:

```text id="q6m3vx"
Is IOC: ☑
Has been sighted: ☑
```

ليه؟

لأنه:

**IOC → عندنا سبب نعتبره malicious.**

**Sighted → شفناه فعلًا في بيئتنا.**

---

# 7️⃣ طب لو Domain Malicious لكن عمرنا ما شفناه؟

يعني مثلا الدومين ده **bad-domain.com** ال TI قالت انه Malicious و روحت اشوف هل هو ظهر عندي قبل كده في البيئة بتاعتنا ولا لأ؟ و الاقيه ملوش ظهور قبل كده ساعتها ممكن يكون:

```text id="r9w2kc"
Is IOC: ☑
Has been sighted: ☐
```

يعني:

**نعرف إنه IOC، لكن مشوفناهوش عندنا قبل كده**

---

# ⭐ مثال السلايد نفسه

السيناريو:

موظف استلم:

```text id="m5z8qv"
Phishing Email
      ↓
MS Word Document
      ↓
Auto-running Macro
      ↓
Connects to malicious domains
```

مثلاً الـ Macro يحاول يتصل بـ:

```text id="u8v4ca"
evil1.com
evil2.com
evil3.com
```

إحنا لقينا الدومينات دي في الـ Email / Macro.

فنضيف:

```text id="z6x2pk"
Domain
evil1.com
evil2.com
evil3.com
```

ونحدد:

```text id="w3n7ls"
Is IOC: ☑
Has been sighted: ☑
```

لأننا في السيناريو شفنا فعليًا محاولة الـ Macro للاتصال بهذه الـ Domains داخل بيئتنا.

---

# 🧠 طيب ليه "Has Been Sighted" مهمة؟

علشان تفرق بين حالتين:

## الحالة 1 — Known IOC ولكن لم يظهر عندنا

```text id="a2k9rm"
Threat Intel
      ↓
evil.com
      ↓
Known Malicious
      ↓
Our Environment?
NO
```

يبقى:

**IOC ✅ / Sighted ❌**

---

## الحالة 2 — Known IOC وظهر عندنا

```text id="n4q7xs"
Threat Intel
      ↓
evil.com
      ↓
Known Malicious
      ↓
Our Environment?
YES
```

يبقى:

**IOC ✅ / Sighted ✅**

ودي أخطر بكتير لأنها بتقول:

**الـ malicious indicator مش مجرد حاجة معروفة في العالم؛ إحنا شفناها فعلًا في بيئتنا.**

---

# 🎯 افهم الأربع حاجات دول

| المصطلح              | معناه                                      |
| -------------------- | ------------------------------------------ |
| **Observable**       | معلومة مهمة ظهرت أثناء التحقيق             |
| **Is IOC**           | هل المعلومة تعتبر Indicator of Compromise؟ |
| **Has been sighted** | هل شفناها فعليًا في بيئتنا؟                |
| **Type**             | نوع المعلومة: IP / Domain / Hash / URL...  |

وأهم علاقة:

```text id="f8y2nd"
Observable
    │
    ├── Is IOC? → هل هو مؤشر اختراق؟
    │
    └── Sighted? → هل ظهر فعلًا عندنا؟
```

---

# ⭐ مثال للفهم :

```text id="j3p8vx"
Domain: evil.com

Observable → ✅
Is IOC → ✅
Has been sighted → ✅
```

معناها:

**لقينا Domain أثناء التحقيق، عندنا سبب نعتبره IOC، وكمان شفناه فعليًا في بيئتنا.**

أما:

```text id="s7m4qa"
Domain: evil.com

Observable → ✅
Is IOC → ✅
Has been sighted → ❌
```

معناها:

**نعرف إنه IOC، لكن لسه ماشفناهوش في بيئتنا.**

وده بالضبط الفرق اللي السلايد عايزة توصله.
