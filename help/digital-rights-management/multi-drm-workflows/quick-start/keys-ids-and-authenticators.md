---
description: 要實施DRM，您需要特定的憑證和金鑰，包括內容加密金鑰或CEK來加密您的內容、保護與ExpressPlay伺服器通訊的客戶驗證器，以及用於識別儲存在金鑰管理系統中的內容加密金鑰的CEKSID。
title: 金鑰、ID和驗證者
exl-id: b769192d-92ad-4b93-84dd-80b182fc6c43
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# 金鑰、ID和驗證者{#keys-ids-and-authenticators}

要實施DRM，您需要特定的憑證和金鑰，包括內容加密金鑰或CEK來加密您的內容、保護與ExpressPlay伺服器通訊的客戶驗證器，以及用於識別儲存在金鑰管理系統中的內容加密金鑰的CEKSID。

您需要這些專案來封裝、授權和播放您的受保護內容：

## 內容加密金鑰 {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

內容加密金鑰(CEK)是用於加密內容的16位元組字串。

**什麼是CEK？** - CEK是封裝程式用來加密內容的金鑰。 它是16位元組的十六進位編碼字串。

**CEK來自何處？**  — 您（內容提供者）使用OpenSSL或Notepad等工具自行建立此金鑰++ 例如：

```
openssl rand 16 -hex > cek_hex_file
```

或(對於Adobe離線封裝程式)：

1. 如上所述或使用其他工具產生16位元組的十六進位編碼字串。 它看起來會像這樣：

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. 開啟Notepad++並貼入16位元組的十六進位字串。
1. 透過Base64將此值從十六進位ASCII轉換 — 將該值編碼以建立 [!DNL keyfile.bin]. (相關說明請參閱 [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**相同的金鑰，不同的名稱？**  — 是，您可能會看到在其他位置有其他名稱引用的CEK，例如：

* ** [！DNL [somefile].bin]** - 「Adobe離線封裝程式」會將CEK稱為[！DNL [somefile].bin]；例如* [!DNL Keyfile.bin]* — 這是您的CEK，由Adobe離線封裝程式使用，採用您用來封裝內容之電腦上的檔案形式。

   您可以「Base64」隨機CEK十六進位字串，並將其儲存為檔案(例如 [!DNL keyfile.bin])，通常位於 [!DNL creds] 目錄下 [!DNL offlinepkgr/]. 在您的封裝程式設定檔案中(例如，您可以將其稱為 [!DNL widevine.xml] 如果您要包裝Widevine DRM)，請在設定檔案中參照CEK，如下所示：

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **內容金鑰**  — 您也可能在呼叫中看到稱為內容索引鍵的CEK ( `&contentKey=`)、錯誤訊息中、支援票證中和其他檔案中的。

**何時/在何處使用它？**

1. 首先，您必須在進行封裝的電腦上提供CEK。 您的封裝工具會使用您的CEK來加密內容。
1. 其次，您需要以某種形式的金鑰管理系統(KMS)儲存CEK，每個CEK都與其自身相關聯 [內容加密金鑰](../../multi-drm-workflows/glossary/glossary-cek.md). 您可以建立自己的KMS，或使用 [ExpressPlay的金鑰儲存裝置](https://www.expressplay.com/developer/key-storage/). 這可讓您的店面（處理客戶權益和授權權杖布建的授權伺服器）使用金鑰ID而不是實際的CEK，從KMS提取客戶的授權權杖（這會更安全）。

## 內容加密金鑰儲存ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

內容加密金鑰儲存ID (CEKSID)可唯一識別將加密的視訊內容解密的儲存金鑰。

**什麼是CEKSID？** - CEKSID是內容加密金鑰(CEK)的唯一識別碼。 CEK是解除鎖定受保護內容所必需的；CEKSID是存取儲存它的CEK所必需的。 當您測試設定時，只要使用相同的資訊進行授權和播放檢查，您就可以在「封裝」時間提供隨機的CEKSID和CEK。

**它來自何處？**  — 您（內容提供者）可以自行建立此ID，也可以使用之類的服務 [ExpressPlay的金鑰儲存裝置](https://www.expressplay.com/developer/key-storage/) 為每個CEK產生CEKSID （並儲存兩者）。 此外，您可以使用隨機產生的CEKSID，或採用適合您商業模式的配置。 例如，您可以使用有意義字串的CEKSID，而不是隨機的十六進位字串（ID名稱可能包含主題、日期、時間等）

**CEKSID還呼叫了什麼？**  — 有時稱為 *內容ID*.

## 客戶驗證者 {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

當您在ExpressPlay中設定管理員帳戶時，客戶驗證器是您從ExpressPlay取得的金鑰。 驗證器用於與ExpressPlay伺服器的通訊。

**什麼是客戶驗證者？**  — 兩個客戶驗證者組成了ExpressPlay註冊服務時為您註冊的ID組（一個用於測試，一個用於生產）。 您一律可在ExpressPlay管理頁面上使用：
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**我何時可以使用此功能？**  — 您將此專案包含在ExpressPlay伺服器的所有呼叫中，例如授權伺服器、 [ExpressPlay金鑰儲存](https://www.expressplay.com/developer/key-storage/)和其他呼叫。
