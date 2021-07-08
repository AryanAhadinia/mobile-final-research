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
علی الرغم سادگی های Flutter خوب است که پیش از شروع دانش native در مورد برنامه سازی موبایل و وب (در صورتی که build برای نسخه وب نیز میخواهید دریافت کنید) داشته باشید.
میتوانید برای مطالعه در مورد SDK پارس سرور برای Android از
[این مقاله](https://github.com/AryanAhadinia/mobile-midterm-research)
که توسط همین گروه نگاشته شده است استفاده کنید.

## شروع به کار

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
(البته این قاعده برای ParseUser ها صدق نمیکند). ساده ترین راه برای پیاده سازی یک ParseACL این است که خواندن و نوشتن در یک آبجکت را به یک کاربر محدود کنیم.
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

میتوانید دسترسی را به تک تک کاربر ها به صورت جداگانه اعطا کنید.
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

## File

</div>
