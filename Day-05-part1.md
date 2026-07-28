<div align="center">

# بِسۡمِ ٱللَّهِ ٱلرَّحۡمَٰنِ ٱلرَّحِيمِ

# 📖 Day 05 - Compromise Will Happen & SOC Organization

</div>

---

# Compromise Will Happen

الاختراق هيحصل يعني هيحصل.

يمكن تكون جملة صادمة، لكن حتى أقوى المؤسسات في العالم ممكن يحصل عندها **Compromise**.

وده لأن في طرق كتير يقدر يستغلها الـ **Attacker**، زي مثلًا:

- كلمة مرور ضعيفة.
- ثغرة أمنية (**Vulnerability**).
- خطأ بشري (**Human Error**).
- أو أي نقطة ضعف تانية.

وده معناه إن مفيش دفاع كامل بنسبة **100%**.

---

# How Will It Affect You?

السؤال المهم مش:

> **"هل هيحصل اختراق؟"**

لكن:

> **"لو حصل اختراق، هيأثر عليك قد إيه؟"**

---

## Outcome 1

> **The adversary succeeds in the initial steps of the attack but is quickly detected and fails to complete the mission.**

الـ **Attacker** نجح في الدخول.

لكن تم اكتشافه بسرعة.

### النتيجة

- المهاجم دخل.
- لكنه مقدرش يكمل هدفه.
- الضرر كان محدود.

---

## Outcome 2

> **The adversary is not detected, runs freely, and causes a huge impact.**

المهاجم نجح في الدخول.

ومحدش اكتشف وجوده.

### النتيجة

- سرقة بيانات.
- تشفير ملفات.
- توقف الخدمات.
- خسائر كبيرة.

---

## الفرق بين النتيجتين

الفرق الحقيقي بين الحالتين هو:

> **Detection**

وهنا بيظهر دور الـ **SOC**.

---

## Not All Adversaries Will Be Blocked from the Get-Go

مش كل المهاجمين هيتم منعهم من البداية.

ممكن بعض الهجمات تعدي كل وسائل الحماية.

علشان كده بدل ما يكون تفكيري:

> "إزاي أمنع أي حد يدخل؟"

يبقى تفكيري:

> "لو حد دخل... أكتشفه بسرعة."

---

## Security Mindset

> **The acknowledgement of this fact and the preparation for what occurs after is what separates a good from a bad security operations team.**

يعني اعترافك بحقيقة إن الاختراق ممكن يحصل، واستعدادك للتعامل معاه، هو اللي بيفرق بين فريق **SOC** قوي وفريق ضعيف.

---

# هدف الـ Blue Team

> **Detect and Minimize Damage from Compromise**

يعني:

- اكتشف الاختراق.
- وقلل الضرر لأقصى درجة ممكنة.

---

> 💡 **Note**

> **Catch the attack as early as possible.**

كل ما اكتشفت الهجوم بدري...

كل ما قلت الخسائر.

وده معناه:

**تقليل الـ Dwell Time.**

---

# Your Company Does Not Solely Exist to Be Secure

الشركة مش موجودة علشان تكون آمنة فقط.

لكن ليها هدف أساسي.

مثلًا:

أمازون هدفها الأساسي بيع المنتجات.

والأمان موجود علشان يساعد الشركة تحقق هدفها.

---

# Loss Prevention

وظيفة الـ **Blue Team** هي:

> **Provide a Loss Prevention Function.**

يعني يقلل أو يمنع الخسائر الناتجة عن الهجمات.

---

## Reduce Cybersecurity Risk to an Acceptable Level

الهدف مش إزالة كل المخاطر.

لأن ده مستحيل.

لكن الهدف هو:

تقليل المخاطر لمستوى مقبول.

---

## Balance Between Security and Productivity

لازم يكون فيه توازن بين:

- Security
- Productivity

لأن زيادة الحماية بشكل مبالغ فيه ممكن تعطل شغل الشركة.

---

## مين اللي بيحدد التوازن ده؟

الإجابة هي:

> **The Organization**

هي اللي بتحدد:

- هل محتاجة أعلى مستوى حماية؟
- ولا ممكن تتقبل جزء من المخاطر؟

مثلًا:

- Military
- Banks

غالبًا هيختاروا حماية عالية.

أما:

- Startup

فممكن يقبلوا نسبة مخاطرة أكبر.

---

أحيانًا كـ **Security Engineer** هتشوف حلول أمنية واضحة.

لكن الإدارة ممكن تقول:

> "إحنا متقبلين الخطر ده."

وده لأنهم شايفين الصورة الكاملة من ناحية:

- التكلفة.
- الإنتاج.
- الأرباح.
- استمرارية العمل.

وفي النهاية...

الإدارة هي صاحبة قرار قبول المخاطر (**Risk Acceptance**).

---

# Inform Decision Makers

> **Blue Teams Must Inform Those Who Make Risk Decisions.**

من أهم وظائف الـ **Blue Team** إنه يوفر للإدارة المعلومات اللازمة لاتخاذ القرار.

زي مثلًا:

- درجة خطورة الثغرة.
- احتمالية استغلالها.
- الـ Impact.
- طرق الحماية المقترحة.

بعد كده...

الإدارة هي اللي تقرر.

---

## Good Information Requires Deep Understanding of Your Craft

علشان أنصح الإدارة بشكل صحيح...

لازم أكون فاهم شغلي كويس.

يعني أكون عارف:

- الهجوم بيشتغل إزاي.
- الثغرة خطورتها قد إيه.
- تأثيرها الحقيقي.
- أفضل طريقة للتعامل معاها.

لأن لو معلوماتي كانت غلط...

الإدارة هتاخد قرار مبني على معلومات غلط.

---

# خلاصة السلايد

الفكرة الأساسية هي تغيير طريقة التفكير.

بدل ما أقول:

> **كل ما زادت الحماية كان أفضل.**

أقول:

> **أفضل حماية هي اللي تقلل المخاطر، وفي نفس الوقت تسمح للبزنس يحقق أهدافه.**

---

# Functional Organization Chart

بعد ما عرفنا يعني إيه **Security Operations**، وإيه هدف الـ **Blue Team**، وإزاي نحدد الـ **Risk**...

يبقى السؤال:

> مين هيعمل كل ده؟

وده الشكل الشائع لتنظيم فرق الـ **SOC**.

```text
                         Incident Lead
                               │
                               ▼
                           SOC Lead
                               │
        ┌──────────────┬──────────────┬──────────────┐
        ▼              ▼              ▼              ▼
    Analysts      Detection      Incident      Engineering &
                  Engineering     Response      Infrastructure
        │                                            │
   ┌────┴────┐                                      ▼
   ▼         ▼                                 System Admin
Tier 1   Tier 2 / Tier 3

──────────────────────────────────────────────────────────────

                SOC Adjacent Functions

     ┌───────────────────────────────────────────────┐
     │ • Threat Intelligence                         │
     │ • Digital Forensics                           │
     │ • Vulnerability Management                    │
     │ • Penetration Testing / Red Team              │
     └───────────────────────────────────────────────┘
```

---

# There Is Much More to Running a SOC Than Analysts Doing Triage

شغل الـ **SOC** أكبر بكتير من مجرد إن الـ **Analyst** يشوف الـ **Alerts**.

في ناس تانية مسؤولة عن حاجات مهمة، زي:

- مين كتب الـ Detection Rule؟
- مين جمع الـ Logs؟
- مين بيحدث الـ SIEM؟
- مين بيطور أدوات الاكتشاف؟

كل دول جزء من فريق الـ **SOC**.
