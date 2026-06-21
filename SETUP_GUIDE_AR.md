# دليل التشغيل — خطوة بخطوة (اقرأه بالترتيب)

الكود كله جاهز. باقي عليك بس خطوتين: (1) تعمل Supabase وتوصله بالكود (2) تنشر الملفات على الإنترنت.
خد وقتك، كل خطوة بسيطة.

---

## الخطوة 1: عمل حساب Supabase (5 دقايق)

1. روح [supabase.com](https://supabase.com) واضغط **Start your project** وسجل دخول بـ Google أو GitHub.
2. اضغط **New Project**.
3. اكتب اسم زي `david-osama-cms`، واختار باسورد قوي لقاعدة البيانات واحفظه في مكان آمن.
4. اختار أقرب Region (ممكن Frankfurt أو London).
5. اضغط **Create new project** واستنى دقيقة لحد ما يخلص.

---

## الخطوة 2: تشغيل أكواد قاعدة البيانات

1. من القائمة الجانبية، افتح **SQL Editor**.
2. اضغط **New query**.
3. افتح الملف `sql/schema.sql` اللي معاك في المشروع، انسخ كل اللي فيه، وحطه في الـ SQL Editor.
4. اضغط **Run** (أو Ctrl+Enter). المفروض يطلعلك "Success. No rows returned".

ده عمل لك 4 جداول (projects, testimonials, settings, before_after) وقفل الحماية عليهم صح.

---

## الخطوة 3: عمل Storage Buckets (مكان حفظ الصور)

من القائمة الجانبية افتح **Storage** واضغط **New bucket** 4 مرات بالظبط بالأسامي دي (مهم تكتبهم بالظبط زي ما هما، حروف صغيرة):

1. `portfolio-images` — فعّل **Public bucket** ✅
2. `testimonial-images` — فعّل **Public bucket** ✅
3. `profile-images` — فعّل **Public bucket** ✅
4. `before-after-images` — فعّل **Public bucket** ✅

---

## الخطوة 4: عمل حساب الأدمن بتاعك (تسجيل الدخول)

1. من القائمة الجانبية افتح **Authentication** → **Users**.
2. اضغط **Add user** → **Create new user**.
3. حط الإيميل والباسورد اللي عايز تدخل بيهم على لوحة التحكم (admin.html).
4. فعّل **Auto Confirm User** ✅ ثم اضغط **Create user**.

ده الإيميل والباسورد اللي هتدخل بيهم على `login.html`.

---

## الخطوة 5: ربط الكود بمشروعك

1. من القائمة الجانبية افتح **Project Settings** (الترس تحت) → **API**.
2. هتلاقي اتنين قيم محتاجهم:
   - **Project URL**
   - **anon public** key (سطر طويل تحت "Project API keys")
3. افتح ملف `js/supabase-client.js` في أي محرر نصوص (حتى Notepad).
4. غيّر السطرين دول بالقيم بتاعتك:
   ```js
   const SUPABASE_URL = "PASTE_YOUR_SUPABASE_PROJECT_URL_HERE";
   const SUPABASE_ANON_KEY = "PASTE_YOUR_SUPABASE_ANON_PUBLIC_KEY_HERE";
   ```
5. احفظ الملف.

**ده آخر تعديل في الكود هتعمله أبداً.** من هنا وبعدين كل حاجة من لوحة التحكم.

---

## الخطوة 6: تجربة محلية (اختياري بس مفيد)

افتح ملف `index.html` بالـ double click في المتصفح — المفروض الموقع يفتح. لو فاضي من الصور، ده طبيعي لأنك لسه ماضفتش حاجة من admin.html.

افتح `admin.html`، هيوديك على `login.html`، سجل دخول بالإيميل والباسورد اللي عملتهم في الخطوة 4، وابدأ ضيف صورة تجربة وشوفها بتظهر في `index.html` بعد الـ Refresh (أو حتى من غير Refresh — الموقع شغال Real-Time).

---

## الخطوة 7: النشر على الإنترنت (Netlify)

1. روح [netlify.com](https://netlify.com) واعمل حساب مجاني.
2. من الصفحة الرئيسية، اسحب (Drag & Drop) فولدر المشروع كله (اللي فيه index.html, admin.html, css, js, sql) في المكان المكتوب عليه "Drag and drop your site folder here".
3. Netlify هيرفعهم ويديك رابط زي `your-site-name.netlify.app`.
4. تقدر تغير اسم الموقع من **Site settings → Change site name**.

كده الموقع والـ admin شغالين أونلاين، متربطين بنفس الـ Supabase، وأي تعديل من admin.html هيظهر فوراً على الموقع لأي حد يفتحه.

---

## ملحوظات مهمة

- **متشاركش الـ service_role key** مع حد ولا تحطه في الكود — احنا مستخدمين بس الـ anon key وده آمن للموقع العام.
- لو عايز تضيف أدمن تاني (حد يساعدك)، ارجع لـ Authentication → Users وضيفه بنفس الطريقة.
- لو حصل أي خطأ وقت الحفظ من admin.html، افتح Developer Console في المتصفح (F12) وابعتلي رسالة الخطأ، هينا أحلها فوراً.
- ملف `sql/schema.sql` فيه كل حاجة لو حبيت تعمل Reset أو تفهم شكل الجداول.
