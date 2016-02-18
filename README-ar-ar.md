
#مقدمة

هذا الدليل هو الترجمة الفرنسية [دليل أسلوب AngularJS] (https://github.com/mgechev/angularjs-style-guide).

والغرض من هذا الدليل الاسلوب هو لتوضيح مجموعة من أفضل الممارسات والمبادئ التوجيهية أسلوب لتطبيق AngularJS.
أنها تأتي:

0. شفرة المصدر AngularJS
0. الشفرة المصدرية أو المواد التي قرأت
0. تجربتي الخاصة.

** 1 ** ملاحظة: هذا الدليل لا يزال في شكل مسودة. الهدف الرئيسي منه هو وضعها من قبل المجتمع، لذلك سيتم ملء الفجوات موضع تقدير كبير من قبل المجتمع بأكمله.

** ** ملاحظة 2: قبل اتباع بعض الترجمات، المبادئ التوجيهية للوثيقة الإنجليزية الأصلية، تأكد من أنها تصل إلى موعد مع [آخر] (https://github.com/mgechev/angularjs-style- دليل / فقاعة / الماجستير / README.md).

في ذلك، فإنك لن تجد المبادئ التوجيهية العامة للتنمية جافا سكريبت. يمكنك العثور عليها في الوثائق التالية:

0. [دليل أسلوب جوجل جافا سكريبت] (http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
0. [دليل أسلوب موزيلا جافا سكريبت] (https://developer.mozilla.org/en-US/docs/Developer_Guide/Coding_Style)
0. [دليل أسلوب جيثب في جافا سكريبت] (https://github.com/styleguide/javascript)
0. [دليل أسلوب دوغلاس كروكفورد في جافا سكريبت] (http://javascript.crockford.com/code.html)
0. [عبر Airbnb جافا سكريبت دليل نمط] (https://github.com/airbnb/javascript)

تطوير AngularJS، دليل الموصى به هو [دليل أسلوب جوجل جافا سكريبت] (http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml).

في الويكي جيثب من AngularJS، هناك قسم مماثل من [ProLoser] (https://github.com/ProLoser)، يمكنك استشارة [هنا] (https://github.com/angular/angular. شبيبة / ويكي).

#table المحتويات

* [عام] (# عامة)
    * [شجرة] (# شجرة)
    * [وسم] (# العلامات)
    * [تحسين دورة التجهيز] (# الأمثل، ودورة ل-العلاج)
    * [أخرى] (# غيرها)
* [وحدات] (# وحدات)
* [تحكم] (# التحكم)
* [المبادئ التوجيهية] (# المبادئ التوجيهية)
* [شروط] (# مرشحات)
* [الخدمات] (# الخدمات)
* [قوالب] (# قوالب)
* [توجيه] (# التوجيه)
* [الاختبارات] (# الاختبارات)
* [المساهمة] (# مساهمة)

# العام

## شجرة

منذ AngularJS تطبيق كبيرة لديها العديد من العناصر، فمن الأفضل لهيكلة في التسلسل الهرمي الدليل.
هناك نهجين رئيسيين:

* إنشاء قسم رفيع المستوى من نوع المكون وأقل ميزة تقسيم. في هذه الطريقة، فإن بنية الدليل تبدو

```
.
├── app
│   ├── app.js
│   ├── controllers
│   │   ├── home
│   │   │   ├── FirstCtrl.js
│   │   │   └── SecondCtrl.js
│   │   └── about
│   │       └── ThirdCtrl.js
│   ├── directives
│   │   ├── home
│   │   │   └── directive1.js
│   │   └── about
│   │       ├── directive2.js
│   │       └── directive3.js
│   ├── filters
│   │   ├── home
│   │   └── about
│   └── services
│       ├── CommonService.js
│       ├── cache
│       │   ├── Cache1.js
│       │   └── Cache2.js
│       └── models
│           ├── Model1.js
│           └── Model2.js
├── partials
├── lib
└── test
```

* إنشاء قسم رفيع المستوى من الأداء الوظيفي وانخفاض نوع مستوى المكونات. هنا مخطط له:

```
.
├── app
│   ├── app.js
│   ├── common
│   │   ├── controllers
│   │   ├── directives
│   │   ├── filters
│   │   └── services
│   ├── home
│   │   ├── controllers
│   │   │   ├── FirstCtrl.js
│   │   │   └── SecondCtrl.js
│   │   ├── directives
│   │   │   └── directive1.js
│   │   ├── filters
│   │   │   ├── filter1.js
│   │   │   └── filter2.js
│   │   └── services
│   │       ├── service1.js
│   │       └── service2.js
│   └── about
│       ├── controllers
│       │   └── ThirdCtrl.js
│       ├── directives
│       │   ├── directive2.js
│       │   └── directive3.js
│       ├── filters
│       │   └── filter3.js
│       └── services
│           └── service3.js
├── partials
├── lib
└── test
```

* عند وضع مبادئ توجيهية، فإنه قد يكون من المناسب وضع كافة الملفات المرتبطة التوجيه (قوالب، CSS ملفات / ساس، وجافا سكريبت) في مجلد واحد. إذا اخترت استخدام هذا النمط شجرة، تكون متسقة واستخدامها في جميع أنحاء المشروع.

```
app
└── directives
    ├── directive1
    │   ├── directive1.html
    │   ├── directive1.js
    │   └── directive1.sass
    └── directive2
        ├── directive2.html
        ├── directive2.js
        └── directive2.sass
```

هذا النهج يمكن الجمع بين كل من بنية الدليل أعلاه.

* والتي كانت واحدة الاختلاف الأخير من بنية الدليل اثنين في [نغ-النمطي] (http://joshdmiller.github.io/ng-boilerplate/#/home). في ذلك، وحدة الاختبارات لمكون معين في نفس المجلد مثل عنصر. بهذه الطريقة، عند تغيير عنصر معين، فمن السهل أن تجد تجاربها. الاختبارات أيضا أن تأخذ مكان لإظهار الوثائق واستخدام الحالات.

```
services
├── cache
│   ├── cache1.js
│   └── cache1.spec.js
└── models
    ├── model1.js
    └── model1.spec.js
```

* و`ملف app.js` يحتوي على تعريف الطرق والتكوين و / أو فتيلة اليدوي (إذا لزم الأمر).
* يجب أن يحتوي كل ملف جافا سكريبت عنصر واحد فقط. يجب تسمية الملف مع اسم المكون.
* استخدام هيكل المشروع نموذجا لالزاوي [الفلاح] (http://yeoman.io) أو [نغ-النمطي] (http://joshdmiller.github.io/ng-boilerplate/#/home).

أنا أفضل أول هيكل لأنه يجعل عناصر مشتركة من الأسهل العثور على.

الاتفاقيات على مكونات تسمية يمكن العثور عليها في القسم من كل مكون.

بمناسبة ##

[TLDR;](http://developer.yahoo.com/blogs/ydn/high-performance-sites-rule-6-move-scripts-bottom-7200.html) وضع البرامج النصية أسفل جدا.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>MyApp</title>
</head>
<body>
  <div ng-app="myApp">
    <div ng-view></div>
  </div>
  <script src="angular.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

حفظ الأشياء بسيطة وإلى مبادئ توجيهية محددة من AngularJS آخر. بهذه الطريقة فمن السهل للتحقق من رمز وايجاد تحسينات في HTML التي يقدمها الإطار (الذي يفيد الصيانة).

```
<form class="frm" ng-submit="login.authenticate()">
  <div>
    <input class="ipt" type="text" placeholder="name" require ng-model="user.name">
  </div>
</form>
```

يجب أن سمات HTML أخرى متابعة توصيات [رمز الدليل] (http://mdo.github.io/code-guide/#html-attribute-order) مارك أوتو.

## تحسين دورة العلاج

* مراقبة فقط أهم المتغيرات (على سبيل المثال، عند استخدام الاتصالات في الوقت الحقيقي، لا تسبب `$ digest` حلقة في كل رسالة وردت).
* بالنسبة للمحتوى تهيئة مرة واحدة فقط ومن ثم لا يتغير، وتقييم استخدام مرة واحدة بصفة مراقب [bindonce] (https://github.com/Pasvaz/bindonce).
* جعل العمليات الحسابية في `$ watch` بسيطة بقدر الإمكان. جعل والحسابات بطيئة وثقيلة في واحد `$ watch` بطء تطبيق كامل (the` $ digest` حلقة ينفذ في موضوع واحد بسبب طبيعة ترابط واحد من جافا سكريبت).
* تعيين المعلمة الثالثة من وظيفة `timeout` $ إلى false لتجنب the` حلقة $ digest` عندما يتأثر أي من المتغيرات التي لاحظها رد` $ timeout`.

## أخرى

* استعمال:
    * `$ Timeout` بدلا of` setTimeout`
    * `$ Window` بدلا of` window`
    * `$ Document` بدلا of` document`
    * `$ Http` بدلا of` .ajax` $

وهذا سيجعل اختبارات أسهل، وفي بعض الحالات، منع سلوك غير متوقع (على سبيل المثال، إذا كنت قد نسيت `نطاق $. $ Apply` in` setTimeout`).

* أتمتة تدفق العمل الخاص بك عن طريق استخدام أدوات مثل:
    * [Yeoman] (http://yeoman.io)
    * [Gulp] (http://gulpjs.com)
    * [Grunt] (http://gruntjs.com)
    * [Bower] (http://bower.io)

* وعد الاستخدام ( `q` $) بدلا من تذكير (رد). وستجعل التعليمات البرمجية الخاصة بك أكثر أناقة ونظيفة وسهلة لمشاهدة، ويخلصك من الاسترجاعات الجحيم.
* استخدم `$ resource` بدلا of` $ http` عندما يكون ذلك ممكنا. وهناك مستوى أعلى من التجريد يسمح لك لانقاذ الكثير من التكرار.
* استخدام AngularJS قبل minifier (كما [نغ-علق] (https://github.com/olov/ng-annotate)) لمنع المشاكل بعد تصغير الحجم.
* لا تستخدم المتغيرات العالمية. حل كل التبعيات باستخدام حقن التبعية.
* لا تلوث بك `$ scope` متناول اليد. فقط إضافة وظائف والمتغيرات التي يتم استخدامها في القوالب.
* القضاء على المتغيرات العالمية مع النخير / بلع لanglober التعليمات البرمجية في التعبير وظيفة استدعي على الفور (الاحتجاج على الفور وظيفة التعبير، IIEF). يمكنك استخدام الإضافات مثل [نخر التفاف] (https://www.npmjs.com/package/grunt-wrap) أو [بلع التفاف] (https://www.npmjs.com/package/gulp-wrap /) لهذا الغرض. مثال (مع بلع)

```Javascript
	gulp.src("./src/*.js")
    .pipe(wrap('(function(){\n"use strict";\n<%= contents %>\n})();'))
    .pipe(gulp.dest("./dist"));
    ```
    
* يفضل استخدام وحدات التحكم بدلا من [ `ngInit`] (https://github.com/angular/angular.js/pull/4366/files). الاستخدام السليم الوحيد ل`ngInit` هو تهيئة خصائص معينة of` ngRepeat`. وبالاضافة الى هذه الحالة، يجب استخدام وحدات التحكم بدلا من `ngInit` تهيئة القيم على الموظفين. التعبير تمريرها إلى `ngInit` يجب تحليلها وتقييمها من قبل مترجم الزاوي تنفيذها في the` خدمة $ parse`. وهذا يؤدي إلى:
    - الآثار المترتبة على الأداء، لأن تنفذ المترجم في جافا سكريبت
    - التخزين المؤقت الماضي خدمة تعبيرات `$ parse` ليس له معنى حقيقي في معظم الحالات، نظرا إلى أن term` ngInit` يتم تقييم مرة واحدة
    - سلاسل كتابة حرف في HTML الخاص بك يمكن أن يخطئ، حيث لا يوجد تكملة أو دعم من قبل محرر النصوص
    - لا يوجد استثناء تنازل في وقت التشغيل
* لا تستخدم البادئة `` $ لأسماء المتغيرات والخصائص والأساليب. محجوز هذا بادئة لAngularJS الاستخدام.
* عندما حل تبعيات التبعيات من نظام حقن (التبعية حقن، DI) من AngularJS، نوع تبعيات في نوع و[مدش]؛ تبعيات متكاملة AngularJS الأول، وجاء لك:

```javascript
module.factory('Service', function ($rootScope, $timeout, MyCustomDependency1, MyCustomDependency2) {
  return {
    //Something
  };
});
```

#Modules

وينبغي أن يعين * وحدات lowerCamelCase. للإشارة إلى أن `حدة b` في هو module` الوحدة الفرعية لل، يمكنك عش في مساحة الاسم utlisant كما` a.b`.

الطرق شيوعا هما لهيكلة وحدات هي:

0. الوظيفة من قبل على & nbsp؛
0. نوع المكون.

حاليا، ليس هناك فرق كبير بين الاثنين ولكن أولا يبدو أكثر نظافة. أيضا، إذا تم تنفيذ تحميل كسول وحدات (حاليا ليس على خارطة طريق لAngularJS)، وسوف تحسين أداء التطبيق.

التحكم #

* لا تعامل مع DOM في وحدات التحكم الخاصة بك. وهذا من شأنه جعل جهاز تحكم أكثر صعوبة لاختبار وسينتهك [مبدأ الفصل بين المخاوف] (https://en.wikipedia.org/wiki/Separation_of_concerns). بدلا من ذلك، استخدم الإرشادات.
* يتم الحصول على اسم وحدة تحكم من وظيفتها (مثل سلة، لوحة الإدارة الصفحة الرئيسية) ب بواسطة `Ctrl`. تتم تسمية وحدات تحكم UpperCamelCase ( `HomePageCtrl`،` ShoppingCartCtrl`، `AdminPanelCtrl`، الخ)
* لا ينبغي أن تكون محددة وحدة تحكم في السياق العالمي (على الرغم من تصاريح qu'AngularJS، وهذا هو عادة سيئة من تلويث مساحة العالمي).
* تعيين وحدات التحكم باستخدام الجداول:

``` JavaScript
module.controller('MyCtrl', ['dependency1', 'dependency2', ..., 'dependencyn', function (dependency1, dependency2, ..., dependencyn) {
  //...body
}]);
```

هذا التعريف يتجنب المشاكل مع تصغير الحجم. يمكنك توليد تعريف المصفوفة تلقائيا باستخدام أدوات مثل [نغ-علق] (https://github.com/olov/ng-annotate) (ومهمة نخر [نخر-NG-علق] (HTTPS : //github.com/mzgol/grunt-ng-annotate)).
* استخدام الأسماء الأصلية من تبعيات وحدة تحكم. هذا وسوف تساعدك على إنتاج رمز أكثر قابلية للقراءة:

```JavaScript
module.controller('MyCtrl', ['$scope', function (s) {
  //...body
}]);
```

أقل قابلية للقراءة

```JavaScript
module.controller('MyCtrl', ['$scope', function ($scope) {
  //...body
}]);
```

هذا ينطبق بشكل خاص على ملف يحتوي خطوط عديدة من التعليمات البرمجية التي سوف تحتاج إلى التمرير. وهذا يمكن أن تجعلك تنسى الذي متغير يرتبط إلى أي التبعية.

* جعل تحكم بسيطة بقدر الإمكان. استخراج المهام شائعة الاستخدام في الخدمة.
* التواصل بين مختلف وحدات تحكم استخدام استدعاء الأسلوب (ممكنة عندما يريد الطفل على التواصل مع الأم) أو $ emit` `،` `و$ broadcast` $ on`. يجب أن يكون الحد الأدنى للرسائل الصادرة والبث.
* تقديم قائمة من جميع الرسائل التي تم تمريرها باستخدام `` emit` $ و $ broadcast`، والتعامل معه بعناية بسبب الصراعات اسم والبق الممكنة.
على سبيل المثال:

 ```JavaScript
   // app.js
   /* * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
   Custom events:
     - 'authorization-message' - description of the message
       - { user, role, action } - data format
         - user - a string, which contains the username
         - role - an ID of the role the user has
         - action - specific ation the user tries to perform
   * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
   ```
* إذا كنت بحاجة إلى تنسيق البيانات ثم لف منطق التنسيق في [فلتر] (# فلتر) وتعلن بأنها تبعية:

```JavaScript
module.filter('myFormat', function () {
  return function () {
    //body...
  };
});

module.controller('MyCtrl', ['$scope', 'myFormatFilter', function ($scope, myFormatFilter) {
  //body...
}]);
```

* ومن الأفضل استخدام بناء الجملة `as` تحكم:

  ```
  <div ng-controller="MainCtrl as main">
     {{ main.title }}
  </div>
  ```

  ```JavaScript
  app.controller('MainCtrl', MainCtrl);

  function MainCtrl () {
    this.title = 'Some title';
  }
  ```

   المزايا الرئيسية لاستخدام بناء الجملة التالي:
* إنشاء المكونات الفردية - الخصائص المتعلقة ليست جزءا من `$ scope` سلسلة النماذج. هذا هو ممارسة جيدة منذ إرث `النموذج $ scope` لديه بعض العوائق الرئيسية (ربما كان هذا السبب في أنه صراط حذف الزاوي 2):
    * ومن الصعب تتبع البيانات لمعرفة أين يذهبون.
    * قيمة تغيير نطاق قد تؤثر على بعض ضعت بشكل غير متوقع.
    * أكثر صعوبة في ريفاكتور (إعادة بيع ديون).
    * حكم النقاط: '[حكم نقطة (باللغة الإنجليزية)] (http://jimhoskins.com/2012/12/14/nested-scopes-in-angularjs.html).
* لا تستخدم `$ scope` باستثناء الحاجة للعمليات الخاصة (مثل نطاق as` $. Broadcast` $) هو التحضير الجيد لAngularJS V2.
* بناء الجملة هو أقرب إلى الصانع جافا سكريبت الخام ( 'الفانيليا').

   اكتشاف بناء الجملة `تحكم as` التفاصيل: [adoptez-la-syntaxe-controller-as](http://www.occitech.fr/blog/2014/06/adoptez-la-syntaxe-controller-as-angularjs/)

* تجنب كتابة منطق الأعمال في وحدة تحكم. نقل منطق الأعمال إلى `modèle` من خلال الخدمة.
  مثلا:

  ```Javascript
  //Ceci est un comportement répandu (mauvais exemple) d'utiliser le contrôleur pour implémenter la logique métier.
  angular.module('Store', [])
  .controller('OrderCtrl', function ($scope) {

    $scope.items = [];

    $scope.addToOrder = function (item) {
      $scope.items.push(item);//-->Logique métier dans le contrôleur
    };

    $scope.removeFromOrder = function (item) {
      $scope.items.splice($scope.items.indexOf(item), 1);//-->Logique métier dans le contrôleur
    };

    $scope.totalPrice = function () {
      return $scope.items.reduce(function (memo, item) {
        return memo + (item.qty * item.price);//-->Logique métier dans le contrôleur
      }, 0);
    };
  });
  ```

  عند استخدام خدمة ك "نموذج" لتنفيذ منطق الأعمال، وهذا ما يبدو وحدة تحكم مثل (انظر "استخدام خدمة مثل نموذج الخاص بك لتنفيذ خدمة طراز):

   ```Javascript
  //Order est utilisé comme un 'modèle'
  angular.module('Store', [])
  .controller('OrderCtrl', function (Order) {

    $scope.items = Order.items;

    $scope.addToOrder = function (item) {
      Order.addToOrder(item);
    };

    $scope.removeFromOrder = function (item) {
      Order.removeFromOrder(item);
    };

    $scope.totalPrice = function () {
      return Order.total();
    };
  });
  ```

  لماذا تنفيذ منطق الأعمال في وحدة تحكم هو ممارسة سيئة؟
* يتم إنشاء مثيل وحدات تحكم لكل طريقة عرض HTML ويتم تدمير تفريغ البصر.
* تحكم ليست قابلة لإعادة الاستخدام - أنها ترتبط إلى العرض HTML.
* لا يقصد من وحدات التحكم الكائنات حقن.

* في حالة وحدات تحكم جزءا لا يتجزأ من استخدام نطاقات متداخلة (مع `controllerAs`)

** ** App.js
```javascript
module.config(function ($routeProvider) {
  $routeProvider
    .when('/route', {
      templateUrl: 'partials/template.html',
      controller: 'HomeCtrl',
      controllerAs: 'home'
    });
});
```
** ** HomeCtrl
```javascript
function HomeCtrl() {
  this.bindingValue = 42;
}
```
**template.html**
```
<div ng-bind="home.bindingValue"></div>
```
#Directives

* اسم المبادئ التوجيهية الخاصة بك lowerCamelCase
* استخدام `` scope` بدلا من scope` $ في وظيفة وصلتك. في تجميع، تجميع وظائف الارتباط قبل / بعد، لديك بالفعل الحجج مرت عندما يتم استدعاء الدالة، فإنك لن تكون قادرا على تغيير استخدام DI. ويستخدم هذا النمط أيضا في التعليمات البرمجية المصدر من AngularJS.
* استخدام البادئات مخصصة للتعليمات الخاصة بك لتجنب المكتبات الخاصة بجهات أخرى لاصطدام الاسم.
* لا تستخدم `` `أو نانوغرام ui` مسبوقة لأنها محجوزة للAngularJS واستخدام AngularJS واجهة المستخدم.
* ينبغي أن يتم التلاعب DOM فقط مع توجيهات.
* إنشاء نطاق معزولة عند وضع مكونات قابلة لإعادة الاستخدام.
* استخدام المبادئ التوجيهية كما السمات أو العناصر بدلا من تعليقات أو الطبقات، وهذا سيجعل رمز أكثر قابلية للقراءة.
* استخدم `$ النطاق. $ في ( '$ تدمير، الجبهة الوطنية)` لتنظيف الأشياء الخاصة بك / المتغيرات. وهذا مفيد خصوصا عند استخدام الإضافات طرف ثالث مثل المبادئ التوجيهية.
* لا تنس أن تستخدم `$ sce` عند وجها لمحتوى غير موثوق بها.

#Filtres

* اسم المرشحات lowerCamelCase الخاص بك.
* جعل الفلتر ضوء ممكن. وغالبا ما يدعون `حلقة $ digest`، وبالتالي خلق تصفية بطيئة سوف تبطئ التطبيق الخاص بك.
* الحد من الفلاتر لشيء واحد، والاحتفاظ بها ومتسقة. ويمكن الحصول على مزيد من التلاعب المعقدة التي تربط بين مرشحات القائمة.

#services

يحتوي هذا القسم على معلومات حول خدمة المكونات في AngularJS. ما لم ينص على خلاف ذلك، فإنها لا تعتمد على الطريقة التي استخدمت لتحديد الخدمات (أي د. Provider` `،` factory`، `service`).

* اسم خدمات camelCase الخاص بك:
  * UpperCamelCase (PascalCase) لخدماتك تستخدم بناه، أي :

```JavaScript
module.controller('MainCtrl', function ($scope, User) {
  $scope.user = new User('foo', 42);
});

module.factory('User', function () {
  return function User(name, age) {
    this.name = name;
    this.age = age;
  };
});
```

  * LowerCamel لجميع الخدمات الأخرى.

* لف منطق الأعمال في الخدمات.
* و`طريقة service` هو الأفضل the` factory` الأسلوب. بهذه الطريقة يمكننا الاستمتاع بالتراث الكلاسيكي أكثر سهولة:

```JavaScript
function Human() {
  //body
}
Human.prototype.talk = function () {
  return "I'm talking";
};

function Developer() {
  //body
}
Developer.prototype = Object.create(Human.prototype);
Developer.prototype.code = function () {
  return "I'm codding";
};

myModule.service('Human', Human);
myModule.service('Developer', Developer);

```

* للحصول على مخبأ الدورة، يمكنك استخدام `$ cacheFactory`. وينبغي أن تستخدم لتخزين نتائج الاستعلام أو العمليات الحسابية الثقيلة.
* إذا خدمة معينة تتطلب التكوين، تعيين الخدمة كمقدم وتكوينه وذلك في رد `config`:

```JavaScript
angular.module('demo', [])
.config(function ($provide) {
  $provide.provider('sample', function () {
    var foo = 42;
    return {
      setFoo: function (f) {
        foo = f;
      },
      $get: function () {
        return {
          foo: foo
        };
      }
    };
  });
});

var demo = angular.module('demo');

demo.config(function (sampleProvider) {
  sampleProvider.setFoo(41);
});
```

#Gabarits

* استخدام `` نغ-NG-bind` أو cloak` بدلا من بسيطة `{{}}` لمنع محتويات الاصطدامات
* تجنب كتابة التعليمات البرمجية المعقدة في قوالب
* عندما كنت في حاجة لتحديد `src` صورة حيوي، use` نانوغرام src` بدلا من` with` src` {} {} `في القالب. هذا هو السماح لدينامية التحديث؟ (NLDT)
* بدلا من استخدام نطاق المتغير $ كسلسلة واستخدامها مع atribut style` و`` {{}} `استخدام Directive` نانوغرام style` مع المعلمات الكائن كما ونطاق المتغيرات كقيم:

```HTML
<script>
...
$scope.divStyle = {
  width: 200,
  position: 'relative'
};
...
</script>

<div ng-style="divStyle">my beautifully styled div which will work in IE</div>;
```

#Routage

* استخدم `resolve` لحل التبعيات قبل أن يتم عرض طريقة العرض.

#Tests

يحدد لاحقا

#Contribution

لأن هذا دليل أسلوب يهدف إلى أن يكون مشروع المجتمع، هي محل تقدير كبير المساهمات. على سبيل المثال، يمكنك المساهمة من خلال تطوير [الاختبارات] المقطع (# اختبارات) أو عن طريق ترجمة دليل في لغتك.

