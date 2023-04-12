---
title: 使用Primetime驗證存取啟用碼時在iOS上的SSO
description: 使用Primetime驗證存取啟用碼時在iOS上的SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# 使用Primetime驗證存取啟用碼時在iOS上的SSO {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 概述

Primetime驗證支援應用程式之間的單一登入(SSO)會根據基礎作業系統以不同方式運作。

本文檔涉及 **iOS上的SSO**，使用Adobe Primetime驗證時 **Access Enabler**.

**Access Enabler** **1.10** 是Adobe Primetime驗證iOS原生SDK的最新版本。 Adobe強烈建議您改用此版本，而不要使用舊版。 如果您使用的是舊版Access Enabler，則可以下載最新版本 [此處](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

iOS上的SSO由下列條件決定：

- 應用必須使用相同 **權杖儲存** （以Access Enabler建立的自定義貼上板的形式）。
- 應用程式必須產生相同的 **裝置ID** (Access Enabler根據MAC地址或IDFV計算設備ID，具體取決於作業系統版本)。

## 行為

SSO行為如下：

- **iOS 6及更低版本**:SSO可在由相同團隊或不同團隊開發的應用程式之間自動運作。 裝置ID是根據MAC位址計算（所有應用程式都會產生相同值），而儲存區域是所有應用程式的共同區域(自訂貼上板可在iOS 6及更低版本的應用程式間共用)。
   - **重要：** 請注意，iOS SDK 1.9.4版已 [將iOS的最低部署目標提高至iOS 7。](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7及更新版本**:SSO可在下列條件下運作：

1. 使用相同的Apple發佈設定檔或屬於相同團隊的設定檔來發佈應用程式。 這是應用程式在iOS 7和更上層共用自訂貼上板的唯一方式。 在所有其他情況下，貼上板會根據應用程式進行沙箱處理。 從 [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html):\+\[UIPasteboard pasdboardWithName:create:\]和+\[UIPasteboard pasdboardWithUniqueName\]現在為指定名稱唯一，僅允許同一應用程式組中的那些應用訪問pasdboard。 如果開發人員嘗試使用已存在的名稱建立貼上板，而這些名稱不屬於同一個應用程式套裝，他們將獲得自己獨特的私人貼上板。 請注意，這不會影響系統提供的貼上板、常規和查找。

1. 應用程式具有相同的套件ID首碼（最後一個元件除外）。 只有共用相同套件ID首碼的應用程式才會計算相同的IDFV。 從 [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#/apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor):在IOS 7中，套件組合（最後一個元件除外）的所有元件都用於產生廠商ID。 如果套件ID只有單一元件，則會使用整個套件ID。

現在來關注 **&#39;iOS 7及更新版本** 情境，因為這是真正使用者最常使用的情形：

這兩個條件（共用同一開發團隊的設定檔且具有通用套件識別碼首碼）都是SSO的必要條件。

以下是可能的組合及其產生的結果：

- **來自相同團隊的設定檔和相同的套件ID首碼**:應用程式將共用相同的貼上板儲存空間，且會有相同的裝置ID(IDFV)。 使用者只需要驗證一次（在使用的第一個應用程式中），驗證狀態就會在所有其他應用程式間共用。 範例流程：

1. 使用者開啟應用程式A（使用套件ID） *com.x.y.AppA*)和未驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B（使用套件ID） *com.x.y.AppB*)，並透過共用應用程式A的授權資料來自動驗證（來自步驟2）
1. 使用者開啟應用程式A且仍通過驗證（從步驟2）

 

- **來自相同團隊但不同套件ID前置詞的設定檔**:應用程式會共用相同的貼上板儲存空間，但會有不同的裝置ID(IDFV)。 使用者必須對每個應用程式執行一次驗證。 範例流程：

1. 使用者開啟應用程式A（使用套件ID） *com.x.y.AppA*)和未驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B（使用套件ID） *com.z.AppB*)，而Access Enabler會偵測第一個應用程式取得的Token（因為儲存是共用的），但由於不同的裝置ID，它不會嘗試透過SSO使用
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A且仍通過驗證（從步驟2）

 

- **來自不同團隊的設定檔（此情境中，套件ID無關）**:應用程式將有不同的貼上板儲存區，且它們之間將禁用SSO。 使用者需要對每個應用程式執行一次驗證，而當在應用程式之間切換時，驗證工作階段會持續存在。 範例流程：


1. 使用者開啟應用程式A且未驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B且未驗證
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A並通過驗證（從步驟2）
1. 使用者開啟應用程式B並通過驗證（從步驟4）

**注意：** 請注意，上述SSO條件適用於透過 **AppleApp Store**. 如果應用程式部署在模擬器上（不適用應用程式簽署）、透過Xcode安裝，或透過Ad Hoc設定檔發佈，您可能會獲得不同結果。

**重要：** 注(**關於AccessEnabler v1.8**):上述第二個案例（來自相同團隊的設定檔，但不同的套件ID前置詞）會為使用者帶來非常不愉快的使用者體驗 **AccessEnabler v1.8** 由同一團隊（媒體公司）開發的應用程式。 當使用者從相同媒體公司轉換應用程式時，系統會自動將其登出，因此，在決定套件ID和發佈設定檔時，應用程式開發人員必須謹慎處理。 此情況的確切情況如下：

應用程式會共用相同的貼上板儲存空間，但會有不同的裝置ID(IDFV)。 使用者需要對每個應用程式執行一次驗證， **但在應用之間切換時，驗證會話將被清除**. 範例流程：

1. 使用者開啟應用程式A（使用套件ID） *com.x.y.AppA*)和未驗證
1. 使用者在應用程式A中執行驗證
1. 使用者開啟應用程式B（使用套件ID） *com.z.AppB*)，而應用程式A建立的權限資料會由Access Enabler自動清除(安全機制可偵測應用程式B中目前計算的裝置ID與儲存在權限權杖（由應用程式A建立）中的裝置ID之間的衝突)
1. 使用者在應用程式B中執行驗證
1. 使用者開啟應用程式A，應用程式B建立的權限資料便會由「存取啟用碼」自動清除(安全機制可偵測應用程式A中目前計算的裝置ID與儲存在權限代號（由應用程式B建立）中的裝置ID之間的衝突)

