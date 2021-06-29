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

## Parse برای Flutter

## شروع به کار

## Object ها

### Object های متفرقه

### افزودن مقدار جدید به Object ها

### ذخیره کردن Object ها با استفاده از pin

## ذخیره سازی

### تغییر شمارنده ها در Object ها

### عملگر های آرایه در Object ها

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

## Cloud Functions

## Relation

## File

</div>
