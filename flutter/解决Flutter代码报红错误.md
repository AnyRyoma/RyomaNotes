# Flutter开发：解决开发中Android代码报红问题

首先在项目文件下的`local.properties`文件中，添加如下代码：



```properties
// Flutter SDK的路径
flutter.sdk=xxx/Flutter/flutter_x.x.x
```

在插件`android`目录的`build.gradle`文件中，添加如下代码：



```gradle
/*此处仅处理因插件项目内报红显示的处理方式 start*/

//获取local.properties配置文件
def localProperties = new Properties()
def localPropertiesFile = rootProject.file('local.properties')
if (localPropertiesFile.exists()) {
    localPropertiesFile.withReader('UTF-8') { reader ->
        localProperties.load(reader)
    }
}
//获取flutter的sdk路径
def flutterRoot = localProperties.getProperty('flutter.sdk')
if (flutterRoot == null) {
    throw new GradleException("Flutter SDK not found. Define location with flutter.sdk in the local.properties file.")
}

/*此处仅处理因插件项目内报红显示的处理方式 end*/

dependencies {
    //此处仅处理因插件项目内报红显示的处理方式
    compileOnly files("$flutterRoot/bin/cache/artifacts/engine/android-arm/flutter.jar")
    compileOnly 'androidx.annotation:annotation:1.2.0'
}
```

