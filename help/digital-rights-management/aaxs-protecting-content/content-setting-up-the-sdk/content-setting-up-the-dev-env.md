---
description: 若要設定Adobe® Access™以供使用，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，請向Adobe Systems Incorporated索取憑證。 您將會獲得多份認證，以保護封裝內容、授權和用戶端與伺服器間通訊的完整性。
seo-description: 若要設定Adobe® Access™以供使用，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，請向Adobe Systems Incorporated索取憑證。 您將會獲得多份認證，以保護封裝內容、授權和用戶端與伺服器間通訊的完整性。
seo-title: 設定開發環境
title: 設定開發環境
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 設定SDK {#setting-up-the-sdk}

若要設定Adobe® Access™以供使用，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，請向Adobe Systems Incorporated索取憑證。 您將會獲得多份認證，以保護封裝內容、授權和用戶端與伺服器間通訊的完整性。

Adobe Access SDK提供兩種類型：
* Adobe Access Core SDK
* Adobe Access Professional SDK

下表顯示Adobe Access SDK的基本比較：

| 功能 | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Flash Access 2.0功能 | 可用 | 可用 |
| 鍵旋轉 | - | 可用 |
| 網域支援 | 可用 | 可用 |
| 增強的授權鏈結 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 預先產生授權 | 可用 | 可用 |
| 內嵌授權 | 可用 | 可用 |

## 設定開發環境 {#setting-up-the-development-environment}

從DVD複製下列SDK檔案，以便用於您的開發環境和Java類路徑：

* adobe-flashaccess-certs.jar（包含Adobe根憑證）
* adobe-flashaccess-sdk.jar（包含Adobe Access核心SDK類別）
* adobe-flashaccess-sdk-pro.jar（包含Adobe Access專業版SDK類別，僅適用於專業版功能）

您也需要位於SDK「協力廠商」檔案夾DVD上的下列第三方JAR檔案：

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relanchingDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

為提升效能，您可選擇部署位於SDK「協力廠商／密碼」資料夾中的平台特定程式庫，以啟用加密作業的原生支援。 若要啟用原生支援，請將平台的程式庫（Windows專用的jsafe.dll,Linux專用的libjsafe.so）新增至路徑。 提供這些庫的32位和64位版本。 （請注意，64位元版本僅應在您有64位元作業系統且您執行64位元版本的Java時使用）。

此外，SDK的選用部分是adobe-flashaccess-lcrm.jar。 只有與Adobe Flash Media Rights Management Server(FMRMS)1.x相容性相關的功能才需要此檔案。 如果您先前已部署FMRMS 1.x，但不想重新封裝FMRMS保護的內容，則必須新增對授權伺服器的支援，讓它能夠處理舊內容和用戶端。
