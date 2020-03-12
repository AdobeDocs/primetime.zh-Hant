---
description: 如果要設定Primetime DRM，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，您還需要向Adobe Systems, Incorporated索取憑證。 然後，Adobe會向您發出多份認證，供您用來保護封裝內容、授權和用戶端與伺服器間通訊的完整性。
seo-description: 如果要設定Primetime DRM，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，您還需要向Adobe Systems, Incorporated索取憑證。 然後，Adobe會向您發出多份認證，供您用來保護封裝內容、授權和用戶端與伺服器間通訊的完整性。
seo-title: 設定您的開發環境
title: 設定您的開發環境
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 設定您的開發環境 {#set-up-your-development-environment}

如果要設定Primetime DRM，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，您還需要向Adobe Systems, Incorporated索取憑證。 然後，Adobe會向您發出多份認證，供您用來保護封裝內容、授權和用戶端與伺服器間通訊的完整性。

Adobe提供Primetime DRM SDK on DVD:

1. 將下列檔案從[!DNL [DRM DVD]/SDK/]複製到您的開發系統（在您的Java類路徑上）:

   * [!DNL adobe-flashaccess-certs.jar] -包含Adobe根憑證
   * [!DNL adobe-flashaccess-sdk.jar] -包含Primetime DRM核心SDK類別
   * [!DNL adobe-flashaccess-sdk-pro.jar] -包含Primetime DRM專業版SDK類別，僅適用於專業版功能

1. 從[!DNL [DRM DVD]/SDK/協力廠商]複製下列檔案至您的開發系統：

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

1. （可選）為提升效能，您可從[!DNL [DRM DVD]/SDK/thirdparty/cryptoj/]將適當的平台特定程式庫複製至您的開發系統，以啟用加密作業的原生支援（請記得將位置放在您的路徑上）:

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >這些資料庫的32位元和64位元版本已推出。 只有在您有64位元作業系統且執行64位元版本的Java時，才應使用64位元版本。

1. （選擇性）若需有關Adobe Flash Media Rights Management Server(FMRMS)1.x相容性的功能，請複製至您 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 的開發系統：

   只有當您先前已部署FMRMS 1.x且不想重新封裝FMRMS保護的內容時，才會部署此軟體。 在這種情況下，您必須將此支援新增至您的授權伺服器，以便它能夠管理舊內容和用戶端。
