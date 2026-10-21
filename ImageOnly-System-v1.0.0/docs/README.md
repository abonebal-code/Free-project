<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Tajawal&size=30&duration=3000&pause=1000&color=FF3333&center=true&vCenter=true&width=600&lines=%F0%9F%96%BC%EF%B8%8F+ImageOnly+System+v1.0.0;%D9%86%D8%B8%D8%A7%D9%85+%D9%81%D9%84%D8%AA%D8%B1%D8%A9+%D8%A7%D9%84%D9%88%D8%B3%D8%A7%D8%A6%D8%B7+%D8%A7%D9%84%D8%B0%D9%83%D9%8A" alt="Typing SVG" />

<br/>

![Discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![Node.js](https://img.shields.io/badge/node.js-18%2B-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Multi-Server](https://img.shields.io/badge/Multi--Server-✓-57f287?style=for-the-badge)
![Hot Reload](https://img.shields.io/badge/Hot--Reload-✓-faa61a?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

<br/>

> **نظام ذكي لفلترة القنوات وضمان أنها تحتوي على وسائط فقط داخل Discord**  
> يحذف أي رسالة نصية أو ستيكر تلقائياً، مع تحذيرات مخصصة ودعم كامل لسيرفرات متعددة.

</div>

---

## 📋 المحتويات

- [✨ الميزات](#-الميزات)
- [⚙️ كيف يعمل](#️-كيف-يعمل)
- [🗂️ هيكل المشروع](#️-هيكل-المشروع)
- [🚀 طريقة التشغيل](#-طريقة-التشغيل)
- [🔧 إعداد السيرفرات](#-إعداد-السيرفرات)
- [🎯 قواعد الفلترة](#-قواعد-الفلترة)
- [🔤 متغيرات رسائل التحذير](#-متغيرات-رسائل-التحذير)
- [📊 مخطط سير العمل](#-مخطط-سير-العمل)

---

## ✨ الميزات

<table>
<tr>
<td width="50%">

### 🎯 فلترة ذكية للوسائط
- كشف الصور والفيديوهات بـ 3 طبقات فحص متتالية
- دعم مرفقات مباشرة، روابط، وـ Discord Embeds
- قائمة ضخمة من نطاقات الوسائط المعروفة (35+)

### 🤖 تحكم كامل بالبوتات
- حظر رسائل البوتات في القنوات المحمية
- قائمة استثناء للبوتات المسموح لها صراحةً
- رسالة تحذير مستقلة خاصة بالبوتات

</td>
<td width="50%">

### 🏠 متعدد السيرفرات
- كل سيرفر له ملف إعدادات منفصل تماماً
- إضافة سيرفر جديد بمجرد إنشاء مجلد
- الجلسات معزولة تماماً بين السيرفرات

### 🔥 Hot Reload
- إعادة تحميل تلقائية عند تعديل أي إعداد
- لا حاجة لإعادة تشغيل البوت أبداً
- نظام Debounce يمنع التحميل المزدوج

### 🔒 نظام صلاحيات مرن
- رتب معفاة من جميع القيود
- بوتات معفاة بشكل انتقائي

### ⚠️ تحذيرات مخصصة بالكامل
- نص عادي أو Embed — الاختيار لك
- حذف تلقائي للتحذير بعد مدة محددة
- متغيرات ديناميكية داخل نص التحذير

</td>
</tr>
</table>

---

## ⚙️ كيف يعمل

```
1. يصل عضو إلى قناة محمية ويرسل رسالة
2. النظام يتحقق: هل الرسالة تحتوي وسائط مقبولة؟

   ✅ صورة / فيديو مرفوع  →  تُترك الرسالة
   ✅ رابط من نطاق وسائط  →  تُترك الرسالة
   ✅ Embed يحتوي وسائط   →  تُترك الرسالة
   ✅ صاحب رتبة معفاة     →  يُتجاهل تماماً

   ❌ نص فقط              →  حذف + تحذير
   ❌ ستيكر               →  حذف + تحذير
   ❌ رسالة بوت            →  حذف + تحذير خاص بالبوت
```

---

## �️ هيكل المشروع

```
ImageOnly-System-v1.0.0/
│
├── 📄 index.js                     ← نقطة الدخول — تهيئة البوت وتحميل الأحداث
├── 📄 config.js                    ← الكونفيج الرئيسي (مسار .env + التوكن + مجلد الإعدادات)
├── 📄 package.json
├── 📄 .env.example                 ← مثال لملف التوكن
│
├── 📁 configs/                     ← إعدادات السيرفرات (مجلد لكل سيرفر)
│   └── 📁 my-server/
│       └── config.js               ← إعدادات السيرفر
│
├── 📁 src/
│   ├── 📁 events/
│   │   └── messageCreate.js        ← الحدث الوحيد المستمع
│   ├── 📁 features/
│   │   └── imageOnly.js            ← منطق الفلترة الأساسي
│   └── 📁 utils/
│       ├── configLoader.js         ← تحميل الإعدادات والـ hot-reload
│       └── logger.js               ← نظام تسجيل الأحداث
│
└── 📁 logs/
    └── activity.log                ← سجل العمليات (يُمسح عند كل تشغيل)
```

---

## 🚀 طريقة التشغيل

### المتطلبات

| المتطلب | الإصدار |
|---------|---------|
| Node.js | `18.0.0` أو أحدث |
| discord.js | `v14` |

> **ملاحظة:** يعمل هذا النظام بشكل **مستقل** بتوكن بوت خاص به، أو يمكن تضمينه داخل بوت Discord.js موجود.

### التثبيت

**1. ثبّت المكتبات:**
```bash
npm install
```

**2. أنشئ ملف `.env`:**

انسخ `.env.example` وسمّه `.env`، ثم ضع فيه توكن البوت:
```env
TOKEN=YOUR_BOT_TOKEN_HERE
```

> اسم المتغير يجب أن يطابق قيمة `tokenEnvKey` في `config.js`

**3. شغّل النظام:**

```bash
# تشغيل مستقل
node index.js
```

أو استدعاء من بوتك الرئيسي:
```js
require('./Codes/ImageOnly-System-v1.0.0/index')(client);
```

### صلاحيات البوت المطلوبة

| الصلاحية | الهدف |
|----------|-------|
| `Manage Messages` | حذف الرسائل المخالفة |
| `Send Messages` | إرسال رسائل التحذير |
| `Embed Links` | إرسال التحذيرات بشكل Embed |
| `View Channels` | رؤية القنوات المحمية |
| `Read Message History` | قراءة الرسائل الواردة |

> **مهم:** يجب تفعيل صلاحية `Message Content Intent` من بوابة Discord Developer Portal.

---

## 🔧 إعداد السيرفرات

### الكونفيج الرئيسي — `config.js`

```js
module.exports = {
  envPath:     '../../.env',   // مسار ملف .env نسبةً لجذر النظام
  tokenEnvKey: 'TOKEN',        // اسم المتغير في .env الذي يحتوي التوكن
  configsDir:  'configs',      // مجلد كونفيجات السيرفرات
  modulesPath: '../../node_modules', // مسار المكتبات المشتركة (اختياري)
};
```

| المفتاح | الوصف |
|---------|-------|
| `envPath` | مسار ملف `.env` نسبةً لجذر النظام |
| `tokenEnvKey` | اسم المتغير في `.env` الذي يحتوي التوكن |
| `configsDir` | مجلد كونفيجات السيرفرات |
| `modulesPath` | مسار `node_modules` مشترك (fallback بعد المحلي) |

---

### إضافة سيرفر جديد

**1. أنشئ مجلداً بأي اسم داخل `configs/`:**
```
configs/
└── my-server-name/
    └── config.js     ← أنشئ هذا الملف
```

> اسم المجلد حر — النظام يقرأ `guildId` من داخل الملف تلقائياً.

**2. انسخ هذا القالب واملأه:**

```js
module.exports = {

  // ─── معلومات السيرفر ────────────────────────────────────────────
  guildId: 'YOUR_GUILD_ID_HERE',   // ← مطلوب

  // ─── القنوات المحمية ────────────────────────────────────────────
  imageOnlyChannels: [
    'CHANNEL_ID_1',   // مثال: قناة-الصور
    'CHANNEL_ID_2',   // مثال: قناة-الفيديوهات
  ],

  // ─── الرتب المعفاة ──────────────────────────────────────────────
  exemptRoles: [
    'ROLE_ID_ADMIN',
    'ROLE_ID_MOD',
  ],

  // ─── البوتات ────────────────────────────────────────────────────
  blockBots: true,        // حظر رسائل البوتات؟
  exemptBots: [
    'BOT_ID_1',           // بوتات مسموح لها رغم blockBots: true
  ],

  // ─── الستيكرات ──────────────────────────────────────────────────
  blockStickers: true,    // حظر الستيكرات؟

  // ─── رسالة التحذير (للأعضاء المخالفين) ─────────────────────────
  warning: {
    enabled:     true,    // تفعيل التحذير
    deleteAfter: 6,       // حذف التحذير بعد كم ثانية (0 = لا تحذف)
    useEmbed:    true,    // Embed أم نص عادي؟

    embed: {
      color:       '#FF3333',
      title:       '🚫 قناة الصور والفيديوهات فقط',
      description: '> يا {user}، تم حذف رسالتك ❌\n\nهذه القناة **مخصصة للوسائط فقط**.',
      thumbnail:   '',    // رابط صورة، أو اتركه فارغاً (صورة المخالف تلقائياً)
      footer:      '⏳ سيُحذف هذا التنبيه بعد {seconds} ثوانٍ',
    },

    // نص عادي — يُستخدم فقط إذا useEmbed = false
    message: 'يا {user} ❌ هذه القناة للوسائط فقط! يُحذف بعد {seconds} ثوانٍ.',
  },

  // ─── رسالة تحذير البوتات ────────────────────────────────────────
  botWarning: {
    enabled:     true,    // false = حذف صامت بدون رسالة
    deleteAfter: 8,

    useEmbed: true,
    embed: {
      color:       '#5865F2',
      title:       '🤖 وصول بوت مرفوض',
      description: '> البوت {user} حاول الإرسال في {channel}\n\n**هذه القناة مخصصة للأعضاء فقط.**',
      thumbnail:   '',
      footer:      '⏳ سيُحذف هذا التنبيه بعد {seconds} ثوانٍ',
    },

    message: '🤖 البوت {user} ممنوع هنا! يُحذف بعد {seconds} ثوانٍ.',
  },

};
```

---

### جدول خيارات إعداد السيرفر

| الخيار | النوع | الوصف |
|--------|-------|-------|
| `guildId` | `string` | ID السيرفر على Discord — **مطلوب** |
| `imageOnlyChannels` | `string[]` | IDs القنوات المحمية |
| `exemptRoles` | `string[]` | رولات معفاة من جميع القيود |
| `blockBots` | `boolean` | حظر رسائل البوتات (افتراضي: `true`) |
| `exemptBots` | `string[]` | IDs بوتات مسموح لها رغم `blockBots: true` |
| `blockStickers` | `boolean` | حظر الستيكرات (افتراضي: `true`) |
| `warning.enabled` | `boolean` | تفعيل/تعطيل رسالة التحذير |
| `warning.deleteAfter` | `number` | ثواني قبل حذف التحذير (`0` = لا يُحذف) |
| `warning.useEmbed` | `boolean` | Embed أم نص عادي |
| `warning.embed.color` | `string` | لون الـ Embed (هيكس مثل `#FF3333`) |
| `warning.embed.title` | `string` | عنوان الـ Embed |
| `warning.embed.description` | `string` | نص الـ Embed (يدعم المتغيرات) |
| `warning.embed.thumbnail` | `string` | رابط صورة جانبية (فارغ = صورة المخالف) |
| `warning.embed.footer` | `string` | تذييل الـ Embed |
| `warning.message` | `string` | نص عادي عند `useEmbed: false` |
| `botWarning` | `object` | نفس بنية `warning` — خاص برسائل البوتات |

---

## 🎯 قواعد الفلترة

### ما المسموح به؟

| النوع | أمثلة |
|-------|-------|
| ✅ صورة مرفوعة مباشرة | `png` `jpg` `jpeg` `gif` `webp` `avif` `heic` |
| ✅ فيديو مرفوع مباشرة | `mp4` `mov` `avi` `mkv` `webm` `flv` |
| ✅ رابط من نطاق وسائط | imgur · tenor · giphy · YouTube · TikTok · Twitter/X · Instagram · Reddit · Twitch · Streamable · Medal.tv · Discord CDN |
| ✅ Discord Embed يحتوي وسائط | صورة / فيديو / GIF / thumbnail داخل الـ embed |
| ✅ رتبة معفاة في `exemptRoles` | يمر بحرية بغض النظر عن المحتوى |

### ما الممنوع؟

| النوع | الإجراء |
|-------|---------|
| ❌ نص فقط بدون وسائط | حذف + `warning` |
| ❌ ستيكر (إذا `blockStickers: true`) | حذف + `warning` |
| ❌ رسالة بوت (إذا `blockBots: true`) | حذف + `botWarning` |
| ❌ رسالة بوت غير معفى | حذف صامت إذا `botWarning.enabled: false` |

---

## 🔤 متغيرات رسائل التحذير

متاحة في أي نص داخل `warning` أو `botWarning`:

| المتغير | القيمة |
|---------|--------|
| `{user}` | منشن المستخدم أو البوت المخالف |
| `{channel}` | منشن القناة التي حدثت فيها المخالفة |
| `{seconds}` | عدد ثواني حذف رسالة التحذير |

---

## � مخطط سير العمل

```
رسالة جديدة في قناة محمية
        │
        ▼
 هل المرسل بوت؟
  ├── نعم ──→ هل هو البوت نفسه أو في exemptBots؟
  │            ├── نعم ──→ ✅ تجاهل
  │            └── لا  ──→ blockBots؟
  │                         ├── false ──→ ✅ تجاهل
  │                         └── true  ──→ ❌ حذف + botWarning
  │
  └── لا ───→ هل له رتبة معفاة؟
               ├── نعم ──→ ✅ تجاهل
               └── لا  ──→ هل يحتوي ستيكر؟
                             ├── نعم ──→ ❌ حذف + warning
                             └── لا  ──→ فحص الوسائط (3 طبقات)
                                          ├── وجدت وسائط ──→ ✅ تجاهل
                                          └── لا وسائط  ──→ ❌ حذف + warning
```

### طبقات فحص الوسائط

```
طبقة 1 — المرفقات المباشرة
  └── MIME type (image/* | video/*) أو امتداد الملف

طبقة 2 — Discord Embeds
  └── embed.image | embed.video | embed.thumbnail | gifv | article

طبقة 3 — روابط في نص الرسالة
  └── نطاق معروف في MEDIA_DOMAINS أو امتداد وسائط في المسار
```

---

## 🔄 Hot Reload

النظام يراقب ملفات الإعدادات تلقائياً — أي تعديل يُطبَّق فوراً بدون إعادة تشغيل:

```
تعديل configs/my-server/config.js
        │
        ▼
[Hot-Reload] my-server/config.js (guild: 123456789)
        │
        ▼
الإعدادات الجديدة تُطبَّق على الرسالة التالية مباشرة
```

---

<div align="center">

**صُنع بـ ❤️ — Abonebal © 2026**

![](https://img.shields.io/badge/Discord.js-v14-5865F2?style=flat-square&logo=discord&logoColor=white)
![](https://img.shields.io/badge/No%20Commands-Event%20Driven-orange?style=flat-square)
![](https://img.shields.io/badge/Multi--Server-✓-green?style=flat-square)

</div>
