---
description: 如果要設定黃金時段DRM，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，您需要向Adobe Systems公司申請證書。 然後，Adobe會向您發出多個憑據，這些憑據用於保護打包內容、許可證的完整性以及客戶端與伺服器之間的通信。
title: 設定開發環境
exl-id: c10f85b6-84bc-444f-9001-f49dc88cf99c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# 設定開發環境 {#set-up-your-development-environment}

如果要設定黃金時段DRM，請從DVD複製檔案。 這些檔案包括包含代碼、證書和第三方類的JAR檔案。 此外，您需要向Adobe Systems公司申請證書。 然後，Adobe會向您發出多個憑據，這些憑據用於保護打包內容、許可證的完整性以及客戶端與伺服器之間的通信。

Adobe提供Mogfire DRM SDK on DVD:

1. 從[!DNL複製以下檔案 [DRM DVD]/SDK/]到開發系統（位於Java類路徑上）:

   * [!DNL adobe-flashaccess-certs.jar]  — 包括Adobe根證書
   * [!DNL adobe-flashaccess-sdk.jar]  — 包括Mogfire DRM核心SDK類
   * [!DNL adobe-flashaccess-sdk-pro.jar]  — 包括Mogfire DRM Professional SDK類，僅專業功能所需

1. 從[!DNL複製以下檔案 [DRM DVD]/SDK/第三方]到您的開發系統：

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

1. （可選）為了提高效能，您可以通過從[!DNL]複製適當的平台特定庫來啟用對加密操作的本機支援 [DRM DVD]/SDK/第三方/cryptoj/]到您的開發系統（請記住將位置放在您的路徑上）:

   * [!DNL jsafe.dll]  — 窗口
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >這些庫的32位和64位版本可用。 只有在您有64位作業系統並且運行64位版本的Java時，才應使用64位版本。

1. （可選）有關AdobeFlash媒體Rights Management伺服器(FMRMS)1.x相容性的功能，請複製 `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` 到您的開發系統：

   僅當您以前部署了FMRMS 1.x且不想重新打包受FMRMS保護的內容時，才部署此項。 在這種情況下，必須將此支援添加到您的許可證伺服器中，以便它能夠管理舊內容和客戶端。
