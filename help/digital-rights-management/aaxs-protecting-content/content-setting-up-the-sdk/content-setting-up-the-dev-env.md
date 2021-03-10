---
description: 要設定Adobe®訪問™以便使用，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，請求Adobe Systems Incorporated的認證。 您將會獲得多份認證，以保護封裝內容、授權和用戶端與伺服器間通訊的完整性。
title: 設定開發環境
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# 設定SDK {#setting-up-the-sdk}

要設定Adobe®訪問™以便使用，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，請求Adobe Systems Incorporated的認證。 您將會獲得多份認證，以保護封裝內容、授權和用戶端與伺服器間通訊的完整性。

Adobe存取SDK有兩種類型：
* Adobe Access CoreSDK
* Adobe Access ProfessionalSDK

下表顯示Adobe存取SDK的基本比較：

| 功能 | Adobe Access CoreSDK | Adobe Access ProfessionalSDK |
|---|---|---|
| Flash Access2.0功能 | 可用 | 可用 |
| 鍵旋轉 | - | 可用 |
| 網域支援 | 可用 | 可用 |
| 增強的授權鏈結 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 預先產生授權 | 可用 | 可用 |
| 內嵌授權 | 可用 | 可用 |

## 設定開發環境{#setting-up-the-development-environment}

從DVD複製下列SDK檔案，以便用於您的開發環境和Java類路徑：

* adobe-flashaccess-certs.jar(包含Adobe根憑證)
* adobe-flashaccess-sdk.jar(包含Adobe Access CoreSDK類別)
* adobe-flashaccess-sdk-pro.jar(包含Adobe Access ProfessionalSDK類別，僅適用於專業版功能)

您也需要位於SDK「協力廠商」檔案夾DVD上的下列第三方JAR檔案：

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

為提升效能，您可選擇部署位於SDK「協力廠商／密碼」資料夾中的平台特定程式庫，以啟用加密作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。 提供這些庫的32位和64位版本。 （請注意，64位元版本僅應在您有64位元作業系統且您執行64位元版本的Java時使用）。

此外，SDK的選用部分是adobe-flashaccess-lcrm.jar。 只有與AdobeFlash介質Rights Management伺服器(FMRMS)1.x相容性相關的功能才需要此檔案。 如果您先前已部署FMRMS 1.x，但不想重新封裝FMRMS保護的內容，則必須新增對授權伺服器的支援，讓它能夠處理舊內容和用戶端。
