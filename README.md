# android_question_anwser
安卓问题与解决方案记录

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
