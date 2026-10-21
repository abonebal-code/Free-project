# 🖼️ ImageOnly-System v1.0.0

> **Developer:** abonebal | **© 2026**

نظام احترافي يضمن أن القنوات المحددة تحتوي على **صور وفيديوهات فقط** — أي رسالة نصية أو ستيكر يتم حذفها فوراً مع إرسال تحذير للمخالف.

---

## 📁 هيكل الملفات

```
ImageOnly-System-v1.0.0/
├── index.js                    ← نقطة الدخول
├── config.json                 ← الكونفيج الرئيسي (التوكن + المسارات)
├── package.json
├── .env.example                ← مثال ملف التوكن
├── configs/
│   └── YOUR_GUILD_ID/
│       └── config.json         ← إعدادات السيرفر
├── src/
│   ├── events/
│   │   └── messageCreate.js
│   ├── features/
│   │   └── imageOnly.js        ← المنطق الأساسي
│   └── utils/
│       └── configLoader.js     ← تحميل الكونفيج والتوكن
└── docs/
    └── README.md
```

---

## ⚙️ إعداد النظام

### الخطوة 1 — ملف `.env`

انسخ `.env.example` وسمّه `.env` وضع فيه التوكن:

```env
imageonly-bot-token=YOUR_BOT_TOKEN_HERE
```

> اسم المتغير يطابق قيمة `tokenEnvKey` في `config.json`

---

### الخطوة 2 — `config.json` الرئيسي

```json
{
  "envPath": "../../.env",
  "tokenEnvKey": "imageonly-bot-token",
  "configsDir": "configs"
}
```

| المفتاح | الوصف |
|---------|-------|
| `envPath` | مسار ملف `.env` نسبةً لجذر النظام |
| `tokenEnvKey` | اسم المتغير في `.env` الذي يحتوي التوكن |
| `configsDir` | مجلد كونفيجات السيرفرات |

---

### الخطوة 3 — كونفيج السيرفر

أنشئ مجلداً باسم **ID السيرفر** داخل `configs/` وضع فيه `config.json`:

```
configs/
└── 1234567890123456789/   ← ID السيرفر
    └── config.json
```

```json
{
  "imageOnlyChannels": ["CHANNEL_ID_1", "CHANNEL_ID_2"],
  "exemptRoles": ["ROLE_ID_ADMIN", "ROLE_ID_MOD"],
  "blockBots": true,
  "blockStickers": true,
  "warning": {
    "enabled": true,
    "deleteAfter": 6,
    "useEmbed": true,
    "embed": {
      "color": "#FF0000",
      "title": "🚫 قناة الصور والفيديوهات فقط",
      "description": "يا {user}، هذه القناة مخصصة للصور والفيديوهات فقط!",
      "footer": "سيتم حذف هذا التنبيه بعد {seconds} ثوانٍ"
    }
  }
}
```

---

## 🎯 قواعد الفلترة

| النوع | الحكم |
|-------|-------|
| صورة مرفوعة (png, jpg, gif, webp...) | ✅ مسموح |
| فيديو مرفوع (mp4, mov, webm...) | ✅ مسموح |
| رابط من نطاق وسائط (imgur, tenor, youtube...) | ✅ مسموح |
| Embed يحتوي صورة أو فيديو | ✅ مسموح |
| نص فقط بدون وسائط | ❌ محذوف |
| ستيكر (إذا `blockStickers: true`) | ❌ محذوف |
| رسالة بوت (إذا `blockBots: true`) | ❌ محذوف صامت |
| رتبة معفاة | ✅ مسموح دائماً |

---

## 🔤 متغيرات رسالة التحذير

| المتغير | القيمة |
|---------|--------|
| `{user}` | منشن المستخدم المخالف |
| `{seconds}` | عدد ثواني الحذف التلقائي للتحذير |
| `{channel}` | منشن القناة |

---

## 🚀 التشغيل

```bash
# تثبيت المكتبات
npm install

# تشغيل مستقل
node index.js
```

أو استدعاء من بوتك الرئيسي:

```js
require('./Codes/ImageOnly-System-v1.0.0/index')(client);
```

---

## 🔄 Hot-Reload

النظام يراقب مجلد `configs/` تلقائياً — أي تعديل في كونفيج سيرفر يُطبَّق فوراً دون إعادة تشغيل البوت.

---

*© 2026 abonebal — All rights reserved*
