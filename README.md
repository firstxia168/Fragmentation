[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Fragmentation-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/5937)
[![Build Status](https://travis-ci.org/YoKeyword/Fragmentation.svg?branch=master)](https://travis-ci.org/YoKeyword/Fragmentation)
[![Download](https://api.bintray.com/packages/yokeyword/maven/Fragmentation/images/download.svg) ](https://bintray.com/yokeyword/maven/Fragmentation/_latestVersion)
[![Hex.pm](https://img.shields.io/hexpm/l/plug.svg)](https://www.apache.org/licenses/LICENSE-2.0)

### [中文版 README.md](https://github.com/YoKeyword/Fragmentation/blob/master/README_CN.md)

# Fragmentation

![](/gif/logo.png)

Fragmentation is a powerful library managing Fragment for Android.

It is designed for "Single Activity + Multi-Fragments" and "Multi-FragmentActivities + Multi-Fragments" architecture to simplify development process.

## Demo
The first demo shows the basic usage of the library. The second one shows the way to implement an app which is similar to WeChat. Complicated nested fragments' usage demo are also showed.

[Download APK](https://www.pgyer.com/fragmentation)

<img src="/gif/demo.gif" width="280px"/> <img src="/gif/wechat.gif" width="280px"/>
 <img src="/gif/nested.gif" width="280px"/>

## Feature

**1. Develop complicated nested fragment app rapidly**

**2. Use fragment's stack view dialog to debug easily**

**3. Add launch mode, startForResult etc. to provide similar behavior of Activity**

**4. Add onBackPressedSupport() method to support back button press monitoring in Fragment**

**5. Add onSupportVisible(), onLazyInitView() to simplify dev**

**6. Easily manage Fragment transition animations**

**7. More compatibility, solve multi-touch, fragments overlapping problems**

**8. Support SwipeBack to pop(Fragmentation_SwipeBack module [README](https://github.com/YoKeyword/Fragmentation/blob/master/fragmentation_swipeback/README.md))**

<img src="/gif/log.png" width="400px"/>      <img src="/gif/SwipeBack.jpg" width="150px"/>

## How do I use Fragmentation?

**1、build.gradle**
````gradle
// appcompat-v7 is required
compile 'me.yokeyword:fragmentation:1.0.6'

// If you don't want to extends SupportActivity/Fragment and would like to customize your own support, just rely on fragmentation-core
// compile 'me.yokeyword:fragmentation-core:1.0.6'

// To get SwipeBack feature, rely on both fragmentation & fragmentation-swipeback
compile 'me.yokeyword:fragmentation:1.0.6'
// Swipeback is based on fragmentation. Refer to SwipeBackActivity/Fragment for your Customized SupportActivity/Fragment
compile 'me.yokeyword:fragmentation-swipeback:1.0.6'
````

**2、 Activity extends SupportActivity**
````java
// since v1.0.0, forced extends of SupportActivity is not required, you can use interface + delegate to implement your own SupportActivity 
public class MainActivity extends SupportActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(...);
      	// Stack view is recommended to initialize in the Application
        Fragmentation.builder()
          	 // show stack view. Mode: BUBBLE, SHAKE, NONE
             .stackViewMode(Fragmentation.BUBBLE)
             .debug(BuildConfig.DEBUG)
             ...
             .install();

        if (findFragment(HomeFragment.class) == null) {
            loadRootFragment(R.id.fl_container, HomeFragment.newInstance());  //load root Fragment
        }
    }
````

**3、 Fragment extends SupportFragment**
````java
// since v1.0.0, forced extends of SupportActivity is not required, you can use interface + delegate to implement your own SupportActivity
public class HomeFragment extends SupportFragment {

    private void xxx() {
      	// launch a new Fragment, other methods: start(fragment,SINGTASK)、startForResult、startWithPop etc.
        start(DetailFragment.newInstance(HomeBean));
      	// check wiki for other pop, find and animation setting related API
    }
}
````

## [WIKI](https://github.com/YoKeyword/Fragmentation/wiki) , [CHANGELOG](https://github.com/YoKeyword/Fragmentation/blob/master/CHANGELOG.md)

## Proguard

Pre-v1.0.5, need to add the proguard-rules:

````xml
-keep class * extends android.support.v4.app.FragmentManager{ *; }
````

## LICENSE
````
Copyright 2016 YoKey

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
````
