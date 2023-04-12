---
title: 傳遞客戶端資訊（設備、連接和應用程式）
description: 傳遞客戶端資訊（設備、連接和應用程式）
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# 傳遞客戶端資訊（設備、連接和應用程式） {#pass-client-info}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 範圍 {#pass-client-info-scope}

本檔案匯總了詳細資訊和逐步指南，用於將客戶端資訊（設備、連接和應用程式）從程式設計師應用程式傳遞到Adobe Primetime Authentication REST API或SDK。

提供客戶資訊的好處有：

* 在某些可支援HBA的設備類型和MVPD的情況下，正確啟用家庭基本身份驗證(HBA)的功能。
* 在某些裝置類型中正確套用TTL的功能（例如，針對電視連線裝置上的驗證工作階段設定較長的TTL）。
* 能夠使用權限服務監控(ESM)在各種設備類型的劃分報表中正確匯總業務度量。
* 取消封鎖正確套用各種業務規則的功能(例如 降級)。

## 概述 {#pass-client-info-overview}

客戶端資訊包括：

* **裝置** 有關設備的硬體和軟體屬性的資訊，用戶試圖從其中使用程式設計師內容。
* **連線** 有關用戶從其連接到Adobe Primetime身份驗證服務和/或程式設計師服務（例如伺服器到伺服器實施）的設備的連接屬性的資訊。
* **應用程式** 關於註冊應用程式的資訊，用戶試圖從其中使用程式設計師內容。

用戶端資訊是以下表所示索引鍵建立的JSON物件。

>[!NOTE]
>
>以下 **鍵** 為 **強制** 要在客戶端資訊JSON對象中發送： **模型**, **osName**.
>
>以下鍵具有 **受限** 值： `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | 金鑰 | 受限 | 說明 | 可能的值 |
|---|---|---|---|---|
|  | primaryHardwareType | #是 | 設備的主硬體類型。 | #值受限：相機資料收集終端案頭嵌入式網路模組電子閱讀器遊戲控制台地理位置追蹤器眼鏡媒體播放器行動電話支付終端插件資料機SetTopBox TV平板電腦無線熱點腕錶未知 |
| #mandatory | 模型 | 否 | 設備的型號。 | 例如iPhone、SM-G930V、AppleTV等。 |
|  | 版本 | 否 | 裝置的版本。 | 例如2.0.1等 |
|  | 製造商 | 否 | 裝置的製造公司/組織。 | 例如三星、LG、中興、華為、摩托羅拉、Apple等 |
|  | 供應商 | 否 | 裝置的銷售公司/組織。 | 例如Apple、三星、LG、Google等 |
| #mandatory | osName | #是 | 裝置的作業系統(OS)名稱。 | #值受限：Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | 是 | 設備的作業系統(OS)組名。 | #值受限：Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | 否 | 設備的作業系統(OS)供應商。 | Amazon Apple Google LG Microsoft Mozilla任天堂Nokia Roku三星Sony Tizen Project |
|  | osVersion | 否 | 裝置的作業系統(OS)版本。 | 例如10.2、9.0.1等 |
|  | browserName | #是 | 瀏覽器的名稱。 | #值受限：Android瀏覽器Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian瀏覽器 |
|  | browserVendor | #是 | 瀏覽器的建立公司/組織。 | #值受限：Amazon Apple Google Microsoft Motorola Mozilla Netscape任天堂Nokia Samsung Sony Ericsson |
|  | browserVersion | 否 | 裝置的瀏覽器版本。 | 例如60.0.3112 |
|  | userAgent | 否 | 裝置的使用者代理。 | 例如Mozilla/5.0(Macintosh;英特爾Mac OS X 10_12_3)AppleWebKit/602.4.8（KHTML，如Gecko）版本/10.0.3 Safari/602.4.8 |
|  | displayWidth | 否 | 裝置的物理螢幕寬度。 |  |
|  | displayHeight | 否 | 裝置的物理螢幕高度。 |  |
|  | displayPpi | 否 | 裝置的物理螢幕像素密度。 | 例如294 |
|  | diagonalScreenSize | 否 | 設備的物理螢幕對角線尺寸（英吋）。 | 例如5.5、10.1 |
|  | connectionIp | 否 | 用於傳送HTTP要求的裝置IP。 | 例如8.8.4.4 |
|  | connectionPort | 否 | 用於傳送HTTP要求的裝置連接埠。 | 例如53124 |
|  | connectionType | 否 | 網路連接類型。 | 例如WiFi、LAN、3G、4G、5G |
|  | connectionSecure | #是 | 網路連接安全狀態。 | #值受限：true — 安全網路為false — 公共熱點為 |
|  | applicationId | 否 | 應用程式的唯一標識符。 | 例如CNN |

## API參考 {#api-ref}

本節介紹在使用Adobe Primetime Authentication REST API或SDK時，負責處理用戶端資訊的API。

### REST API {#rest-api}

Adobe Primetime驗證服務支援以下列方式接收用戶端資訊：

* As a **標題：&quot;X-Device-Info&quot;**
* As a **查詢參數：&quot;device_info&quot;**
* As a **貼文參數：&quot;device_info&quot;**

>[!IMPORTANT]
>
>在所有三種情況中，標題或參數的裝載必須 **Base64編碼和URL編碼**.

**SDK**

#### JavaScript SDK {#js-sdk}

AccessEnabler JavaScript SDK預設會建置用戶端資訊JSON物件，除非被覆寫，否則這些物件將傳遞至Adobe Primetime驗證服務。

AccessEnabler JavaScript SDK支援 **僅覆蓋** 來自用戶端資訊JSON物件的「applicationId」索引鍵，透過 [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))&#39;s *applicationId* 選項參數。

>[!CAUTION]
>
>此 `applicationId` 參數值必須是純文字字串值。
>如果程式設計師應用程式決定傳遞applicationId，則其餘的客戶端資訊密鑰仍由AccessEnabler JavaScript SDK計算。

#### iOS/tvOS SDK {#ios-tvos-sdk}

AccessEnabler iOS/tvOS SDK預設會建置用戶端資訊JSON物件，除非被覆寫，否則這些物件將傳遞至Adobe Primetime驗證服務。

AccessEnabler iOS/tvOS SDK支援 **壓倒一切** 用戶端資訊JSON物件，透過 [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)s device_info參數。

>[!CAUTION]
>
>此 *device_info* 參數值必須是 **Base64編碼** *NSString* 值。
>
>如果程式設計師應用程式決定通過 *device_info*，則由AccessEnabler iOS/tvOS SDK計算的所有客戶端資訊密鑰將被覆蓋。 因此，計算並傳遞盡可能多索引鍵的值非常重要。 如需實作的詳細資訊，請參閱 [概述](#pass-client-info-overview) 表格和 [iOS/tvOS逐步指南](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

此 `AccessEnabler` Android/FireOS SDK依預設會建置用戶端資訊JSON物件，除非遭覆寫，否則這些物件將會傳遞至Adobe Primetime驗證服務。

此 `AccessEnabler` Android/FireOS SDK支援 **壓倒一切** 用戶端資訊JSON物件，透過 [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)&#39;s `device_info` 參數。

>[!NOTE]
>
>此 `device_info` 參數值必須是 **Base64編碼** 字串值。

>[!IMPORTANT]
>
>如果程式設計師應用程式決定通過 `device_info`，則所有用戶端資訊金鑰由 `AccessEnabler` Android/FireOS SDK將被覆寫。 因此，計算並傳遞盡可能多索引鍵的值非常重要。 如需實作的詳細資訊，請參閱 [概述](#pass-client-info-overview) 表格和 [Android](#android) 和 [FireOS](#fire-tv) 逐步指南。

## 逐步指南 {#cookbooks}

本節提供一本逐步指南，說明在不同裝置類型的情況下，如何建立用戶端資訊JSON物件。

>[!IMPORTANT]
>
>已標籤的鍵  **!** 必須傳送。

### Android {#android}

設備資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------------------------|---------------|
| ! | 模型 | Build.MODEL | GT-I9505 |
|  | 供應商 | Build.BRAND | 三星 |
|  | 製造商 | Build.MANUFACTURER | 三星 |
| ! | 版本 | Build.DEVICE | jflte |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | 硬式編碼 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

連接資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

應用資訊可以通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
必須將裝置、連線和應用程式資訊新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，如果是Adobe Primetime Authentication REST API，值必須是 **URL編碼**.

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
* 公共類 [建置](https://developer.android.com/reference/android/os/Build.html){target=_blank} （在Java開發人員的檔案中）。


### FireTV {#fire-tv}

設備資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（例如） |
|---|---------------|-----------------------------|--------------|
| ! | 模型 | Build.MODEL | AFTM |
|  | 供應商 | Build.BRAND | Amazon |
|  | 製造商 | Build.MANUFACTURER | Amazon |
| ! | 版本 | Build.DEVICE | 蒙托亞 |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | 硬式編碼 | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

連接資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

應用資訊可以通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
必須將裝置、連線和應用程式資訊新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，如果是Adobe Primetime Authentication REST API，值必須是 **URL編碼**.

>[!NOTE]
**資源：**
* 公共類 [建置](https://developer.android.com/reference/android/os/Build.html){target=_blank} 在Android開發人員檔案中。
* [識別FireTV裝置](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

設備資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|------------------------|--------------|
| ! | 模型 | uname.machine | iPhone |
|  | 供應商 | 硬式編碼 | Apple |
|  | 製造商 | 硬式編碼 | Apple |
| ! | 版本 | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

連接資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [可達性currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


應用資訊可以通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
必須將裝置、連線和應用程式資訊新增至相同的JSON物件。 之後，產生的物件必須經過Base64編碼。 此外，如果是Adobe Primetime Authentication REST API，值必須經過URL編碼。

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
* [關於可達性](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

設備資訊可通過以下方式構建：

| 金鑰 | 來源 | 值（範例） |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | 模型 | 硬式編碼 | &quot;Roku&quot; |
|  | 供應商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;、&quot;Roku&quot; |
|  | 製造商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;、&quot;Roku&quot; |
| ! | 版本 | ifDeviceInfo.GetModelDetails().ModelNumber | 《5303X》 |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | 硬式編碼 | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

連接資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;、&quot;WiredConnection&quot; |
|  | connectionSecure | 硬式編碼 | 如果連線為true, |

應用資訊可以通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---------------|-----------|--------------|
|  | applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
必須將裝置、連線和應用程式資訊新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，如果是Adobe Primetime Authentication REST API，值必須經過URL編碼。

>[!NOTE]
如需詳細資訊，請參閱 [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

設備資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 值（範例） |
|---|---|---|---|
| ! | 模型 | EasClientDeviceInformation.SystemProductName |  |
|  | 供應商 | 硬式編碼 | Microsoft |
|  | 製造商 | 硬式編碼 | Microsoft |
| ! | 版本 | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

連接資訊可通過以下方式構建：

|  | 金鑰 | 來源 | 範例 |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | NetworkAuthenticationType | 「無」、「Wpa」等 |

應用資訊可以通過以下方式構建：

| 金鑰 | 來源 | 值（範例） |
|---|---|---|
| applicationId | 硬式編碼 | CNN |

>[!IMPORTANT]
必須將裝置、連線和應用程式資訊新增至相同的JSON物件。 之後，產生的物件必須 **Base64編碼**. 此外，如果是Adobe Primetime Authentication REST API，值必須是 **URL編碼**.

**資源**

* [EasClientDeviceInformation類](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [DisplayInformation類](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


