---
description: 若要設定Adobe®存取™使用，請從DVD複製檔案。 這些檔案包含包含程式碼、憑證和協力廠商類別的JAR檔案。 此外，請向Adobe Systems Incorporated要求憑證。 您將獲得多個認證，用於保護封裝內容、授權及使用者端與伺服器之間通訊的完整性。
title: 設定開發環境
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 設定SDK {#setting-up-the-sdk}

若要設定Adobe®存取™使用，請從DVD複製檔案。 這些檔案包含包含程式碼、憑證和協力廠商類別的JAR檔案。 此外，請向Adobe Systems Incorporated要求憑證。 您將獲得多個認證，用於保護封裝內容、授權及使用者端與伺服器之間通訊的完整性。

Adobe存取SDK提供兩種型別：
* ADOBE ACCESS CORE SDK
* ADOBE ACCESS PROFESSIONAL SDK

下表顯示Adobe存取SDK的基本比較：

| 功能 | ADOBE ACCESS CORE SDK | ADOBE ACCESS PROFESSIONAL SDK |
|---|---|---|
| Flash Access2.0功能 | 可用 | 可用 |
| 金鑰輪換 | - | 可用 |
| 網域支援 | 可用 | 可用 |
| 增強授權鏈結 | 可用 | 可用 |
| 同步處理訊息 | 可用 | 可用 |
| 授權預先產生 | 可用 | 可用 |
| 內嵌授權 | 可用 | 可用 |

## 設定開發環境 {#setting-up-the-development-environment}

從DVD複製以下SDK檔案，以用於您的開發環境和Java類別路徑：

* adobe-flashaccess-certs.jar (包含Adobe根憑證)
* adobe-flashaccess-sdk.jar (包含Adobe Access Core SDK類別)
* adobe-flashaccess-sdk-pro.jar (包含Adobe Access Professional SDK類別，僅適用於Professional功能)

您還需要下列第三方JAR檔案，這些檔案也位於SDK的「第三方」資料夾中的DVD上：

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

為改善效能，您可以部署位於SDK「thirdparty/cryptoj」資料夾中的平台特定程式庫，選擇性地啟用密碼編譯作業的原生支援。 若要啟用原生支援，請將您平台的程式庫（適用於Windows的jsafe.dll或適用於Linux的libjsafe.so）新增至路徑。 提供這些程式庫的32位元和64位元版本。 （請注意，只有在您有64位元作業系統且您執行64位元版Java時，才應該使用64位元版）。

此外，SDK的選用部分為adobe-flashaccess-lcrm.jar。 只有與AdobeFlash媒體Rights Management伺服器(FMRMS) 1.x相容性相關的功能才需要此檔案。 如果您先前已部署FMRMS 1.x，並且不想重新封裝受FMRMS保護的內容，則必須新增對授權伺服器的支援，使其能夠處理舊的內容和使用者端。
