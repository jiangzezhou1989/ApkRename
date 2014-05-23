This project contains 4 utilities:
    apkRename.sh
    apkRenameAndInstall.sh
    setAxmlPkgName.jar   (in lib/)
    apkSign.sh

--------------------------------------------------------------------------------------------
apkRename.sh

Usage: apkRename.sh [OPTIONS] apkPath_or_packageName newPackageName
  This utility changes APK's package name (not java package name) and
  prepend java package name to partial class name in AndroidManifest.xml:
    Application,Activity,Receiver,Service...
    backupAgent,manageSpaceActivity,targetActivity...
    meta value(only if start with dot)

Note:
 If apkPath_or_packageName ends with .apk then means a apk file to be changed,
   otherwise means a packageName and will pull file from device to:
   ./tmpForApkRename/app.apk then change it

 If newPackageFullName ends with ! then it will remove conflict settings:
   <original-package>,<provider>,android:protectionLevel,process,sharedUserId

 For system app, it will pull app's odex file and convert to dex, add to apk.

 The result APK file is not signed, to install it please use apkSign.sh.

Options:
  -H <host>              - Name of adb server host (default: localhost)
  -P <port>              - Port of adb server (default: 5037)
  -s <devSerialNumber>   - Device Serial Number or qualifier

Examples:
 apkRename.sh com.example.app     com.exampe.newapp
 apkRename.sh com.android.browser com.exampe.newapp!
 apkRename.sh -s HTC123123 com.android.browser com.exampe.newapp!

--------------------------------------------------------------------------------------------
apkRenameAndInstall

Usage: apkRename.sh [OPTIONS] apkPath_or_packageName newPackageName
  This utility changes APK's package name (not java package name) and
  prepend java package name to partial class name in AndroidManifest.xml:
    Application,Activity,Receiver,Service...
    backupAgent,manageSpaceActivity,targetActivity...
    meta value(only if start with dot)

Note:
 If apkPath_or_packageName ends with .apk then means a apk file to be changed,
   otherwise means a packageName and will pull file from device to:
   ./tmpForApkRename/app.apk then change it

 If newPackageFullName ends with ! then it will remove conflict settings:
   <original-package>,<provider>,android:protectionLevel,process,sharedUserId

 For system app, it will pull app's odex file and convert to dex, add to apk.

 The result APK file is not signed, to install it please use apkSign.sh.

Options:
  -H <host>              - Name of adb server host (default: localhost)
  -P <port>              - Port of adb server (default: 5037)
  -s <devSerialNumber>   - Device Serial Number or qualifier

Examples:
 apkRename.sh com.example.app     com.exampe.newapp
 apkRename.sh com.android.browser com.exampe.newapp!
 apkRename.sh -s HTC123123 com.android.browser com.exampe.newapp!
macq:ApkRename macq$ ./apkRenameAndInstall.sh
too few arguments
Usage: apkRenameAndInstall.sh [OPTIONS] packageName newPackageName debugKeyStoreFile
  This script get app from all connected android device and change app name
  then install a new one to devices.
  When -s option is specified, only the specified device will be applied.

Options:
  -H <host>              - Name of adb server host (default: localhost)
  -P <port>              - Port of adb server (default: 5037)
  -s <devSerialNumber>   - Device Serial Number or qualifier
  --update               - Update app

Examples:
   apkRenameAndInstall.sh com.android.browser com.android.mybrowser ~/.android/debug.keystore
   apkRenameAndInstall.sh -s HTC12334 com.android.browser com.android.mybrowser ~/.android/debug.keystore