---
title: 使用Primetime Authentication Access Enabler時iOS上的SSO
description: 使用Primetime Authentication Access Enabler時iOS上的SSO
exl-id: 882f0abb-2e6e-461d-a375-3ab410991935
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# 使用Primetime Authentication Access Enabler時iOS上的SSO {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 概觀

Primetime驗證支援的應用程式之間的單一登入(SSO)會根據基礎作業系統以不同方式運作。

本檔案地址 **iOS上的SSO**，使用Adobe Primetime驗證時 **存取啟用程式**.

**存取啟用程式** **1.10** 是Adobe Primetime驗證iOS原生SDK的最新版本。 Adobe強烈建議您改用此版本，不要再使用舊版。 如果您使用的是舊版Access Enabler，您可以下載最新版本 [此處](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

iOS上的SSO受下列條件支配：

- 應用程式必須使用相同的 **權杖儲存** （以Access Enabler建立的自訂作業範圍形式）。
- 應用程式必須產生相同的 **裝置ID** (Access Enabler會根據MAC位址或IDFV （視作業系統版本而定）計算裝置ID。)

## 行為

SSO行為如下：

- **iOS 6及以下版本**：SSO可在相同團隊或不同團隊開發的應用程式之間自動運作。 裝置ID是根據MAC位址計算（所有應用程式中都會產生相同的值），而且儲存區域對所有應用程式都是通用的(自訂作業範圍可跨iOS 6及較低版本的應用程式共用)。
   - **重要：** 請注意，iOS SDK 1.9.4版已 [將最低iOS部署目標提高至iOS 7。](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7和更高版本**：SSO的運作條件如下：

1. 應用程式是使用相同的Apple發佈設定檔發佈，或是屬於相同團隊的設定檔發佈。 這是應用程式在iOS 7和更高版本上共用自訂剪貼簿的唯一方法。 在所有其他情況下，作業範圍會依應用程式而沙箱。 從 [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html)： \+\[UIPasteboard作業區域名稱:create:\]和+\[UIPasteboard作業範圍具有UniqueName\]現在會唯一指定名稱，僅允許相同應用程式群組中的應用程式存取作業範圍。 如果開發人員嘗試以已存在的名稱建立作業範圍，且不屬於相同應用程式套裝，將取得專屬的私人作業範圍。 請注意，這不會影響系統提供的剪貼簿、一般和尋找。

1. 應用程式具有相同的套件組合ID首碼（最後一個元件以外的所有元件）。 只有共用相同套件ID首碼的應用程式才會計算相同的IDFV。 從 [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor)：在IOS 7上，組合的所有元件（最後一個元件除外）都會用來產生廠商ID。 如果套件ID只有單一元件，則會使用整個套件ID。

現在來著重於 **&#39;iOS 7和更高版本&#39;** 情境，因為這是實際使用者最常使用的情境：

兩個條件（共用來自相同開發團隊的設定檔並具有通用組合識別碼首碼）是SSO的必要條件。

以下是可能的組合及其產生的結果：

- **來自相同團隊和相同套件組合ID首碼的設定檔**：應用程式會共用相同的作業範圍儲存空間，且裝置識別碼(IDFV)相同。 使用者只需驗證一次（在使用的第一個應用程式中），且驗證狀態將在所有其他應用程式之間共用。 範例流程：

1. 使用者開啟應用程式A （含套件編號） *com.x.y.AppA*)且已取消驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B （含套件組合ID） *com.x.y.AppB*)並透過共用應用程式A的權益資料來自動驗證（來自步驟2）
1. 使用者開啟應用程式A且仍通過驗證（來自步驟2）

 

- **來自相同團隊但不同套件組合ID首碼的設定檔**：應用程式將共用相同的作業範圍儲存空間，但會有不同的裝置ID (IDFV)。 使用者需要針對每個應用程式驗證一次。 範例流程：

1. 使用者開啟應用程式A （含套件編號） *com.x.y.AppA*)且已取消驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B （含套件組合ID） *com.z.AppB*)和Access Enabler會偵測到第一個應用程式取得的權杖（因為儲存空間已共用），但因為不同的裝置ID，所以不會嘗試透過SSO使用權杖
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A且仍通過驗證（來自步驟2）

 

- **來自不同團隊的設定檔（此情境中不會包含套件組合ID）**：應用程式會有不同的作業範圍儲存空間，而且兩者之間的SSO將會停用。 使用者需要為每個應用程式驗證一次，並且在應用程式之間切換時，驗證工作階段將持續存在。 範例流程：


1. 使用者開啟應用程式A且未驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B且未驗證
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A並驗證（從步驟2）
1. 使用者開啟應用程式B並驗證（從步驟4）

**注意：** 請注意，上述的SSO條件適用於透過 **Apple App Store**. 如果應用程式部署在模擬器上（應用程式簽署不適用）、使用Xcode安裝或透過Ad Hoc設定檔發佈，您可能會獲得不同的結果。

**重要：** 附註(**關於AccessEnabler v1.8**)：上述第二個案例（來自相同團隊但不同套件ID首碼的設定檔）會為的使用者帶來非常不愉快的使用者體驗。 **AccessEnabler v1.8** 跨由同一團隊（媒體公司）開發的應用程式。 使用者在來自相同媒體公司的應用程式之間轉換時將自動登出，因此，應用程式開發人員在決定套件ID和發佈設定檔時，必須小心。 此案例的確切情況如下所示：

應用程式將共用相同的作業範圍儲存空間，但會有不同的裝置ID (IDFV)。 使用者需要針對每個應用程式驗證一次， **但是在應用程式之間切換時，將會清除驗證工作階段**. 範例流程：

1. 使用者開啟應用程式A （含套件編號） *com.x.y.AppA*)且已取消驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B （含套件組合ID） *com.z.AppB*)，且應用程式A建立的權益資料會由Access Enabler自動清除（安全性機制，會偵測應用程式B中目前計算的裝置ID與應用程式A建立的權益代號中儲存的裝置ID之間是否有衝突）
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A，應用程式B建立的權益資料會由Access Enabler自動清除（安全性機制，會偵測應用程式A中目前計算的裝置ID與應用程式B建立的權益代號中儲存的裝置ID之間的衝突）
