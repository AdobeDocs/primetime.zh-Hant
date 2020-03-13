---
seo-title: 關於CRL檔案
title: 關於CRL檔案
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 關於CRL檔案 {#about-crl-files}

為了正常運作，個人化和授權伺服器需要在執行中的應用程式伺服器（例如Tomcat）上，將數個憑證撤銷清單(CRL)檔案快取至磁碟。 新的CRL檔案必須定期在磁碟上下載和快取。 如果允許磁碟上CRL檔案的有效期失效，個性化伺服器將拒絕將客戶機個性化，而許可證伺服器將拒絕頒發許可證。

快取至磁碟的CRL必須有與對應URL相符的檔案名稱。 在檔案名中，冒號&#39;:&#39;和&#39;/&#39;斜槓等特殊字元將轉換為下划線&#39;_&#39;。

以下是個人化和授權伺服器都使用的外部托管CRL清單：

* **中級CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效性：從建立開始大約12個月

* **根CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：從創作到創作約5年

* **最新CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 檔案： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：從創作開始約3個月

以下是僅由許可證伺服器使用的外部托管CRL:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* 有效性：從創作開始約3個月

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* 檔案： [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* 有效性：從創作開始約3個月

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* 檔案： [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* 有效性：從創作開始約3個月

除了上述CRL外，您還必須建立並維護額外的CRL。 這是個性化CA CRL，如本文檔的「創 [建個性化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 」部分所指定。

CRL預計在到期前45天更新。 這應可讓您有足夠的時間從網際網路取得和安裝新產生的CRL。 您必須在CRL檔案過期之前小心更新。
