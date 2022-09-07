# android_question_anwser
安卓常见问题与解决方案记录
有新的问题可以提到issue中，我会整理后更新这些问题
还有一些我自己用过比较好用的库，我也整理到了另一个仓库中，有需要可以前往查看 [https://github.com/JackiePenghe/android_usefull_responsitory](https://github.com/JackiePenghe/android_usefull_responsitory)

### 引入aar包(jar包同理)

在需要引入包的module的build.gradle中加入这些依赖库，加入的位置如下

```xml
android {
    ...
}
dependencies {
    ...
    //在此处添加依赖
}
```

#### 方式1：
```xml
    //引入指定的aar库(下方的aars表示与module目录中"src"文件夹同级的目录名，可以是libs，也可以是新建的其它文件目录)
    //每次同名的aar文件有变更时不会实时生效，需要注释后同步一次，再取消注释后同步一次可生效
    implementation files("aars/xxxx.aar")
```
目录结构如图：

![image](https://user-images.githubusercontent.com/20922322/184358740-5cd405cf-851d-4a16-8842-97ec7efb56ff.png)

#### 方式2：
```xml
//引入aars目录下的所有aar包（每次有新的aar或同名的aar文件有变更时不会实时生效，需要注释后同步一次，再取消注释后同步一次可生效）
implementation fileTree(include: ['*.aar'], dir: 'aars')
```


### 更改Activity supportActionbar/actionbar的“3点菜单”按钮（溢出菜单图标）颜色

更改style文件

```xml
  <!--  这是程序的主题  -->
  <style name="AppTheme" parent="....." >
    <!--  更改溢出菜单的style  -->
    <item name="actionOverflowButtonStyle">@style/MyOverflowButtonStyle</item>
  </style>
  
   <!--  溢出菜单的按钮的style  -->
  <style name="MyOverflowButtonStyle" parent="Widget.AppCompat.ActionButton.Overflow">
     <!--  溢出菜单按钮的颜色  -->
    <item name="android:tint">@color/black</item>
  </style>
```

### 更改Activity supportActionbar/actionbar 菜单选项（溢出菜单的Item）文本的颜色

```xml
 <!--  这是程序的主题  -->
  <style name="AppTheme" parent="....." >
    <!--  更改溢出菜单的style  -->
    <item name="android:itemTextAppearance">@style/MyCustomMenuTextAppearance</item>
  </style>

<!--  溢出菜单选项的item的style  -->
<style name="MyCustomMenuTextAppearance" parent="@android:style/TextAppearance.Widget.IconMenu.Item">
    <item name="android:textColor">@color/overflow_text_color</item>
</style>
```

### 通过更改主题变更Button的默认文本颜色

```xml
 <!--  这是程序的主题  -->
  <style name="AppTheme" parent="....." >
    <!--  更改Button按钮的文本颜色（注意，此颜色不仅仅用于Button的文本颜色）  -->
    <item name="colorOnPrimary">@color/color_on_secondary</item>
  </style>
```

### Button的background属性无效

```xml
  <!--  加入app:backgroundTint="@null"屏蔽backgroundTint的影响即可  -->
  <Button
       app:backgroundTint="@null"
       .../>
```

### 判断当前Activity是否用户可见

java

```java
    public boolean isActivityVisible(Activity activity){
        return activity.getWindow().getDecorView().getVisibility() == View.VISIBLE;
    }
```

kotlin

```kotlin
    fun isActivityVisible(activity:Activity):Boolean{
        return activity.window.decorView.visibility == View.VISIBLE
    }
```

### 绑定 TabLayout与Fragment

使用TabLayoutMediator类即可

kotlin

```kotlin
 TabLayoutMediator(tabLayout,viewPager2,{ tab, position ->
           //TODO configure the tab for the page at position
            //TODO 为当前位置的tab配置一些基本属性
        }) 
```

java

```java
 new TabLayoutMediator(tabLayout, viewPager2, (tab, position) -> {
    //TODO configure the tab for the page at position
    //TODO 为当前位置的tab配置一些基本属性
        });
```

### string.xml 前后的' '(空格字符)会被trim

使用转义字符 &amp;#160; 替换单个 ' ',有几个替换几个

```xml
    <!--空格无效-->
    <string name="test"> 测试文本 </string>
    <!--空格有效-->
    <string name="test">&#160;测试文本&#160;</string>
```


### 常用xml转义字符及表示方式

```xml
&#160;      不断行的空白（1个字符宽度）
&#8194;     半个空白（1个字符宽度）
&#8195;     一个空白（2个字符宽度）
&#8201;     窄空白（小于1个字符宽度）
&lt;        小于号  
&gt;        大于号  
&amp;       与符号  
&apos;      单引号  
&quot;      双引号
```

### 更改Android Studio生成的APK文件的名称

在项目的主module的build.gradle中配置

```gradle
android {
   ···
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
        applicationVariants.all {
            variant ->
                variant.outputs.all {
                    output -> outputFileName = "你想更改的应用名称.apk"
                }
        }
    }
  ···
}
```

### 配置签名

在项目的主module的build.gradle中配置

```gradle
android {
   ···
    signingConfigs {
        def alias = "alias" //签名文件内，签名的别名
        def password = "aliasPassword" //签名文件内，指定签名的别名后，该签名的密码
        def filePath = "signture.jks"  //签名文件路径，默认目录与build.gradle文件路径一致，可用 "./" 或 "../"配置相对路径，也可直接填入完整的绝对路径
        def storePassword1 = "signtureFilePassword"  //签名文件密码
        
        //debug签名
        debug {
            keyAlias alias
            keyPassword password
            storeFile file(filePath)
            storePassword(storePassword1)
        }
        //release签名，可手动更改，配置与debug时不同的参数
        release {
            keyAlias alias
            keyPassword password
            storeFile file(filePath)
            storePassword(storePassword1)
        }
    }
   ···
}
```
