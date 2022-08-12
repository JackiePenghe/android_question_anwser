# android_question_anwser
安卓问题与解决方案记录

# 引入aar包(jar包同理)
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
  
   <!--  溢出菜单的style  -->
  <style name="MyOverflowButtonStyle" parent="Widget.AppCompat.ActionButton.Overflow">
     <!--  溢出菜单的颜色  -->
    <item name="android:tint">@color/black</item
  </style>
```

# Button的background属性无效

```xml
  <!--  加入app:backgroundTint="@null"屏蔽backgroundTint的影响即可  -->
  <Button
       app:backgroundTint="@null"
       .../>
```
