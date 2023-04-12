---
title: Amazon FireOS應用程式註冊
description: Amazon FireOS應用程式註冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Amazon FireOS應用程式註冊 {#amazon-fireos-application-registration}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 簡介 {#intro}

從3.0版的FireOS AccessEnabler SDK開始，我們將更改Adobe伺服器的身份驗證機制。 我們推出的概念為「軟體陳述式」字串，可用來取得存取權杖，此權杖稍後會用於SDK對我們伺服器發出的所有呼叫，而非使用公開金鑰和密碼系統來簽署requestorID。 除了軟體陳述式外，您還需要為應用程式建立深層連結。

如需詳細資訊，請參閱 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#what}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體陳述式，供我們的伺服器用來標識Adobe系統中的應用程式。 在初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於註冊具有Adobe的應用程式。 註冊後，SDK會收到用於取得存取權杖的用戶端ID和用戶端密碼。 SDK對伺服器進行的任何呼叫都需要有效的存取權杖。 SDK負責註冊應用程式、取得及重新整理存取權杖。

**注意：** 軟體語句是應用程式專用的，並且單個軟體語句不能用於多個應用程式。 請注意，這也適用於提供多個通道存取權的應用程式。

## 如何獲取軟體聲明？ {#how-to}

### 如果您可以存取Adobe的TVE控制面板：

- 開啟瀏覽器並導覽至 <https://console.auth.adobe.com>
- 導覽至 `Channels` 區段，然後選取您的頻道。
- 導覽至 `Registered Applications` 標籤。
- 按一下 `Add new application`.
- 提供應用程式的名稱和版本，並選取將可用它的平台（例如，在本例中為Android）。
- 通過從已為程式設計師配置的域清單中選擇提供域名。
- 推送您的變更至伺服器，然後導覽回您頻道的「已註冊應用程式」標籤。
- 您應該會看到包含所有已註冊應用程式的清單。 按一下 `Download` 按鈕（位於您剛建立的應用程式上）。 注意：您可能需要等待幾分鐘，才能準備好下載軟體陳述式。
- 將下載文本檔案。 將其內容用作軟體聲明。

如需詳細資訊，請參閱 [Dynamic Client註冊管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您無權訪問Adobe的TVE儀表板：

將票證提交至 <tve-support@adobe.com>. 請包括所有必要的資訊，包括渠道、應用程式名稱、版本和平台，我們的支援團隊將為您建立軟體聲明。

## 如何使用軟體聲明？ {#use}

獲取軟體陳述式後，您需要將其作為參數傳入Access Enabler建構子中。 建議將軟體陳述式托管在遠程位置。 這樣，您就可以輕鬆地撤銷和更改軟體陳述式，而無需發佈新版本的應用程式。

## 如何使用軟體陳述式 {#use-both}

在應用程式的資源檔案中 `strings.xml` 新增下列程式碼：

```XML
<string name="software_statement">softwarestatement value</string>
```
