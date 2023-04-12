---
title: 在iOS上重設Temp Pass
description: 在iOS上重設Temp Pass
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# 在iOS上重設Temp Pass {#reset-temp-pass-on-ios}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

iOS示範應用程式包含專用畫面，可重設臨時通過TTL。 重置操作需要以下資訊：

- **環境：** 指定將接收重設Temp Pass網路呼叫的Adobe付費電視通訊伺服器端點。 可能的值： **普雷誇爾** (*mgmt-prequal.auth-staging.adobe.com*), **發行** (*mgmt.auth.adobe.com*)或 **自訂** (保留供Adobe內部測試之用)。
- **OAuth2承載代號：** OAuth2令牌是授權程式設計師進行Adobe付費電視驗證所必需的。 從專用付費電視驗證OAuth2端點(例如， *curl -u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials&quot;*)。
- **請求者ID:** 當前程式設計師的唯一ID。 此值會從示範應用程式的主畫面（要求者欄位）讀取。
- **臨時傳遞ID:** 臨時傳遞MVPD的唯一ID。
- **裝置ID:** 由示範應用程式計算的雜湊裝置ID。
- **一般密鑰：** 某些Temp Pass MVPD（即下一個可擴充的Temp Pass功能）支援重設Temp Pass的一般金鑰（與裝置ID並列）。

上述所有參數( *一般金鑰*)是必填欄位。 以下是將由示範應用程式執行之參數與相關網路呼叫的範例（範例為*curl *命令的形式）:

- **環境：** 發行(*mgmt.auth.adobe.com*)
- **OAuth2承載代號：** H4j7cF3GtJX81BrsgDa10GwSizVz
- **程式設計師ID:** 參考
- **臨時傳遞ID:** TempPassREF
- **裝置ID:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991 
- **一般密鑰：** null（未提供值）

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

DELETEHTTP要求 **/reset** 端點，傳遞 *OAuth2承載代號* 在授權標題和 *裝置ID*, *請求者ID* 和 *臨時傳遞ID(MVPD ID)* 作為參數。

如果程式設計師為 *一般金鑰*，則會執行另一個HTTP呼叫(這次是 **/reset/generic** 端點)，傳遞 *一般金鑰* 內 *key* 要求參數。

例如，設定 *一般金鑰* 傳送至電子郵件地址雜湊（針對支援此類功能的Temp Pass MVPD）會產生下列HTTP呼叫(電子郵件為 `user@domain.com` 其SHA-256雜湊為 `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

必須強調的是，在演示應用程式中重置Temp Pass對同一設備上的程式設計師應用程式可能沒有相同的效果。 這是因為設備ID（由演示應用程式和AccessEnabler計算）可能與設備上的所有應用程式不同：

- iOS 6及以下版本：設備ID是使用MAC地址計算的（所有應用程式均不重複），因此在演示應用程式中重置Temp Pass將在設備上的所有其他程式設計師應用程式中重置它。

- iOS 7及以上版本：設備ID是根據IDFV（供應商的ID）值計算的，該值對於具有相同捆綁ID前置詞（即除最後一個元件外的所有元件）的所有應用程式來說都是唯一的。 由於演示應用和程式設計師應用具有不同的捆綁ID，因此在演示應用中重置Temp Pass對程式設計師應用沒有影響。

最後一個使用案例(iOS 7及更新版本)是最常見的案例，讓我們看看程式設計師如何在此情況下為其應用程式重設Temp Pass。 有數個選項：

1. 將代碼從演示應用程式移植到程式設計師應用程式。 此 *TempPassResetViewController* 和 *DeviceIdDemoApp* 類包含用於重置Temp Pass的核心邏輯，並可以輕鬆修改這些邏輯並包含在程式設計師應用程式中。

1. 執行HTTP要求以重設Temp Pass，具有 *捲曲*. 可透過計算程式設計人員應用程式的IDFV並套用SHA-256雜湊至該ID，來取得device\_Id參數(范常式式碼位於 *DeviceIdDemoApp* 類別)。

1. 只需將程式設計師應用程式的雜湊IDFV指定為 *一般金鑰*. 這會產生兩個網路呼叫：一個用於重置演示應用的Temp Pass（與程式設計師無關），另一個用於重置程式設計師應用的Temp Pass。

上述所有選項都相似，由程式設計師根據實施的簡便性選擇一個選項。 

