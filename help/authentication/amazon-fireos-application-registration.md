---
title: AmazonFireOS應用程式註冊
description: AmazonFireOS應用程式註冊
exl-id: 650fd4a2-dfc3-4c74-9b5b-6bea832a28ca
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# AmazonFireOS應用程式註冊 {#amazon-fireos-application-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#intro}

從FireOS AccessEnabler SDK的3.0版開始，我們正在更改Adobe伺服器的身份驗證機制。 我們不使用公鑰和密碼系統來簽名請求者ID ，而是引入了「軟體語句」字串的概念，該字串可用於獲取訪問令牌，該令牌稍後用於SDK對我們的伺服器進行的所有調用。 除了軟體語句外，您還需要為應用程式建立深度連結。

詳細資訊，請參閱 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#what}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體聲明，供我們的伺服器用來識別Adobe系統中的應用程式。 初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於使用Adobe註冊應用程式。 註冊後，SDK將接收一個客戶端ID和一個客戶端密鑰，用於獲取訪問令牌。 SDK對我們的伺服器進行的任何調用都需要有效的訪問令牌。 SDK負責註冊應用程式、獲取和刷新訪問令牌。

**注：** 軟體語句是特定於應用程式的，單個軟體語句不能用於多個應用程式。 請注意，這同樣適用於提供訪問多個渠道的應用程式。

## 如何獲取軟體聲明？ {#how-to}

### 如果您有權訪問Adobe的TVE儀表板：

- 開啟瀏覽器並導航到 <https://console.auth.adobe.com>
- 導航到 `Channels` 的子菜單。
- 導航到 `Registered Applications` 頁籤。
- 按一下 `Add new application`。
- 為應用程式提供名稱和版本，並選擇可用的平台(如 Android是我們的例子)。
- 通過從已為程式設計師配置的域清單中選擇來提供域名。
- 將更改推送到伺服器，然後導航回通道的「已註冊的應用程式」頁籤。
- 您應看到包含所有註冊應用程式的清單。 按一下 `Download` 按鈕。 注：您可能需要等待幾分鐘，才能準備好下載軟體語句。
- 將下載文本檔案。 將其內容用作軟體聲明。

詳細資訊，請參閱 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您沒有訪問Adobe的TVE儀表板的權限：

將票證提交到 <tve-support@adobe.com>。 請包括所有必要資訊，包括渠道、應用程式名稱、版本和平台，我們支援團隊的人員將為您建立軟體聲明。

## 如何使用軟體聲明？ {#use}

獲取軟體語句後，您需要將其作為Access Enabler建構子中的參數傳遞。 我們建議在遠程位置托管軟體語句。 這樣，您就可以輕鬆地撤消和更改軟體語句，而無需釋放新版本的應用程式。

## 如何使用軟體語句 {#use-both}

在應用程式的資源檔案中 `strings.xml` 添加以下代碼：

```XML
<string name="software_statement">softwarestatement value</string>
```
