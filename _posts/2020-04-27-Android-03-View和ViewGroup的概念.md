---
layout: post
title:  Android-03-View和ViewGroup的概念
date:  2020-04-27 10:16:20 +0800
categories: [Android]
tags: [Android, tutorial]
published: true
---

# Android-03——View和ViewGroup的概念

* any list
{:toc}

## UI Overview

在Android APP中，所有的用户界面元素是由View和ViewGroup的对象构成的。View是绘制在屏幕上的用户能够与之交互的一个对象。而ViewGroup则是一个用于存放其他View(和ViewGroup)对象的布局容器

Android为我们提供了一个View和ViewGroup子类的集合，集合中提供了一些常用的输入控件(比如按钮和文本域)和各种各样的布局模式(比如线性或者相对布局)



## User Interface Layout

你的APP的用户界面上的每一个组件都是使用View和ViewGroup对象的层次结构来构成的。每个ViewGroup都是要给看不见的用于组织子View的容器，而它的子View可能是输入控机制那活着在UI上绘制了某块区域的小部件。有了层次数，你就可以根据自己的需要，设计简单或者复杂的布局了。



定义你的布局，你可以在带按摩中实例化View对象并且开始构建你的树，但是最容易西河最搞笑的方法来定义你的布局试试用一个XML文件，用XML来构成布局更加符合人的阅读习惯，而XML类似于HTML使用XML元素的名称代表一个View。所以<TextView>元素会在你的界面创建一个类似TextView控件，而一个<LinearLayout>则会创建一个LinearLayout的容器！



比如下面的例子就是一个简单的垂直布局上面有一个文本试图和一个按钮，就像下面这样：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent" 
              android:layout_height="fill_parent"
              android:orientation="vertical" >
    <TextView android:id="@+id/text"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="I am a TextView" />
    <Button android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="I am a Button" />
</LinearLayout>
```



## User Interface Components

你无需全部用View和ViewGroup对象来创建你的UI布局。Android给我们提供了一些app控件，标准的UI布局，你只需要定义内容。这些UI组件都有其属性介绍的API文档，比如操作栏，对话框和状态通知栏等。



> Android里的图形界面都是由View和ViewGroup以及他们的子类构成的：
> View：所有可视化控件的父类,提供组件描绘和时间处理方法
> ViewGroup： View类的子类，可以拥有子控件,可以看作是容器
> Android UI中的控件都是按照这种层次树的结构堆叠得，而创建UI布局的方式有两种，
> 自己在Java里写代码或者通过XML定义布局，后者显得更加方便和容易理解！
> 也是我们最常用的手段！另外我们一般很少直接用View和ViewGroup来写布局，更多的
> 时候使用它们的子类控件或容器来构建布局！