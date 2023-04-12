---
title: iOS/tvOS應用程式註冊
description: iOS/tvOS應用程式註冊
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# iOS/tvOS應用程式註冊 {#iostvos-application-registration}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#Intro}

從iOS/tvOS AccessEnabler SDK的3.0版開始，我們將更改Adobe伺服器的驗證機制。 我們推出的概念為軟體陳述式字串，可用來取得存取權杖，供SDK對伺服器發出的所有呼叫之後使用，而非使用公開金鑰和密碼系統來簽署requestorID。 除了軟體陳述式外，您還需要為應用程式設定自訂URL配置。

如需詳細資訊，請參閱 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)

## 什麼是軟體聲明？ {#Soft_state}

軟體語句是JWT令牌，包含有關應用程式的資訊。 每個應用程式都應有一個唯一的軟體語句，供我們的伺服器用來標識Adobe系統中的應用程式。 在初始化AccessEnabler SDK時需要傳遞軟體語句，該語句將用於註冊具有Adobe的應用程式。 註冊後，SDK會收到用於取得存取權杖的用戶端ID和用戶端密碼。 SDK對伺服器進行的任何呼叫都需要有效的存取權杖。 SDK負責註冊應用程式、取得及重新整理存取權杖。

**注意：** 軟體語句是應用程式專用的，並且同一個軟體語句不能用於多個應用程式。 請注意，程式設計師級軟體語句也遵循同樣的規則，即它們只能用於單個應用程式，無論是單通道還是多通道。 此限制也適用於自訂配置。

## 如何獲取軟體聲明？ {#obtain}

### 如果您可以存取Adobe的TVE控制面板：

- 開啟瀏覽器並導覽至 <https://console.auth.adobe.com>
- 導覽至 `Channels` 區段，然後選取您的頻道。
- 導覽至 `Registered Applications` 標籤。
- 按一下 `Add new application`.
- 提供應用程式的名稱和版本，並選取可用的平台。 iOS/tvOS。
- 推送您的變更至伺服器，然後導覽回管道的「已註冊應用程式」標籤。
- 您應該會看到一個包含所有已註冊應用程式的清單。 按一下   `Download` 按鈕（位於您剛建立的應用程式上）。 您可能需要等待幾分鐘，才能準備好下載軟體陳述式。
- 將下載文本檔案。 將其內容用作軟體聲明。

如需詳細資訊，請參閱 [動態客戶端註冊管理](/help/authentication/dynamic-client-registration-management.md).

### 如果您無權訪問Adobe的TVE儀表板：

將票證提交至 <tve-support@adobe.com>. 請包括所有必要的資訊，如通道、應用程式名稱、版本和平台，我們的支援團隊將為您建立軟體聲明。

## 如何使用軟體聲明？ {#use}

獲取軟體陳述式後，您需要將其作為參數傳入Access Enabler建構子中。 建議將軟體陳述式托管在遠程位置。 這樣，您就可以輕鬆撤銷和更改軟體陳述式，而不發佈新版本的應用程式。

## 為您的應用程式產生自訂URL配置 {#generating}

### 如果您可以存取Adobe的TVE控制面板：

- 開啟瀏覽器並導覽至 <https://console.auth.adobe.com>
- 導覽至 `Channels` 區段，然後選取您的頻道。
- 導覽至 `Custom Schemes` 標籤。
- 按一下 `Generate a new custom scheme`.
- 將為您的應用程式產生新的自訂配置。 例如： `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- 推送您的變更至伺服器。

### 如果您無權訪問Adobe的TVE儀表板：

將票證提交至 <tve-support@adobe.com>. 請加入管道id，我們支援團隊的人員會為您建立自訂配置。

## 如何使用自訂配置 {#use_custom}

在應用程式的 `info.plist` 檔案新增下列程式碼：

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
