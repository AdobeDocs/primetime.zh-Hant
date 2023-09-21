---
title: 關於CRL檔案
description: 關於CRL檔案
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 關於CRL檔案 {#about-crl-files}

為了正常運作， Individualization和License伺服器需要在執行中的應用程式伺服器（例如Tomcat）上將數個憑證撤銷清單(CRL)檔案快取到磁碟。 新的CRL檔案必須定期在磁碟上下載和快取。 如果允許磁碟上的CRL檔案的有效期過期，Individualization Server將拒絕個人化使用者端，而License Server將拒絕簽發授權。

快取至磁碟的CRL必須具有符合對應URL的檔案名稱。 特殊字元（例如冒號「：」和「/」斜線）會轉換為檔案名稱中的底線「_」。

以下為個人化及授權伺服器所使用的外部代管CRL清單：

* **中繼CRL：**

   * URL： [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效性：在建立後約12個月內有效

* **根CRL：**

   * URL： [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：從建立起約5年有效

* **最新CRL：**

   * URL： [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 檔案： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：在建立後約3個月內有效

若要瞭解授權伺服器可使用的外部託管CRL，請聯絡Adobe支援。

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

除了外部代管的CRL之外，您還可以建立和維護額外的CRL。 這是個人化CA CRL，如 [建立個人化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 小節。

CRL排程在到期前45天更新。 這樣您應該有足夠的時間從網際網路取得並安裝新產生的CRL。 您必須小心更新CRL檔案，才能使其過期。
