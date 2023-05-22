---
title: 重置臨時傳遞iOS
description: 重置臨時傳遞iOS
exl-id: 53a22fae-192c-4b4c-9d63-fd9a2d960923
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# 重置臨時傳遞iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

iOS演示應用包括用於重置臨時通過TTL的專用螢幕。 重置操作需要以下資訊：

- **環境：** 指定將接收重置Temp Pass網路呼叫的Adobe付費電視通過伺服器終結點。 可能的值： **普雷誇爾** (*mgmt-prequal.auth-staging.adobe.com*) **發佈** (*mgmt.auth.adobe.com*)或 **自定義** (保留用於Adobe內部測試)。
- **OAuth2持有者令牌：** OAuth2令牌是授權程式設計師進行Adobe付費電視身份驗證的必要條件。 這樣的令牌可以從專用的付費電視認證OAuth2端點獲得(例如， *捲曲 — u &quot;\&lt;consumer _key=&quot;&quot;>:\&lt;consumer _secret=&quot;&quot; _key=&quot;&quot;>*&quot; *&quot;https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials&quot;*)。
- **請求者ID:** 當前程式設計師的唯一ID。 此值從演示應用的主螢幕（請求者欄位）中讀取。
- **臨時通過ID:** 臨時傳遞MVPD的唯一ID。
- **設備ID:** 已散列由演示應用計算的設備ID。
- **一般密鑰：** 某些臨時傳遞MVPD（即下一個可擴展的臨時傳遞功能）支援用於重置臨時傳遞的泛型鍵（與設備ID一起）。

以上所有參數( *泛型鍵*)是必填項。 下面是演示應用程式將執行的參數和關聯網路調用的示例（該示例以*curl *command的形式顯示）:

- **環境：** 發佈(*mgmt.auth.adobe.com*)
- **OAuth2持有者令牌：** H4j7cF3GtJX81BrsgDa10GwSizVz
- **程式設計師ID:** 參考
- **臨時通過ID:** 臨時通過REF
- **設備ID:** f23804a37802993fdc8e28a7f244dfe088b6a9ea214577728e6731fa69991 
- **一般密鑰：** 空（未提供值）

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

DELETEHTTP請求將發送給 **/reset** 端點，傳遞 *OAuth2持有者令牌* 和 *設備ID*。 *請求者ID* 和 *臨時傳遞ID(MVPD ID)* 作為參數。

如果程式設計師為 *泛型鍵*，將執行另一個HTTP調用(此次 **/reset/generic** 端點)，傳遞 *泛型鍵* 內 *鍵* 請求參數。

例如，設定 *泛型鍵* 到電子郵件地址哈希（對於支援此類功能的臨時傳遞MVPD）將生成以下HTTP調用(電子郵件為 `user@domain.com` 其SHA-256哈希為 `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

必須強調，在演示應用中重置Temp Pass對同一設備上的程式設計師應用可能沒有相同效果。 這是由於設備ID（由演示應用和AccessEnabler計算）對於設備上的所有應用程式可能不相同：

- iOS6及以下：設備ID是使用MAC地址計算的（所有應用都唯一），因此在演示應用中重置臨時通道將在設備上的所有其他程式設計師應用程式中重置它。

- iOS7及上：設備ID是基於IDFV（供應商的ID）值計算的，該值對於具有相同捆綁ID前置詞（即除最後一個元件外的所有元件）的所有應用程式都是唯一的。 由於演示應用和程式設計師應用具有不同的捆綁ID，因此在演示應用中重置臨時通行證不會對程式設計師應用產生任何影響。

最後一個用例(iOS7和更高版本)是最常見的，因此，讓我們看看程式設計師在這種情況下如何為其應用程式重置臨時通行證。 有幾種選擇：

1. 將代碼從演示應用程式埠到程式設計師應用程式。 的 *TempPassResetViewController* 和 *設備IdDemoApp* 類包含用於重置Temp Pass的核心邏輯，並且可以輕鬆修改這些邏輯並將其包含在程式設計師應用程式中。

1. 執行HTTP請求以重置臨時傳遞 *捲曲*。 通過計算程式設計師應用程式的IDFV並在其上應用SHA-256散列(示例代碼在 *設備IdDemoApp* 類)。

1. 只需將程式設計師應用的散列IDFV指定為 *泛型鍵*。 這將導致兩個網路呼叫：一個用於為演示應用程式重置Temp Pass（與程式設計師無關），另一個用於為程式設計師應用程式重置Temp Pass。

以上所有選項都類似，程式設計師需要根據實施的容易程度來選擇。
