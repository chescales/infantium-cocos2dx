infantium-cocos2dx
==================

Dependencies:
-------------

This project requires the EasyNDK project to run. You can find it here: [EasyNDK repository](https://github.com/vedi/EasyNDK>)

General info about the integration:
-----------------------------------

You can find more info about the integration process with Infantium in its developers webpage: [Infantium Dev Center](http://docs.infantium.com/walkthroughs/game_walkthrough.html)

Some info about how to integrate:
---------------------------------

1. Add to Activity:onCreate:

  InfantiumManager.initModule(this);

2. Add to Activity:onPause:

  InfantiumManager.onPause();

3. Add to Activity:onResume:

  InfantiumManager.onResume();

4. Add to Activity new method:

``````````````````java
public JSONObject infantium_easyNDK(JSONObject params) {
    Log.v("infantium_easyNDK", "infantium_easyNDK called");
    Log.v("infantium_easyNDK", "Passed params are : " + params.toString());
    JSONObject retParams = InfantiumBridge.dispatchNDKCall(params);

    try {
        Log.v("infantium_easyNDK", "Returned Params params are : " + retParams.toString());
    }
    catch (NullPointerException e) {
        Log.v("infantium_easyNDK", "returned null params");
    }
    return retParams;
}
``````````````````

5. Add rights to the manifest:

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>

6. In cocos2d-x AppDelegate:applicationDidFinishLaunching add:

  InfantiumModule.init(apiUser, apiKey, contentAppUuid);

7. Do not forget to add dependencies to project.properties & Android.mk.

8. Optionally for iOS stubs. Add method to RootViewController:

``````````````````c++
(NSObject *)infantium_easyNDK:(NSObject *)params {
    NSLog(@"infantium_easyNDK call");
    NSDictionary *parameters = (NSDictionary*) params;
    NSLog(@"Passed params are : %@", parameters);

    NSObject *retParams = [InfantiumBridge dispatchNDKCall:parameters];
    NSLog(@"RetParams params are : %@", retParams);

    return retParams;
}
``````````````````
