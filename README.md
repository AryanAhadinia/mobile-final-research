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

### Query های پیچیده

### Query های ارتباطی(relational)

### شمارش Object ها

### Query های live

## ParseLiveList

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
