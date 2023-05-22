---
description: 要設定Adobe® Access™以供使用，請從DVD中複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，還向Adobe Systems Incorporated申請證書。 您將獲得多個憑據，用於保護打包內容、許可證和客戶端與伺服器之間通信的完整性。
title: 建立開發環境
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 設定SDK {#setting-up-the-sdk}

要設定Adobe® Access™以供使用，請從DVD中複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，還向Adobe Systems Incorporated申請證書。 您將獲得多個憑據，用於保護打包內容、許可證和客戶端與伺服器之間通信的完整性。

Adobe訪問SDK有兩種類型：
* Adobe Access CoreSDK
* Adobe Access ProfessionalSDK

下表顯示了Adobe訪問SDK的基本比較：

| 功能 | Adobe Access CoreSDK | Adobe Access ProfessionalSDK |
|---|---|---|
| Flash Access2.0功能 | 可用 | 可用 |
| 鍵旋轉 | - | 可用 |
| 域支援 | 可用 | 可用 |
| 增強的許可證連結 | 可用 | 可用 |
| 同步消息 | 可用 | 可用 |
| 許可證預生成 | 可用 | 可用 |
| 嵌入式許可證 | 可用 | 可用 |

## 建立開發環境 {#setting-up-the-development-environment}

從DVD中，複製以下SDK檔案以用於開發環境和Java類路徑：

* adobe-flashaccess-certs.jar(包含Adobe根證書)
* adobe-flashaccess-sdk.jar(包含Adobe Access CoreSDK類)
* adobe-flashaccess-sdk-pro.jar(包含Adobe Access ProfessionalSDK類，僅專業功能所需)

您還需要SDK「第三方」資料夾中DVD上的以下第三方JAR檔案：

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons discovery-0.4.jar
* commons logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

為了提高效能，您可以選擇通過部署位於SDK「第三方/密碼」資料夾中的平台特定庫來啟用對加密操作的本機支援。 要啟用本機支援，請將平台的庫（用於Windows的jsafe.dll或用於Linux的libjsafe.so）添加到路徑中。 提供了這些庫的32位和64位版本。 （請注意，只有在您有64位作業系統並且運行64位版本的Java時，才應使用64位版本）。

此外，SDK的一個可選部分是adobe-flashaccess-lcrm.jar。 只有與AdobeFlash媒體Rights Management伺服器(FMRMS)1.x相容性相關的功能才需要此檔案。 如果您以前部署了FMRMS 1.x，並且不想重新打包受FMRMS保護的內容，則必須向許可證伺服器添加支援，以便它能夠處理舊內容和客戶端。
