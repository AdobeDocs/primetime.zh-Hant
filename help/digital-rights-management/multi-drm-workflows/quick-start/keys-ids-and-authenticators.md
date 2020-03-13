---
description: 要實施DRM，您需要特定的憑證和金鑰，包括內容加密金鑰或CEK來加密您的內容、用於保護與ExpressPlay伺服器通信的客戶驗證器，以及用於識別儲存在密鑰管理系統中的內容加密密鑰的CEKSID。
seo-description: 要實施DRM，您需要特定的憑證和金鑰，包括內容加密金鑰或CEK來加密您的內容、用於保護與ExpressPlay伺服器通信的客戶驗證器，以及用於識別儲存在密鑰管理系統中的內容加密密鑰的CEKSID。
seo-title: 金鑰、ID和驗證器
title: 金鑰、ID和驗證器
uuid: 9e5b1a64-b4e9-442f-ac15-26831aaf585d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 金鑰、ID和驗證器{#keys-ids-and-authenticators}

要實施DRM，您需要特定的憑證和金鑰，包括內容加密金鑰或CEK來加密您的內容、用於保護與ExpressPlay伺服器通信的客戶驗證器，以及用於識別儲存在密鑰管理系統中的內容加密密鑰的CEKSID。

您需要以下項目來封裝、授權和播放您的受保護內容：

## 內容加密金鑰 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

內容加密金鑰(CEK)是用來加密內容的16位元組字串。

**什麼是CEK?** - CEK是您的封裝人員用來加密內容的金鑰。 這是16位元組的十六進位編碼字串。

**CEK從何而來？** -您（內容提供者）使用OpenSSL或Notepad++等工具自行建立此金鑰。 例如：

```
openssl rand 16 -hex > cek_hex_file
```

或（適用於Adobe Offline Packager）:

1. 產生16位元組的十六進位編碼字串，如上所述，或使用其他工具。 它看起來會像這樣：

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 開啟記事本++並貼入16位元組十六進位字串。
1. 使用Base64編碼將此值從十六進位ASCII轉換為值，以建立您的 [!DNL keyfile.bin]。 (本節內容包 [](../../multi-drm-workflows/quick-start/package-your-content.md)括。)

**相同的鑰匙，不同的名字？** -是的，您可能會在其他地方看到其他名稱所參照的CEK，例如：

* ** [!DNL [somefile].bin]** - Adobe Offline Packager將CEK稱為[!DNL [somefile].bin];例如* [!DNL Keyfile.bin]* —— 這是Adobe Offline Packager使用的CEK，以檔案形式呈現在您用來封裝內容的機器上。

   您「Base64」您的隨機CEK十六進位字串，並將它儲存為檔案(例如 [!DNL keyfile.bin])，通常位於下方 [!DNL creds] 的目錄中 [!DNL offlinepkgr/]。 在Packager配置檔案中(例如，如果您要為Widevine DRM打包 [!DNL widevine.xml] ，則可以調用它)，您在配置檔案中將CEK按如下方式參照：

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **內容金鑰** -您也可以在呼叫( `&contentKey=`)、錯誤訊息、支援票證和其他檔案中，看到稱為內容金鑰的CEK。

**何時／在何處使用？**

1. 首先，您需要在進行包裝的機器上提供CEK。 您的封裝工具會使用您的CEK來加密您的內容。
1. 其次，您需要以某種形式的密鑰管理系統(KMS)儲存CEK，每個CEK都與其自己的內容加密密鑰 [相關聯](../../multi-drm-workflows/glossary/glossary-cek.md)。 您可以建立自己的KMS，或使用 [ExpressPlay的密鑰儲存](https://www.expressplay.com/developer/key-storage/)。 這可讓您的店面（您的權益伺服器，負責處理客戶權益和授權Token布建）使用金鑰ID而非實際CEK從KMS中提取客戶的授權Token（這更安全）。

## 內容加密密鑰儲存ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

內容加密密鑰儲存ID(CEKSID)唯一地標識對加密的視頻內容解密的儲存密鑰。

**什麼是CEKSID?** - CEKSID是內容加密金鑰(CEK)的唯一識別碼。 CEK是解除鎖定受保護內容的必要工具；ceksid是存取儲存CEK的必要條件。 當您測試設定時，只要您使用相同的資訊進行授權和播放檢查，就可以在封裝時提供隨機的CEKSID和CEK。

**從哪來的？** -您（內容提供者）可以自行建立此ID，或者您可以使用 [ExpressPlay的金鑰儲存空間](https://www.expressplay.com/developer/key-storage/) ，為每個CEK產生CEKSID（並儲存這兩個CEK）。 此外，您還可以使用隨機產生的CEKSID，或採用符合您商業模型的方案。 例如，您可以使用有意義的字串而非隨機十六進位字串的CEKSID（ID名稱可能包含主體、日期、時間等）

**CEKSID還叫什麼？** -有時稱為內 *容ID*。

## 客戶驗證器 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

客戶驗證器是您在ExpressPlay中設定管理帳戶時，從ExpressPlay取得的金鑰。 驗證器用於與ExpressPlay伺服器通信。

**什麼是客戶驗證器？** -兩個客戶驗證器組成一對ID — 一個用於測試，一個用於生產。 當您註冊他們的服務時，ExpressPlay會為您註冊。 您可在ExpressPlay管理頁面上隨時使用這些功能：
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**我什麼時候用這個？** -將此內容納入對ExpressPlay伺服器的所有呼叫中— 例如，授權伺服器、 [ExpressPlay金鑰儲存](https://www.expressplay.com/developer/key-storage/)，以及其他呼叫。
