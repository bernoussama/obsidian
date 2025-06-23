list third party packages
```sh
adb shell pm list packages -3
```
get path to apk
```sh
adb shell pm path <package_name>
```
pull the APK from the phone:
```sh
adb pull <path_to_apk>
```

## REverse engineering
disasemble
```sh
apktool d <name>.apk
```
repackage
```sh
# inside disasembled apk directory
apktool b
```
### sign
generate signature
```sh
keytool -genkey -v -keystore research.keystore -alias research_key -keyalg RSA -keysize 2048 -validity 10000
```
sign apk
```sh
jarsigner -verbose -keystore research.keystore app.apk research_key
# on newer apps use
~/Android/Sdk/build-tools/34.0.0/apksigner sign --ks ./research.keystore ./aligned.apk
```