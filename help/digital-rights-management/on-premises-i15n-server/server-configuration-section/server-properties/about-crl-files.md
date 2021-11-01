---
title: 關於CRL檔案
description: 關於CRL檔案
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 關於CRL檔案 {#about-crl-files}

為了正常運行，個性化和許可證伺服器需要有多個快取到正在運行的應用程式伺服器（如Tomcat）上磁碟的證書吊銷清單(CRL)檔案。 必須定期下載新的CRL檔案並將其快取到磁碟上。 如果允許磁碟上CRL檔案的有效期失效，則個性化伺服器將拒絕對客戶端進行個性化，許可證伺服器將拒絕頒發許可證。

快取到磁碟的CRL必須具有與相應URL匹配的檔案名。 冒號「：」和「/」斜線等特殊字元會在檔案名稱中轉換為底線「_」。

以下是個人化伺服器和許可證伺服器所使用的外部托管CRL的清單：

* **中間CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效性：從建立起大約12個月

* **根CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 檔案： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：從創作開始大約5年

* **最新CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 檔案： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：建立後約3個月有效

要了解許可證伺服器可以使用的外部托管CRL，請與Adobe支援聯繫。

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

除了外部托管的CRL外，您還可以建立和維護附加的CRL。 這是個性化CA CRL，如 [建立個性化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 一節。

CRL計畫在過期45天前更新。 這樣，您就有足夠的時間從Internet獲取和安裝新生成的CRL。 您必須在CRL檔案過期之前對其進行更新。
