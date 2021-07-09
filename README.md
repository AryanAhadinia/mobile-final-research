<p align="center">
    <img src="https://github.com/AryanAhadinia/mobile-final-research/blob/master/assets/header.jpg?raw=true" height="250px" alt="flutter + parse">
    <br/>
Parse Flutter SDK
    <br/>
برنامه سازی موبایل، دانشگاه صنعتی شریف
    <br/>
ارائه دهنده درس: جناب آقای امید جعفری نژاد
    <br/>
نویسندگان: آرین احدی نیا، شهاب حسینی مقدم، محمدحسین کاشانی جباری
</p>

<div dir="rtl">

## پیش از شروع خوب است که ... 
علی الرغم سادگی های Flutter خوب است که پیش از شروع دانش native در مورد برنامه سازی موبایل داشته باشید.
میتوانید برای مطالعه در مورد SDK پارس سرور برای Android از
[این مقاله](https://github.com/AryanAhadinia/mobile-midterm-research)
که توسط همین گروه نگاشته شده است استفاده کنید.

## Parse Server چیست؟
پارس سرور یک mobile Platform as a Service یا به اختصار یک mPaaS است.
به عبارت ساده‌تر یک backend آماده است که عمده کار برنامه نویسی آن مربوط به استفاده آن در client میشود.
در پارس سرور بسیاری از روتین های برنامه نویسی backend از قبیل حساب کاربری و عملکردهای پیچیده مربوط به آن مانند فراموشی رمز عبور، تایید ایمیل و یا ذخیره و دریافت داده و یا ذخیره داده و دریافت آن از طریق کوئری های متنوع پیاده‌سازی شده است.
در عین حال در پارس سرور میتوان منطق ویژه سازی شده برای پروژه مورد نظر را پیاده‌سازی کرد.

## Parse Flutter SDK چیست؟
SDK فلاتر در بستر فلاتر، API هایی را در اختیار ما قرار میدهند که بتوانیم به سرور (که با پارس سرور پیاده‌سازی شده است) وصل شویم.
برای اتصال به سرور از راهبرد های متفاوتی از جمله استفاده از HTTP request به صورت خام استفاده کنیم. عمده مزیت استفاده از SDK دو چیز است. اول آنکه به مراتب ساده‌تر است.
چرا که به طور اختصاصی برای اتصال به سرور های پارس طراحی شده در صورتی که HTTP request برای کاربرد بسیار گسترده تری میباشد.
دوم اینکه بسیاری از موارد پیچیده از جمله caching، مدیریت خطا و تلاش مجدد برای ارسال request و بسیاری موارد SDK به خوبی انجام شده است و در نتیجه برنامه نویس از انجام آنها نیز آسوده میشود.
سومین مزیت استفاده از SDK در نظر نویسندگان این مقاله این است که برای شروع پروژه، چارچوبی برای کار اعضای تیم مشخص میشود و بخشی از کار معماری پروژه انجام میگیرد.
در این نوشته عمدتا در مورد Parse Flutter SDK صحبت خواهیم کرد.

## مزایای استفاده از Parse Server و SDK های آن چیست؟
عمده مزیت های استفاده از Parse Platform عبارت است از
1. کار انجام backend و کار های پیچیده backend مانند مباحث امنیتی به صورت عمده ای کم میشود.
2. SDK ها کار ارتباط میان client و server را ساده میکنند.
3. کارهایی از قبیل caching، میدیریت خطا و ... توسط SDK در کلاینت انجام میشوند.
4. ساختار اولیه پروژه در شروع کار با Parse Server شکل میگیرد.
5. پلتفرم پارس کاملا open-source است و کد سرور و SDK ها در GitHub موجود است.
6. پارس سرور در شرکت بزرگی مانند Facebook ایجاد شده و community توسط این شرکت هدایت شده است.
7. community استفاده از این پلتفرم نسبتا بزرگ است.

## ساختار نوشته
تلاش میکنیم تا با حفظ ساختار اصلی مستندات Parse، نوشته ای بنویسیم که کاربر پس از خواندن آن، پارس سرور و علی الخصوص Parse Flutter SDK را درک کند و بتواند از آن استفاده کند و در ادامه بتواند با مطالعه مستندات اصلی دانش خود را گسترش دهد.
منابع اصلی این مقاله عبارتند از
1. [مستند Parse Flutter SDK در pub.dev](https://pub.dev/packages/parse_server_sdk)
2. [مستند Parse Flutter SDK در وبسایت Parse Server](https://github.com/parse-community/Parse-SDK-Flutter/tree/master/packages/flutter)
3. [مستندات عمومی موحود در وبسایت Parse Server](https://parseplatform.org/)

## هوشیار باشید! 
جدا از SDK پارس سرور برای Flutter، یک SDK برای زبان Dart نیز وجود دارد.
لطفا این دو را از یک دیگر تمییز دهید و آنها را اشتباه نگیرید.

## شروع به کار

### مرحله اول 
ابتدا باید dependency مربوط به SDK را به فایل pubspec.yaml اضافه کنیم.
با استفاده از فرمان زیر در خط فرمان (Terminal / Command line) dependency اضافه خواهد شد.

<div dir="ltr">

```
$ flutter pub add parse_server_sdk_flutter
```
</div>

توجه کنید که از این SDK میتوان build برای موارد زیر دریافت کرد.
1. Android
2. iOS
3. Linux
4. macOS
5. Windows

#### توجه کنید 
امکان دریافت build برای نسخه وب وجود ندارد!

#### در حاشیه 
پس از اضافه شدن dependency میتواند به صورت زیر آن را در کد import کنید.

<div dir="ltr">

```Dart
import 'package:parse_server_sdk_flutter/generated/i18n.dart';
import 'package:parse_server_sdk_flutter/parse_server_sdk.dart';
```
</div>

#### در حاشیه 
[لینک صفحه pub.dev مربوط به dependency](https://pub.dev/packages/parse_server_sdk_flutter/install)

### مرحله دوم 
در این مرحله مشابه آنکه در اندروید در `onCreate` در کلاس Application پارس را initialize میکردیم.
در اینجا نیز در اولین call، کار initialization را انجام میدهیم.

<div dir="ltr">

```Dart
await Parse().initialize(
        keyApplicationId,
        keyParseServerUrl);
```
</div>

در صورت نیاز، میتوانیم سایر موارد را در صورت نیاز در همین تابع مقدار دهی کنیم. به عنوان مثال اگر نیاز به استفاده از storage داشته باشیم (کاربرد آن توضیح داده خواهد شد) میتوانیم به صورت زیر آن را نیز initial کنیم.

<div dir="ltr">

```Dart
await Parse().initialize(
  	keyParseApplicationId, 
  	keyParseServerUrl,
  	coreStore: await CoreStoreSembastImp.getInstance());
```
</div>

سایر موارد نیز به صورت مشابه میتوان initial کرد.

<div dir="ltr">

```Dart
await Parse().initialize(
        keyApplicationId,
        keyParseServerUrl,
        clientKey: keyParseClientKey, // Required for some setups
        debug: true, // When enabled, prints logs to console
        liveQueryUrl: keyLiveQueryUrl, // Required if using LiveQuery 
        autoSendSessionId: true, // Required for authentication and ACL
        securityContext: securityContext, // Again, required for some setups
        coreStore: await CoreStoreSharedPrefsImp.getInstance()); // Local data storage method. Will use SharedPreferences instead of Sembast as an internal DB
```
</div>

## Object ها
مشابه حوزه اندروید و  به صورت کلی منطق حاکم بر پلتفرم پارس، ابجکت ها مجموعه از key-value های دارای id هستند. 
### Object های متفرقه


### افزودن مقدار جدید به Object ها


### ذخیره کردن Object ها با استفاده از pin


## Storage

ذخیره‌سازی دو نوع امن و نا امن دارد؛ در حال حاضر دو گزینه برای این کار پیش رو داریم:

- SharedPreferences : این مورد تنها wrapper ای برای NSUserDefaults در iOS و SharedPreferences در اندروید است.

- Sembast (Simple Embedded Application Store database): این مورد ذخیره سازی امن را ارائه میدهد.

شیوه ذخیره سازی در پارامتر coreStore در
parse().initialize
تعریف میشود.

### تغییر شمارنده ها در Object ها

ابتدا Object را فراخوانی کرده، سپس به شکل زیر عمل میکنیم:

<div dir="ltr">

```Dart
var response = await dietPlan.increment("count", 1);
```
</div>

همچنین میتوان از تابع save استفاده کرد:

<div dir="ltr">

```Dart
dietPlan.setIncrement('count', 1);
dietPlan.setDecrement('count', 1);
var response = dietPlan.save()
```
</div>

### عملگر های آرایه در Object ها

Object را دریافت کرده و سپس داریم:

<div dir="ltr">

```Dart
var response = await dietPlan.add("listKeywords", ["a", "a","d"]);

var response = await dietPlan.addUnique("listKeywords", ["a", "a","d"]);

var response = await dietPlan.remove("listKeywords", ["a"]);
```
</div>

در صورت استفاده از تابع save نیز فرآیند به این صورت خواهد بود:

<div dir="ltr">

```Dart
dietPlan.setAdd('listKeywords', ['a','a','d']);
dietPlan.setAddUnique('listKeywords', ['a','a','d']);
dietPlan.setRemove('listKeywords', ['a']);
var response = dietPlan.save()
```
</div>

## Query ها

زمانی که شما پروژه را راه‌اندازی کرده‌اید و می‌خواهید کار را شروع کنید، می‌تواند با صدا زدن این تابع، دیتا را از سرور دریافت کنید:

<div dir="ltr">

```Dart
var apiResponse = await ParseObject('ParseTableName').getAll();

if (apiResponse.success){
  for (var testObject in apiResponse.result) {
    print(ApplicationConstants.APP_NAME + ": " + testObject.toString());
  }
}
```
</div>

یا می‌توانید که یک آبجکت را کمک آی‌دی از سرور بگیرید:

<div dir="ltr">

```Dart
var dietPlan = await DietPlan().getObject('R5EonpUDWy');

if (dietPlan.success) {
  print(ApplicationConstants.keyAppName + ": " + (dietPlan.result as DietPlan).toString());
} else {
  print(ApplicationConstants.keyAppName + ": " + dietPlan.exception.message);
}
```
</div>

برای کوئری زدن برای آبجکت‌های کاربر، می‌توانید از تابع `()ParseUser.forQuery` به این شکل استفاده کنید:
    
<div dir="ltr">

```Dart
var queryBuilder  = QueryBuilder<ParseUser>(ParseUser.forQuery())
  ..whereEqualTo('activated', true);

var response = await queryBuilder.query();

if (response.success) {
  print(response.results);
} else {
  print(response.exception.message);
}
```
</div>

#### روش‌های فرعی Query

تابع استاندارد Query که تابع `()query` یک عدد `ParseResponse` برمی‌گرداند که شامل نتیجه یا ارور می‌باشد. به عنوان یک راه دیگر، می‌تواند از `()Future<List<T>> find` برای دریافت گزینه‌ها استفاده کنید. این تابع یک `Future` برمی‌گرداند که یک ارور یا یک `List` که آبجکت‌های کوئری‌شده را در بر می‌گیرد. یک تفاوتی که وجود دارد این است که در هنگامی که آبجکتی با Query تطابق ندارد، `()Future<List<T>> find` یک لیست خالی به جای ارور "بدون نتیجه" برمی‌گرداند.

### Query های پیچیده

شما می‌توانید Queryهای پیچیده بسازید تا دیتابیستان را حسابی به چالش بکشید.

<div dir="ltr">

```Dart
var queryBuilder = QueryBuilder<DietPlan>(DietPlan())
  ..startsWith(DietPlan.keyName, "Keto")
  ..greaterThan(DietPlan.keyFat, 64)
  ..lessThan(DietPlan.keyFat, 66)
  ..equals(DietPlan.keyCarbs, 5);

var response = await queryBuilder.query();

if (response.success) {
  print(ApplicationConstants.keyAppName + ": " + ((response.results as List<dynamic>).first as DietPlan).toString());
} else {
  print(ApplicationConstants.keyAppName + ": " + response.exception.message);
}
```
</div>

اگر شما می‌خواهید که آبجکت‌هایی را بیابید که با یکی از چندین Query تطابق پیدا کند، شما می‌توانید از تابع `Querybuilder.or` استفاده کنید تا یک Query بسازید که یک OR از تمامی Queryهاییست که به آن پاس داده شده است. برای مثال اگر شما می‌خواهید بازیکنانی که تعداد زیادی برد یا تعداد کمی برد دارند را بیابید، می‌توانید این کار را کنید:

<div dir="ltr">

```Dart
ParseObject playerObject = ParseObject("Player");

QueryBuilder<ParseObject> lotsOfWins =
    QueryBuilder<ParseObject>(playerObject))
      ..whereGreaterThan('wins', 50);

QueryBuilder<ParseObject> fewWins =
    QueryBuilder<ParseObject>(playerObject)
      ..whereLessThan('wins', 5);

QueryBuilder<ParseObject> mainQuery = QueryBuilder.or(
      playerObject,
      [lotsOfWins, fewWins],
    );

var apiResponse = await mainQuery.query();
```
</div>

این قابلیت‌ها در دسترس هستند:

- برابری و نابرابری
- شامل بودن
- کوچکتر/بزرگتر (مساوی) بودن
- آغاز شدن و پایان یافتن با یک پترن خاص
- نزدیک بودن از نظر مسافتی
- Regex
- و ...

### Query های ارتباطی(relational)

برای بازیابی کردن آبجکت‌هایی که یک فیلدی دارند که شامل یک آبجکتی است که با یک Query خاصی تطابق دارد، شما می‌توانید از `whereMatchesQuery` استفاده کنید. برای مثال تصور کنید که شما یک کلاس Post و یک کلاس Comment دارید که هر Comment یک پوینتر به Post مربوط به آن دارد. شما می‌توانید Commentها را در Postهای عکس‌دار با این کار بیابید:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> queryPost =
    QueryBuilder<ParseObject>(ParseObject('Post'))
      ..whereValueExists('image', true);

QueryBuilder<ParseObject> queryComment =
    QueryBuilder<ParseObject>(ParseObject('Comment'))
      ..whereMatchesQuery('post', queryPost);

var apiResponse = await queryComment.query();
```

</div>

اگر می‌خواهید متضاد حالت قبل، یعنی جایی که آن آبجکت‌های درون فیلد با Query تطابق ندارند را بازیابی کنید، می‌توانید با کمک `whereDoesNotMatchQuery` مانند زیر عمل کنید. مثال مانند بخش قبل است فقط دنبال Commentها در Postهای بدون عکس هستیم:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> queryPost =
    QueryBuilder<ParseObject>(ParseObject('Post'))
      ..whereValueExists('image', true);

QueryBuilder<ParseObject> queryComment =
    QueryBuilder<ParseObject>(ParseObject('Comment'))
      ..whereDoesNotMatchQuery('post', queryPost);

var apiResponse = await queryComment.query();
```

</div>

شما می‌توانید از تابع `whereMatchesKeyInQuery` استفاده کنید تا آبجکت‌هایی را بگیرید که یک کلید تطابق دارد با مقدار یک کلید در یک مجموعه از آبجکت‌ها که با یک Query دیگر تطابق دارند. برای مثال، یک کلاس داریم که تیم‌های ورزشی را دارد و شهر سکونت یک کاربر را هم ذخیره می‌کنید. شما می‌توانید یک Query منتشر کنید که تیم‌های ورزشی شهر کاربر که رکورد برد دارند را به عنوان یک لیست بیابید. این Query به این شکل خواهد بود:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> teamQuery =
    QueryBuilder<ParseObject>(ParseObject('Team'))
      ..whereGreaterThan('winPct', 0.5);

QueryBuilder<ParseUser> userQuery =
    QueryBuilder<ParseUser>ParseUser.forQuery())
      ..whereMatchesKeyInQuery('hometown', 'city', teamQuery);

var apiResponse = await userQuery.query();
```

</div>

برای گرفتن متضاد حالت قبل، می‌توانید از تابع `whereDoesNotMatchKeyInQuery` استفاده کنید و مشابه مثال قبل، این بار تیم‌های شهر کاربر که رکورد باخت دارند را بیابید:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> teamQuery =
    QueryBuilder<ParseObject>(ParseObject('Team'))
      ..whereGreaterThan('winPct', 0.5);

QueryBuilder<ParseUser> losingUserQuery =
    QueryBuilder<ParseUser>ParseUser.forQuery())
      ..whereDoesNotMatchKeyInQuery('hometown', 'city', teamQuery);

var apiResponse = await losingUserQuery.query();
```
</div>

برای فیلتر کردن سطرها بر اساس آی‌دی‌های آبجکت‌ها از پوینترها در یک جدول ثانویه، می‌توانید از نوتیشن نقطه استفاده کنید:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> rolesOfTypeX =
    QueryBuilder<ParseObject>(ParseObject('Role'))
      ..whereEqualTo('type', 'x');

QueryBuilder<ParseObject> groupsWithRoleX =
    QueryBuilder<ParseObject>(ParseObject('Group')))
      ..whereMatchesKeyInQuery('objectId', 'belongsTo.objectId', rolesOfTypeX);

var apiResponse = await groupsWithRoleX.query();
```
</div>

### شمارش Object ها

اگر برای شما فقط تعداد بازی‌های یک بازیکن مهم است:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> queryPlayers =
    QueryBuilder<ParseObject>(ParseObject('GameScore'))
      ..whereEqualTo('playerName', 'Jonathan Walsh');
var apiResponse = await queryPlayers.count();
if (apiResponse.success && apiResponse.result != null) {
  int countGames = apiResponse.count;
}
```

</div>

### Query های live

این ابزار به شما این امکان را می‌دهد که از یک `QueryBuilder` استفاده کنید. هنگام استفاده، سرور به کلاینت‌ها اطلاع می‌دهد که یک `ParseObject` با `QueryBuilder` ساخته یا آپدیت شده است.

 `ParseLiveQuery` شامل دو قسمت است، قسمت سرور `LiveQuery` و قسمت کلاینت `LiveQuery`. برای استفاده از `LiveQuery`ها نیاز است که هر دو را راه بیندازید. راهنمای کانفیگ سرور پارس‌سرور در اینجا https://docs.parseplatform.org/parse-server/guide/#live-queries موجود است و تمرکز این مقاله روی آن نیست.

با وارد کردن پارامتر `liveQueryUrl` در `Parse Live Query`، `Parse().initialize` را راه‌اندازی کنید:

<div dir="ltr">

```Dart
Parse().initialize(
      keyApplicationId,
      keyParseServerUrl,
      clientKey: keyParseClientKey,
      debug: true,
      liveQueryUrl: keyLiveQueryUrl,
      autoSendSessionId: true);
```

</div>

`LiveQuery` را declare کنید:

<div dir="ltr">

```Dart
final LiveQuery liveQuery = LiveQuery();
```

</div>

`QueryBuilder`ی که قرار است توسط `LiveQuery` تحت نظارت قرار بگیرد را راه بیندازید:

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> query =
  QueryBuilder<ParseObject>(ParseObject('TestAPI'))
  ..whereEqualTo('intNumber', 1);
```

</div>

<b>یک `subscription` بسازید</b>، و شما می‌توانید که `event`های مربوط به `LiveQuery` را از طریق این `subscription` دریافت کنید. بار اولی که شما تابع `subscribe` را صدا بزنید، ما سعی می‌کنیم که ارتباط `WebSocket` را به سرور `LiveQuery` برای شما باز کنیم.

<div dir="ltr">

```Dart
Subscription subscription = await liveQuery.client.subscribe(query);
```

</div>

<b>مدیریت کردن `event`ها</b>، ما `event`های متنوعی تعریف کرده ایم که شما را به یک آبجکت `subscription` می‌رساند.

<b>`event` ساختن</b>، زمانی که یک `ParseObject` جدید ساخته شده است و `QueryBuilder` قولی که شما به آن `subscribe` کرده‌اید را عملی می‌کند، شما این `event` را دریافت می‌کنید. آن آبجکت همان `ParseObject`ی است که ساخته شده بود.

<div dir="ltr">

```Dart
subscription.on(LiveQueryEvent.create, (value) {
    print('*** CREATE ***: ${DateTime.now().toString()}\n $value ');
    print((value as ParseObject).objectId);
    print((value as ParseObject).updatedAt);
    print((value as ParseObject).createdAt);
    print((value as ParseObject).get('objectId'));
    print((value as ParseObject).get('updatedAt'));
    print((value as ParseObject).get('createdAt'));
});
```

</div>

<b>`event` آپدیت</b>، زمانی که یک `ParseObject` موجود که `QueryBuilder` به شما قول داده بود، آپدیت می‌شود، شما این `event` را دریافت می‌کنید. آبجکت همان `ParseObject`ی است که آپدیت شده بود و محتوای آن، آخرین مقادیر موجود در همان `ParseObject` است.

<div dir="ltr">

```Dart
subscription.on(LiveQueryEvent.update, (value) {
    print('*** UPDATE ***: ${DateTime.now().toString()}\n $value ');
    print((value as ParseObject).objectId);
    print((value as ParseObject).updatedAt);
    print((value as ParseObject).createdAt);
    print((value as ParseObject).get('objectId'));
    print((value as ParseObject).get('updatedAt'));
    print((value as ParseObject).get('createdAt'));
});
```

</div>

<b>`event` ورود</b>، زمانی که مقدار قدیمی `ParseObject` موجود، طبق معیارهای `QueryBuilder` نیست ولی مقدار جدید با معیارها تطابق دارد،این `event` را دریافت می‌کنید. این آبجکت همان `ParseObject`ی است که به `QueryBuilder` وارد می‌شود. محتوای آن آخرین مقدار موجود در `ParseObject` است.

<div dir="ltr">

```Dart
subscription.on(LiveQueryEvent.enter, (value) {
    print('*** ENTER ***: ${DateTime.now().toString()}\n $value ');
    print((value as ParseObject).objectId);
    print((value as ParseObject).updatedAt);
    print((value as ParseObject).createdAt);
    print((value as ParseObject).get('objectId'));
    print((value as ParseObject).get('updatedAt'));
    print((value as ParseObject).get('createdAt'));
});
```

</div>

<b>`event` خروج</b>، زمانی که مقدار جدید `ParseObject` موجود، طبق معیارهای `QueryBuilder` نیست ولی مقدار قبلی با معیارها تطابق دارد، این `event` را دریافت می‌کنید. این آبجکت همان `ParseObject`ی است که `QueryBuilder` را ترک می‌کند. محتوای آن آخرین مقدار موجود در `ParseObject` است.

<div dir="ltr">

```Dart
subscription.on(LiveQueryEvent.leave, (value) {
    print('*** LEAVE ***: ${DateTime.now().toString()}\n $value ');
    print((value as ParseObject).objectId);
    print((value as ParseObject).updatedAt);
    print((value as ParseObject).createdAt);
    print((value as ParseObject).get('objectId'));
    print((value as ParseObject).get('updatedAt'));
    print((value as ParseObject).get('createdAt'));
});
```

</div>

<b>`event` حذف</b>، زمانیست که یک `ParseObject` موجود طبق معیارهای `QueryBuikder` است، پاک شده است. در این هنگام، شما این `event` را دریافت می‌کنید. این آبجکت همان `ParseObject`ی است که حذف شده است.

<div dir="ltr">

```Dart
subscription.on(LiveQueryEvent.delete, (value) {
    print('*** DELETE ***: ${DateTime.now().toString()}\n $value ');
    print((value as ParseObject).objectId);
    print((value as ParseObject).updatedAt);
    print((value as ParseObject).createdAt);
    print((value as ParseObject).get('objectId'));
    print((value as ParseObject).get('updatedAt'));
    print((value as ParseObject).get('createdAt'));
});
```

</div>

<b>`unsubscribe`</b>، اگر شما می‌خواهید که از یک `QueryBuilder` دیگر `event` دریافت نکنید، می‌توانید `unsubscribe` کنید. بعد از این حرکت، شما دیگر هیچ `event`ی از این `QueryBuilder` دریافت نمی‌کنید و ارتباط `WebSocket` به سرور `LiveQuery` بسته می‌شود.

<div dir="ltr">

```Dart
liveQuery.client.unSubscribe(subscription);
```

</div>

<b>`قطع ارتباط`</b>، در حالتی که ارتباط کلاینت با سرور ناگهانی قطع شود، `LiveQuery` به صورت خودکار تلاش می‌کند که ارتباط دوباره برقرار شود. `LiveQuery` در بازه‌هایی با طول‌هایی که به مرور افزایش می‌یابند صبر می‌کند تا ارتباط دوباره را امتحان کند. به صورت پیش‌فرض، این بازه‌ها این اعداد هستند: `[10000 ,5000 ,2000 ,1000 ,500 ,0]` برای موبایل و `[5000 ,2000 ,1000 ,500 ,0]` برای وب. شما می‌توانید که این‌ها را با ساختن یک لیست با استفاده از پارامتر `liveListRetryIntervals` در `()Parse.initialize` تغییر دهید. ("۱-" به این معنی است که دیگر برقراری ارتباط صورت نگیرد.)

## ParseLiveList
در مواردی میخواهیم که لیست حاصل از یک کوئری را به کاربر نمایش بدهیم.
ممکن است هدف ما این باشد که دائما نتیجه بروز شده را به کاربر نمایش دهیم.
یک روش برای انجام این کار استفاده از LiveQuery است.
اما SDK ابزاری را در اختیار ما قرار میدهد که بوسیه آن نمایش لیست، آپدیت شدن و تغییرات آن توسط SDK مدیریت میشود.
با استفاده از ابزار ParseLiveList میتوانیم لیست حاصل از نتیجه یک کوئری را به سادگی نمایش دهیم و نتیجه آن را up to date نگه داریم.

تمامی ارتباط با ParseLiveList از طریق ParseLiveListWidget صورت میگیرد. به وسیله آن میتوانیم تیجه یک کوئری را به صورت منظم نشان دهیم و آپدیت کنیم.

<div dir="ltr">

```Dart
ParseLiveListWidget<ParseObject>(
  query: query,
  reverse: false,
  childBuilder:
      (BuildContext context, ParseLiveListElementSnapshot<ParseObject> snapshot) {
    if (snapshot.failed) {
      return const Text('something went wrong!');
    } else if (snapshot.hasData) {
      return ListTile(
        title: Text(
          snapshot.loadedData.get("text"),
        ),
      );
    } else {
      return const ListTile(
        leading: CircularProgressIndicator(),
      );
    }
  },
);
```
</div>

در مثال فوق، لیستی از متون نمایش داده میشود.
در زمان بارگیری، یک CircularProgressIndicator نمایش داده میشود.
و در صورت بروز خطا، پیغام خطا نمایش داده میشود.

میتوانیم با اضافه کردن listLoadingElement، در زمان لودینگ نیز انمیشن مناسب مانند ProgressBar نمایش بدهیم.

<div dir="ltr">

```Dart
ParseLiveListWidget<ParseObject>(
  query: query,
  childBuilder: childBuilder,
  listLoadingElement: Center(
    child: CircularProgressIndicator(),
  ),
);
```
</div>

همچنین میتوانیم با مقداردهی به Duration، زمان اجرای انیمیشن ها را مدیریت کنیم.

<div dir="ltr">

```Dart
ParseLiveListWidget<ParseObject>(
  query: query,
  childBuilder: childBuilder,
  duration: Duration(seconds: 1),
);
```
</div>

توجه کنید که در حالت کلی، پارامتر ها به صورت lazy loading دریافت میشوند.
ممکن است که بخواهیم پارامتر هایی حتما بارگیری شوند.
در این صورت آن پارامترها را در PreloadedColumns مشخص میکنیم.
نحوه دسترسی به این پارامتر ها در مثال زیر مشخص است.

<div dir="ltr">

```Dart
ParseLiveListWidget<ParseObject>(
  query: query,
  lazyLoading: true,
  preloadedColumns: ["test1", "sender.username"],
  childBuilder:
      (BuildContext context, ParseLiveListElementSnapshot<ParseObject> snapshot) {
    if (snapshot.failed) {
      return const Text('something went wrong!');
    } else if (snapshot.hasData) {
      return ListTile(
        title: Text(
          snapshot.loadedData.get<String>("text"),
        ),
      );
    } else {
      return ListTile(
        title: Text(
          "loading comment from: ${snapshot.preLoadedData?.get<ParseObject>("sender")?.get<String>("username")}",
        ),
      );
    }
  },
);
```
</div>

همچنین میتوانیم با قرار دادن lazyLoading = false، تمامی ابجکت را بارگیری کنیم.

## Users

برای ساختن یک user جدید به صورت زیر میتوان عمل کرد:

<div dir="ltr">

```Dart
Parse.initialize(new Parse.Configuration.Builder(context)
  .server(...)
  .applicationId(...)
  .enableLocalDataStore()
  .build());
```
</div>

حال برای این که این آبجکت ParseUser را در سرور signUp کنیم به صورت زیر عمل میکنیم:

<div dir="ltr">

```Dart
var response = await user.signUp();
if (response.success) user = response.result;
```
</div>

دقت کنید تکه کد بالا از کلیدواژه await استفاده میکند. یعنی این عمل به صورت asynchronous انجام میشود
و هر وقت که پاسخ از سمت سرور دریافت شد ادامه کار انجام میشود.

برای login کردن user هم میتوان مشابه قسمت قبل از کلیدواژه await استفاده کرد تا منتظر پاسخ سرور بمانیم:

<div dir="ltr">

```Dart
var response = await user.login();
if (response.success) user = response.result;
```
</div>

در هر دو فرآیند در response اطلاعاتی در مورد خطایی که ممکن است باعث عدم اجرای دستور
شده است آمده باشد.

برای logout کردن میتوان به طریقه زیر عمل کرد:

<div dir="ltr">

```Dart
var response = await user.logout();
if (response.success) {
    print('User logout');
}
```
</div>

برای مدیریت کردن token های session و یا برای بررسی این که در حال حاضر چه کاربری login کرده است میتوان به صورت زیر عمل کرد:

<div dir="ltr">

```Dart
user = ParseUser.currentUser();
```
</div>

اضافه کردن داده های جدید به کاربر:

<div dir="ltr">

```Dart
var user = ParseUser("TestFlutter", "TestPassword123", "TestFlutterSDK@gmail.com")
            ..set("userLocation", "FlutterLand");

```
</div>

کارهای دیگری که میتوان با ParseUser انجام داد شامل:
- درخواست بازنشانی رمزعبور
  
- درخواست تایید ایمیل
  
- دریافت تمام کاربران

- ذخیره و نابود کردن کاربر

- Query زدن

### ثبت نام و ورود 3rd party

معمولا ارائه دهندگان خدمات لاگین از کتاب خانه های مخصوص خودشان استفاده میکنند اما در فلاتر میتوان
با استفاده از متد LoginWith که در ParseUser ها موجود است میتوان نام ارائه دهنده سرویس به همراه اطلاعات مورد نیاز برای لاگین را در
یک مپ وارد کرد و به کمک این متد لاگین کرد.
در زیر مثالی از login برای facebook آورده شده که در آن از کتابخانه https://pub.dev/packages/flutter_facebook_login استفاده شده است:

<div dir="ltr">

```Dart
Future<void> goToFacebookLogin() async {
       final FacebookLogin facebookLogin = FacebookLogin();
       final FacebookLoginResult result = await facebookLogin.logInWithReadPermissions(['email']);
   
       switch (result.status) {
         case FacebookLoginStatus.loggedIn:
           final ParseResponse response = await ParseUser.loginWith(
               'facebook',
               facebook(result.accessToken.token,
                   result.accessToken.userId,
                   result.accessToken.expires));
   
           if (response.success) {
             // User is logged in, test with ParseUser.currentUser()
           }
           break;
         case FacebookLoginStatus.cancelledByUser:
               // User cancelled
           break;
         case FacebookLoginStatus.error:
               // Error
           break;
       }
     }

```
</div>

همچنین لاگین کردن با کمک حساب google نیز امکان‌پذیر است. در این مثال از کتابخانه
https://pub.dev/packages/google_sign_in استفاده شده است.

<div dir="ltr">

```Dart
class OAuthLogin {
  final GoogleSignIn _googleSignIn = GoogleSignIn( scopes: ['email', 'https://www.googleapis.com/auth/contacts.readonly'] );
  
  signInGoogle() async {
    GoogleSignInAccount account = await _googleSignIn.signIn();
    GoogleSignInAuthentication authentication = await account.authentication;
    await ParseUser.loginWith(
          'google',
          google(authentication.accessToken!, _googleSignIn.currentUser!.id,
              authentication.idToken!));
  }
}

```
</div>

## امنیت برای Object ها - ParseACL

در Parse برای تامین امنیت Object ها از ParseACL استفاده میشود.
ParseACL لیستی است که مشخص میکند چه کسانی میتوانند از یک Object بخوانند و یا در آن بنویسند.
هر Object به صورت پیش فرض یک لیست کنترل دسترسی دارد که همگی یک پیاده‌سازی از ParseACL هستند.

اگر ParseACL برای یک Object مشخص نشده باشد، آن Object عمومی تلقی میشود، یعنی همه میتوانند در آن بنویسند یا از آن بخوانند
(البته این قاعده برای ParseUser ها صدق نمیکند). ساده‌ترین راه برای پیاده‌سازی یک ParseACL این است که خواندن و نوشتن در یک آبجکت را به یک کاربر محدود کنیم.
برای این کار هنگامی که یک کاربر login کرده است new ParseACL(user) یک لیست دسترسی جدید میسازد که دسترسی را تنها به همان کاربر میدهد.
با ذخیره کردن یک Object با متد ACL ،save آن نیز ذخیره میشود:

<div dir="ltr">

```Dart
ParseUser user = await ParseUser.currentUser() as ParseUser;
ParseACL parseACL = ParseACL(owner: user);
  
ParseObject parseObject = ParseObject("TestAPI");
...
parseObject.setACL(parseACL);
var apiResponse = await parseObject.save();

```
</div>

میتوانید دسترسی را به هر یک از کاربر ها به صورت جداگانه اعطا کنید.
برای این کار از متد های setReadAccess و setWriteAccess استفاده کنید:

<div dir="ltr">

```Dart
ParseUser user = await ParseUser.currentUser() as ParseUser;
ParseACL parseACL = ParseACL();
//grant total access to current user
parseACL.setReadAccess(userId: user.objectId, allowed: true);
parseACL.setWriteAccess(userId: user.objectId, allowed: true);
//grant read access to userId: 'TjRuDjuSAO' 
parseACL.setReadAccess(userId: 'TjRuDjuSAO', allowed: true);
parseACL.setWriteAccess(userId: 'TjRuDjuSAO', allowed: false);

ParseObject parseObject = ParseObject("TestAPI");
...
parseObject.setACL(parseACL);
var apiResponse = await parseObject.save();
```
</div>

همچنین میتوانید به تمام کاربران به صورت یکجا اجازه خواندن و نوشتن را بدهید.
 برای این کار میتوان از متد های setPublicReadAccess و setPublicWriteAccess استفاده کرد:

<div dir="ltr">

```Dart
ParseACL parseACL = ParseACL();
parseACL.setPublicReadAccess(allowed: true);
parseACL.setPublicWriteAccess(allowed: true);

ParseObject parseObject = ParseObject("TestAPI");
...  
parseObject.setACL(parseACL);
var apiResponse = await parseObject.save();

```
</div>

عملیات هایی که مجاز به انجام آن نیستید؛ مانند پاک کردن Object ای که اجازه نوشتن در آن را ندارید؛
منجر به خطا با کد 101 میشوند:'ObjectNotFound'.
نمایش این پیغام خطا باعث میشود که افراد نتوانند بفهمند که کدام ObjectId ها وجود ندارند و کدام ها موجودند اما اجازه نوشتن در آن را ندارند.

به شیوه زیر میتوان ACL یک Object را دریافت کرد:

<div dir="ltr">

```Dart
ParseACL parseACL = parseObject.getACL();
```
</div>

## Config

ParseConfig مجموعه ای از داده های پیکربندی(Configuration) است که میتوان آن را از Parse dashboard تنظیم کرد.
برای گرفتن map ای از تمام config های موجود میتوانید به صورت زیر عمل کنید:

<div dir="ltr">

```Dart
var response = await ParseConfig().getConfigs();
```
</div>

و برای اضافه کردن config میتوانید به صورت زیر عمل کنید:

<div dir="ltr">

```Dart
ParseConfig().addConfig('TestConfig', 'testing')
```
</div>

## Cloud Functions

به کمک Cloud Function ها میتوانید بخشی از کد را روی سرور خود اجرا کنید و نتیجه آن را به کاربر برگردانید.
از مزیت های استفاده از این روش این است که میتوانید این function ها را بروزرسانی کنید و این تغییر برای کاربران بدون نیاز به بروزرسانی برنامه اعمال شود.
همچنین گاهی اوقات ممکن است که عملیاتی نیاز به حجم شدید داده یا پردازش نیاز داشته باشد که در این مواقع نیز میتوان با انجام پردازش روی سرور و فرستان نتیجه به کاربر اجرا را سریع تر کرد.

مثال: فرض کنید برنامه ای دارید که کاربران در آن میتوانند به فیلم های سینمایی امتیاز دهند. هر امتیاز به شکل زیر است:

<div dir="ltr">

```Json
{
  "movie": "The Matrix",
  "stars": 5,
  "comment": "Too bad they never made any sequels."
}
```
</div>

برای این که به کاربر نشان دهید امتیاز میانگین یک فیلم چقدر است میتوانید تمام امتیاز هایی که فیلم گرفته را برایش ارسال کنید اما این روش داده و پهنای باند زیادی نیاز دارد.
پس به جای این کار نتیجه را روی سرور محاسبه میکنید و برای کاربر تنها یک عدد ارسال میکنید.

تابع سمت سرور به صورت زیر خواهد بود:

<div dir="ltr">

```JavaScript 
Parse.Cloud.define("averageStars", async (request) => {
    const query = new Parse.Query("Review");
    query.equalTo("movie", request.params.movie);
    const results = await query.find();
    let sum = 0;
    for (let i = 0; i < results.length; ++i) {
        sum += results[i].get("stars");
    }
    return sum / results.length;
});
```
</div>

Cloud Function ها یک JSON را به عنوان ورودی میگیرند.
برای این که چنین تابعی را از سمت کلاینت فراخوانی کنیم میتوانیم به صورت زیر عمل کنیم:

<div dir="ltr">

```Dart 
final ParseCloudFunction function = ParseCloudFunction('averageStars');
final Map<String, String> params = <String, String>{'movie': 'The Matrix'};
final ParseResponse result =
    await function.executeObjectFunction<ParseObject>(params);
if (result.success) {
  if (result.result is ParseObject) {
    print(result.result);
  }
}
```
</div>

## Relation
مطابق منطق Parse، میتوانیم بین object ها relation برقرار کنیم. اضافه کردن و حذف کردن relation به شکل زیر است.

<div dir="ltr">

```Dart
dietPlan.addRelation('fruits', [ParseObject("Fruits")..set("objectId", "XGadzYxnac")]);
```

</div>

<div dir="ltr">

```Dart
dietPlan.removeRelation('fruits', [ParseObject("Fruits")..set("objectId", "XGadzYxnac")]);
```

</div>

همچنین میتوان با توجه به relation ها کوئری دریافت کرد. دریافت کوئری به وسیله relation به صورت زیر است.

<div dir="ltr">

```Dart
QueryBuilder<ParseObject> query =
    QueryBuilder<ParseObject>(ParseObject('Fruits'))
      ..whereRelatedTo('fruits', 'DietPlan', DietPlan.objectId);
```

</div>

## File
سه کلاس برای فایل ها در SDK وجود دارد:
1. `ParseFileBase`: این یک کلاس abstract است که همه انواع فایل را میتواند مدیریت کند.
2. `ParseFile`: این کلاس از `ParseFileBase` گسترش یافته است (extended). در تمام پلتفرم ها به جز web، از این فرمت برای ذخیره‌سازی فایل ها استفاده میشود. در این کلاس از File در dart:io استفاده میشود.
3. `ParseWebFile`: این کلاس معادل `ParseFile` است که در وب استفاده میشود. با این تفاوت که از Uint8List استفاده میشود.

همچنین میتوان با extend کردن کلاس های دلخواه را ایجاد کرد.

آپلود و دانلود فایل در Parse ساده است. مثال زیر را در نظر بگیرید. با توجه به اینکه فایل از چه نوعی است، میتوان رفتار را تمییز داد. همچنین میتوان در زمانی که هنوز progress کامل نشده، progressBar را نمایش داد.

<div dir="ltr">

```Dart
//A short example for showing an image from a ParseFileBase
Widget buildImage(ParseFileBase image){
  return FutureBuilder<ParseFileBase>(
    future: image.download(),
    builder: (BuildContext context,
    AsyncSnapshot<ParseFileBase> snapshot) {
      if (snapshot.hasData) {
        if (kIsWeb) {
          return Image.memory((snapshot.data as ParseWebFile).file);
        } else {
          return Image.file((snapshot.data as ParseFile).file);
        }
      } else {
        return CircularProgressIndicator();
      }
    },
  );
}
```

</div>

</div>
