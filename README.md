<p align="center">
  <img src="http://i.imgur.com/ogfeKrK.png">
</p>

Kontakt.io Android SDK
===========

The Kontakt.io Android SDK is a library for Android OS that provides developers with components to help build applications using Kontakt.io devices.

**For full documentation please see [docs website].**

## Latest Version

Latest version is 7.0.12.2

## Quickstart
1. Add Gradle dependency into your app's `build.config`
``` Groovy
dependencies {
    compile 'io.kontakt.mvn:sdk:{latest_version}'
}
```

2. Add necessary permissions into your `AndroidManifest`
``` XML
<uses-permission android:name="android.permission.BLUETOOTH"/> // add android:maxSdkVersion="30" when compiling against sdk 31 or higher
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/> // add android:maxSdkVersion="30" when compiling against sdk 31 or higher
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

// Access fine location is necessary when sdk version is equal / bigger than Android 10; below that you can use ACCESS_COARSE_LOCATION for BT scanning; when targetting Android 12 or higher, and BLUETOOTH_SCAN does not have neverForLocation tag, ACCESS_FINE_LOCATION should also be present in the manifest file
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
// When compiling against and targetting sdk=31 and higher
<uses-permission android:name="android.permission.BLUETOOTH_SCAN" /> // you could also add "neverForLocation"=true and remove ACCESS_FINE_LOCATION permission if location is used only for bt scanning purposes
// When compiling against and targetting sdk=31 and higher
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```

3. Add ProximityService int your `AndroidManifest` application section
```XML
<service android:name="com.kontakt.sdk.android.ble.service.ProximityService" android:exported="false"/>
```
4. Make sure Bluetooth is enabled on your device. 

5. [Ask about the necessary runtime permissions](https://developer.android.com/training/permissions/requesting.html)

6. Create simple activity that will scan for both iBeacons and Eddystones
``` Java
public class MainActivity extends AppCompatActivity {

  private ProximityManager proximityManager;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    KontaktSDK.initialize("YOUR_API_KEY");

    proximityManager = ProximityManagerFactory.create(this);
    proximityManager.setIBeaconListener(createIBeaconListener());
    proximityManager.setEddystoneListener(createEddystoneListener());
  }

  @Override
  protected void onStart() {
    super.onStart();
    startScanning();
  }

  @Override
  protected void onStop() {
    proximityManager.stopScanning();
    super.onStop();
  }

  @Override
  protected void onDestroy() {
    proximityManager.disconnect();
    proximityManager = null;
    super.onDestroy();
  }

  private void startScanning() {
    proximityManager.connect(new OnServiceReadyListener() {
      @Override
      public void onServiceReady() {
        proximityManager.startScanning();
      }
    });
  }

  private IBeaconListener createIBeaconListener() {
    return new SimpleIBeaconListener() {
      @Override
      public void onIBeaconDiscovered(IBeaconDevice ibeacon, IBeaconRegion region) {
        Log.i("Sample", "IBeacon discovered: " + ibeacon.toString());
      }
    };
  }

  private EddystoneListener createEddystoneListener() {
    return new SimpleEddystoneListener() {
      @Override
      public void onEddystoneDiscovered(IEddystoneDevice eddystone, IEddystoneNamespace namespace) {
        Log.i("Sample", "Eddystone discovered: " + eddystone.toString());
      }
    };
  }
}
```

Samples App
===========
For SDK usage samples see the [Samples App](https://github.com/kontaktio/kontakt-beacon-admin-sample-app)

Kontakt.io Administration App
===========
To manage Kontakt.io devices please use our [Administration App](https://play.google.com/store/apps/details?id=io.kontakt.app).
<p align="left">
  <img src="http://i.imgur.com/phFdFPq.png">
</p>

## License
Licensed under Creative Commons Attribution-NoDerivs 3.0 Unported

<p>
THE WORK (AS DEFINED BELOW) IS PROVIDED UNDER THE TERMS OF THIS CREATIVE COMMONS PUBLIC LICENSE ("CCPL" OR "LICENSE"). THE WORK IS PROTECTED BY COPYRIGHT AND/OR OTHER APPLICABLE LAW. ANY USE OF THE WORK OTHER THAN AS AUTHORIZED UNDER THIS LICENSE OR COPYRIGHT LAW IS PROHIBITED.

BY EXERCISING ANY RIGHTS TO THE WORK PROVIDED HERE, YOU ACCEPT AND AGREE TO BE BOUND BY THE TERMS OF THIS LICENSE. TO THE EXTENT THIS LICENSE MAY BE CONSIDERED TO BE A CONTRACT, THE LICENSOR GRANTS YOU THE RIGHTS CONTAINED HERE IN CONSIDERATION OF YOUR ACCEPTANCE OF SUCH TERMS AND CONDITIONS.
</p>

You may obtain copy of the license at https://creativecommons.org/licenses/by-nd/3.0/legalcode

For more information please visit our [docs website].

[docs website]:https://kontakt-api-docs.stoplight.io/docs/dev-ctr-sdks/ZG9jOjMwMzg3NjUz-getting-started
