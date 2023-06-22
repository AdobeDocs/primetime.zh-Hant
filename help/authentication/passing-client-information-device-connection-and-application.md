---
title: 傳遞使用者端資訊（裝置、連線和應用程式）
description: 傳遞使用者端資訊（裝置、連線和應用程式）
exl-id: 0b21ef0e-c169-48ff-ac01-25411cfece1e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# 傳遞使用者端資訊（裝置、連線和應用程式） {#pass-client-info}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。


## 範圍 {#pass-client-info-scope}

本檔案彙總了從程式設計人員應用程式傳遞使用者端資訊（裝置、連線和應用程式）至Adobe Primetime Authentication REST API或SDK的詳細資訊和逐步指南。

提供使用者端資訊的好處包括：

* 在某些裝置型別和可支援HBA的MVPD的情況下，能夠正確啟用Home Base Authentication (HBA)。
* 在某些裝置型別的情況下正確套用TTL的功能（例如，為電視連線裝置上的驗證工作階段設定較長的TTL）。
* 能夠使用Entitlement Service Monitoring (ESM)在各種裝置型別的劃分報表中正確彙總業務量度。
* 解除封鎖正確套用各種商業規則(例如： 降級)。

## 概觀 {#pass-client-info-overview}

使用者端資訊包含：

* **裝置** 使用者嘗試使用程式設計人員內容的裝置之軟硬體屬性的相關資訊。
* **連線** 使用者連線至Adobe Primetime Authentication Services及/或程式設計人員服務時所使用之裝置的連線屬性相關資訊（例如伺服器對伺服器實作）。
* **應用** 有關使用者嘗試使用程式設計人員內容的註冊應用程式的資訊。

使用者端資訊是JSON物件，使用下表所示的金鑰建置。

>[!NOTE]
>
>下列專案 **金鑰** 是 **強制** 要在使用者端資訊JSON物件中傳送： **模型**， **osName**.
>
>下列鍵具有 **受限制** 值： `primaryHardwareType`， `osName`， `osFamily`， `browserName`， `browserVendor`， `connectionSecure`.

|  | 金鑰 | 受限制 | 說明 | 可能的值 |
|---|---|---|---|---|
|  | primaryHardwareType | #是 | 裝置的主要硬體型別。 | #值受限： Camera DataCollectionTerminal Desktop EmbeddedNetworkModule eReader遊戲主機GeolocationTracker Glass MediaPlayer MobilePhone PaymentTerminal PluginModem SetTopBox TV Tablet WirelessHotspot腕錶未知 |
| #mandatory | 模型 | 否 | 裝置的型號名稱。 | 例如iPhone、SM-G930V、AppleTV等。 |
|  | 版本 | 否 | 裝置的版本。 | 例如2.0.1等。 |
|  | 製造商 | 否 | 裝置的製造公司/組織。 | 例如三星、LG、中興、華為、摩托羅拉、Apple等。 |
|  | 廠商 | 否 | 裝置的銷售公司/組織。 | 例如Apple、Samsung、LG、Google等。 |
| #mandatory | osName | #是 | 裝置的作業系統(OS)名稱。 | #限制的值： Android Chrome作業系統Linux Mac作業系統X OpenBSD Roku作業系統Windows iOS tvOS webOS |
|  | osFamily | 是 | 裝置的作業系統(OS)群組名稱。 | #限制的值： Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | 否 | 裝置的作業系統(OS)供應商。 | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Sony Tizen Project |
|  | osVersion | 否 | 裝置的作業系統(OS)版本。 | 例如10.2、9.0.1等。 |
|  | browserName | #是 | 瀏覽器的名稱。 | #限制的值： Android瀏覽器Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian瀏覽器 |
|  | browserVendor | #是 | 瀏覽器的建置公司/組織。 | #值受限： Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|  | browserVersion | 否 | 裝置的瀏覽器版本。 | 例如60.0.3112 |
|  | userAgent | 否 | 裝置的使用者代理。 | 例如Mozilla/5.0 (Macintosh；Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 （KHTML，如Gecko）版本/10.0.3 Safari/602.4.8 |
|  | displaywidth | 否 | 裝置的實體熒幕寬度。 |  |
|  | displayheight | 否 | 裝置的實體熒幕高度。 |  |
|  | displayPpi | 否 | 裝置的實體熒幕畫素密度。 | 例如294 |
|  | 對角熒幕大小 | 否 | 裝置的實體熒幕對角尺寸（英吋）。 | 例如5.5、10.1 |
|  | connectionIp | 否 | 用於傳送HTTP要求的裝置IP。 | 例如8.8.4.4 |
|  | connectionPort | 否 | 用於傳送HTTP要求的裝置連線埠。 | 例如53124 |
|  | connectionType | 否 | 網路連線型別。 | 例如WiFi、LAN、3G、4G、5G |
|  | connectionSecure | #是 | 網路連線安全性狀態。 | #值會受到限制： true — 若是安全網路false — 若是公用連結區 |
|  | applicationId | 否 | 應用程式的唯一識別碼。 | 例如CNN |

## API參考 {#api-ref}

本節介紹負責在使用Adobe Primetime驗證REST API或SDK時處理使用者端資訊的API。

### REST API {#rest-api}

Adobe Primetime驗證服務支援以下列方式接收使用者端資訊：

* As a **標頭： &quot;X-Device-Info&quot;**
* As a **查詢引數： &quot;device_info&quot;**
* As a **post引數： &quot;device_info&quot;**

>[!IMPORTANT]
>
>在所有三個案例中，標頭或引數的裝載必須是 **Base64編碼和URL編碼**.

**SDK**

#### JavaScript SDK {#js-sdk}

AccessEnabler JavaScript SDK預設會建置使用者端資訊JSON物件，除非覆寫，否則會傳遞至Adobe Primetime驗證服務。

AccessEnabler JavaScript SDK支援 **僅覆寫** 「applicationId」金鑰從使用者端資訊JSON物件透過 [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))的 *applicationId* options引數。

>[!CAUTION]
>
>此 `applicationId` 引數值必須是純文字字串值。
>如果程式設計師應用程式決定傳遞applicationId，其餘的使用者端資訊金鑰仍會由AccessEnabler JavaScript SDK計算。

#### iOS/tvOS SDK {#ios-tvos-sdk}

AccessEnabler iOS/tvOS SDK預設會建置使用者端資訊JSON物件，除非覆寫，否則會傳遞至Adobe Primetime驗證服務。

AccessEnabler iOS/tvOS SDK支援 **覆寫整個** 使用者端資訊JSON物件，透過 [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)的裝置資訊引數。

>[!CAUTION]
>
>此 *device_info* 引數值必須是 **Base64編碼** *NSString* 值。
>
>如果程式設計師應用程式決定傳遞 *device_info*，則由AccessEnabler iOS/tvOS SDK運算出的所有使用者端資訊金鑰將會覆寫。 因此，請務必計算並傳遞儘可能多的索引鍵的值。 如需實作的詳細資訊，請參閱 [概觀](#pass-client-info-overview) 表格和 [iOS/tvOS逐步指南](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

此 `AccessEnabler` Android/FireOS SDK預設會建置使用者端資訊JSON物件，除非覆寫，否則會傳遞至Adobe Primetime驗證服務。

此 `AccessEnabler` Android/FireOS SDK支援 **覆寫整個** 使用者端資訊JSON物件，透過 [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)的/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)的 `device_info` 引數。

>[!NOTE]
>
>此 `device_info` 引數值必須是 **Base64編碼** 字串值。

>[!IMPORTANT]
>
>如果程式設計師應用程式決定傳遞 `device_info`，然後由計算的所有使用者端資訊金鑰 `AccessEnabler` 將覆寫Android/FireOS SDK。 因此，請務必計算並傳遞儘可能多的索引鍵的值。 如需實作的詳細資訊，請參閱 [概觀](#pass-client-info-overview) 表格和 [Android](#android) 和 [FireOS](#fire-tv) 逐步指南。

## 逐步指南 {#cookbooks}

本節提供在不同裝置型別情況下建立使用者端資訊JSON物件的逐步指南。

>[!IMPORTANT]
>
>標示為的金鑰  **！** 為必填，才能傳送。

### Android {#android}

裝置資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------------------------|---------------|
| ! | 模型 | Build.MODEL | GT-I9505 |
|  | 廠商 | Build.BRAND | samsung |
|  | 製造商 | Build.MANUFACTURER | samsung |
| ! | 版本 | Build.DEVICE | jflte |
|  | displaywidth | DisplayMetrics.widthPixels | 600 |
|  | displayheight | DisplayMetrics.heightPixels | 800 |
| ! | osName | 硬式編碼 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

連線資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

應用程式資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
裝置、連線和應用程式資訊必須新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，若是Adobe Primetime驗證REST API，該值必須為 **URL已編碼**.

**程式碼範例**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**資源：**
* 公用類別 [建置](https://developer.android.com/reference/android/os/Build.html){target=_blank} （在Java開發人員檔案中）。


### FireTV {#fire-tv}

裝置資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（例如） |
|---|---------------|-----------------------------|--------------|
| ! | 模型 | Build.MODEL | AFTM |
|  | 廠商 | Build.BRAND | Amazon |
|  | 製造商 | Build.MANUFACTURER | Amazon |
| ! | 版本 | Build.DEVICE | montoya |
|  | displaywidth | DisplayMetrics.widthPixels |  |
|  | displayheight | DisplayMetrics.heightPixels |  |
| ! | osName | 硬式編碼 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

連線資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

應用程式資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
裝置、連線和應用程式資訊必須新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，若是Adobe Primetime驗證REST API，該值必須為 **URL已編碼**.

>[!NOTE]
**資源：**
* 公用類別 [建置](https://developer.android.com/reference/android/os/Build.html){target=_blank} （位於Android開發人員檔案中）。
* [識別FireTV裝置](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

裝置資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|------------------------|--------------|
| ! | 模型 | uname.machine | iPhone |
|  | 廠商 | 硬式編碼 | Apple |
|  | 製造商 | 硬式編碼 | Apple |
| ! | 版本 | uname.machine | 8,1 |
|  | displaywidth | UIScreen.mainScreen | 320 |
|  | displayheight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

連線資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [連線能力currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


應用程式資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
裝置、連線和應用程式資訊必須新增至相同的JSON物件。 之後，產生的物件必須經過Base64編碼。 此外，若是Adobe Primetime驗證REST API，值必須經過URL編碼。

**程式碼範例**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**資源：**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [關於連線能力](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

裝置資訊的建構方式如下：

| 金鑰 | 來源 | 值（範例） |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | 模型 | 硬式編碼 | &quot;Roku&quot; |
|  | 廠商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;、&quot;Roku&quot; |
|  | 製造商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;、&quot;Roku&quot; |
| ! | 版本 | ifDeviceInfo.GetModelDetails().ModelNumber | 「5303X」 |
|  | displaywidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayheight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | 硬式編碼 | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

連線資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | 「WifiConnection」、「WiredConnection」 |
|  | connectionSecure | 硬式編碼 | 如果連線有線，則為true |

應用程式資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
裝置、連線和應用程式資訊必須新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，若是Adobe Primetime驗證REST API，值必須經過URL編碼。

>[!NOTE]
如需詳細資訊，請參閱 [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

裝置資訊的建構方式如下：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | 模型 | EasClientDeviceInformation.SystemProductName |  |
|  | 廠商 | 硬式編碼 | Microsoft |
|  | 製造商 | 硬式編碼 | Microsoft |
| ! | 版本 | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displaywidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayheight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

連線資訊的建構方式如下：

|  | 金鑰 | 來源 | 範例 |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | 「無」、「Wpa」等 |

應用程式資訊的建構方式如下：

| 金鑰 | 來源 | 值（範例） |
|---|---|---|
| applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
裝置、連線和應用程式資訊必須新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，若是Adobe Primetime驗證REST API，該值必須為 **URL已編碼**.

**資源**

* [EasClientDeviceInformation類別](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [顯示資訊類別](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)
