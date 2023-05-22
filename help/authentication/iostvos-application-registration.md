---
title: iOS/tvOS應用程式註冊
description: iOS/tvOS應用程式註冊
exl-id: 89ee6b5a-29fa-4396-bfc8-7651aa3d6826
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# iOS/tvOS應用程式註冊 {#iostvos-application-registration}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#Intro}

從iOS/tvOS AccessEnabler SDK的3.0版開始，我們正在更改Adobe伺服器的身份驗證機制。 我們不使用公鑰和密碼系統來簽名請求者ID ，而是引入了Software語句字串的概念，該字串可用於獲取訪問令牌，該令牌稍後用於SDK對我們的伺服器進行的所有調用。 除了軟體語句外，您還需要應用程式的自定義URL方案。

有關詳細資訊，請參見 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#Soft_state}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體語句，供我們的伺服器用來識別Adobe系統中的應用程式。 初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於使用Adobe註冊應用程式。 註冊後，SDK將接收一個客戶端ID和一個客戶端密鑰，用於獲取訪問令牌。 SDK對我們的伺服器進行的任何調用都需要有效的訪問令牌。 SDK負責註冊應用程式、獲取和刷新訪問令牌。

**注：** 軟體語句是特定於應用程式的，同一軟體語句不能用於多個應用程式。 請注意，程式設計師級軟體語句也遵循相同的語句，即它們只能用於單個應用程式 — 無論是單通道還是多通道。 此限制也適用於自定義方案。

## 如何獲取軟體聲明？ {#obtain}

### 如果您有權訪問Adobe的TVE儀表板：

- 開啟瀏覽器並導航到 <https://console.auth.adobe.com>
- 導航到 `Channels` 的子菜單。
- 導航到 `Registered Applications` 頁籤。
- 按一下 `Add new application`。
- 為應用程式提供名稱和版本，並選擇可用的平台。 iOS/電視作業系統。
- 將更改推送到伺服器，然後導航回渠道的「已註冊的應用程式」頁籤。
- 您應看到所有已註冊應用程式的清單。 按一下   `Download` 按鈕。 您可能需要等待幾分鐘，才能下載軟體聲明。
- 將下載文本檔案。 將其內容用作軟體聲明。

有關詳細資訊，請參閱 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md)。

### 如果您沒有訪問Adobe的TVE儀表板的權限：

將票證提交到 <tve-support@adobe.com>。 請包括所有必要資訊，如渠道、應用程式名稱、版本和平台，我們支援團隊的人員將為您建立軟體聲明。

## 如何使用軟體聲明？ {#use}

獲取軟體語句後，您需要將其作為Access Enabler建構子中的參數傳遞。 我們建議在遠程位置托管軟體語句。 這樣，您就可以輕鬆撤消和更改軟體語句，而不會發佈新版本的應用程式。

## 為應用程式生成自定義URL方案 {#generating}

### 如果您有權訪問Adobe的TVE儀表板：

- 開啟瀏覽器並導航到 <https://console.auth.adobe.com>
- 導航到 `Channels` 的子菜單。
- 導航到 `Custom Schemes` 頁籤。
- 按一下 `Generate a new custom scheme`。
- 將為您的應用程式生成新的自定義方案。 例如： `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- 將更改推送到伺服器。

### 如果您沒有訪問Adobe的TVE儀表板的權限：

將票證提交到 <tve-support@adobe.com>。 請包括渠道ID，我們支援團隊的人員將為您建立自定義方案。

## 如何使用自定義方案 {#use_custom}

在您的應用程式中 `info.plist` 檔案添加以下代碼：

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
