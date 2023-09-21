---
description: 如果要設定Primetime DRM，請從DVD複製檔案。 這些檔案包含JAR檔案，其中包含程式碼、憑證和協力廠商類別。 此外，您需要向Adobe Systems， Incorporated索取憑證。 然後Adobe會向您發出多個認證，用於保護封裝內容、授權以及使用者端與伺服器之間通訊的完整性。
title: 設定您的開發環境
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 設定您的開發環境 {#set-up-your-development-environment}

如果要設定Primetime DRM，請從DVD複製檔案。 這些檔案包含JAR檔案，其中包含程式碼、憑證和協力廠商類別。 此外，您需要向Adobe Systems， Incorporated索取憑證。 然後Adobe會向您發出多個認證，用於保護封裝內容、授權以及使用者端與伺服器之間通訊的完整性。

Adobe在DVD上提供Primetime DRM SDK：

1. 從[！DNL]複製下列檔案 [DRM DVD]/SDK/]至您的開發系統（在Java類別路徑上）：

   * [!DNL adobe-flashaccess-certs.jar]  — 包含Adobe根憑證
   * [!DNL adobe-flashaccess-sdk.jar]  — 包含Primetime DRM核心SDK類別
   * [!DNL adobe-flashaccess-sdk-pro.jar]  — 包含Primetime DRM Professional SDK類別，僅適用於Professional功能

1. 從[！DNL]複製下列檔案 [DRM DVD]/SDK/thirdparty]至您的開發系統：

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. （選擇性）為改善效能，您可以從[！DNL複製適當的平台特定程式庫，以啟用密碼編譯作業的原生支援 [DRM DVD]/SDK/thirdparty/cryptoj/]至您的開發系統（請記得將位置放置於您的路徑上）：

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

     >[!NOTE]
     >
     >這些程式庫有32位元和64位元版本可供使用。 如果您有64位元作業系統，且您執行64位元版本的Java，則應該只使用64位元版本。

1. （選用）如需AdobeFlash媒體Rights Management伺服器(FMRMS) 1.x相容性的相關功能，請複製 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 至您的開發系統：

   僅當您先前已部署FMRMS 1.x且不想重新封裝受FMRMS保護的內容時，才部署此專案。 在此情況下，您必須將此支援新增至您的授權伺服器，以便伺服器能夠管理舊的內容和使用者端。
