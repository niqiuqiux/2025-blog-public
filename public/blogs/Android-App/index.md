# Android 应用开发基础教程

## 📚 目录

1. [开发环境搭建](#1-开发环境搭建)
2. [Java/Kotlin 基础](#2-javakotlin-基础)
3. [Android 项目结构](#3-android-项目结构)
4. [Android 四大组件](#4-android-四大组件)
5. [AndroidManifest.xml](#5-androidmanifestxml)
6. [应用打包与签名](#6-应用打包与签名)
7. [常用组件与API](#7-常用组件与api)
8. [实践项目](#8-实践项目)

---

## 1. 开发环境搭建

### 1.1 安装 Android Studio

#### 系统要求
- **操作系统**: Windows 10/11, macOS 10.14+, Linux
- **内存**: 至少 8GB RAM（推荐 16GB）
- **磁盘空间**: 至少 10GB 可用空间
- **Java**: JDK 11 或更高版本

#### 安装步骤
1. 从官网下载 Android Studio: https://developer.android.com/studio
2. 运行安装程序，按照向导完成安装
3. 首次启动时，选择 Standard 安装类型
4. 等待 SDK 和工具下载完成

#### 配置 SDK
```bash
# 查看 SDK 位置
# Windows: C:\Users\<用户名>\AppData\Local\Android\Sdk
# macOS/Linux: ~/Library/Android/sdk 或 ~/Android/Sdk

# 配置环境变量
# Windows: 添加到 PATH
#   ANDROID_HOME = C:\Users\<用户名>\AppData\Local\Android\Sdk
#   PATH += %ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools

# macOS/Linux: 添加到 ~/.bashrc 或 ~/.zshrc
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools
```

### 1.2 创建第一个项目

#### 创建新项目
1. 打开 Android Studio
2. 选择 "New Project"
3. 选择模板（如 Empty Activity）
4. 配置项目：
   - **Name**: MyFirstApp
   - **Package name**: com.example.myfirstapp
   - **Save location**: 选择保存路径
   - **Language**: Java 或 Kotlin
   - **Minimum SDK**: API 21 (Android 5.0)
5. 点击 "Finish"

#### 项目结构
```
MyFirstApp/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/myfirstapp/
│   │   │   │   └── MainActivity.java
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   └── activity_main.xml
│   │   │   │   ├── values/
│   │   │   │   │   └── strings.xml
│   │   │   │   └── mipmap/
│   │   │   │       └── ic_launcher.png
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   ├── build.gradle
│   └── proguard-rules.pro
├── build.gradle
└── settings.gradle
```

### 1.3 配置模拟器或真机

#### 创建 AVD (Android Virtual Device)
1. 打开 AVD Manager: Tools → Device Manager
2. 点击 "Create Device"
3. 选择设备型号（如 Pixel 5）
4. 选择系统镜像（推荐 API 30+）
5. 配置 AVD 设置
6. 点击 "Finish"

#### 连接真机
```bash
# 1. 启用开发者选项
# 设置 → 关于手机 → 连续点击"版本号"7次

# 2. 启用 USB 调试
# 设置 → 系统 → 开发者选项 → USB 调试

# 3. 连接设备
adb devices

# 4. 如果设备未识别，安装驱动
# Windows: 安装设备制造商提供的 USB 驱动
```

---

## 2. Java/Kotlin 基础

### 2.1 Java 基础语法

#### 基本数据类型
```java
// 整数类型
byte b = 127;           // 1 字节，-128 到 127
short s = 32767;        // 2 字节，-32768 到 32767
int i = 2147483647;     // 4 字节，-2^31 到 2^31-1
long l = 9223372036854775807L;  // 8 字节

// 浮点类型
float f = 3.14f;        // 4 字节
double d = 3.14159;     // 8 字节

// 字符类型
char c = 'A';           // 2 字节，Unicode

// 布尔类型
boolean bool = true;    // 1 位
```

#### 面向对象基础
```java
// 类定义
public class Person {
    // 成员变量
    private String name;
    private int age;
    
    // 构造函数
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // 方法
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    // 静态方法
    public static void printInfo() {
        System.out.println("Person class");
    }
}

// 继承
public class Student extends Person {
    private String school;
    
    public Student(String name, int age, String school) {
        super(name, age);
        this.school = school;
    }
}
```

#### 集合框架
```java
// List
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.get(0);  // "Apple"

// Map
Map<String, Integer> map = new HashMap<>();
map.put("Apple", 10);
map.put("Banana", 20);
map.get("Apple");  // 10

// Set
Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Banana");
set.contains("Apple");  // true
```

### 2.2 Kotlin 基础语法

#### 基本语法
```kotlin
// 变量声明
var mutableVar: String = "Hello"  // 可变变量
val immutableVar: Int = 42        // 不可变变量

// 类型推断
var name = "Kotlin"  // 自动推断为 String
var count = 10       // 自动推断为 Int

// 空安全
var nullable: String? = null
var nonNull: String = "Hello"

// 安全调用
val length = nullable?.length  // 如果 nullable 为 null，返回 null
val length2 = nullable?.length ?: 0  // Elvis 操作符，如果为 null 返回 0
```

#### 函数定义
```kotlin
// 普通函数
fun add(a: Int, b: Int): Int {
    return a + b
}

// 单表达式函数
fun multiply(a: Int, b: Int) = a * b

// 默认参数
fun greet(name: String = "World") {
    println("Hello, $name!")
}

// 扩展函数
fun String.removeSpaces(): String {
    return this.replace(" ", "")
}
```

#### 类和对象
```kotlin
// 类定义
class Person(val name: String, var age: Int) {
    // 初始化块
    init {
        println("Person created: $name")
    }
    
    // 方法
    fun getInfo(): String {
        return "$name is $age years old"
    }
}

// 数据类
data class User(val id: Int, val name: String)

// 单例对象
object Singleton {
    fun doSomething() {
        println("Singleton method")
    }
}
```

### 2.3 Android 开发常用 Java/Kotlin 特性

#### 匿名内部类
```java
// Java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // 处理点击事件
    }
});
```

```kotlin
// Kotlin
button.setOnClickListener {
    // 处理点击事件
}
```

#### Lambda 表达式
```java
// Java 8+
list.forEach(item -> System.out.println(item));
```

```kotlin
// Kotlin
list.forEach { item -> println(item) }
```

#### 异步处理
```java
// Java - 使用 Handler
Handler handler = new Handler(Looper.getMainLooper());
handler.post(new Runnable() {
    @Override
    public void run() {
        // 更新 UI
    }
});
```

```kotlin
// Kotlin - 使用协程
lifecycleScope.launch {
    val result = withContext(Dispatchers.IO) {
        // 后台操作
    }
    // 更新 UI
}
```

---

## 3. Android 项目结构

### 3.1 项目目录结构

#### 完整项目结构
```
MyApp/
├── .gradle/                    # Gradle 构建缓存
├── .idea/                      # IDE 配置
├── app/                        # 应用模块
│   ├── src/
│   │   ├── main/              # 主源代码
│   │   │   ├── java/          # Java 源代码
│   │   │   │   └── com/example/myapp/
│   │   │   │       ├── MainActivity.java
│   │   │   │       └── ...
│   │   │   ├── kotlin/        # Kotlin 源代码（如果使用 Kotlin）
│   │   │   ├── res/           # 资源文件
│   │   │   │   ├── layout/   # 布局文件
│   │   │   │   ├── values/   # 值资源
│   │   │   │   ├── drawable/ # 图片资源
│   │   │   │   ├── mipmap/   # 应用图标
│   │   │   │   └── ...
│   │   │   ├── assets/        # 原始资源文件
│   │   │   └── AndroidManifest.xml
│   │   ├── test/              # 单元测试
│   │   └── androidTest/       # 集成测试
│   ├── build.gradle           # 模块构建配置
│   └── proguard-rules.pro     # ProGuard 规则
├── build.gradle               # 项目构建配置
├── settings.gradle            # 项目设置
└── gradle.properties          # Gradle 属性
```

### 3.2 资源文件 (res/)

#### layout/ - 布局文件
```xml
<!-- activity_main.xml -->
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:textSize="18sp" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />

</LinearLayout>
```

#### values/ - 值资源
```xml
<!-- strings.xml -->
<resources>
    <string name="app_name">My Application</string>
    <string name="hello_world">Hello World!</string>
</resources>

<!-- colors.xml -->
<resources>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
</resources>

<!-- dimens.xml -->
<resources>
    <dimen name="margin_small">8dp</dimen>
    <dimen name="margin_medium">16dp</dimen>
    <dimen name="margin_large">24dp</dimen>
</resources>
```

#### drawable/ - 图片资源
- **位图**: PNG, JPG, WebP
- **矢量图**: XML drawable
- **九宫格**: .9.png

```xml
<!-- drawable/ic_launcher_background.xml -->
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp"
    android:height="24dp"
    android:viewportWidth="24"
    android:viewportHeight="24">
    <path
        android:fillColor="#FF000000"
        android:pathData="M12,2L2,7v10c0,5.55 3.84,10.74 9,12 5.16,-1.26 9,-6.45 9,-12V7l-10,-5z"/>
</vector>
```

### 3.3 AndroidManifest.xml

#### 基本结构
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp">

    <!-- 权限声明 -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <!-- 应用信息 -->
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme">

        <!-- Activity 声明 -->
        <activity
            android:name=".MainActivity"
            android:label="@string/app_name">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest>
```

---

## 4. Android 四大组件

### 4.1 Activity（活动）

#### Activity 生命周期
```java
public class MainActivity extends AppCompatActivity {
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 初始化操作
    }
    
    @Override
    protected void onStart() {
        super.onStart();
        // Activity 可见但未获得焦点
    }
    
    @Override
    protected void onResume() {
        super.onResume();
        // Activity 获得焦点，可以交互
    }
    
    @Override
    protected void onPause() {
        super.onPause();
        // Activity 失去焦点
    }
    
    @Override
    protected void onStop() {
        super.onStop();
        // Activity 不可见
    }
    
    @Override
    protected void onDestroy() {
        super.onDestroy();
        // Activity 被销毁
    }
    
    @Override
    protected void onRestart() {
        super.onRestart();
        // Activity 从停止状态重新启动
    }
}
```

#### Activity 生命周期图
```
onCreate() → onStart() → onResume() → [运行中]
                                      ↓
onPause() ← onStop() ← onDestroy() ← [销毁]
         ↑
    onRestart()
```

#### Activity 间跳转
```java
// 启动 Activity
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
intent.putExtra("key", "value");
startActivity(intent);

// 启动 Activity 并等待结果
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivityForResult(intent, REQUEST_CODE);

// 接收结果
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == REQUEST_CODE && resultCode == RESULT_OK) {
        String result = data.getStringExtra("result");
    }
}
```

### 4.2 Service（服务）

#### Service 类型
1. **Started Service**: 通过 startService() 启动
2. **Bound Service**: 通过 bindService() 绑定

#### Started Service
```java
public class MyService extends Service {
    
    @Override
    public void onCreate() {
        super.onCreate();
        // 服务创建时调用
    }
    
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // 服务启动时调用
        // 执行后台任务
        return START_STICKY;  // 服务被杀死后自动重启
    }
    
    @Override
    public void onDestroy() {
        super.onDestroy();
        // 服务销毁时调用
    }
    
    @Override
    public IBinder onBind(Intent intent) {
        return null;  // Started Service 返回 null
    }
}

// 启动服务
Intent intent = new Intent(this, MyService.class);
startService(intent);

// 停止服务
stopService(intent);
```

#### Bound Service
```java
public class BoundService extends Service {
    
    private final IBinder binder = new LocalBinder();
    
    public class LocalBinder extends Binder {
        BoundService getService() {
            return BoundService.this;
        }
    }
    
    @Override
    public IBinder onBind(Intent intent) {
        return binder;
    }
    
    public void doSomething() {
        // 服务方法
    }
}

// 绑定服务
ServiceConnection connection = new ServiceConnection() {
    @Override
    public void onServiceConnected(ComponentName name, IBinder service) {
        BoundService.LocalBinder binder = (BoundService.LocalBinder) service;
        BoundService myService = binder.getService();
        myService.doSomething();
    }
    
    @Override
    public void onServiceDisconnected(ComponentName name) {
        // 服务断开连接
    }
};

Intent intent = new Intent(this, BoundService.class);
bindService(intent, connection, Context.BIND_AUTO_CREATE);
```

### 4.3 BroadcastReceiver（广播接收器）

#### 静态注册
```xml
<!-- AndroidManifest.xml -->
<receiver android:name=".MyReceiver">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>
```

```java
public class MyReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (Intent.ACTION_BOOT_COMPLETED.equals(intent.getAction())) {
            // 处理开机完成广播
        }
    }
}
```

#### 动态注册
```java
public class MainActivity extends AppCompatActivity {
    private BroadcastReceiver receiver;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        // 创建接收器
        receiver = new BroadcastReceiver() {
            @Override
            public void onReceive(Context context, Intent intent) {
                // 处理广播
            }
        };
        
        // 注册接收器
        IntentFilter filter = new IntentFilter();
        filter.addAction("com.example.MY_ACTION");
        registerReceiver(receiver, filter);
    }
    
    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 注销接收器
        unregisterReceiver(receiver);
    }
}

// 发送广播
Intent intent = new Intent("com.example.MY_ACTION");
intent.putExtra("data", "value");
sendBroadcast(intent);
```

### 4.4 ContentProvider（内容提供者）

#### 创建 ContentProvider
```java
public class MyContentProvider extends ContentProvider {
    
    private static final String AUTHORITY = "com.example.myapp.provider";
    private static final UriMatcher uriMatcher = new UriMatcher(UriMatcher.NO_MATCH);
    
    static {
        uriMatcher.addURI(AUTHORITY, "items", 1);
        uriMatcher.addURI(AUTHORITY, "items/#", 2);
    }
    
    @Override
    public boolean onCreate() {
        // 初始化数据库等
        return true;
    }
    
    @Override
    public Cursor query(Uri uri, String[] projection, String selection,
                       String[] selectionArgs, String sortOrder) {
        switch (uriMatcher.match(uri)) {
            case 1:
                // 查询所有
                break;
            case 2:
                // 查询单个
                break;
        }
        return null;
    }
    
    @Override
    public Uri insert(Uri uri, ContentValues values) {
        // 插入数据
        return null;
    }
    
    @Override
    public int update(Uri uri, ContentValues values, String selection,
                     String[] selectionArgs) {
        // 更新数据
        return 0;
    }
    
    @Override
    public int delete(Uri uri, String selection, String[] selectionArgs) {
        // 删除数据
        return 0;
    }
    
    @Override
    public String getType(Uri uri) {
        return null;
    }
}
```

#### 使用 ContentProvider
```java
// 查询数据
Uri uri = Uri.parse("content://com.example.myapp.provider/items");
Cursor cursor = getContentResolver().query(uri, null, null, null, null);

// 插入数据
ContentValues values = new ContentValues();
values.put("name", "Item 1");
getContentResolver().insert(uri, values);

// 更新数据
ContentValues values = new ContentValues();
values.put("name", "Updated Item");
getContentResolver().update(uri, values, null, null);

// 删除数据
getContentResolver().delete(uri, null, null);
```

---

## 5. AndroidManifest.xml

### 5.1 清单文件详解

#### 基本元素
```xml
<manifest>
    <!-- 包名 -->
    <manifest package="com.example.myapp">
    
    <!-- 权限声明 -->
    <uses-permission android:name="android.permission.INTERNET" />
    
    <!-- 应用配置 -->
    <application>
        <!-- 组件声明 -->
    </application>
</manifest>
```

### 5.2 权限声明

#### 系统权限
```xml
<!-- 网络权限 -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

<!-- 存储权限 -->
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

<!-- 位置权限 -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

<!-- 相机权限 -->
<uses-permission android:name="android.permission.CAMERA" />
```

#### 运行时权限（Android 6.0+）
```java
// 检查权限
if (ContextCompat.checkSelfPermission(this, Manifest.permission.CAMERA)
        != PackageManager.PERMISSION_GRANTED) {
    // 请求权限
    ActivityCompat.requestPermissions(this,
            new String[]{Manifest.permission.CAMERA},
            REQUEST_CODE);
}

// 处理权限请求结果
@Override
public void onRequestPermissionsResult(int requestCode, String[] permissions,
                                       int[] grantResults) {
    if (requestCode == REQUEST_CODE) {
        if (grantResults.length > 0 && grantResults[0] == 
                PackageManager.PERMISSION_GRANTED) {
            // 权限已授予
        } else {
            // 权限被拒绝
        }
    }
}
```

### 5.3 组件声明

#### Activity 声明
```xml
<activity
    android:name=".MainActivity"
    android:label="@string/app_name"
    android:theme="@style/AppTheme"
    android:screenOrientation="portrait"
    android:launchMode="standard">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

#### Service 声明
```xml
<service
    android:name=".MyService"
    android:enabled="true"
    android:exported="false" />
```

#### BroadcastReceiver 声明
```xml
<receiver
    android:name=".MyReceiver"
    android:enabled="true"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>
```

#### ContentProvider 声明
```xml
<provider
    android:name=".MyContentProvider"
    android:authorities="com.example.myapp.provider"
    android:enabled="true"
    android:exported="true" />
```

### 5.4 应用配置

#### 应用基本信息
```xml
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:theme="@style/AppTheme"
    android:usesCleartextTraffic="false"
    android:networkSecurityConfig="@xml/network_security_config">
</application>
```

#### 元数据
```xml
<application>
    <meta-data
        android:name="com.google.android.gms.version"
        android:value="@integer/google_play_services_version" />
</application>
```

---

## 6. 应用打包与签名

### 6.1 构建 APK

#### Debug APK
```bash
# 使用 Gradle 构建
./gradlew assembleDebug

# 输出位置
# app/build/outputs/apk/debug/app-debug.apk
```

#### Release APK
```bash
# 构建 Release APK
./gradlew assembleRelease

# 输出位置
# app/build/outputs/apk/release/app-release-unsigned.apk
```

### 6.2 应用签名

#### 生成密钥库
```bash
# 使用 keytool 生成密钥库
keytool -genkeypair -v -keystore my-release-key.jks
    -keyalg RSA -keysize 2048 -validity 10000
    -alias my-key-alias

# 需要输入的信息：
# - 密钥库密码
# - 密钥密码
# - 姓名、组织等信息
```

#### 配置签名
```gradle
// app/build.gradle
android {
    signingConfigs {
        release {
            storeFile file('my-release-key.jks')
            storePassword 'your-store-password'
            keyAlias 'my-key-alias'
            keyPassword 'your-key-password'
        }
    }
    
    buildTypes {
        release {
            signingConfig signingConfigs.release
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'),
                    'proguard-rules.pro'
        }
    }
}
```

#### 使用 Android Studio 签名
1. Build → Generate Signed Bundle / APK
2. 选择 APK
3. 选择或创建密钥库
4. 选择构建类型（Release）
5. 点击 Finish

### 6.3 APK 结构

#### APK 文件结构
```
app.apk (ZIP 格式)
├── META-INF/              # 签名信息
│   ├── MANIFEST.MF
│   ├── CERT.SF
│   └── CERT.RSA
├── AndroidManifest.xml    # 清单文件（二进制）
├── classes.dex            # DEX 字节码
├── resources.arsc         # 资源索引
├── res/                   # 资源文件
│   ├── layout/
│   ├── values/
│   └── ...
└── assets/                # 原始资源（如果有）
```

#### 查看 APK 内容
```bash
# 解压 APK（APK 是 ZIP 文件）
unzip app.apk -d app_extracted/

# 查看 DEX 文件
dexdump classes.dex

# 查看 AndroidManifest.xml（需要工具）
aapt dump xmltree app.apk AndroidManifest.xml
```

### 6.4 应用版本管理

#### 版本配置
```gradle
// app/build.gradle
android {
    defaultConfig {
        applicationId "com.example.myapp"
        versionCode 1          // 内部版本号（整数）
        versionName "1.0"      // 用户可见版本号（字符串）
    }
}
```

#### 版本信息获取
```java
try {
    PackageInfo packageInfo = getPackageManager()
            .getPackageInfo(getPackageName(), 0);
    int versionCode = packageInfo.versionCode;
    String versionName = packageInfo.versionName;
} catch (PackageManager.NameNotFoundException e) {
    e.printStackTrace();
}
```

---

## 7. 常用组件与 API

### 7.1 布局组件

#### LinearLayout（线性布局）
```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Item 1" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Item 2" />

</LinearLayout>
```

#### RelativeLayout（相对布局）
```xml
<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 1" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button1"
        android:layout_alignParentEnd="true"
        android:text="Button 2" />

</RelativeLayout>
```

#### ConstraintLayout（约束布局）
```xml
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### 7.2 常用控件

#### TextView
```xml
<TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello World"
    android:textSize="18sp"
    android:textColor="#000000"
    android:gravity="center" />
```

#### EditText
```xml
<EditText
    android:id="@+id/editText"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="Enter text"
    android:inputType="text"
    android:maxLines="1" />
```

#### Button
```xml
<Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Click Me"
    android:onClick="onButtonClick" />
```

```java
public void onButtonClick(View view) {
    // 处理点击事件
}
```

#### ImageView
```xml
<ImageView
    android:id="@+id/imageView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/ic_launcher"
    android:scaleType="centerCrop" />
```

### 7.3 数据存储

#### SharedPreferences
```java
// 写入数据
SharedPreferences prefs = getSharedPreferences("MyPrefs", MODE_PRIVATE);
SharedPreferences.Editor editor = prefs.edit();
editor.putString("name", "John");
editor.putInt("age", 25);
editor.apply();

// 读取数据
String name = prefs.getString("name", "Default");
int age = prefs.getInt("age", 0);
```

#### 文件存储
```java
// 写入文件
String filename = "myfile.txt";
String content = "Hello World";
FileOutputStream fos = openFileOutput(filename, Context.MODE_PRIVATE);
fos.write(content.getBytes());
fos.close();

// 读取文件
FileInputStream fis = openFileInput(filename);
BufferedReader reader = new BufferedReader(new InputStreamReader(fis));
String line = reader.readLine();
reader.close();
```

#### SQLite 数据库
```java
// 创建数据库
public class DatabaseHelper extends SQLiteOpenHelper {
    private static final String DATABASE_NAME = "mydb.db";
    private static final int DATABASE_VERSION = 1;
    
    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }
    
    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)");
    }
    
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS users");
        onCreate(db);
    }
}

// 使用数据库
DatabaseHelper dbHelper = new DatabaseHelper(this);
SQLiteDatabase db = dbHelper.getWritableDatabase();

// 插入数据
ContentValues values = new ContentValues();
values.put("name", "John");
db.insert("users", null, values);

// 查询数据
Cursor cursor = db.query("users", null, null, null, null, null, null);
while (cursor.moveToNext()) {
    String name = cursor.getString(cursor.getColumnIndex("name"));
}
cursor.close();
```

### 7.4 网络请求

#### 使用 HttpURLConnection
```java
// 在后台线程中执行
new Thread(new Runnable() {
    @Override
    public void run() {
        try {
            URL url = new URL("https://api.example.com/data");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            
            BufferedReader reader = new BufferedReader(
                    new InputStreamReader(conn.getInputStream()));
            String line;
            StringBuilder response = new StringBuilder();
            while ((line = reader.readLine()) != null) {
                response.append(line);
            }
            reader.close();
            
            // 更新 UI（需要在主线程）
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    // 更新 UI
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}).start();
```

#### 使用 Retrofit（推荐）
```java
// 定义 API 接口
public interface ApiService {
    @GET("users/{id}")
    Call<User> getUser(@Path("id") int id);
}

// 创建 Retrofit 实例
Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("https://api.example.com/")
        .addConverterFactory(GsonConverterFactory.create())
        .build();

ApiService service = retrofit.create(ApiService.class);

// 发起请求
Call<User> call = service.getUser(1);
call.enqueue(new Callback<User>() {
    @Override
    public void onResponse(Call<User> call, Response<User> response) {
        User user = response.body();
        // 处理响应
    }
    
    @Override
    public void onFailure(Call<User> call, Throwable t) {
        // 处理错误
    }
});
```

---

## 8. 实践项目

### 8.1 项目一：计算器应用

#### 功能要求
- 基本四则运算
- 清除功能
- 显示计算结果

#### 实现步骤
1. 创建布局文件（使用 GridLayout）
2. 实现计算逻辑
3. 处理按钮点击事件
4. 显示计算结果

### 8.2 项目二：待办事项应用

#### 功能要求
- 添加待办事项
- 删除待办事项
- 标记完成状态
- 使用 SQLite 存储数据

#### 实现步骤
1. 设计数据库表结构
2. 创建数据库帮助类
3. 实现列表显示（使用 RecyclerView）
4. 实现添加/删除功能
5. 实现状态更新

### 8.3 项目三：天气应用

#### 功能要求
- 获取当前位置
- 调用天气 API
- 显示天气信息
- 使用网络请求

#### 实现步骤
1. 申请位置权限
2. 获取当前位置
3. 调用天气 API（如 OpenWeatherMap）
4. 解析 JSON 数据
5. 显示天气信息

---

## 9. 调试与测试

### 9.1 日志输出

#### 使用 Log
```java
Log.v("TAG", "Verbose message");    // 详细日志
Log.d("TAG", "Debug message");      // 调试日志
Log.i("TAG", "Info message");       // 信息日志
Log.w("TAG", "Warning message");    // 警告日志
Log.e("TAG", "Error message");      // 错误日志
```

#### 查看日志
```bash
# 查看所有日志
adb logcat

# 过滤特定标签
adb logcat -s TAG

# 清除日志
adb logcat -c
```

### 9.2 断点调试

#### 设置断点
1. 在代码行号左侧点击
2. 运行应用（Debug 模式）
3. 触发断点
4. 查看变量值
5. 单步执行

### 9.3 单元测试

#### 创建测试类
```java
@RunWith(AndroidJUnit4.class)
public class ExampleUnitTest {
    @Test
    public void addition_isCorrect() {
        assertEquals(4, 2 + 2);
    }
}
```

---

## 10. 总结

### 10.1 核心知识点
1. **开发环境**: Android Studio, SDK, 模拟器/真机
2. **编程语言**: Java/Kotlin 基础
3. **项目结构**: 目录组织, 资源管理
4. **四大组件**: Activity, Service, BroadcastReceiver, ContentProvider
5. **清单文件**: AndroidManifest.xml 配置
6. **打包签名**: APK 构建与签名
7. **常用组件**: 布局, 控件, 数据存储, 网络请求

### 10.2 学习建议
1. **多动手实践**: 完成每个实践项目
2. **阅读官方文档**: Android Developer 官网
3. **参考示例代码**: GitHub 上的开源项目
4. **加入社区**: Stack Overflow, Android 开发者社区

### 10.3 进阶方向
- **Material Design**: 学习 Material 设计规范
- **架构模式**: MVP, MVVM, Clean Architecture
- **Jetpack 组件**: ViewModel, LiveData, Room, Navigation
- **Kotlin 协程**: 异步编程
- **性能优化**: 内存优化, 启动优化

---

