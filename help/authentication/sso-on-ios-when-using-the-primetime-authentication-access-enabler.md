---
title: iOS上使用黃金時段身份驗證Access Enabler時的SSO
description: iOS上使用黃金時段身份驗證Access Enabler時的SSO
exl-id: 882f0abb-2e6e-461d-a375-3ab410991935
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# iOS上使用黃金時段身份驗證Access Enabler時的SSO {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 概述

基於黃金時段身份驗證的應用程式之間的單一登錄(SSO)工作方式不同，具體取決於底層作業系統。

此文檔地址 **iOS**，使用Adobe Primetime身份驗證時 **訪問啟用碼**。

**訪問啟用碼** **1.10** 是Adobe Primetime身份驗證iOS本機SDK的最新版本。 Adobe強烈建議您轉到此版本，而不是保留舊版本。 如果您使用的是Access Enabler的較舊版本，則可以下載最新版本 [這裡](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library)。

iOS上的SSO由以下條件規定：

- 應用必須使用相同 **令牌儲存** （以Access Enabler建立的自定義貼上板的形式）。
- 應用必須生成相同的 **設備ID** (Access Enabler根據MAC地址或IDFV計算設備ID，具體取決於作業系統版本)。

## 行為

SSO行為如下：

- **iOS6號及以下**:SSO在由同一團隊或不同團隊開發的應用程式之間自動工作。 設備ID是根據MAC地址計算的（所有應用中都產生相同的值），並且儲存區域是所有應用的公用區域(自定義貼上板可在iOS6和更低版本的應用之間共用)。
   - **重要提示：** 請注意，iOSSDK 1.9.4版 [將iOS的最低部署目標提高到iOS7](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS7號及以上**:SSO將在以下條件下工作：

1. 應用使用同一Apple分發配置檔案或屬於同一團隊的配置檔案發佈。 這是應用共用iOS7及更高版本定制貼上板的唯一方式。 在所有其他情況下，貼上板會按應用程式沙盒。 從 [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html):\+\[UIPasteboard pasteboardWithName:create:\]和+\[UIPasteboard貼上板WithUniqueName\]現在使給定名稱唯一，只允許同一應用程式組中的那些應用程式訪問貼上板。 如果開發人員嘗試使用已存在的名稱建立貼上板，並且他們不是同一應用套件的一部分，他們將獲得自己獨特的專用貼上板。 請注意，這不會影響系統提供的貼上板、常規和查找。

1. 應用具有相同的捆綁包ID前置詞（除最後一個元件外的所有元件）。 只有共用相同捆綁包ID前置詞的應用程式才會計算相同的IDFV。 從 [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#/apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor):在IOS7上，捆綁包的所有元件（最後一個元件除外）都用於生成供應商ID。 如果束ID僅具有單個元件，則使用整個束ID。

現在，我們來關注 **「iOS7及更高版本」** 場景，因為它是真正用戶最頻繁的：

這兩種條件（共用同一開發團隊的配置檔案並具有公共捆綁標識符前置詞）都是SSO的必需條件。

以下是可能的組合及其產生的結果：

- **來自同一組和同一捆綁ID前置詞的配置檔案**:應用將共用相同的貼上板儲存，並將具有相同的設備ID(IDFV)。 用戶只需驗證一次（在使用的第一個應用中），驗證狀態將在所有其他應用之間共用。 示例流：

1. 用戶開啟應用A（帶捆綁ID） *com.x.y.AppA*)和未驗證
1. 用戶在應用A中執行身份驗證
1. 用戶開啟應用B（帶捆綁ID） *com.x.y.AppB*)，並通過共用應用A的權利資料（從步驟2）自動驗證
1. 用戶開啟應用A並仍經過身份驗證（從步驟2）

 

- **來自同一組但不同捆綁ID前置詞的配置檔案**:應用將共用相同的貼上板儲存，但將具有不同的設備ID(IDFV)。 用戶需要對每個應用進行一次身份驗證。 示例流：

1. 用戶開啟應用A（帶捆綁ID） *com.x.y.AppA*)和未驗證
1. 用戶在應用A中執行身份驗證
1. 用戶開啟應用B（帶捆綁ID） *com.z.AppB*)和Access Enabler檢測由第一個應用獲取的令牌（因為儲存是共用的），但由於設備ID不同，它不會嘗試通過SSO使用它
1. 用戶在應用B中執行身份驗證
1. 用戶開啟應用A並仍經過身份驗證（從步驟2）

 

- **來自不同團隊的配置檔案（此方案中捆綁包ID不相關）**:應用程式將具有不同的貼上板儲存，並且它們之間將禁用SSO。 用戶需要對每個應用進行一次身份驗證，並且在應用之間切換時，身份驗證會話將保持持久性。 示例流：


1. 用戶開啟應用A並未通過身份驗證
1. 用戶在應用A中執行身份驗證
1. 用戶開啟應用B並未通過身份驗證
1. 用戶在應用B中執行身份驗證
1. 用戶開啟應用A並經過身份驗證（從步驟2）
1. 用戶開啟應用B並進行身份驗證（從步驟4）

**注：** 請注意，在通過 **AppleApp Store**。 如果應用部署在模擬器上（其中應用簽名不適用），安裝時使用Xcode或通過點對點配置檔案分發，則可能會得到不同的結果。

**重要提示：** 附註(**關於AccessEnabler v1.8**):上述第二個方案（來自同一團隊但不同捆綁ID前置詞的配置檔案）將為該團隊的用戶帶來非常不愉快的用戶體驗 **AccessEnabler v1.8** 跨由同一團隊（媒體公司）開發的應用程式。 在同一媒體公司的應用程式之間轉換時，用戶將自動註銷，因此，在確定捆綁包ID和分發配置檔案時，應用程式開發人員必須小心。 本例中的確切情形如下：

應用將共用相同的貼上板儲存，但將具有不同的設備ID(IDFV)。 用戶需要對每個應用進行一次身份驗證， **但在應用之間切換時，身份驗證會話將被清除**。 示例流：

1. 用戶開啟應用A（帶捆綁ID） *com.x.y.AppA*)和未驗證
1. 用戶在應用A中執行身份驗證
1. 用戶開啟應用B（帶捆綁ID） *com.z.AppB*)，應用A建立的權利資料由Access Enabler自動擦除（安全機制可檢測應用B中當前計算的設備ID與應用A建立的權利令牌中儲存的設備ID之間的衝突）
1. 用戶在應用B中執行身份驗證
1. 用戶開啟應用A，由應用B建立的權利資料由Access Enabler自動擦除（安全機制可檢測應用A中當前計算的設備ID與應用B建立的權利令牌中儲存的設備ID之間的衝突）
