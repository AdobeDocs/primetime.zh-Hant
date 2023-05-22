---
title: 傳遞客戶端資訊（設備、連接和應用程式）
description: 傳遞客戶端資訊（設備、連接和應用程式）
exl-id: 0b21ef0e-c169-48ff-ac01-25411cfece1e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# 傳遞客戶端資訊（設備、連接和應用程式） {#pass-client-info}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 範圍 {#pass-client-info-scope}

本文檔聚合了用於將客戶端資訊（設備、連接和應用程式）從程式設計師應用程式傳遞到Adobe Primetime驗證REST API或SDK的詳細資訊和指南。

提供客戶資訊的好處是：

* 在某些可支援HBA的設備類型和MVPD的情況下，能夠正確啟用家庭基本身份驗證(HBA)。
* 在某些設備類型的情況下正確應用TTL（例如，為電視連接設備上的驗證會話配置較長的TTL）。
* 能夠使用權利服務監控(ESM)在設備類型的故障報告中正確聚合業務度量。
* 取消阻止正確應用各種業務規則的能力(例如 降級)。

## 概述 {#pass-client-info-overview}

客戶端資訊包括：

* **設備** 有關設備的硬體和軟體屬性的資訊，用戶試圖從其中使用程式設計師內容。
* **連接** 關於用戶從其連接到Adobe Primetime認證服務和/或程式設計師服務（例如伺服器到伺服器實現）的設備的連接屬性的資訊。
* **應用程式** 有關已註冊應用程式的資訊，用戶試圖從其中使用程式設計師內容。

客戶端資訊是使用下表中顯示的鍵構建的JSON對象。

>[!NOTE]
>
>以下 **鍵** 是 **強制** 要在客戶端資訊JSON對象中發送： **模型**。 **osName**。
>
>以下鍵具有 **限制** 值： `primaryHardwareType`。 `osName`。 `osFamily`。 `browserName`。 `browserVendor`。 `connectionSecure`。

|  | 鍵 | 受限 | 說明 | 可能的值 |
|---|---|---|---|---|
|  | primaryHardwareType | #是 | 設備的主硬體類型。 | #值受限制：相機資料收集終端案頭嵌入式網路模組eReader遊戲控制台地理位置跟蹤器眼鏡媒體播放器手機支付終端插件調制解調器機頂盒電視平板電腦無線熱點手錶未知 |
| #mandatory | 模型 | 否 | 設備的型號名稱。 | 例如，iPhone、SM-G930V、AppleTV等。 |
|  | 版本 | 否 | 設備的版本。 | 例如2.0.1等。 |
|  | 製造商 | 否 | 設備的製造公司/組織。 | 如三星、LG、中興、華為、摩托羅拉、Apple等。 |
|  | 供應商 | 否 | 設備的銷售公司/組織。 | 例如，Apple、三星、LG、Google等。 |
| #mandatory | osName | #是 | 設備的作業系統(OS)名稱。 | #值受限制：Android Chrome OS LinuxMacOS OS X OpenBSD Roku OS WindowsiOSOS webOS |
|  | os系列 | 是 | 設備的作業系統(OS)組名稱。 | #值受限制：Android BSD Linux PlayStation OS Roku OS Symbian Tizen WindowsiOSmacOS電視OS webOS |
|  | 作業系統供應商 | 否 | 設備的作業系統(OS)供應商。 | AmazonAppleGoogleLGMicrosoftMozilla任天堂Nokia Roku三星Sony Tizen項目 |
|  | os版本 | 否 | 設備的作業系統(OS)版本。 | 例如10.2、9.0.1等。 |
|  | 瀏覽器名稱 | #是 | 瀏覽器的名稱。 | #值受限制：Android瀏覽器Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian瀏覽器 |
|  | 瀏覽器供應商 | #是 | 瀏覽器的建築公司/組織。 | #值受限制：AmazonAppleGoogleMicrosoft摩托羅拉Mozilla Netscape任天堂諾基亞三星索尼愛立信 |
|  | 瀏覽器版本 | 否 | 設備的瀏覽器版本。 | 例如60.0.3112 |
|  | 用戶代理 | 否 | 設備的用戶代理。 | 例如Mozilla/5.0(Macintosh;英特爾MacOS X 10_12_3)AppleWebKit/602.4.8（KHTML，如Gecko）版本/10.0.3 Safari/602.4.8 |
|  | 顯示寬度 | 否 | 設備的物理螢幕寬度。 |  |
|  | displayHeight | 否 | 設備的物理螢幕高度。 |  |
|  | 顯示Ppi | 否 | 設備的物理螢幕像素密度。 | 例如294 |
|  | 對角螢幕大小 | 否 | 設備的物理螢幕對角尺寸（英吋）。 | 例如5.5、10.1 |
|  | 連接IP | 否 | 用於發送HTTP請求的設備的IP。 | 例如8.8.4.4 |
|  | 連接埠 | 否 | 用於發送HTTP請求的設備埠。 | 例如53124 |
|  | 連接類型 | 否 | 網路連接類型。 | 例如WiFi、LAN、3G、4G、5G |
|  | 連接安全 | #是 | 網路連接安全狀態。 | #值受限制：true — 在安全網路為false時 — 在公共熱點時 |
|  | 應用程式ID | 否 | 應用程式的唯一標識符。 | 例如CNN |

## API引用 {#api-ref}

本節介紹在使用Adobe Primetime驗證REST API或SDK時負責處理客戶端資訊的API。

### REST API {#rest-api}

Adobe Primetime認證服務支援通過以下方式接收客戶端資訊：

* 作為 **標題：&quot;X-Device-Info&quot;**
* 作為 **查詢參數：&quot;設備_資訊&quot;**
* 作為 **post參數：&quot;設備_資訊&quot;**

>[!IMPORTANT]
>
>在所有三種情況中，頭或參數的負載必須是 **Base64編碼和URL編碼**。

**SDK**

#### JavaScript SDK {#js-sdk}

預設情況下，AccessEnabler JavaScript SDK會生成客戶端資訊JSON對象，該對象將傳遞給Adobe Primetime身份驗證服務，除非被覆蓋。

AccessEnabler JavaScript SDK支援 **僅覆蓋** 客戶端資訊JSON對象中的「applicationId」鍵 [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))`s *應用程式ID* 選項參數。

>[!CAUTION]
>
>的 `applicationId` 參數值必須是純文字檔案字串值。
>如果程式設計師應用程式決定傳遞applicationId，則其餘的客戶端資訊鍵仍將由AccessEnabler JavaScript SDK計算。

#### iOS/電視作業系統SDK {#ios-tvos-sdk}

預設情況下，AccessEnableriOS/tvOS SDK會生成客戶端資訊JSON對象，該對象將傳遞給Adobe Primetime身份驗證服務，除非被覆蓋。

AccessEnableriOS/tvOS SDK支援 **壓倒整體** 客戶端資訊JSON對象通過 [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)的device_info參數。

>[!CAUTION]
>
>的 *設備資訊* 參數值必須是 **Base64編碼** *NSString* 值。
>
>如果程式設計師應用程式決定通過 *設備資訊*，則由AccessEnableriOS/tvOS SDK計算的所有客戶端資訊密鑰將被覆蓋。 因此，計算並傳遞盡可能多的鍵值非常重要。 有關實施的詳細資訊，請參見 [概述](#pass-client-info-overview) 和 [iOS/電視OS烹飪書](#ios-tvos)。

#### Android/FireOS SDK {#and-fire-os-sdk}

的 `AccessEnabler` 預設情況下，Android/FireOS SDK會生成客戶端資訊JSON對象，該對象將傳遞給Adobe Primetime身份驗證服務，除非被覆蓋。

的 `AccessEnabler` Android/FireOS SDK支援 **壓倒整體** 客戶端資訊JSON對象通過 [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)`s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)`s `device_info` 的下界。

>[!NOTE]
>
>的 `device_info` 參數值必須是 **Base64編碼** 字串值。

>[!IMPORTANT]
>
>如果程式設計師應用程式決定通過 `device_info`，則由 `AccessEnabler` Android/FireOS SDK將被覆蓋。 因此，計算並傳遞盡可能多的鍵值非常重要。 有關實施的詳細資訊，請參見 [概述](#pass-client-info-overview) 和 [安卓](#android) 和 [FireOS](#fire-tv) 烹飪書。

## 烹飪書 {#cookbooks}

本節介紹了一本手冊，用於在不同設備類型的情況下構建客戶端資訊JSON對象。

>[!IMPORTANT]
>
>標籤為  **!** 必須發送。

### 安卓 {#android}

設備資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|-----------------------------|---------------|
| ! | 模型 | Build.MODEL | GT-I9505 |
|  | 供應商 | Build.BRAND | 三星 |
|  | 製造商 | Build.MANUFACTURER | 三星 |
| ! | 版本 | Build.DEVICE | jflt |
|  | 顯示寬度 | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | 硬編碼 | 安卓 |
| ! | os版本 | Build.VERSION.RELEASE | 5.0.1 |

連接資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---|---|---|
| ! | 連接類型 | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | 連接安全 |  |  |

應用資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | 應用程式ID | 硬編碼 | 美國有線電視新聞網 |

>[!IMPORTANT]
必須將設備、連接和應用程式資訊添加到同一JSON對象。 之後，生成的對象必須 **Base64編碼**。 此外，在Adobe Primetime驗證REST API的情況下，值必須為 **URL編碼**。

**示例代碼**

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
* 公共類 [構建](https://developer.android.com/reference/android/os/Build.html){target=_blank} 在Java開發者文檔中。


### 火電視 {#fire-tv}

設備資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（例如） |
|---|---------------|-----------------------------|--------------|
| ! | 模型 | Build.MODEL | AFTM |
|  | 供應商 | Build.BRAND | Amazon |
|  | 製造商 | Build.MANUFACTURER | Amazon |
| ! | 版本 | Build.DEVICE | 蒙托亞 |
|  | 顯示寬度 | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | 硬編碼 | 安卓 |
| ! | os版本 | Build.VERSION.RELEASE | 5.1.1 |

連接資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|------------------|--------|---------------|
| ! | 連接類型 |  |  |
|  | 連接安全 |  |  |

應用資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | 應用程式ID | 硬編碼 | 美國有線電視新聞網 |

>[!IMPORTANT]
必須將設備、連接和應用程式資訊添加到同一JSON對象。 之後，生成的對象必須 **Base64編碼**。 此外，在Adobe Primetime驗證REST API的情況下，值必須為 **URL編碼**。

>[!NOTE]
**資源：**
* 公共類 [生成](https://developer.android.com/reference/android/os/Build.html){target=_blank} Android開發者的文檔。
* [識別FireTV設備](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/電視OS {#ios-tvos}

設備資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|------------------------|--------------|
| ! | 模型 | uname.machine | iPhone |
|  | 供應商 | 硬編碼 | Apple |
|  | 製造商 | 硬編碼 | Apple |
| ! | 版本 | uname.machine | 8,1 |
|  | 顯示寬度 | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | os版本 | UIDevice.systemVersion | 10.2 |

連接資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|------------------|-------------------------------------------|--------------|
| ! | 連接類型 | [可接通性currentReachabilityStatus] |  |
|  | 連接安全 |  |  |


應用資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | 應用程式ID | 硬編碼 | 美國有線電視新聞網 |

>[!IMPORTANT]
必須將設備、連接和應用程式資訊添加到同一JSON對象。 隨後，生成的對象必須是Base64編碼。 此外，在Adobe Primetime驗證REST API的情況下，值必須是URL編碼。

**示例代碼**

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
* [UID設備](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [未命名](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [關於可接通性](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### 羅庫 {#roku}

設備資訊可以通過以下方式構建：

| 鍵 | 源 | 值（示例） |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | 模型 | 硬編碼 | 《羅庫》 |
|  | 供應商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;夏普&quot;、&quot;Roku&quot; |
|  | 製造商 | ifDeviceInfo.GetModelDetails().VendorName | &quot;夏普&quot;、&quot;Roku&quot; |
| ! | 版本 | ifDeviceInfo.GetModelDetails().ModelNumber | 「5303X」 |
|  | 顯示寬度 | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | 硬編碼 | 《羅庫》 |
| ! | os版本 | ifDeviceInfo.getVersion() |  |

連接資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---|---|---|
| ! | 連接類型 | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;,&quot;WiredConnection&quot; |
|  | 連接安全 | 硬編碼 | 如果連接為有線，則為true |

應用資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---------------|-----------|--------------|
|  | 應用程式ID | 硬編碼 | 美國有線電視新聞網 |

>[!IMPORTANT]
必須將設備、連接和應用程式資訊添加到同一JSON對象。 之後，生成的對象必須 **Base64編碼**。 此外，在Adobe Primetime驗證REST API的情況下，值必須是URL編碼。

>[!NOTE]
有關詳細資訊，請參見 [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

設備資訊可以通過以下方式構建：

|  | 鍵 | 源 | 值（示例） |
|---|---|---|---|
| ! | 模型 | EasClientDeviceInformation.SystemProductName |  |
|  | 供應商 | 硬編碼 | Microsoft |
|  | 製造商 | 硬編碼 | Microsoft |
| ! | 版本 | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | 顯示寬度 | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | os版本 | EasClientDeviceInformation.SystemFirmwareVersion |  |

連接資訊可以通過以下方式構建：

|  | 鍵 | 源 | 示例 |
|---|---|---|---|
| ! | 連接類型 |  |  |
|  | 連接安全 | 網路驗證類型 | 「無」、「WPA」等 |

應用資訊可以通過以下方式構建：

| 鍵 | 源 | 值（示例） |
|---|---|---|
| 應用程式ID | 硬編碼 | 美國有線電視新聞網 |

>[!IMPORTANT]
必須將設備、連接和應用程式資訊添加到同一JSON對象。 之後，生成的對象必須 **Base64編碼**。 此外，在Adobe Primetime驗證REST API的情況下，值必須為 **URL編碼**。

**資源**

* [EasClientDeviceInformation類](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [DisplayInformation類](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)
