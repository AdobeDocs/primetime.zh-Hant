---
description: 要實施DRM，您需要特定的證書和密鑰，包括內容加密密鑰或CEK以加密您的內容，需要用於保護與ExpressPlay伺服器通信的客戶驗證器，以及用於識別儲存在密鑰管理系統中的內容加密密鑰的CEKSID。
title: 密鑰、ID和身份驗證器
exl-id: b769192d-92ad-4b93-84dd-80b182fc6c43
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 密鑰、ID和身份驗證器{#keys-ids-and-authenticators}

要實施DRM，您需要特定的證書和密鑰，包括內容加密密鑰或CEK以加密您的內容，需要用於保護與ExpressPlay伺服器通信的客戶驗證器，以及用於識別儲存在密鑰管理系統中的內容加密密鑰的CEKSID。

您需要這些項目來打包、許可和播放受保護的內容：

## 內容加密密鑰 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

內容加密密鑰(CEK)是用於加密內容的16位元組字串。

**CEK是什麼？** - CEK是打包員用於加密內容的密鑰。 是16位元組的十六進位編碼字串。

**CEK從何而來？**  — 您（內容提供商）使用OpenSSL或Notepad++等工具自行建立此密鑰。 例如：

```
openssl rand 16 -hex > cek_hex_file
```

或(用於Adobe離線打包程式):

1. 生成16位元組的十六進位編碼字串，如上所示或使用其他工具。 它會是這樣的：

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 開啟記事本++並貼上到16位元組的十六進位字串中。
1. 將此值從十六進位ASCII轉換為Base64編碼，以建立 [!DNL keyfile.bin]。 (此部分包含於 [](../../multi-drm-workflows/quick-start/package-your-content.md)。)

**相同的鑰匙，不同的名字？**  — 是的，您可能會在其他位置看到其他名稱所引用的CEK，例如：

* ** [!DNL [某個檔案].bin]** -Adobe離線打包程式將CEK引用為[!DNL [某個檔案].bin;例如，* [!DNL Keyfile.bin]* — 這是Adobe離線打包程式使用的CEK，形式為您用於打包內容的電腦上的檔案。

   您「Base64」您的隨機CEK十六進位字串，並將其另存為檔案(例如， [!DNL keyfile.bin])，通常位於 [!DNL creds] 目錄下 [!DNL offlinepkgr/]。 在Packager配置檔案中(例如，您可以將其調用 [!DNL widevine.xml] 如果要為Widevine DRM打包)，則在配置檔案中將CEK引用如下：

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **內容密鑰**  — 在呼叫中，您還可能看到稱為內容鍵的CEK( `&contentKey=`)、錯誤消息、支援票證以及其他文檔中。

**何時/何處使用它？**

1. 首先，您需要在進行打包的電腦上提供CEK。 您的打包工具使用CEK來加密您的內容。
1. 其次，您需要將CEK儲存在某種形式的密鑰管理系統(KMS)中，每個CEK都與其自己的CEK關聯 [內容加密密鑰](../../multi-drm-workflows/glossary/glossary-cek.md)。 您可以建立自己的KMS或使用 [ExpressPlay的密鑰儲存](https://www.expressplay.com/developer/key-storage/)。 這樣，您的店面（處理客戶權利和許可證令牌設定的授權伺服器）就可以使用密鑰ID而不是實際CEK從KMS中為客戶提取許可證令牌（這更加安全）。

## 內容加密密鑰儲存ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

內容加密密鑰儲存ID(CEKSID)唯一地標識對加密的視頻內容段進行解密的儲存密鑰。

**CEKSID是什麼？** - CEKSID是內容加密密鑰(CEK)的唯一標識符。 CEK是解鎖受保護內容所必需的；CEKSID是從儲存CEK的位置訪問CEK所必需的。 在測試安裝程式時，只要在許可和回放檢查中使用相同的資訊，就可以在打包時提供隨機CEKSID和CEK。

**從哪來的？**  — 您（內容提供商）可以自己建立此ID，或者您可以使用服務，如 [ExpressPlay的密鑰儲存](https://www.expressplay.com/developer/key-storage/) 為每個CEK生成CEKSID（並儲存兩個CEKSID）。 此外，您可以使用隨機生成的CEKSID，或使用適合您的業務模型的方案。 例如，您可以使用CEKSID，這些CEKSID是有意義的字串，而不是隨機的十六進位字串（ID名稱可能由主題、日期、時間等組成）

**CEKSID還叫什麼？**  — 有時稱為 *內容ID*。

## 客戶驗證器 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

在ExpressPlay中設定管理員帳戶時，客戶驗證器是您從中獲得的密鑰。 驗證器用於與ExpressPlay伺服器的通信。

**什麼是客戶身份驗證器？**  — 兩個客戶身份驗證器組成一對ID，一個用於測試，一個用於生產，ExpressPlay在您註冊服務時為您註冊。 在ExpressPlay管理頁上，您始終可以使用它們：
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**我什麼時候用這個？**  — 將此內容包括在所有對ExpressPlay伺服器的調用中 — 例如，許可證伺服器、 [ExpressPlay密鑰儲存](https://www.expressplay.com/developer/key-storage/)和其他呼叫。
