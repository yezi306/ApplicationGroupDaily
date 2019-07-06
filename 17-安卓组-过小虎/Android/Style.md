### 样式
当我们描述一个控件有许多共同的属性时，可以像CSS一样定义一个样式，往后的控件就可以采用这个样式
```
//在valus文件下。
<?xml version="1.0" encoding="utf-8">
    <resources>
        <style name = "s1">
            <item name= "android:textSize">18sp</item>
        </style>
        
        <style name = "s1">
            <item></item>
        </style>
    </resources>
```
```
//在控件中引用

<TextView
    style="@style/s1">
</TextView>
```
