# Android特种机安装第三方应用

## 1.准备工作

> 目标机器连接PC并开启USB调试

需要用到的工具：

* [apktool](https://github.com/iBotPeaches/Apktool)
* keytool
* jarsigner

需要用到的命令：

* 检查连接的设备：`adb devices`
* 卸载应用：`adb shell pm uninstall --user 0 <package>`
* 安装应用：`adb install <apk>`
* 冻结应用：`adb shell pm disable-user <package>`
* 解冻应用：`adb shell pm default-state <package>`
* 查看APK包名的信息：`aapt dump badging <apk>`
* 查看APK所在的路径：`adb shell pm path <package>`
* 导出APK：`cp <path> /sdcard/`，`adb pull <apk_path> <apk>`

## 2.更换对应APK包名

> 第一种方法

反编译APK：

```bash
apktool d your-app.apk
```

修改：

1. 打开`AndroidManifest.xml`文件，修改`package`包名、`android:label`应用名称
2. 打开`apktool.yml`文件
   * 查找`renameManifestPackage`参数，将`null`值改成对应的包名
   * 更改版本号：`version`、`versionCode`、`versionName`
3. 将ic_launcher.png替换至以下文件夹：
   * `res/mipmap-mdpi`
   * `res/mipmap-hdpi`
   * `res/mipmap-xhdpi`
   * `res/mipmap-xxhdpi`
   * `res/mipmap-xxxhdpi`

编译APK：

```bash
apktool b your-app -o new-app.apk
```

---

> 第二种方法

1. 使用[AXMLPrinter](https://github.com/digitalsleuth/AXMLPrinter2)反编译APK内的`AndroidManifest.xml`文件，然后修改文件内的包名以及版本号、应用名称

   ```bash
   java -jar AXMLPrinter2.jar AndroidManifest.xml > Out.xml
   ```

2. 使用[XML2AXML](https://github.com/codyi96/xml2axml)重新编译`AndroidManifest.xml`文件，然后替换目标APK中的文件

   ```bash
   java -jar xml2axml-2.0.1.jar e AndroidManifest.xml Okay.xml
   ```

3. 删除`META-INF`文件夹下的`*.RSA`、`*.SF`文件

4. 将ic_launcher.png替换至以下文件夹：
   * `res/mipmap-mdpi`
   * `res/mipmap-hdpi`
   * `res/mipmap-xhdpi`
   * `res/mipmap-xxhdpi`
   * `res/mipmap-xxxhdpi`

---

> 第三种方法

使用MT管理器的应用共存功能，再修改`AndroidManifest.xml`：

* `android:label`：应用名称
* `android:version`：版本号Code和版本名Name
* 根据`android:icon`提供的路径修改图标

## 3.数字签名

生成签名证书：

```bash
keytool -genkeypair -alias yuxiang-key -keyalg RSA -validity 20000 -keystore yuxiang-key.jks
```

签名：

```bash
jarsigner --verbose -keystore yuxiang-key.jks -signedjar 已签名.apk 未签名.apk yuxiang-key
```

## 4.APK包名参考

可被替换的包名：

| 包名                         | 应用名         |
| ---------------------------- | -------------- |
| com.kingsoft.moffice_pro     | WPS Office     |
| com.thdqalqwq.macdwyhga      | 中英文翻译词典 |
| com.test.turnoff             | 省电管理       |
| com.iflytek.data.migration   | 数据迁移       |
| com.xiyou.english            | 西柚英语       |
| com.iflytek.learn.english    | 学了英语       |
| com.ets100.secondary         | E听说中学      |
| com.iflytek.tab1.errorbook   | 错题集         |
| com.edutools.plyflash        | Edu SWF Player |
| com.iflytek.ScreenRecorder   | ScreenRecorder |
| com.iflytek.sharedwhiteboard | 共享白板       |
| com.iflytek.tab1.lessonplan  | 学习资料       |
| com.iflytek.elpmobile.mcv    | 微课视频       |
| com.iflytek.commoncamera     | 拍照讲解       |

被冻结的应用：

| 包名                        | 应用名   |
| --------------------------- | -------- |
| com.huawei.android.launcher | 华为桌面 |
| com.android.browser         | 浏览器   |
| com.huawei.hidisk           | 文件管理 |

可使用命令`adb shell pm default-state <package>`解冻

## 5.推荐方案

```
省电管理（com.test.turnoff）
文件管理器+（com.alphainventor.filemanager） / Link2SD（com.buak.Link2SD）

西柚英语（com.xiyou.english）
via（mark.via）

数据迁移（com.iflytek.data.migration）
v2RayNG（com.v2ray.ang） / Clash（com.github.kr328.clash）

洛雪音乐（cn.toside.music.mobile）
错题集（com.iflytek.tab1.errorbook）
```

## 6.反host屏蔽参考

```
cc
com
net
org
hk
men
gov
cn
info
lu
io
```

```
pm
xyz
top
pub
tech
ink
int
co
biz
tv
pro
us
jp
mo
tw
de
me
vip
```