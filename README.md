# ali_real_person

本項目參考 https://github.com/jaylin507/ali_real_person



#### SDK 版本

* android: rpsdk-4.6.2-open
* iOS: 4.6.2



## 常見問題

##### 應用程序啟動後，啟用認證閃退

類似報錯 https://del.dog/peceruhywo.txt

> 簽名配置問題，務必 debug 使用 v2SigningEnabled false



## 安裝

#### pubspec.yaml

```
  ali_real_person:
    git: git://github.com/qoli/ali_real.git
```

#### 使用方法

```dart
import 'package:ali_real_person/ali_real_person.dart';

AliRealPerson.startRealPerson(token, (value) {
    //返回字符串
    // "1" 认证成功,
    // "2"  认证失败
    // "-1"  未认证
  });
```





## Android 集成

#### 圖像文件

請把 **yw_1222_xxx.jpg** 移動到 **android/app/src/main/res/drawable** 



#### AndroidManifest.xml 

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools" package=",,,">
	...
	
	//需要添加權限
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.CAMERA" />
	
	//修改此處
	<application android:allowBackup="false" tools:replace="label,allowBackup" android:name="io.flutter.app.FlutterApplication" android:label="IDJGLOBAL" android:icon="@mipmap/ic_launcher">
	
	...
	</application>
</manifest>

```



#### android/app/build.gradle

引入插件

```yaml
repositories {
    flatDir {
        dirs project(':ali_real_person').file('libs') //加載插件內容
    }
}
```

#### android/app/build.gradle

#### 簽名配置

https://help.aliyun.com/document_detail/127598.html

> 如果无法降低Gradle Plugin及Gradle版本，需要在您工程的App模块下的build.gradle中添加签名配置。

```yaml
signingConfigs {
        release {
            storeFile file('test.jks')
            storePassword "test1234"
            keyAlias "key0"
            keyPassword "test1234"

            v1SigningEnabled true
            v2SigningEnabled true
        }
        debug {
            storeFile file('test.jks')
            storePassword "test1234"
            keyAlias "key0"
            keyPassword "test1234"

            v1SigningEnabled true
            v2SigningEnabled false //debug 必須false
        }
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
            signingConfig signingConfigs.release
        }

        debug {
            minifyEnabled false
            signingConfig signingConfigs.debug
        }
}
```





#### gradle-wrapper.properties

可採用 5.6.4

```bash
distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.4-all.zip

```



#### android/build.gradle

可採用 3.6.4

```
classpath 'com.android.tools.build:gradle:3.6.4'
```





## iOS 集成

請必須把 **RPSDK.bundle** 和 **yw_1222_xxx.jpg** 拖放到 xcode

確保 **Build Phases** 存在上述文件。

![image-20210325234049527](https://gitee.com/qoli/u-pic/raw/master/uPic/image-20210325234049527.png)

#### 修改 ali_real_person.podspec 文件

```
  s.info_plist = { 'CFBundleIdentifier' => 'com.abc.efg.ali-real-person' }
  s.pod_target_xcconfig = { 'PRODUCT_BUNDLE_IDENTIFIER': 'com.abc.efg.ali-real-person' }
```

到最后 end 之前

文件位置请查看图片

![image-20210503211121246](https://gitee.com/qoli/u-pic/raw/master/uPic/image-20210503211121246.png)