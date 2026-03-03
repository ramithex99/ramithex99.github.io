## خطة تنفيذ بداية إعادة تصميم Restaurant Cards (Home)

### الملخص
الهدف هو تنفيذ إعادة تصميم بطاقات المطاعم في `apps/customer` بشكل **UI-first** (كما اخترت) مع الحفاظ على سلامة المعمارية الحالية، ودعم العربية/الفرنسية/الإنجليزية، وتطبيق قواعد responsive المطلوبة بدون إدخال تغييرات backend أو providers ثقيلة في هذه الدفعة.

### نطاق التنفيذ (الدفعة الحالية)
1. تحديث:
`apps/customer/lib/features/home/widgets/talabat_restaurant_card_large.dart`  
`apps/customer/lib/features/home/widgets/talabat_restaurant_tile.dart`  
`apps/customer/lib/features/home/widgets/talabat_restaurant_list_item.dart`  
`apps/customer/lib/features/home/widgets/talabat_restaurant_rating_badge.dart`  
`apps/customer/lib/features/home/widgets/talabat_horizontal_restaurant_card.dart` (متزامن مع التصميم الجديد كما تم الاتفاق)
2. تحديث ملفات العرض التي تتحكم بالـ grid/featured layout لضبط responsive:
`apps/customer/lib/features/home/presentation/talabat_home_restaurants_list_sliver.dart`  
`apps/customer/lib/features/home/presentation/talabat_home_popular_restaurants_grid_section.dart`
3. إضافة مفاتيح l10n جديدة (EN/AR/FR) عند الحاجة فقط.

---

## الحالة الحالية التي بُنيت عليها الخطة
1. الملفات المستهدفة موجودة وكلها أقل من 200 سطر حاليًا.
2. `MerchantProfile` يحتوي حقولًا كافية للعرض الأساسي (`storeName`, `storeImage`, `storeLogo`, `ratingAvg`, `ratingCount`, `storeCategory`, `isOnline`, `acceptingOrders`, `workingHours`, `promoActive`, `discountValue`) لكنه لا يحتوي حقولًا دقيقة جاهزة لـ ETA/Distance/MinOrder/Promoted.
3. يوجد `CachedNetworkImage` و shimmer infrastructure جاهز في المشروع.
4. لا يوجد responsive breakpoints مطبّق حاليًا لهذه البطاقات على شكل `<360 / 360-400 / >400`.

---

## التغييرات/الإضافات على الواجهات العامة (APIs/Interfaces)
1. `TalabatRestaurantRatingBadge`:
   - إضافة `reviewCount` (افتراضي `0`).
   - الإبقاء على `rating` و `compact`.
   - تطبيق لون ديناميكي حسب rating threshold.
2. الحفاظ على API لبقية البطاقات كما هو قدر الإمكان لتقليل churn.
3. إضافة helper presentation-only جديد (بدون business logic/network):
   - `talabat_restaurant_card_presenter.dart` لتجهيز نصوص العرض fallback.
4. إضافة helper responsive جديد:
   - `talabat_restaurant_card_responsive.dart` لتوحيد breakpoints والقيم.

---

## خطة التنفيذ التفصيلية (Decision-Complete)

### المرحلة 1: طبقة الأساس (Presentation + Responsive)
1. إنشاء `talabat_restaurant_card_responsive.dart` بقيم موحدة:
   - `<360`: تقليل الخط 2sp وتقليل أحجام الصور/الأبعاد إلى 80%.
   - `360-400`: القيم الافتراضية.
   - `>400`: padding أكبر + تمكين 3 أعمدة في grid.
2. إنشاء `talabat_restaurant_card_presenter.dart` بدوال pure لعرض:
   - `deliveryTimeText` (fallback: `20-30 min`).
   - `deliveryFeeText` (Free Delivery إذا `discountValue <= 0` وإلا `{value} DZD`).
   - `distanceText` (fallback: `1.2 km`).
   - `closedOpensAtText` (fallback: `Closed • Opens at 11:00` مع محاولة قراءة `workingHours` إن أمكن بدون async).
   - `categoryText` fallback إلى `l.restaurant`.
   - `promotedVisible` fallback على `promoActive`.
3. منع وضع business logic داخل widget trees؛ كل التحويلات النصية والاشتقاق في helper فقط.

### المرحلة 2: تحديث Rating Badge
1. تعديل `talabat_restaurant_rating_badge.dart`:
   - العرض: `⭐ 4.5 (120+)`.
   - اللون:
     - `>=4.5` أخضر.
     - `3.5..4.4` برتقالي.
     - `<3.5` أحمر.
   - دعم `compact` بدون كسر الاستخدامات الحالية.
2. تمرير `merchant.ratingCount` من كل call sites.

### المرحلة 3: إعادة تصميم Featured/Large Card
1. تعديل `talabat_restaurant_card_large_image_stack.dart` ليشمل:
   - صورة hero عبر `CachedNetworkImage` مع shimmer placeholder.
   - gradient overlay من أسفل لأعلى (`black` alpha `0.6`).
   - شعار المطعم دائري `48x48` أسفل-يسار فوق الصورة.
   - اسم المطعم فوق الصورة (`bold`, `16sp`, أبيض).
   - badge خصم في أعلى-يمين عند وجود offer (`20% OFF`).
   - زر القلب في أعلى-يمين مع إزاحة أسفل badge الخصم (حل تعارض top-right).
   - pill للمسافة (`1.2 km`).
   - حالة الإغلاق: overlay رمادي + نص `Closed • Opens at ...`.
2. تعديل `talabat_restaurant_card_large.dart`:
   - صف rating pill الجديد.
   - صف delivery info بصيغة:
     - `🚚 20-30 min • 💰 Free delivery`
     - أو `🚚 20-30 min • 💰 150 DZD`.
   - الحفاظ على التفاعل الحالي (tap + favorite toggle).
3. قرار الأبعاد:
   - baseline featured size: `280x200`.
   - في الشاشات الصغيرة/الكبيرة يتم scale عبر helper.
   - في سياقات parent الضيقة يُستخدم `constraints + Flexible` لمنع overflow.

### المرحلة 4: تحديث Horizontal Card (Sync)
1. تعديل `talabat_horizontal_restaurant_card.dart` ليستخدم نفس language البصرية:
   - Cached image + shimmer.
   - rating badge الجديد.
   - delivery row موحد.
   - حالة closed/promo بنفس الرموز اللونية.
2. الحفاظ على API الحالي (merchant فقط) مع تحديث داخلي فقط.

### المرحلة 5: تحديث Grid Tile + List Item
1. `talabat_restaurant_tile.dart`:
   - هيكل 4:3 للصورة أعلى + info أسفل.
   - اسم سطر واحد ellipsis.
   - category سطر واحد (`Pizza • Italian` style عبر fallback category).
   - rating + delivery time في سطر.
   - `Min 500 DZD` fallback (UI-first).
2. `talabat_restaurant_list_item.dart`:
   - صورة يسار `100x100` radius `12`.
   - يمين: اسم، category، rating + review count، delivery time + fee، distance.
   - badge `Promoted` عند `promoActive`.
3. تطبيق `maxLines` + `TextOverflow.ellipsis` على كل النصوص المعرضة للتمدد.

### المرحلة 6: Responsive في الشاشات الحاوية
1. `talabat_home_restaurants_list_sliver.dart`:
   - grid mode:
     - `<400`: عمودان.
     - `>400`: 3 أعمدة.
   - تعديل `childAspectRatio` و`spacing` حسب responsive profile.
2. `talabat_home_popular_restaurants_grid_section.dart`:
   - نفس قاعدة الأعمدة `2/3`.
   - نفس scaling للقيم البصرية.
3. التأكد أن أي fixed width تم استبداله بـ `Flexible/Expanded` أو constraints ذكية.

### المرحلة 7: Localization
1. إضافة المفاتيح الجديدة فقط في:
   - `apps/customer/lib/l10n/app_en.arb`
   - `apps/customer/lib/l10n/app_ar.arb`
   - `apps/customer/lib/l10n/app_fr.arb`
2. أمثلة مفاتيح:
   - `restaurantClosedOpensAt(time)`
   - `restaurantPromoted`
   - `restaurantMinOrderAmount(amount)`
   - `restaurantDeliveryInfo(eta, fee)`
   - `restaurantDistanceKm(km)` (إن لزم)
3. تشغيل `flutter gen-l10n` بعد الإضافة.

### المرحلة 8: التحقق النهائي
1. `dart format` لكل الملفات المعدلة.
2. `flutter analyze` (workdir: `apps/customer`) ويجب `0 issues`.
3. `flutter test` (workdir: `apps/customer`) ويجب النجاح الكامل.
4. فحص UI يدوي على 3 أحجام:
   - عرض 350
   - عرض 390
   - عرض 430+
5. فحص لغات `EN/AR/FR` مع dark/light والتأكد من عدم overflow.

---

## حالات الاختبار المطلوبة (Acceptance Scenarios)
1. Rating badge:
   - `4.7` يظهر أخضر.
   - `4.0` يظهر برتقالي.
   - `3.2` يظهر أحمر.
   - يعرض review count صحيحًا.
2. Large card:
   - وجود الصورة/placeholder دائمًا.
   - ظهور الشعار 48x48 فوق الصورة.
   - overlay الإغلاق يظهر عند `!isOnline || !acceptingOrders`.
   - badge الخصم والقلب لا يتداخلان.
3. Tile/List:
   - النصوص الطويلة لا تكسر layout.
   - سلوك min order/distance/promoted يظهر حسب الـ presenter.
4. Responsive:
   - `<360` الخطوط أصغر 2sp.
   - `>400` grid = 3 أعمدة.
5. Localization:
   - لا توجد نصوص إنجليزية hardcoded في الملفات المستهدفة.
   - AR/FR تظهر دون قص أو overflow.

---

## الافتراضات والاختيارات المعتمدة
1. **تم اعتماد UI-first** لهذه الدفعة (بدون ربط backend إضافي لـ ETA/Distance/Open time).
2. **تم اعتماد تحديث horizontal card** في نفس الدفعة ليتماشى بصريًا.
3. `discountValue` يُستخدم في هذه الدفعة كـ delivery fee display (لأن اسم الحقل لا يعكس المعنى الحالي بدقة).
4. `promoActive` يُستخدم كـ flag لعرض discount/promoted في الواجهة.
5. fallback القيم:
   - ETA: `20-30 min`
   - Distance: `1.2 km`
   - Min order: `500 DZD`
   - Opens at: `11:00` عند غياب بيانات قابلة للعرض.
