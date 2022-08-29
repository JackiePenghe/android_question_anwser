# android_question_anwser
安卓常见问题与解决方案记录
有新的问题可以提到issue中，我会整理后更新这些问题
还有一些我自己用过比较好用的库，我也整理到了另一个仓库中，有需要可以前往查看 [https://github.com/JackiePenghe/android_usefull_responsitory](https://github.com/JackiePenghe/android_usefull_responsitory)

#### 目录总览：

引入aar包(jar包同理)

更改Activity supportActionbar/actionbar的“3点菜单”按钮（溢出菜单图标）颜色

Button的background属性无效

判断当前Activity是否用户可见


# 引入aar包(jar包同理)

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

## 方式1：
```xml
    //引入指定的aar库(下方的aars表示与module目录中"src"文件夹同级的目录名，可以是libs，也可以是新建的其它文件目录)
    //每次同名的aar文件有变更时不会实时生效，需要注释后同步一次，再取消注释后同步一次可生效
    implementation files("aars/xxxx.aar")
```
目录结构如图：

![image](https://user-images.githubusercontent.com/20922322/184358740-5cd405cf-851d-4a16-8842-97ec7efb56ff.png)

## 方式2：
```xml
//引入aars目录下的所有aar包（每次有新的aar或同名的aar文件有变更时不会实时生效，需要注释后同步一次，再取消注释后同步一次可生效）
implementation fileTree(include: ['*.aar'], dir: 'aars')
```


# 更改Activity supportActionbar/actionbar的“3点菜单”按钮（溢出菜单图标）颜色

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

# 更改Activity supportActionbar/actionbar 菜单选项文本的颜色

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

# Button的background属性无效

```xml
  <!--  加入app:backgroundTint="@null"屏蔽backgroundTint的影响即可  -->
  <Button
       app:backgroundTint="@null"
       .../>
```

# 判断当前Activity是否用户可见

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
