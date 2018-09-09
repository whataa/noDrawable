# NoDrawable [![API](https://img.shields.io/badge/API-16%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=16) [![platform](https://img.shields.io/badge/platform-android-brightgreen.svg)](https://developer.android.com/index.html) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/whataa/noDrawable/blob/master/LICENSE) [![Build Status](https://travis-ci.org/whataa/noDrawable.svg?branch=master)](https://travis-ci.org/whataa/noDrawable)

NoDrawable is a library aim to reduce the drawable.xml file by 99%, you can define the drawable attributes on any View directly in the layout file.


## Feature

#### ① Low cost

Just let your project support DataBinding. And the library has only one core method.

#### ② Highly readable

Directly declare the drawable attributes in the View of the layout, and see the final effect of the View at a glance;

#### ③ Support any view

Just like using the attributes of View itself, it works on any View;

## Set-up

1. Add the JitPack repository to your root build file：


```
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
2. Add the dependency to your app build.gradle [![](https://jitpack.io/v/whataa/noDrawable.svg)](https://jitpack.io/#whataa/noDrawable)
```
dependencies {
    ...
    implementation 'com.github.whataa:noDrawable:${RELEASE}'
}  
```
3. let your project support DataBinding：

```
android {
    ...
    dataBinding {
        enabled = true
    }
}
```


## Usage

1. Convert your layout to the form of DataBinding：


```
<layout>
    <!-- your real layout -->
<layout>
```
2. Declare the drawable attributes in the your View：

> Suppose there is a Button background is rounded and red


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


3. inflate your layout in the Activity：

> Suppose your layout file is named activity_main.xml
```
DataBindingUtil.setContentView(this, R.layout.activity_main);
```

Now, run and see the effect.

## Document

> Note: This library only provides support for the most commonly used attributes in daily development. It does not support all drawable attributes.

attribute | Description | Example
---|---|---
drawable_shapeMode | shape's type，please see `@ShapeMode` | `@{0}` 
drawable_solidColor | solid's color | @{0xffffffff}
drawable_strokeColor | stroke's color | @{0xffffffff}
drawable_strokeWidth | stroke's width | @{1}
drawable_strokeDash |  | @{2}
drawable_strokeDashGap |  | @{2}
drawable_radius |  | @{10}
drawable_radiusLT |  | @{10}
drawable_radiusLB | | @{10}
drawable_radiusRT | | @{10}
drawable_radiusRB | | @{10}
drawable_startColor | | @{0xffffffff}
drawable_centerColor | | @{0xffffffff}
drawable_endColor | | @{0xffffffff}
drawable_orientation |@Orientation | @{0}
drawable_gradientType |@GradientType | @{0}
drawable_radialCenterX |，0~1 | @{0.5}
drawable_radialCenterY |，0~1 | @{0.5}
drawable_radialRadius | | @{10}
drawable_width |  | @{10}
drawable_height | | @{10}
drawable_marginLeft |  | @{-1}
drawable_marginTop |  | @{-1}
drawable_marginRight |  | @{-1}
drawable_marginBottom |  | @{-1}
drawable_ringThickness | | @{10}
drawable_ringThicknessRatio | | @{1}
drawable_ringInnerRadius | | @{10}
drawable_ringInnerRadiusRatio | | @{1}


Also supports the common state of the selector tag, including：`checked, checkable, enabled, focused, pressed, selected`：

- drawable_checked_solidColor
- drawable_checkable_solidColor
- drawable_enabled_solidColor
- ...

In addition, noDrawable also provide attribute that can directly specify the reference to drawable.xml, as shown in the following example:

attribute | Description | Example
---|---|--
drawable | normal state | @{@drawable/shape_button}
drawable_checked | checked state | @{@drawable/shape_button}
drawable_checkable | checkable state | @{@drawable/shape_button}
drawable_enabled | enabled state | @{@drawable/shape_button}
drawable_focused | focused state | @{@drawable/shape_button}
drawable_pressed | pressed state | @{@drawable/shape_button}
drawable_selected | selected state | @{@drawable/shape_button}

## Notice

- The attribute does not have a qualifier like `android:` or `app:` at the beginning;
- Layout must be inflated according to the DataBinding scheme (ie can not use setContentView (xxx)), otherwise there is no effect;
- Data binding must be in the form of `@{}`, which is a constraint on DataBinding;
- NoDrawable internally processes the values in `@{}` for dp units, please look the `Drawables.create` method;
- NoDrawable presets several optional integer values in the values file to indicate the corresponding enumerated types for improved readability.
- Some attribute may not be what you want after adding them. please see if the usage is correct.
- When building failed：cannot find symbol class DataBinderMapperImpl ，please check out [issues#1](https://github.com/whataa/noDrawable/issues/1)

## Limit

- Minimum supported Android SDK version is 16.
- Only the most commonly used drawable attributes are supported, and other attributes can be extended by yourself;
- Determined by the nature of DataBinding, the drawable effect cannot be previewed in real time in the layout editor;

## License

[Apache-2.0](https://opensource.org/licenses/Apache-2.0)