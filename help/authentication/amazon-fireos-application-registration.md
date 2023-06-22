---
title: Amazon FireOS應用程式註冊
description: Amazon FireOS應用程式註冊
exl-id: 650fd4a2-dfc3-4c74-9b5b-6bea832a28ca
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Amazon FireOS應用程式註冊 {#amazon-fireos-application-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 簡介 {#intro}

從FireOS AccessEnabler SDK 3.0版開始，我們將透過Adobe的伺服器變更驗證機制。 我們不使用公開金鑰和秘密系統來簽署requestorID，而是引入軟體陳述式字串的概念，該字串可用來取得存取權杖，該權杖稍後會用於SDK對我們的伺服器進行的所有呼叫。 除了軟體宣告之外，您還需要為應用程式建立深層連結。

如需詳細資訊，請參閱 [動態使用者端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體宣告？ {#what}

軟體陳述式是包含應用程式相關資訊的JWT權杖。 每個應用程式都應該有專屬的軟體宣告，我們的伺服器會使用它來識別Adobe系統中的應用程式。 當您初始化AccessEnabler SDK時，需要傳遞軟體陳述式，並將用來註冊具有Adobe的應用程式。 註冊後，SDK會收到使用者端ID和使用者端密碼，此密碼將用於取得存取權杖。 SDK對伺服器發出的任何呼叫都需要有效的存取Token。 SDK負責註冊應用程式、取得和重新整理存取權杖。

**注意：** 軟體陳述式是應用程式專屬的，個別軟體陳述式不能用於多個應用程式。 請注意，這也適用於提供多個管道存取權的應用程式。

## 如何取得軟體宣告？ {#how-to}

### 如果您有AdobeTVE儀表板的存取權：

- 開啟瀏覽器並導覽至 <https://console.auth.adobe.com>
- 導覽至 `Channels` 區段並選取您的頻道。
- 導覽至 `Registered Applications` 標籤。
- 按一下 `Add new application`.
- 提供應用程式的名稱和版本，並選取可使用它的平台（例如我們案例中的Android）。
- 從已為程式設計師設定的網域清單中選擇，以提供網域名稱。
- 將變更推播至伺服器，然後導覽回您管道的「已註冊的應用程式」標籤。
- 您應該會看到包含所有已註冊應用程式的清單。 按一下 `Download` 按鈕。 注意：您可能需要等待幾分鐘，軟體陳述式才可供下載。
- 將會下載文字檔。 將其內容當做您的軟體宣告使用。

如需詳細資訊，請參閱 [Dynamic Client註冊管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您沒有AdobeTVE儀表板的存取權：

將票證提交至 <tve-support@adobe.com>. 請包含所有必要資訊，包括頻道、應用程式名稱、版本和平台，我們的支援團隊會有人為您建立軟體宣告。

## 如何使用軟體宣告？ {#use}

取得軟體陳述式後，您需要在Access Enabler建構函式中將其當作引數傳遞。 我們建議將軟體宣告託管於遠端位置。 如此一來，您就可以輕鬆地撤銷和變更「軟體陳述式」，而不需發行新版的應用程式。

## 如何使用軟體宣告 {#use-both}

在應用程式的資源檔案中 `strings.xml` 新增下列程式碼：

```XML
<string name="software_statement">softwarestatement value</string>
```
