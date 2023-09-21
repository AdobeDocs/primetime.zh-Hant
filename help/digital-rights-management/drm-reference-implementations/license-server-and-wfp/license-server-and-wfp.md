---
description: 參考實作伺服器可協助您建立使用Adobe Primetime DRM Java SDK所有功能的完整授權伺服器。
title: 授權伺服器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 授權伺服器 {#license-server}

參考實作伺服器可協助您建立使用Adobe Primetime DRM Java SDK所有功能的完整授權伺服器。

在此實作中，會根據資料庫中的使用者專案來驗證使用者。 此伺服器包含發行授權的示範商業邏輯，並提供Flash MediaRights Management伺服器1.0和1.5的相容性支援。

## 授權伺服器需求 {#license-server-requirements}

授權伺服器需求：

* 安裝Tomcat 6.0或更新版本
* 安裝資料庫，例如MySQL (可在DVD上取得，位於 [!DNL Third Party\MySQL])
* 確保您已安裝Java 1.6或更新版本
* 若要執行範例建置指令碼，請確定您有Ant 1.8或更新版本

安裝Tomcat和MySQL之後，請連絡Adobe取得一組必要的DRM認證。

## 建置授權伺服器 {#build-the-license-server}

>[!NOTE]
>
>只有在您想要修改原始程式碼時，才需要建立授權伺服器。 為了評估目的，您只需在出貨時使用WAR檔案即可。

參考實作授權伺服器包含所有授權伺服器原始碼( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)，以及Ant建置指令碼( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)，您可依據您的業務需求自訂授權伺服器。

1. 修改Ant建置指令碼，以指定Primetime DRM SDK、Tomcat、MySQL和Log4J的位置。

   開啟 [!DNL build-refimpl.xml] 檔案並設定這些屬性值：

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 使用執行Ant建置指令碼 `all` 屬性，位於Ant建置指令碼所在的目錄中。

   ```
   ant -f build-refimpl.xml all
   ```

   Ant建置指令碼會建立 [!DNL refimpl-build/wars] 包含伺服器WAR檔案的目錄。
