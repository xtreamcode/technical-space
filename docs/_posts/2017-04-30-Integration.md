# 3rd Party Integration Android

## Precondition
1. Generate a keystore (keytool comes with JDK)
```
   keytool -genkey -v -keystore <RELEASE_KEY_PATH> -alias <RELEASE_KEY_ALIAS> -keyalg RSA -keysize 2048 -validity 10000
   E.g. <RELEASE_KEY_PATH> = app.keystore and <RELEASE_KEY_ALIAS> = app.key
``` 
2. Sign the android app
```
  jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore <RELEASE_KEY_PATH> <APP>-unsigned.apk <RELEASE_KEY_ALIAS>
```

## Facebook
1. Create a facebook developer account at https://developers.facebook.com
2. Goto Settings -> Basic -> Add Platform -> Android
3. Update the Google Play Package Name to `%ionicProject%\platform\android\AndroidManifest.xml` -> xpath = `manifest\@package`
4. Update Class Name to `com.facebook.LoginActivity`
5. Generate a keyhashes from keystore, PS: use openssl-0.9.8e_X64 only, will not work with openssl-0.9.8k_X64
```
  keytool -exportcert -alias <RELEASE_KEY_ALIAS> -keystore <RELEASE_KEY_PATH> | openssl sha1 -binary | openssl base64
```
6. Paste the keyhashes displayed into Key Hashes in facebook
7. Install cordova-plugin-facebook4 (recommend to uninstall and install for existing app)
```
  cordova plugin add cordova-plugin-facebook4 --save --variable APP_ID="<App ID from Facebook>" --variable APP_NAME="Display Name from Facebook"
```

## References
1. [Ionic Publishing Guide](http://ionicframework.com/docs/v1/guide/publishing.html)
2. [Facebook Cordova Plugin](https://github.com/jeduan/cordova-plugin-facebook4)
