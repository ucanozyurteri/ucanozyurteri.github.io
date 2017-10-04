---
layout: post
title: ListViews
---
## ListView

Merhabalar, bu yazıda ListView yapısını basit bir örnekten daha karmaşık olana doğru anlatmaya çalışacağım.

"ListView: Kendisine verilen View yapılarını listeli bir şekilde görüntülemeye yarayan Android Widget'ıdır. İçerisindeki View satırlarında bir veya birden çok TextView ve ImageView gibi yapıları barındırabilir."

Öncelikle basit bir örnek ile başlayalım. Varsayılan ayarlarla yeni bir proje açalım ve activity_main.xml dosyasına gelip @id'si myList olan bir ListView ekleyelim:

```java
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.ugurcan.myapplication.MainActivity">

     <ListView
         android:id="@+id/myList"
         android:layout_width="match_parent"
         android:layout_height="match_parent"></ListView>

</android.support.constraint.ConstraintLayout>

```
