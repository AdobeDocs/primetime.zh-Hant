---
title: Android應用程式註冊
description: Android應用程式註冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---



# Android應用程式註冊 {#android-application-registration}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

從3.0版的Android AccessEnabler SDK開始，我們將更改Adobe伺服器的驗證機制。 我們推出的概念為軟體陳述式字串，可用來取得存取權杖，供SDK對伺服器發出的所有呼叫之後使用，而非使用公開金鑰和密碼系統來簽署requestorID。 除了軟體陳述式外，您還需要為應用程式建立深層連結。

如需詳細資訊，請參閱 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#what}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體語句，供我們的伺服器用來標識Adobe系統中的應用程式。 在初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於註冊具有Adobe的應用程式。 註冊後，SDK會收到用於取得存取權杖的用戶端ID和用戶端密碼。 SDK對伺服器進行的任何呼叫都需要有效的存取權杖。 SDK負責註冊應用程式、取得及重新整理存取權杖。

>[!NOTE]
>
>軟體語句是應用程式專用的，並且單個軟體語句不能用於多個應用程式。 請注意，程式設計師級軟體語句具有相同的約束，它們只能用於單個應用程式，無論是單通道還是多通道。

## 如何獲取軟體聲明？ {#how-to-get-ss}

### 如果您可以存取Adobe的TVE控制面板：

* 開啟瀏覽器並導覽至 [Adobe Primetime TVE儀表板](https://console.auth.adobe.com).
* 導覽至 `Channels` 區段，然後選取您的頻道。
* 導覽至 `Registered Applications` 標籤。
* 按一下 `Add new application`.
* 提供應用程式的名稱和版本，並選取可用的平台。 在我們的案例中是Android。
* 通過從已為程式設計師配置的域清單中選擇提供域名。
* 推送您的變更至伺服器，然後導覽回您頻道的「已註冊應用程式」標籤。
* 您應該會看到包含所有已註冊應用程式的清單。 選取 **下載** 按鈕（位於您剛建立的應用程式上）。 您可能需要等待幾分鐘，才能準備好下載軟體陳述式。
* 將下載文本檔案。 將其內容用作軟體聲明。

如需詳細資訊，請參閱 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您無權訪問Adobe的TVE儀表板：

將票證提交至 `tve-support@adobe.com`. 請包括所有必要資訊，如通道、應用程式名稱、版本和平台，我們支援團隊的人員將為您建立軟體聲明。

## 如何使用軟體聲明？ {#how-to-use-ss}

獲取軟體陳述式後，您需要將其作為參數傳入Access Enabler建構子中。 建議將軟體陳述式托管在遠程位置。 這樣，您就可以輕鬆撤銷和更改軟體陳述式，而不發佈新版本的應用程式。

## 為您的應用程式建立並使用深層連結 {#create}

在Android上，使用作為深層連結值，即建立軟體陳述式時選取之網域名稱的反面

建立的深層連結在Android裝置上應有唯一值。 當多個應用程式使用相同的深層連結值時，驗證和登出流程會干擾。

## 如何使用軟體陳述式和深層連結 {#use-both}

在應用程式的資源檔案中 `strings.xml` 新增下列程式碼：

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```

