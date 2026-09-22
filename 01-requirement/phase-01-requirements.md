# Phase 01 --- Requirements Analysis Baseline

> **Hospital Management System (HMS)**
>
> **Requirements → Business Scope → Use Cases → Rules → Data Evidence →
> Traceability**
>
> **Version:** 1.0\
> **Phase:** `01-requirements`\
> **Classification:** `SRS-DERIVED`\
> **Source of Truth:** HMS Software Requirements Specification (SRS)

------------------------------------------------------------------------

## 1. Purpose

هذه الوثيقة هي خط الأساس الرسمي للمرحلة الأولى من هندسة قاعدة بيانات
نظام إدارة المستشفى.

الهدف ليس تصميم قاعدة البيانات بعد، وإنما تحويل الـ SRS إلى **مرجع منظم
وقابل للتتبع** يمكن الاعتماد عليه في المراحل التالية:

``` text
SRS
 │
 ├── Functional Requirements
 ├── Non-Functional Requirements
 ├── Actors
 ├── Use Cases
 ├── Scope / Constraints
 └── Existing Conceptual ER Diagram
          │
          ▼
   Requirements Analysis
          │
          ▼
   Business Rules & Events
          │
          ▼
   Domain Modeling
          │
          ▼
   Conceptual Data Model
          │
          ▼
   Logical Data Model
          │
          ▼
   Physical Database
```

> **قاعدة هذه المرحلة:** لا يتم اختراع متطلبات أو حقول أو علاقات غير
> مثبتة في الـ SRS.

------------------------------------------------------------------------

# 2. Document Control

  Item                 Value
  -------------------- ---------------------------------------------
  Project              Hospital Management System
  Document             Phase 01 --- Requirements Analysis Baseline
  Version              1.0
  Status               Baseline
  Source               HMS SRS
  Current Phase        Requirements Analysis
  Next Phase           Domain Modeling
  Database Design      Not started in this phase
  SQL Implementation   Not started in this phase

------------------------------------------------------------------------

# 3. Authority & Evidence Model

لمنع خلط المتطلبات بالافتراضات، يتم تصنيف كل معلومة في المشروع إلى:

  -----------------------------------------------------------------------
  Classification                      Meaning
  ----------------------------------- -----------------------------------
  `SRS-DERIVED`                       مذكورة صراحة في وثيقة المتطلبات

  `DERIVED`                           استنتاج منطقي مباشر من متطلب موثق،
                                      ويجب تتبعه إلى مصدره

  `UNSPECIFIED`                       لم يحددها الـ SRS

  `OPEN-ISSUE`                        نقطة تحتاج قراراً أو توضيحاً من صاحب
                                      المتطلبات

  `DESIGN-DECISION`                   قرار هندسي يتم اتخاذه لاحقاً ولا
                                      يعتبر متطلباً أصلياً
  -----------------------------------------------------------------------

### قاعدة التتبع

``` text
Requirement
    ↓
Business Rule
    ↓
Business Event / Concept
    ↓
Domain Model
    ↓
Logical Entity
    ↓
Database Structure
```

إذا لم يوجد مصدر أعلى للسلسلة، فلا يجوز اعتبار العنصر متطلباً أصلياً.

------------------------------------------------------------------------

# 4. Project Scope

وفقاً للـ SRS، النظام هو تطبيق ويب مركزي يربط العمليات الأساسية للمستشفى.

## داخل النطاق

``` mermaid
flowchart LR
    HMS["Hospital Management System"]

    HMS --> PR["Patient Registration"]
    HMS --> AS["Appointment Scheduling"]
    HMS --> CC["Clinical Care"]
    HMS --> LAB["Laboratory Services"]
    HMS --> PH["Pharmacy Management"]
    HMS --> BILL["Billing & Payments"]
    HMS --> ADM["System Administration"]
    HMS --> PORTAL["Patient Self-Service"]
```

### المجالات الوظيفية

1.  Patient Registration
2.  Appointment Scheduling
3.  Clinical Care
4.  Laboratory Services
5.  Pharmacy Management
6.  Billing
7.  System Administration
8.  Patient Self-Service

------------------------------------------------------------------------

# 5. Explicitly Out of Scope

الـ SRS يحدد العناصر التالية خارج النطاق:

``` mermaid
flowchart TB
    OUT["Outside SRS Scope"]

    OUT --> DEV["Actual software development & coding"]
    OUT --> HW["Hardware setup & configuration"]
    OUT --> MOBILE["Mobile application development"]
    OUT --> EXTINS["External insurance system integrations"]
    OUT --> LABEQ["Specialized diagnostic equipment integration"]
```

> هذه العناصر لا يجب أن تتحول إلى متطلبات قاعدة بيانات في هذه المرحلة.

------------------------------------------------------------------------

# 6. Actors

  -----------------------------------------------------------------------
  Actor                               Responsibility Evidence
  ----------------------------------- -----------------------------------
  Patient                             حجز المواعيد والوصول إلى بياناته
                                      وتقاريره وفواتيره

  Receptionist                        تسجيل المرضى، المواعيد، الإدخال،
                                      النقل، الخروج

  Doctor                              الرعاية السريرية، التشخيص،
                                      الملاحظات، الوصفات، طلب الفحوصات

  Lab Technician                      معالجة طلبات المختبر ورفع التقارير

  Pharmacist                          التحقق من الوصفات وصرف الأدوية
                                      وإدارة المخزون

  Accountant                          الفواتير، التأمين، المدفوعات،
                                      التقارير المالية

  Admin                               إدارة المستخدمين والأدوار
                                      والصلاحيات والأطباء والأقسام
                                      والتقارير

  Administrator                       النسخ الاحتياطي ومراقبة صحة النظام

  System                              الإشعارات، التحقق، العمليات الآلية،
                                      التنبيهات
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 7. Functional Requirements

## FR-01 → FR-17

  ID      Requirement
  ------- -------------------------------------------------------
  FR-01   تسجيل دخول جميع الموظفين باسم مستخدم وكلمة مرور فريدة
  FR-02   التحقق من بيانات الدخول ومنح الوصول حسب الدور
  FR-03   إعادة تعيين كلمة المرور عبر البريد المسجل
  FR-04   إنشاء وتعديل وحذف حسابات المستخدمين بواسطة Admin
  FR-05   إسناد الأدوار والصلاحيات للمستخدمين
  FR-06   إدارة ملفات الأطباء والتخصص والقسم
  FR-07   إنشاء وإدارة أقسام المستشفى
  FR-08   تسجيل المرضى ببيانات شخصية وطبية
  FR-09   منح كل مريض معرفاً فريداً
  FR-10   تحديث بيانات المريض
  FR-11   حجز وإلغاء وإعادة جدولة المواعيد
  FR-12   فحص تعارضات المواعيد قبل التأكيد
  FR-13   إضافة المرضى إلى قائمة الانتظار عند عدم وجود مواعيد
  FR-14   إدخال المريض وتعيين الجناح والسرير
  FR-15   نقل المريض بين الأجنحة
  FR-16   إخراج المريض بعد تسوية جميع الفواتير
  FR-17   تمكين الطبيب من مشاهدة التاريخ والسجل الطبي الكامل

## FR-18 → FR-34

  ID      Requirement
  ------- -----------------------------------------------
  FR-18   تسجيل التشخيصات والملاحظات السريرية
  FR-19   إنشاء وصفات رقمية
  FR-20   طلب فحوصات مخبرية وتحديد معلماتها
  FR-21   معالجة طلبات المختبر ورفع النتائج
  FR-22   إشعار الطبيب والمريض عند رفع التقرير
  FR-23   التحقق من الوصفات قبل صرف الأدوية
  FR-24   صرف الأدوية وتحديث المخزون تلقائياً
  FR-25   ضبط تنبيهات إعادة التخزين
  FR-26   تتبع الأدوية القريبة من الانتهاء
  FR-27   إنشاء فواتير مفصلة لخدمات المريض
  FR-28   تطبيق التغطية التأمينية
  FR-29   تسجيل المدفوعات وإصدار الإيصالات
  FR-30   إنشاء التقارير المالية
  FR-31   تنفيذ النسخ الاحتياطي يدوياً أو تلقائياً
  FR-32   مراقبة صحة وأداء النظام
  FR-33   إرسال الإشعارات الآلية
  FR-34   تمكين المريض من مشاهدة ملفه وتقاريره وفواتيره

------------------------------------------------------------------------

# 8. Non-Functional Requirements

  -----------------------------------------------------------------------
  ID                      Category                Requirement
  ----------------------- ----------------------- -----------------------
  NFR-01                  Performance             دعم 500 مستخدم متزامن
                                                  على الأقل

  NFR-02                  Security                فرض RBAC

  NFR-03                  Security                تشفير كلمات المرور
                                                  والبيانات الحساسة

  NFR-04                  Speed                   الإجراءات الشائعة أقل
                                                  من 3 ثوانٍ تحت الحمل
                                                  الطبيعي

  NFR-05                  Usability               قابلية الاستخدام
                                                  للموظفين غير التقنيين

  NFR-06                  Reliability             توفر لا يقل عن 99%

  NFR-07                  Scalability             تحمل نمو بيانات المرضى
                                                  والمعاملات لسنوات

  NFR-08                  Backup                  نسخ احتياطي يومي تلقائي
                                                  ونسخ يدوي عند الحاجة

  NFR-09                  Compatibility           دعم Chrome وFirefox
                                                  وEdge وSafari

  NFR-10                  Availability            إتاحة 24/7 مع أقل توقف
                                                  مخطط ممكن

  NFR-11                  Maintainability         تصميم Modular قابل
                                                  للتحديث والاستبدال

  NFR-12                  Data Integrity          منع سجلات المرضى
                                                  المكررة والتحقق من
                                                  البيانات قبل الحفظ
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 9. Requirement Landscape

``` mermaid
mindmap
  root((HMS Requirements))
    Administration
      Authentication
      Users
      Roles
      Permissions
      Doctors
      Departments
    Patient Management
      Registration
      Patient ID
      Updates
      Appointments
      Waitlist
    Inpatient
      Admission
      Ward
      Bed
      Transfer
      Discharge
    Clinical Care
      History
      Medical Record
      Diagnosis
      Observations
      Prescription
    Laboratory
      Lab Request
      Test Parameters
      Processing
      Lab Report
      Notifications
    Pharmacy
      Prescription Verification
      Medicine Issue
      Inventory
      Restock
      Expiry
    Finance
      Billing
      Insurance
      Payments
      Receipts
      Financial Reports
    System Services
      Backup
      Health Monitoring
      Notifications
    Patient Portal
      Profile
      Lab Reports
      Bills
```

------------------------------------------------------------------------

# 10. Use Case Landscape

الـ SRS يحتوي على 50 Use Cases موزعة على مجالات النظام:

  Group                     Use Cases
  ------------------------- ---------------
  General System Services   UC-01 → UC-04
  Administration & HR       UC-05 → UC-11
  Patient Access            UC-12 → UC-17
  Ward & Bed Management     UC-18 → UC-21
  Clinical Care             UC-22 → UC-29
  Laboratory                UC-30 → UC-33
  Pharmacy                  UC-34 → UC-38
  Financial Services        UC-39 → UC-44
  System/Admin Services     UC-45 → UC-47
  Patient Self Services     UC-48 → UC-50

``` mermaid
flowchart LR
    U["Use Cases 01–50"]

    U --> G["General"]
    U --> A["Administration"]
    U --> P["Patient Access"]
    U --> W["Ward & Bed"]
    U --> C["Clinical Care"]
    U --> L["Laboratory"]
    U --> PH["Pharmacy"]
    U --> F["Financial"]
    U --> S["System Services"]
    U --> PS["Patient Self-Service"]
```

------------------------------------------------------------------------

# 11. Core Business Process Map

``` mermaid
flowchart TD
    START["Patient enters hospital"]

    START --> REG["Register / Identify Patient"]
    REG --> APPT["Appointment"]
    APPT --> CLINIC["Clinical Care"]

    CLINIC --> DIAG["Diagnosis / Observations"]
    DIAG --> RX["Prescription"]
    DIAG --> LABREQ["Lab Request"]

    RX --> PHARM["Prescription Verification"]
    PHARM --> DISP["Medicine Issue"]
    DISP --> STOCK["Inventory Update"]

    LABREQ --> LABPROC["Lab Processing"]
    LABPROC --> REPORT["Lab Report"]
    REPORT --> NOTIFY["Notification"]

    START --> ADMIT["Admission"]
    ADMIT --> BED["Ward / Bed Assignment"]
    BED --> TRANSFER["Transfer"]
    TRANSFER --> BED

    CLINIC --> BILL["Billing"]
    DISP --> BILL
    REPORT --> BILL
    BED --> BILL

    BILL --> INS["Insurance"]
    INS --> PAYMENT["Payment"]
    PAYMENT --> RECEIPT["Receipt"]

    PAYMENT --> CHECK{"All Bills Cleared?"}
    CHECK -->|Yes| DISCHARGE["Discharge"]
    CHECK -->|No| CHECK

    DISCHARGE --> END["Patient Discharged"]
```

> هذا المخطط يمثل تدفقاً تجميعياً مستنداً إلى حالات الاستخدام والمتطلبات،
> وليس Workflow تقنياً نهائياً.

------------------------------------------------------------------------

# 12. Business Events Extracted From Requirements

الأحداث التالية تظهر مباشرة أو بصورة لازمة من سلوكيات الـ SRS:

``` mermaid
flowchart TB
    subgraph Patient["Patient Lifecycle"]
        E1["Patient Registered"]
        E2["Appointment Booked"]
        E3["Appointment Cancelled / Rescheduled"]
        E4["Patient Admitted"]
        E5["Patient Transferred"]
        E6["Patient Discharged"]
    end

    subgraph Clinical["Clinical Events"]
        E7["Diagnosis Recorded"]
        E8["Observation Recorded"]
        E9["Prescription Created"]
        E10["Lab Requested"]
    end

    subgraph Lab["Laboratory Events"]
        E11["Lab Processing Started"]
        E12["Lab Report Uploaded"]
    end

    subgraph Pharmacy["Pharmacy Events"]
        E13["Prescription Verified"]
        E14["Medicine Issued"]
        E15["Stock Alert"]
        E16["Expiry Flag"]
    end

    subgraph Finance["Financial Events"]
        E17["Bill Generated"]
        E18["Insurance Applied"]
        E19["Payment Recorded"]
        E20["Receipt Issued"]
    end
```

------------------------------------------------------------------------

# 13. Business Rules

هذه القواعد هي خلاصة سلوكية مستخرجة من المتطلبات وحالات الاستخدام، وليست
مخطط SQL.

  ID      Rule
  ------- -------------------------------------------------------
  BR-01   لكل مريض معرف فريد
  BR-02   يجب التحقق من عدم وجود سجل مريض مكرر قبل التسجيل
  BR-03   فحص تعارض المواعيد قبل تأكيد الحجز
  BR-04   سبب الإلغاء/إعادة الجدولة مطلوب
  BR-05   إلغاء الموعد خلال ساعة يتطلب موافقة Admin حسب UC
  BR-06   قائمة الانتظار تعمل بترتيب الوصول
  BR-07   لا يتم إدخال المريض إلا مع توفر سرير
  BR-08   النقل يتطلب توفر السرير في الوجهة
  BR-09   تحرير السرير القديم عند النقل
  BR-10   تسجيل تاريخ ووقت وسبب النقل
  BR-11   لا يتم إخراج المريض قبل تسوية الفواتير
  BR-12   إنشاء ملخص خروج وإرفاقه بالسجل
  BR-13   التشخيص مطلوب قبل إنشاء الوصفة للحالة الحالية
  BR-14   الوصفة ترسل إلى الصيدلية
  BR-15   عند عدم توفر الدواء يتم تنبيه الطبيب
  BR-16   طلب المختبر يمر بحالة معالجة قبل الاكتمال
  BR-17   التقرير يرتبط بطلب الفحص والمريض والطبيب حسب SRS
  BR-18   لا يصرف الدواء قبل التحقق من الوصفة
  BR-19   الكمية السالبة للمخزون غير صالحة
  BR-20   التنبيه يظهر عند الوصول إلى حد إعادة التخزين
  BR-21   الأدوية القريبة من الانتهاء يتم تعليمها
  BR-22   الفاتورة يجب أن تكون مفصلة حسب نوع الخدمة
  BR-23   الدفع الأكبر من الرصيد المستحق مرفوض
  BR-24   المدفوعات الجزئية مسموحة ويتم تتبعها
  BR-25   إصدار الإيصال يتطلب وجود دفعة
  BR-26   الإشعارات المطلوبة ترسل خلال المدة المحددة في الـ SRS
  BR-27   فشل الإشعار يعاد حتى 3 مرات وفق المتطلب
  BR-28   المريض يرى بياناته وتقاريره وفواتيره الخاصة به فقط

------------------------------------------------------------------------

# 14. Lifecycle Models

## Appointment

``` mermaid
stateDiagram-v2
    [*] --> Booked
    Booked --> Cancelled
    Booked --> Rescheduled
    Rescheduled --> Booked
```

## Laboratory Request

``` mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> InProgress
    InProgress --> Completed
```

## Prescription Verification

``` mermaid
stateDiagram-v2
    [*] --> PendingVerification
    PendingVerification --> Verified
    PendingVerification --> FlaggedForReview
```

## Inpatient Status

``` mermaid
stateDiagram-v2
    [*] --> InPatient
    InPatient --> Discharged
```

> لم تتم إضافة حالات أخرى غير مثبتة في الـ SRS.

------------------------------------------------------------------------

# 15. Data Concepts Explicitly Evidenced by the SRS

المفاهيم التالية تظهر في الـ SRS أو ER Diagram:

``` mermaid
erDiagram
    PATIENT
    APPOINTMENT
    DOCTOR
    PRESCRIPTION
    STAFF
    MEDICINE
    DIAGNOSIS
    LAB_REQUEST
    LAB_REPORT
    WARD
    BED
    BILL
    PAYMENT
```

## Core Concepts

  Concept        Evidence
  -------------- ----------------------------------------
  Patient        FR-08..FR-10, UC-12..UC-17
  Doctor         FR-06, FR-17..FR-22
  Department     FR-06..FR-07
  Appointment    FR-11..FR-13
  Prescription   FR-19, FR-23..FR-24
  Medicine       FR-19, FR-24..FR-26
  Diagnosis      FR-18
  Lab Request    FR-20..FR-21
  Lab Report     FR-21..FR-22
  Ward           FR-14..FR-15
  Bed            FR-14..FR-15
  Bill           FR-27..FR-30
  Payment        FR-29
  Staff          Appears in the SRS conceptual ER model

------------------------------------------------------------------------

# 16. Conceptual Relationship Evidence

العلاقات التالية يمكن تتبعها إلى المتطلبات دون تحويلها بعد إلى PK/FK:

``` mermaid
flowchart LR
    Patient["Patient"]

    Patient --> Appointment["Appointment"]
    Doctor["Doctor"] --> Appointment

    Patient --> Admission["Admission / Inpatient context"]
    Ward["Ward"] --> Bed["Bed"]
    Bed --> Admission

    Patient --> Diagnosis["Diagnosis"]
    Doctor --> Diagnosis

    Patient --> Prescription["Prescription"]
    Doctor --> Prescription

    Patient --> LabRequest["Lab Request"]
    Doctor --> LabRequest
    LabRequest --> LabReport["Lab Report"]

    Prescription --> Medicine["Medicine"]
    Medicine --> Inventory["Inventory context"]

    Patient --> Bill["Bill"]
    Bill --> Payment["Payment"]
```

> بعض المفاهيم مثل `Admission` و`Inventory context` ظهرت من سلوك
> المتطلبات، بينما تفاصيلها الداخلية غير محددة في الـ SRS.

------------------------------------------------------------------------

# 17. Traceability Matrix

## Requirement → Business Area

  Requirement Range   Business Area
  ------------------- --------------------------------
  FR-01..FR-05        Authentication & Authorization
  FR-06..FR-07        Administration
  FR-08..FR-10        Patient Management
  FR-11..FR-13        Appointments
  FR-14..FR-16        Inpatient / Ward / Bed
  FR-17..FR-20        Clinical Care
  FR-21..FR-22        Laboratory
  FR-23..FR-26        Pharmacy
  FR-27..FR-30        Finance
  FR-31..FR-33        System Services
  FR-34               Patient Portal

## Requirement → Data Concept

``` mermaid
flowchart LR
    FR08["FR-08 Registration"] --> Patient["Patient"]
    FR09["FR-09 Unique ID"] --> Patient

    FR11["FR-11 Appointment"] --> Appointment["Appointment"]
    FR12["FR-12 Conflict"] --> Appointment

    FR14["FR-14 Admission"] --> Ward["Ward"]
    FR14 --> Bed["Bed"]

    FR18["FR-18 Diagnosis"] --> Diagnosis["Diagnosis"]
    FR19["FR-19 Prescription"] --> Prescription["Prescription"]

    FR20["FR-20 Lab Request"] --> LabRequest["Lab Request"]
    FR21["FR-21 Lab Result"] --> LabReport["Lab Report"]

    FR24["FR-24 Issue Medicine"] --> Medicine["Medicine"]
    FR24 --> Inventory["Inventory"]

    FR27["FR-27 Billing"] --> Bill["Bill"]
    FR29["FR-29 Payment"] --> Payment["Payment"]
```

------------------------------------------------------------------------

# 18. Use Case → Business Event Traceability

  Use Case                        Business Event
  ------------------------------- -------------------------------------
  UC-12 Register Patient          Patient Registered
  UC-13 Update Patient            Patient Information Updated
  UC-15 Book Appointment          Appointment Booked
  UC-16 Cancel/Reschedule         Appointment Cancelled / Rescheduled
  UC-17 Waitlist                  Patient Added to Waitlist
  UC-18 Admit Patient             Patient Admitted
  UC-20 Transfer Patient          Patient Transferred
  UC-21 Discharge                 Patient Discharged
  UC-25 Diagnose Patient          Diagnosis Recorded
  UC-26 Record Observations       Observation Recorded
  UC-27 Prescribe Medicine        Prescription Created
  UC-28 Request Lab Test          Lab Requested
  UC-30 Process Lab Test          Lab Processing
  UC-31 Upload Lab Report         Lab Report Uploaded
  UC-34 Verify Prescription       Prescription Verified
  UC-35 Issue Medicine            Medicine Issued
  UC-39 Generate Bill             Bill Generated
  UC-40 Apply Insurance           Insurance Applied
  UC-41 Record Payment            Payment Recorded
  UC-42 Issue Receipt             Receipt Issued
  UC-47 Automated Notifications   Notification Sent

------------------------------------------------------------------------

# 19. Security & Data Integrity Evidence

``` mermaid
flowchart TB
    USER["User"]
    AUTH["Authentication"]
    RBAC["Role-Based Access Control"]
    VALIDATE["Input Validation"]
    INTEGRITY["Data Integrity"]
    DATA["Hospital Data"]

    USER --> AUTH
    AUTH --> RBAC
    RBAC --> VALIDATE
    VALIDATE --> INTEGRITY
    INTEGRITY --> DATA
```

متطلبات مرتبطة:

-   `FR-01` → Authentication
-   `FR-02` → Role-based access
-   `FR-04..FR-05` → User/Roles/Permissions
-   `NFR-02` → RBAC
-   `NFR-03` → Encryption
-   `NFR-12` → Duplicate prevention + validation

------------------------------------------------------------------------

# 20. Audit Evidence

الـ SRS يفرض بعض آثار التدقيق، منها:

  Area                      Evidence
  ------------------------- ----------------------------------------
  Patient update            تسجيل التغيير مع التاريخ والوقت
  Patient transfer          تسجيل التاريخ والوقت والسبب
  Diagnosis logs            لا يمكن حذفها
  Medicine expiry removal   الإزالة تسجل
  Notifications             تسجيل فشل الإرسال
  Backup                    تسجيل نتيجة العملية والتنبيه عند الفشل
  Health checks             تسجيل نتائج الفحص

> لا يعني ذلك أن نموذج الـ Audit النهائي قد تم تصميمه. طريقة التخزين ما
> زالت قراراً لاحقاً.

------------------------------------------------------------------------

# 21. Important Unspecified Areas

هذه النقاط **ليست متطلبات ناقصة يجب اختراعها**؛ بل عناصر تحتاج قراراً قبل
تصميم النموذج المنطقي.

  -----------------------------------------------------------------------
  Area                                Current Status
  ----------------------------------- -----------------------------------
  Patient full attribute set          `UNSPECIFIED`

  Medical Record internal structure   `UNSPECIFIED`

  Visit / Encounter model             `UNSPECIFIED`

  Appointment duration/slot structure `UNSPECIFIED`

  Doctor working schedule             `UNSPECIFIED`

  Ward → Room hierarchy               `UNSPECIFIED`

  Bed lifecycle states                `UNSPECIFIED` beyond
                                      availability/occupancy behavior

  Admission structure                 `UNSPECIFIED`

  Diagnosis coding standard           `UNSPECIFIED`

  Observation types/units             `UNSPECIFIED`

  Prescription line/item structure    `UNSPECIFIED`

  Laboratory test catalog             `UNSPECIFIED`

  Lab reference ranges                `UNSPECIFIED`

  Medicine batch/lot model            `UNSPECIFIED`

  Inventory locations                 `UNSPECIFIED`

  Insurance fields/rules              `UNSPECIFIED`

  Tax/discount rules                  `UNSPECIFIED`

  Currency model                      `UNSPECIFIED`

  Payment method values               `UNSPECIFIED`

  Refunds                             Not specified

  Credit notes                        Not specified

  Purchasing                          Not specified

  Suppliers                           Not specified

  General Ledger / Chart of Accounts  Not specified

  Journal Entries                     Not specified

  External insurance integration      Explicitly outside scope

  Mobile application                  Explicitly outside scope
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 22. Critical Ambiguities

## Staff vs. Role-based Actors

الـ SRS يستخدم Actors مثل:

``` text
Receptionist
Doctor
Lab Technician
Pharmacist
Accountant
Admin
Administrator
Patient
```

وفي الـ conceptual ER model يظهر مفهوم `Staff`.

لذلك:

``` text
Actor / Role
      │
      ├── Business responsibility
      │
      └── Possible data representation
```

لكن العلاقة الدقيقة بين `Staff`, `User`, `Role`, و`Doctor` **لا يجب
حسمها في Phase 01**.

------------------------------------------------------------------------

# 23. Requirements Quality Gate

قبل الانتقال إلى Phase 02 يجب أن نستطيع الإجابة عن:

-   ما الذي يجب أن يفعله النظام؟
-   من يقوم بكل عملية؟
-   ما هي حدود النظام؟
-   ما هي الحالات الرئيسية؟
-   ما هي الأحداث التجارية؟
-   ما هي قواعد العمل الصريحة؟
-   ما هي المفاهيم البيانية التي ظهرت فعلاً؟
-   ما الذي لم يحدده الـ SRS؟
-   ما الذي يحتاج قراراً من صاحب المشروع؟

``` mermaid
flowchart TD
    A["SRS Reviewed"] --> B{"Scope Clear?"}
    B -->|Yes| C{"Requirements Extracted?"}
    B -->|No| X["Open Issue"]

    C -->|Yes| D{"Use Cases Mapped?"}
    C -->|No| X

    D -->|Yes| E{"Business Rules Identified?"}
    D -->|No| X

    E -->|Yes| F{"Data Evidence Mapped?"}
    E -->|No| X

    F -->|Yes| G{"Unknowns Documented?"}
    F -->|No| X

    G -->|Yes| H["Phase 01 Baseline"]
    G -->|No| X
```

------------------------------------------------------------------------

# 24. What Phase 01 Does NOT Contain

هذه المرحلة لا تحتوي على:

``` text
❌ SQL Tables
❌ Primary Keys
❌ Foreign Keys
❌ SQL Data Types
❌ Indexes
❌ Stored Procedures
❌ Views
❌ EF Core Entities
❌ Migrations
❌ DBMS-specific syntax
❌ Physical storage decisions
```

الانتقال الصحيح:

``` text
Phase 01
Requirements
   ↓
Phase 02
Domain Modeling
   ↓
Phase 03
Conceptual Data Modeling
   ↓
Phase 04
Logical Data Modeling
   ↓
Phase 05
Physical Database Design
   ↓
Phase 06
Implementation
```

------------------------------------------------------------------------

# 25. Phase 01 → Phase 02 Contract

Phase 02 يجب أن يبدأ من هذا المستند، وليس من SQL.

### Inputs

-   Functional Requirements
-   Non-Functional Requirements
-   Actors
-   Use Cases
-   Scope
-   Business Rules
-   Business Events
-   Explicit Data Concepts
-   Open Issues

### Outputs المتوقعة في Phase 02

``` text
Business Concepts
        ↓
Business Events
        ↓
Relationships
        ↓
Cardinalities
        ↓
States & Lifecycles
        ↓
Domain Boundaries
        ↓
Conceptual Domain Model
```

------------------------------------------------------------------------

# 26. Engineering Principle

المشروع لا يتبع المسار:

``` text
"أفكر في جدول → أكتب SQL → أكتشف المتطلبات لاحقاً"
```

بل:

``` mermaid
flowchart LR
    REQ["Requirements"]
    RULES["Business Rules"]
    EVENTS["Business Events"]
    CONCEPTS["Business Concepts"]
    DOMAIN["Domain Model"]
    CONCEPTUAL["Conceptual Model"]
    LOGICAL["Logical Model"]
    PHYSICAL["Physical Design"]
    SQL["Implementation"]

    REQ --> RULES
    RULES --> EVENTS
    EVENTS --> CONCEPTS
    CONCEPTS --> DOMAIN
    DOMAIN --> CONCEPTUAL
    CONCEPTUAL --> LOGICAL
    LOGICAL --> PHYSICAL
    PHYSICAL --> SQL
```

------------------------------------------------------------------------

# 27. Repository Placement

هذا المستند يمثل محتوى:

``` text
phase/
└── 01-requirements/
    ├── README.md
    ├── requirements-analysis.md
    ├── functional-requirements.md
    ├── non-functional-requirements.md
    └── traceability.md
```

أو، إذا أردت وثيقة واحدة قوية للمرحلة:

``` text
docs/
└── 01-requirements/
    └── README.md
```

### Recommended

اعتبار `README.md` هو **بوابة المرحلة**، مع نقل الجداول التفصيلية لاحقاً
إلى ملفات منفصلة عندما يكبر المشروع.

------------------------------------------------------------------------

# 28. Suggested Git Commit

``` bash
git add docs/01-requirements/README.md

git commit -m "docs(requirements): establish phase 01 requirements baseline"
```

------------------------------------------------------------------------

# 29. Phase 01 Definition of Done

لا تعتبر المرحلة الأولى مكتملة إلا إذا:

-   [x] تم توثيق نطاق النظام
-   [x] تم توثيق ما هو خارج النطاق
-   [x] تم توثيق Actors
-   [x] تم استخراج FR-01 → FR-34
-   [x] تم استخراج NFR-01 → NFR-12
-   [x] تم تنظيم Use Cases
-   [x] تم استخراج Business Rules
-   [x] تم تحديد Business Events
-   [x] تم توثيق Data Concepts الظاهرة في SRS
-   [x] تم بناء Traceability
-   [x] تم توثيق Lifecycle Models المطلوبة
-   [x] تم توثيق Audit Evidence
-   [x] تم فصل المتطلبات عن الاستنتاجات
-   [x] تم توثيق العناصر غير المحددة
-   [x] لم يتم اختراع Schema أو SQL

------------------------------------------------------------------------

# 30. Final Baseline

``` text
                    ┌──────────────────────┐
                    │         SRS          │
                    │  Source of Truth     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  PHASE 01            │
                    │  Requirements        │
                    │  Analysis            │
                    └──────────┬───────────┘
                               │
          ┌────────────────────┼────────────────────┐
          ▼                    ▼                    ▼
     Requirements         Business Rules       Use Cases
          │                    │                    │
          └────────────────────┼────────────────────┘
                               ▼
                    ┌──────────────────────┐
                    │ Business Events      │
                    │ & Data Evidence      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ PHASE 02             │
                    │ Domain Modeling      │
                    └──────────────────────┘
```

## Core Rule

> **No undocumented assumption becomes a database fact.**

أي عنصر غير موجود في الـ SRS أو غير مشتق منه بشكل قابل للتتبع يجب أن
يبقى:

`UNSPECIFIED` → `OPEN-ISSUE` → `DECISION` → ثم يدخل إلى التصميم.

------------------------------------------------------------------------

## Source

**Primary source:** `HMS_SRS_Report_62669_62338_63780(2).pdf`

هذه الوثيقة تعكس متطلبات الـ SRS كما تم تحليلها، ولا تضيف متطلبات
تشغيلية جديدة إلى النظام.
