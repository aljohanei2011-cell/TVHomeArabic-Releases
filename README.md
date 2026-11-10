# الواجهة العربية — لشاشات Android TV وGoogle TV

واجهة رئيسية عربية: مواقيت الصلاة والأذان، والطقس، والمباريات، والأخبار، والأذكار، بثلاثة أشكال (الكلاسيكي، والليلة العربية بخط الثلث، والزجاجي) وثيمات الأندية.

**التثبيت:** نزّل ملف `TVHomeArabic.apk` من أحدث إصدار في صفحة [الإصدارات](../../releases/latest) وثبّته على الشاشة. بعدها يتحدّث التطبيق من داخله.

---

<a id="guide"></a>
## دليل المتقدمين (أوامر الكمبيوتر)

لا يحتاجها أغلب المستخدمين: كل شيء يُضبط من إعدادات التطبيق. هذه الأوامر للشاشات التي تمنع ذلك (مثل بعض شاشات TCL وشاومي وChromecast).

**قبل البدء:** فعّل «خيارات المطوّر» ثم «تصحيح USB» أو «تصحيح الشبكة» في الشاشة، واتصل بها من الكمبيوتر:

```
adb connect <عنوان الشاشة>:5555
```

### جعل الواجهة العربية هي الرئيسية

```
adb shell cmd package set-home-activity app.tvhome.arabic/.MainActivity
```

للعودة إلى الواجهة الأصلية، اعرف اسمها أولًا ثم ضعه مكان الاسم في الأمر السابق:

```
adb shell cmd package query-activities --brief -a android.intent.action.MAIN -c android.intent.category.HOME
adb shell cmd package set-home-activity <اسم الحزمة>/<اسم الشاشة>
```

### تفعيل «تحويل زر Home» تلقائيًا وعودته وحده إن أوقفه النظام

```
adb shell pm grant app.tvhome.arabic android.permission.WRITE_SECURE_SETTINGS
```

### السماح بالتشغيل بعد إقلاع الشاشة (TCL وشاومي)

```
adb shell appops set app.tvhome.arabic APP_AUTO_START allow
adb shell appops write-settings
```

### شاشة التوقف «الواجهة العربية» إن كانت الشاشة تخفي قائمتها

```
adb shell settings put secure screensaver_components app.tvhome.arabic/.ArabicDream
adb shell settings put secure screensaver_enabled 1
```

### «تابع المشاهدة» إن كانت الشاشة لا تعرض صفحة الإذن

```
adb shell cmd notification allow_listener app.tvhome.arabic/app.tvhome.arabic.MediaWatch
```

---

الخط: ثمانية · شعارات الأندية لأصحابها.
