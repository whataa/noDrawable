Here is [English Doc](https://github.com/whataa/noDrawable/blob/master/README_EN.md)

# NoDrawable [![API](https://img.shields.io/badge/API-16%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=16) [![platform](https://img.shields.io/badge/platform-android-brightgreen.svg)](https://developer.android.com/index.html) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/whataa/noDrawable/blob/master/LICENSE) [![Build Status](https://travis-ci.org/whataa/noDrawable.svg?branch=master)](https://travis-ci.org/whataa/noDrawable)

Nodrawable是一个旨在减少99%的drawable.xml文件的库，可直接在布局文件中对任意View声明drawable属性。

方案原理：[一种巧妙的drawable.xml替代方案](https://juejin.im/post/5b95c6a0e51d450e664b0aa0)

演示Demo：[一种巧妙的drawable.xml替代方案-效果篇](http://linjiang.tech/2018/09/08/%E4%B8%80%E7%A7%8D%E5%B7%A7%E5%A6%99%E7%9A%84drawable.xml%E6%9B%BF%E4%BB%A3%E6%96%B9%E6%A1%88-%E6%95%88%E6%9E%9C%E7%AF%87/)

## 特性

#### ① 成本低

仅需开启DataBinding，核心仅一个方法；

#### ② 高可读性

直接在布局中的View标签声明drawable属性，对View最终效果一目了然；

#### ③ 适配任意View

像使用View自身的属性一样，作用于任何View；

## 集成

> 你可以按照以下方式集成，也可以直接拷贝库文件到项目中，仅2个类。

1. 在root's build.gradle中加入Jitpack仓库：

```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
2. 添加依赖到你的app's build.gradle中 [![](https://jitpack.io/v/whataa/noDrawable.svg)](https://jitpack.io/#whataa/noDrawable)
```
dependencies {
    ...
    implementation 'com.github.whataa:noDrawable:${RELEASE}'
}  
```
3. 让你的项目支持DataBinding：

```
android {
    ...
    dataBinding {
        enabled = true
    }
}
```


## 使用

1. 将你的布局转化为DataBinding的形式：


```
<layout>
    <!-- 你的布局内容 -->
<layout>
```
2. 在需要的View标签中声明drawable属性（**注意，没有限定符**）：

> 假如一个Button的背景是圆角，并且是红色的


```
<layout>
    ...
    <Button
        drawable_radius="@{10}"
        drawable_solidColor="@{0xffff0000}"
        android:layout_width="150dp"
        android:layout_height="50dp" />
    ...
<layout>
```


3. 在Activity中应用你的布局：

> 假设你的布局文件名为activity_main.xml
```
DataBindingUtil.setContentView(this, R.layout.activity_main);
```

现在，运行看看效果吧。

## 属性文档

> 说明：本项目仅提供对日常开发中最常用的属性支持，并非支持所有drawable属性。

属性名 | 说明 | 用例
---|---|---
drawable_shapeMode | shape的类型，参考`@ShapeMode`注解 | `@{0}` 
drawable_solidColor | solid标签的颜色 | @{0xffffffff}
drawable_strokeColor | stroke标签的颜色 | @{0xffffffff}
drawable_strokeWidth | stroke标签的宽度 | @{1}
drawable_strokeDash | stroke标签的虚线中的实线段长度 | @{2}
drawable_strokeDashGap | stroke标签的虚线中的虚线段长度 | @{2}
drawable_radius | corner标签的圆角 | @{10}
drawable_radiusLT | corner标签的圆角-左上 | @{10}
drawable_radiusLB |corner标签的圆角-左下 | @{10}
drawable_radiusRT |corner标签的圆角-右上 | @{10}
drawable_radiusRB |corner标签的圆角-右下 | @{10}
drawable_startColor |gradient标签的渐变起始色 | @{0xffffffff}
drawable_centerColor |gradient标签的渐变中间色 | @{0xffffffff}
drawable_endColor |gradient标签的渐变结束色 | @{0xffffffff}
drawable_orientation |gradient标签的渐变方向，参考@Orientation注解 | @{0}
drawable_gradientType |gradient标签的渐变类型，参考@GradientType注解 | @{0}
drawable_radialCenterX |gradient标签的radial类型的中心X，0~1 | @{0.5}
drawable_radialCenterY |gradient标签的radial类型的中心Y，0~1 | @{0.5}
drawable_radialRadius |gradient标签的radial类型的半径 | @{10}
drawable_width | size标签的宽 | @{10}
drawable_height |size标签的高 | @{10}
drawable_marginLeft | inset标签的insetLeft | @{-1}
drawable_marginTop | inset标签的insetTop | @{-1}
drawable_marginRight | inset标签的insetght | @{-1}
drawable_marginBottom | inset标签的insetbottom | @{-1}
drawable_ringThickness |shape为ring类型时的厚度 | @{10}
drawable_ringThicknessRatio |shape为ring类型时的厚度比例 | @{1}
drawable_ringInnerRadius |shape为ring类型时的内径半径 | @{10}
drawable_ringInnerRadiusRatio |shape为ring类型时的内径半径比例 | @{1}


同时还支持selector标签的常用状态，包括：`checked, checkable, enabled, focused, pressed, selected`，对应以上的属性名如下举例：

- drawable_checked_solidColor
- drawable_checkable_solidColor
- drawable_enabled_solidColor
- ...

另外，还提供了直接指定drawable.xml引用的属性，如下举例：

属性名 | 说明 | 用例
---|---|--
drawable | 普通状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_checked | checked状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_checkable | checkable状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_enabled | enabled状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_focused | focused状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_pressed | pressed状态下的drawable引用属性 | @{@drawable/shape_button}
drawable_selected | selected状态下的drawable引用属性 | @{@drawable/shape_button}

## 注意事项

- 属性开头没有形如 `android:` 或 `app:` 的限定符；
- 引入布局时，必须按照DataBinding的方案来引入（即不能用setContentView(xxx)），否则没有效果；
- 数据绑定必须使用`@{}`的形式，这是DataBinding的约束；
- 本库以在内部将`@{}`中的数值处理为了dp单位，具体可查看`Drawables.create`方法；
- 本库在values文件中预置了几个可选的integer值用以表示对应的枚举类型，用以提高可读性；
- 有些属性添加后可能不是你想要的效果，你可以参考该 [链接](https://keeganlee.me/post/android/20150830) 查看用法是否正确（个人觉得该链接的文章写得非常好）；
- 编译错误出现：cannot find symbol class DataBinderMapperImpl 时，请查看[issues#1](https://github.com/whataa/noDrawable/issues/1)

## 限制

- 最低支持的Android SDK版本为 16 ；
- 仅支持绝大多数常用的drawable属性，其它属性可自行扩展；
- 由DataBinding的特性决定，drawable效果在布局编辑器中无法实时预览；

## 开源协议

[Apache-2.0](https://opensource.org/licenses/Apache-2.0)