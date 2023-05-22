---
description: 參考實現伺服器可幫助您建立使用Adobe PrimetimeDRM Java SDK所有功能的全功能許可證伺服器。
title: 許可證伺服器
exl-id: a928b7ac-9191-4b8c-b038-eb92a09286fa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 許可證伺服器 {#license-server}

參考實現伺服器可幫助您建立使用Adobe PrimetimeDRM Java SDK所有功能的全功能許可證伺服器。

在該實現中，基於資料庫中的用戶條目對用戶進行認證。 該伺服器包括用於頒發許可證的演示業務邏輯，並為Flash媒體Rights Management伺服器1.0和1.5提供相容性支援。

## 許可證伺服器要求 {#license-server-requirements}

許可證伺服器要求：

* 安裝Tomcat 6.0或更高版本
* 安裝資料庫，如MySQL（可在DVD上使用） [!DNL Third Party\MySQL])
* 確保安裝了Java 1.6或更高版本
* 要運行示例生成指令碼，請確保您有Ant 1.8或更高版本

安裝Tomcat和MySQL後，請與Adobe聯繫以獲取所需的DRM憑據集。

## 生成許可證伺服器 {#build-the-license-server}

>[!NOTE]
>
>只有在您要修改原始碼時，才需要構建許可證伺服器。 為了進行評估，您只需將WAR檔案作為發運的檔案使用即可。

參考實現許可證伺服器包括所有許可證伺服器原始碼( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)，以及Ant生成指令碼( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)，您可以通過它定制許可證伺服器以滿足您的業務需求。

1. 修改Ant生成指令碼以指定Mogifle DRM SDK、Tomcat、MySQL和Log4J的位置。

   開啟 [!DNL build-refimpl.xml] 文本編輯器中的檔案，並設定以下屬性值：

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 使用 `all` 屬性，位於Ant生成指令碼所在的目錄中。

   ```
   ant -f build-refimpl.xml all
   ```

   Ant生成指令碼建立 [!DNL refimpl-build/wars] 包含伺服器WAR檔案的目錄。
