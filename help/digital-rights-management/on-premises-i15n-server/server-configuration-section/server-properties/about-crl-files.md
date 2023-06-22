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

為了正常運作，個人化和授權伺服器需要有多個「憑證撤銷清單」(CRL)檔案快取到執行應用程式伺服器（例如Tomcat）上的磁碟。 新的CRL檔案必須定期在磁碟上下載和快取。 如果允許磁碟上的CRL檔案的有效期過期，Individualization Server將拒絕個人化使用者端，而License Server將拒絕簽發授權。

快取至磁碟的CRL必須具有符合對應URL的檔案名稱。 特殊字元（例如冒號「：」和「/」斜線）在檔案名稱中會轉換為底線「_」。

以下為個人化和授權伺服器使用的外部託管CRL清單：

* **中級CRL：**

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
   * 有效性：有效期限為建立後約3個月

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

除了外部託管的CRL之外，您還可以建立和維護其他CRL。 這是個人化CA CRL，如 [建立個人化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 區段。

CRL排程在到期前45天更新。 這樣您應該有足夠的時間從網際網路取得並安裝新產生的CRL。 您必須小心更新CRL檔案，才能使其過期。
