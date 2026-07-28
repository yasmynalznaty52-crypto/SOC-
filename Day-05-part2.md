# SOC Roles

## 1) SOC Analyst

وظيفته الأساسية:

- Monitoring
- Investigation
- Triage

يعني يراقب الـ **Alerts**، ويبدأ يجمع المعلومات، ويحدد الأولوية، ولو الـ **Incident** أكبر من صلاحياته يعمل **Escalation**.

---

## 2) Detection Engineers

دول مسؤولين عن كتابة وتطوير الـ **Detection Rules**.

يعني هم اللي يعلموا الـ:

- SIEM
- EDR
- IDS

إزاي يكتشفوا الهجمات.

بمعنى إنهم بيحولوا معرفة الهجمات إلى **Detection Logic**.

---

## 3) Threat Hunters

دول بيدوروا على المهاجم حتى لو مفيش **Alert**.

وبيبحثوا في:

- Logs
- Network Traffic
- Running Processes
- Authentication Logs

علشان يكتشفوا أي نشاط مشبوه.

---

## 4) Engineers

دول مسؤولين عن البنية التحتية الخاصة بالـ **SOC**.

زي مثلًا:

- تركيب الـ SIEM.
- توصيل الـ Logs.
- إدارة الـ Infrastructure.
- حل المشاكل التقنية.

---

## 5) System Administrators

دول مسؤولين عن:

- Servers
- Operating Systems
- Active Directory
- Windows
- Linux

ولو فريق الـ **SOC** محتاج:

- Logs
- تغيير إعدادات.
- أو تنفيذ إجراءات على الأجهزة.

فبيتواصل مع الـ **System Administrators**.

---

## 6) SOC Adjacent Functions

في فرق مش شغالة جوه الـ **SOC** بشكل مباشر.

لكن شغلها مرتبط بيه جدًا.

زي:

- DFIR (Digital Forensics & Incident Response)
- GRC (Governance, Risk & Compliance)
- Malware Analysis
- Vulnerability Management
- Threat Intelligence
- Penetration Testing / Red Team

---

> 💡 **Note**

> **There is no one size fits all.**

مفيش شكل واحد مناسب لكل الشركات.

كل شركة بتبني الـ **SOC** حسب:

- حجمها.
- الميزانية.
- عدد الموظفين.
- طبيعة العمل.

---

علشان أعرف التنظيم ناجح ولا لأ...

مش أبص على الرسم التنظيمي.

لكن أبص على الأداء الحقيقي للفريق.

---

طيب إمتى أغير التنظيم؟

لما ألاحظ إن في مشاكل بدأت تظهر بين الـ **Teams**.

زي:

- بطء في الاستجابة.
- سوء تواصل.
- تأخير في تسليم الـ Incidents.
- تضارب في المسؤوليات.

---

> **Ultimately, everyone in all these potential groups needs to work closely with one another.**

في النهاية...

كل الفرق دي لازم تشتغل مع بعض باستمرار.
