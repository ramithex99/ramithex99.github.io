# 📊 تقرير تحليل مشروع DropDeli
> **تاريخ التقرير:** 07 مارس 2026  
> **المشروع:** DropDeli — منصة توصيل غذاء ومنتجات متكاملة  
> **نوع المشروع:** Flutter Monorepo (Melos)  
> **قاعدة البيانات:** Supabase (PostgreSQL)

---

## 📁 1. نظرة عامة على الهيكل

```
dropdeli/
├── apps/
│   ├── customer/        ← تطبيق العميل
│   ├── driver/          ← تطبيق السائق
│   ├── merchant/        ← تطبيق التاجر
│   └── admin/           ← لوحة الإدارة
├── packages/
│   ├── core/            ← منطق الأعمال المشترك
│   ├── supabase_client/ ← طبقة قاعدة البيانات
│   └── ui/              ← مكتبة الواجهات المشتركة
├── supabase/            ← إعدادات Supabase
└── 31 ملف SQL          ← مخططات قاعدة البيانات
```

---

## 📈 2. إحصائيات الكود

### إجمالي المشروع

| المقياس | القيمة |
|---------|--------|
| **إجمالي ملفات lib (Dart)** | **1,431 ملف** |
| **إجمالي أسطر الكود** | **244,425 سطر** |
| **عدد التطبيقات** | 4 تطبيقات |
| **عدد الحزم المشتركة** | 3 حزم |
| **عدد ملفات SQL** | 31 ملف |

---

### توزيع ملفات Lib والأسطر حسب التطبيق

| التطبيق | ملفات .dart في lib | أسطر الكود | النسبة |
|---------|-------------------|-----------|--------|
| 📱 **customer** (تطبيق العميل) | 1,040 | 101,792 | 41.6% |
| 🖥️ **admin** (لوحة الإدارة) | 85 | 63,723 | 26.1% |
| 🚗 **driver** (تطبيق السائق) | 94 | 39,019 | 16.0% |
| 🏪 **merchant** (تطبيق التاجر) | 82 | 24,029 | 9.8% |
| 📦 **package/core** | 89 | 7,065 | 2.9% |
| 🎨 **package/ui** | 31 | 6,601 | 2.7% |
| 🔗 **package/supabase_client** | 10 | 2,196 | 0.9% |
| **الإجمالي** | **1,431** | **244,425** | 100% |

---

## 🏗️ 3. البنية المعمارية

### نمط التصميم
- **Monorepo** مُدار بـ **Melos**
- **State Management:** Riverpod (flutter_riverpod + riverpod_annotation + riverpod_generator)
- **Navigation:** GoRouter
- **Architecture Pattern:** Feature-first مع Clean Architecture
- **Backend:** Supabase (PostgreSQL + Storage + Auth + Edge Functions + Realtime)

### الحزم المشتركة (packages/)

| الحزمة | الوصف | ملفات | أسطر |
|--------|-------|-------|------|
| `dropdeli_core` | نماذج البيانات، منطق الأعمال، واجهات المستودعات | 89 | 7,065 |
| `dropdeli_ui` | نظام التصميم، مكونات الواجهة المشتركة، الثيم | 31 | 6,601 |
| `dropdeli_supabase` | تنفيذ Supabase لواجهات المستودعات، Auth | 10 | 2,196 |

---

## 🌟 4. تحليل ميزات كل تطبيق

---

### 📱 4.1 تطبيق العميل (Customer App)
> **1,040 ملف | 101,792 سطر | 27 وحدة (Feature)**

#### وحدات الميزات

| الوحدة | الملفات | الوصف |
|--------|---------|-------|
| 🛒 **cart** | 161 | السلة المتقدمة، الخصومات، الكوبونات، تتبع الأسعار |
| 🏠 **home** | 151 | الصفحة الرئيسية، Stories، Flash Sales، قوائم الاقتراح |
| ⚙️ **settings** | 74 | إعدادات الحساب، الإشعارات، الخصوصية |
| 📍 **tracking** | 54 | تتبع الطلب على الخريطة في الوقت الفعلي |
| 👥 **group_order** | 49 | نظام الطلب الجماعي مع أصدقاء |
| 🍽️ **restaurant** | 41 | صفحة المطعم، القوائم، التقييمات |
| 📦 **orders** | 41 | إدارة الطلبات، التاريخ، إعادة الطلب |
| 🎁 **rewards** | 41 | نقاط المكافآت، محفظة المكافآت |
| 🔍 **search** | 37 | البحث المتقدم، الفلاتر، الاقتراحات |
| 📸 **social** | 34 | المراجعات الاجتماعية، الصور، التعليقات |
| 💳 **subscription** | 25 | الاشتراكات الشهرية والسنوية |
| 🏷️ **offers** | 19 | العروض والتخفيضات |
| ❤️ **favorites** | 18 | المفضلات والمطاعم المحفوظة |
| 👤 **profile** | 17 | الملف الشخصي، صورة المستخدم |
| 🔗 **referral** | 13 | نظام الإحالة والمكافآت |
| 🏆 **challenges** | 13 | تحديات الغاميفيكيشن |
| 🆕 **onboarding** | 12 | شاشات التعريف للمستخدمين الجدد |
| 🔐 **auth** | 11 | تسجيل الدخول، OTP، Social Login |
| 🔎 **discovery** | 11 | اكتشاف المطاعم والمنتجات |
| 🏠 **addresses** | 10 | إدارة عناوين التوصيل |
| 🎮 **gamification** | 10 | نقاط، شارات، لوحة الصدارة |
| 🔔 **notifications** | 7 | الإشعارات الفورية |
| 💰 **wallet** | 5 | محفظة العميل الرقمية |
| 💬 **support** | 3 | الدعم والمساعدة |
| 🚗 **ride** | 1 | نظام الرحلات |
| 💬 **chat** | 1 | الدردشة المباشرة |
| 📦 **package** | 1 | إرسال وتتبع الطرود |

#### المكتبات المستخدمة (Customer)
| الفئة | المكتبات |
|-------|---------|
| State Management | `flutter_riverpod`, `riverpod_annotation` |
| Navigation | `go_router` |
| UI/Animation | `google_fonts`, `flutter_animate`, `lottie`, `confetti`, `shimmer`, `carousel_slider` |
| Maps & Location | `google_maps_flutter`, `flutter_map`, `geolocator`, `geocoding`, `latlong2` |
| Backend | `supabase_flutter`, `http` |
| Notifications | `onesignal_flutter` |
| Media | `cached_network_image`, `image_picker` |
| Payment | `flutterwave_standard` |
| Audio | `audioplayers` |
| Utils | `flutter_dotenv`, `intl`, `url_launcher`, `share_plus`, `shared_preferences`, `crypto`, `timeago`, `badges`, `permission_handler` |
| Charts | `fl_chart` |

---

### 🖥️ 4.2 لوحة الإدارة (Admin App)
> **85 ملف | 63,723 سطر | 25 وحدة (Feature)**

#### وحدات الميزات

| الوحدة | الوصف |
|--------|-------|
| 📊 **dashboard** | لوحة التحكم الرئيسية، إحصائيات فورية |
| 👥 **customers** | إدارة العملاء، الحجب، البحث |
| 🏪 **merchants** | إدارة التجار، المراجعة، الموافقة |
| 🚗 **drivers** | إدارة السائقين، تتبع الأداء |
| 📦 **orders** | مراقبة جميع الطلبات |
| 💰 **payouts** | إدارة المدفوعات للتجار والسائقين |
| 💳 **transactions** | تتبع جميع المعاملات المالية |
| 📈 **reports** | تقارير تفصيلية وإحصائيات |
| 📣 **offers** | إنشاء وإدارة العروض الترويجية |
| 📍 **delivery_zones** | إدارة مناطق التوصيل |
| 🗺️ **live_map** | خريطة حية للسائقين والطلبات |
| 📝 **content** | إدارة المحتوى والبانرات |
| 💬 **reviews** | مراجعة ومشرفة التقييمات |
| 🔔 **notifications** | إرسال إشعارات جماعية |
| 📋 **applications** | طلبات الانضمام للتجار الجدد |
| 📉 **insights** | تحليلات وأنماط الاستخدام |
| 🏬 **design_studio** | تصميم واجهات التطبيق |
| 🔑 **roles** | إدارة أدوار وصلاحيات المشرفين |
| 📂 **documents** | إدارة الوثائق والملفات |
| 🔍 **audit** | سجلات التدقيق والنشاط |
| 💼 **commissions** | إدارة نسب العمولات |
| ⚙️ **settings** | إعدادات المنصة الشاملة |
| 💬 **support** | نظام دعم المستخدمين |
| 🛍️ **products** | إدارة المنتجات الإدارية |
| 🏠 **shell** | هيكل التطبيق والتنقل |

#### المكتبات المستخدمة (Admin)
| الفئة | المكتبات |
|-------|---------|
| Data Tables | `data_table_2` |
| Charts | `fl_chart` |
| Maps | `flutter_map`, `latlong2` |
| File Upload | `file_picker`, `image_picker_web` |
| UI | `google_fonts`, `flutter_animate`, `shimmer` |
| Backend | `supabase_flutter`, `flutter_dotenv` |

---

### 🚗 4.3 تطبيق السائق (Driver App)
> **94 ملف | 39,019 سطر | 17 وحدة (Feature)**

#### وحدات الميزات

| الوحدة | الوصف |
|--------|-------|
| 🏠 **home** | الشاشة الرئيسية، الحالة، قبول الطلبات |
| 📦 **orders** | إدارة الطلبات النشطة والتاريخ |
| 📍 **active_order** | تنفيذ الطلب الحالي خطوة بخطوة |
| 🗺️ **multi_order** | إدارة طلبات متعددة في آن واحد |
| 📋 **multi_orders** | قائمة الطلبات المتعددة |
| 💰 **earnings** | الأرباح اليومية، الأسبوعية، الشهرية |
| 💸 **expenses** | تتبع النفقات (بنزين، صيانة) |
| 💳 **wallet** | محفظة السائق الرقمية |
| 🎯 **quests** | مهام ومكافآت أداء |
| 🔥 **hot_zones** | مناطق الطلب العالي على الخريطة |
| 👤 **profile** | الملف الشخصي، الوثائق |
| 🔐 **auth** | تسجيل الدخول والتحقق |
| 💬 **chat** | الدردشة مع العملاء والمطاعم |
| 🛡️ **safety** | ميزات السلامة وطوارئ |
| 🔔 **notifications** | الإشعارات الفورية للطلبات |
| ⚙️ **settings** | إعدادات الحساب والتفضيلات |
| 💼 **subscription** | اشتراك السائق Pro |
| 💬 **support** | الدعم والمساعدة |
| 🏠 **shell** | هيكل التطبيق |

#### المكتبات المستخدمة (Driver)
| الفئة | المكتبات |
|-------|---------|
| Maps | `google_maps_flutter`, `flutter_map`, `geolocator`, `latlong2` |
| Audio | `just_audio` |
| TTS | `flutter_tts` |
| Subscriptions | `purchases_flutter` (RevenueCat) |
| QR | `qr_flutter` |
| Notifications | `onesignal_flutter` |
| UI | `google_fonts`, `flutter_animate`, `shimmer`, `cached_network_image` |

---

### 🏪 4.4 تطبيق التاجر (Merchant App)
> **82 ملف | 24,029 سطر | 14 وحدة (Feature)**

#### وحدات الميزات

| الوحدة | الوصف |
|--------|-------|
| 📊 **dashboard** | لوحة التحكم، مبيعات اليوم، الطلبات النشطة |
| 📦 **orders** | استلام وإدارة الطلبات بشكل فوري |
| 🍽️ **menu** | إدارة القائمة، الأصناف، الفئات |
| 📦 **inventory** | إدارة المخزون والتوافر |
| 📣 **promotions** | العروض والخصومات والكوبونات |
| 📸 **stories** | قصص ترويجية (مثل Instagram Stories) |
| 🏢 **branches** | إدارة أفرع أو المواقع المتعددة |
| 📍 **delivery_zones** | تحديد مناطق التوصيل الخاصة |
| 📊 **analytics** | تحليلات المبيعات والأداء |
| 💰 **payout** | طلبات السحب والمدفوعات |
| 👤 **profile** | ملف المتجر، الصور، ساعات العمل |
| 🔐 **auth** | تسجيل الدخول والتحقق |
| 💬 **support** | التواصل مع الدعم |
| ⚙️ **settings** | إعدادات المتجر |
| 🏠 **shell** | هيكل التطبيق |

#### المكتبات المستخدمة (Merchant)
| الفئة | المكتبات |
|-------|---------|
| Charts | `fl_chart` |
| QR | `qr_flutter` |
| Biometrics | `local_auth` (بصمة/وجه) |
| Maps | `google_maps_flutter`, `flutter_map`, `geolocator` |
| Audio | `just_audio` |
| Notifications | `onesignal_flutter` |
| UI | `google_fonts`, `flutter_animate`, `shimmer`, `badges` |

---

## 🗄️ 5. قاعدة البيانات (Supabase SQL)

### ملفات SQL المطوّرة (31 ملف)

| الملف | الحجم | الوصف |
|-------|-------|-------|
| `supabase_fresh_install.sql` | 25.9 KB | السكيما الكاملة للتثبيت الجديد |
| `supabase_migration.sql` | 23.7 KB | ملف الانتقال والتهجير |
| `supabase_gamification.sql` | 21.8 KB | نظام الغاميفيكيشن الكامل |
| `supabase_group_orders.sql` | 19.3 KB | نظام الطلب الجماعي |
| `supabase_delivery_pins.sql` | 18.2 KB | أكواد تأكيد التوصيل |
| `supabase_subscriptions.sql` | 16.2 KB | نظام الاشتراكات |
| `supabase_referral_program.sql` | 13.5 KB | برنامج الإحالة |
| `supabase_seed_data.sql` | 13.4 KB | بيانات أولية للتجربة |
| `supabase_rewards_wallet.sql` | 13.3 KB | محفظة المكافآت |
| `supabase_birthday_rewards.sql` | 13.0 KB | مكافآت أعياد الميلاد |
| `supabase_working_hours.sql` | 10.1 KB | ساعات العمل للمتاجر |
| `supabase_loyalty_system.sql` | 9.3 KB | نظام الولاء والنقاط |
| `supabase_merchant_stories.sql` | 8.5 KB | قصص التجار |
| `supabase_stories.sql` | 8.5 KB | نظام القصص العام |
| `supabase_performance_indexes.sql` | 8.3 KB | فهارس تحسين الأداء |
| `supabase_platform_settings.sql` | 7.6 KB | إعدادات المنصة |
| `supabase_inventory_promotions.sql` | 7.6 KB | العروض على المخزون |
| `supabase_customer_wallet.sql` | 7.5 KB | محفظة العميل |
| `supabase_flash_sales.sql` | 6.5 KB | مبيعات Flash (وقت محدود) |
| `supabase_delivery_zones.sql` | 5.3 KB | مناطق التوصيل |
| `supabase_branches.sql` | 4.5 KB | الأفرع المتعددة |
| `supabase_more_products.sql` | 4.2 KB | توسعة المنتجات |
| `supabase_favorites_enhanced.sql` | 3.8 KB | المفضلات المحسّنة |
| `supabase_map_settings.sql` | 3.6 KB | إعدادات الخريطة |
| `supabase_group_orders_merchant_rls.sql` | 3.5 KB | سياسات RLS للطلب الجماعي |
| `supabase_admin_policies.sql` | 3.4 KB | سياسات الصلاحيات للإدارة |
| `supabase_merchant_media_storage.sql` | 2.9 KB | تخزين وسائط التجار |
| `supabase_merchant_applications.sql` | 2.8 KB | طلبات التجار الجدد |
| `supabase_fix_policies.sql` | 1.5 KB | إصلاحات سياسات الأمان |
| `supabase_comments_table.sql` | 0.8 KB | جدول التعليقات |
| `supabase_favorites_table.sql` | 0.6 KB | جدول المفضلات |

---

## 🌟 6. الميزات الشاملة للمنصة

### 🔐 المصادقة والأمان
- تسجيل دخول بالبريد/الهاتف + OTP
- Google Sign-In و Apple Sign-In
- Row Level Security (RLS) في Supabase
- المصادقة البيومترية (بصمة/وجه) في تطبيق التاجر
- سياسات أمان متخصصة لكل دور

### 🗺️ الخرائط والتوصيل
- تتبع السائق في الوقت الفعلي (Google Maps + Flutter Map)
- تعيين مناطق التوصيل الجغرافية
- خريطة حية للأدمن
- Hot Zones (مناطق الطلب العالي) للسائقين
- أكواد PIN للتأكيد عند التسليم
- دعم الطلبات المتعددة في آن واحد للسائق

### 💰 النظام المالي
- محفظة رقمية للعملاء والسائقين
- دفع عبر Flutterwave
- إدارة عمولات التاجر والسائق
- سحب أرباح تلقائي/يدوي (Payouts)
- تتبع نفقات السائق
- تقارير مالية تفصيلية في الأدمن

### 🎮 الغاميفيكيشن والمكافآت
- نظام نقاط ولاء متكامل
- تحديات يومية/أسبوعية (Challenges & Quests)
- شارات الإنجاز
- لوحة الصدارة
- مكافآت أعياد الميلاد
- برنامج إحالة صديق مع مكافآت
- محفظة مكافآت منفصلة
- Confetti Animation عند الفوز

### 👥 الطلب الاجتماعي والجماعي
- نظام الطلب الجماعي (Group Order) مع مشاركة الأصدقاء
- مراجعات اجتماعية مع صور
- نظام التعليقات
- المفضلات والقوائم الشخصية

### 📣 التسويق والعروض
- Flash Sales (عروض محدودة الوقت)
- كوبونات وأكواد خصم
- قصص إعلانية (Merchant / Platform Stories)
- عروض المخزون والكميات المحدودة
- نظام اشتراكات للعملاء والسائقين (Pro)
- RevenueCat لإدارة الاشتراكات (Driver)

### 🔔 الإشعارات
- إشعارات فورية عبر OneSignal
- إشعارات صوتية (audioplayers / just_audio)
- Text-to-Speech للسائقين (flutter_tts)
- إشعارات جماعية من لوحة الإدارة

### 🌐 التدويل والتوطين
- دعم متعدد اللغات (flutter_localizations) في جميع التطبيقات
- ملفات l10n في كل تطبيق
- تنسيق تواريخ وأرقام محلي (intl)

### 🏬 إدارة المتجر (Merchant)
- إدارة قائمة كاملة (Menu، Categories، Items)
- إدارة مخزون مع إشعارات النفاق
- الأفرع المتعددة لنفس التاجر
- ساعات العمل وأوقات الإغلاق
- QR Code للتاجر
- وسائط الصور (Gallery لكل صنف)

### 🖥️ لوحة الإدارة
- إدارة شاملة لجميع الكيانات
- جداول بيانات متقدمة (data_table_2)
- تحليلات ورسوم بيانية (fl_chart)
- نظام أدوار وصلاحيات متعدد المستويات
- سجل تدقيق للنشاطات
- Design Studio لتخصيص الواجهة
- رفع الملفات والصور (file_picker، image_picker_web)
- خريطة حية ومراقبة في الوقت الفعلي

---

## 🛠️ 7. مجموعة التقنيات (Tech Stack)

| الفئة | التقنية |
|-------|---------|
| **Framework** | Flutter 3.x (Dart ≥3.0) |
| **Architecture** | Feature-first + Clean Architecture |
| **State Management** | Riverpod 2.x + Code Generation |
| **Navigation** | GoRouter 14.x |
| **Backend** | Supabase (PostgreSQL + Auth + Storage + Edge Functions + Realtime) |
| **Monorepo** | Melos |
| **Maps** | Google Maps Flutter + Flutter Map (OSM) |
| **Push Notifications** | OneSignal |
| **Payments** | Flutterwave Standard |
| **In-App Purchases** | RevenueCat (purchases_flutter) |
| **Auth Providers** | Google Sign-In + Apple Sign-In |
| **Charts** | fl_chart |
| **Code Generation** | build_runner + json_serializable + riverpod_generator |
| **CI/CD** | GitHub Actions (.github/) |

---

## 📊 8. ملخص الملفات النهائي

```
📦 إجمالي ملفات lib/.dart : 1,431 ملف
📝 إجمالي أسطر الكود     : 244,425 سطر
📱 عدد التطبيقات         : 4 تطبيقات
📦 الحزم المشتركة        : 3 حزم
🗄️ ملفات SQL             : 31 ملف
⚙️  وحدات الميزات (Features): 83+ وحدة إجمالاً
```

---

*تم إنشاء هذا التقرير تلقائياً بتحليل كود المشروع — DropDeli © 2026*
