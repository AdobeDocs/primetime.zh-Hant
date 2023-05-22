---
title: Android應用程式註冊
description: Android應用程式註冊
exl-id: 6238bd87-ac97-4a5c-9d92-3631f7b2d46a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# Android應用程式註冊 {#android-application-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#intro}

從Android AccessEnabler SDK的3.0版開始，我們正在更改Adobe伺服器的身份驗證機制。 我們不使用公鑰和密碼系統來簽名請求者ID ，而是引入了Software語句字串的概念，該字串可用於獲取訪問令牌，該令牌稍後用於SDK對我們的伺服器進行的所有調用。 除軟體語句外，您還需要為應用程式建立深度連結。

有關詳細資訊，請參見 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#what}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體語句，供我們的伺服器用來識別Adobe系統中的應用程式。 初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於使用Adobe註冊應用程式。 註冊後，SDK將接收一個客戶端ID和一個客戶端密鑰，用於獲取訪問令牌。 SDK對我們的伺服器進行的任何調用都需要有效的訪問令牌。 SDK負責註冊應用程式、獲取和刷新訪問令牌。

>[!NOTE]
>
>軟體語句是特定於應用程式的，單個軟體語句不能用於多個應用程式。 請注意，程式設計師級軟體語句具有相同的約束條件，它們只能用於單個應用程式，無論是單通道還是多通道。

## 如何獲取軟體聲明？ {#how-to-get-ss}

### 如果您有權訪問Adobe的TVE儀表板：

* 開啟瀏覽器並導航到 [Adobe PrimetimeTVE儀表板](https://console.auth.adobe.com)。
* 導航到 `Channels` 的子菜單。
* 導航到 `Registered Applications` 頁籤。
* 按一下 `Add new application`。
* 為應用程式提供名稱和版本，並選擇可用的平台。 安卓。
* 通過從已為程式設計師配置的域清單中選擇來提供域名。
* 將更改推送到伺服器，然後導航回通道的「已註冊的應用程式」頁籤。
* 您應看到包含所有註冊應用程式的清單。 選擇 **下載** 按鈕。 您可能需要等待幾分鐘，才能下載軟體聲明。
* 將下載文本檔案。 將其內容用作軟體聲明。

有關詳細資訊，請參見 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md)

### 如果您沒有訪問Adobe的TVE儀表板的權限：

將票證提交到 `tve-support@adobe.com`。 請包括所有必要的資訊，如渠道、應用程式名稱、版本和平台，我們支援團隊的人員將為您建立軟體聲明。

## 如何使用軟體聲明？ {#how-to-use-ss}

獲取軟體語句後，您需要將其作為Access Enabler建構子中的參數傳遞。 我們建議在遠程位置托管軟體語句。 這樣，您就可以輕鬆撤消和更改軟體語句，而不會發佈新版本的應用程式。

## 為應用程式建立和使用深度連結 {#create}

在Android上，將建立軟體語句時選擇的域名的反向作為深連結值

建立的深層連結在Android設備上應具有唯一值。 當多個應用程式使用相同的深連結值時，驗證和註銷流將會干擾。

## 如何使用軟體語句和深層連結 {#use-both}

在應用程式的資源檔案中 `strings.xml` 添加以下代碼：

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```
