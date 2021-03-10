---
description: 參考實施伺服器可協助您建立使用Adobe PrimetimeDRM Java SDK所有功能的完整功能授權伺服器。
title: 授權伺服器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 許可證伺服器{#license-server}

參考實施伺服器可協助您建立使用Adobe PrimetimeDRM Java SDK所有功能的完整功能授權伺服器。

在此實施中，根據資料庫中的用戶條目來驗證用戶。 此伺服器包含授權的展示商業邏輯，並提供Flash媒體Rights Management伺服器1.0和1.5的相容性支援。

## 許可證伺服器要求{#license-server-requirements}

授權伺服器需求：

* 安裝Tomcat 6.0或更新版本
* 安裝資料庫，例如MySQL（可在DVD上獲得，位於[!DNL Third Party\MySQL]）
* 確定您已安裝Java 1.6或更新版本
* 要運行示例構建指令碼，請確保您有Ant 1.8或更高版本

安裝Tomcat和MySQL後，請與Adobe聯繫以獲得所需的DRM憑據集。

## 構建許可證伺服器{#build-the-license-server}

>[!NOTE]
>
>只有當您要修改原始碼時，才需要建立授權伺服器。 為了進行評估，您只需將WAR檔案按發運方式使用即可。

參考實施許可證伺服器包括所有許可證伺服器原始碼(`([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)，以及Ant構建指令碼(`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)，您可以用它定制許可證伺服器以滿足您的業務需求。

1. 修改Ant構建指令碼以指定Primetime DRM SDK、Tomcat、MySQL和Log4J的位置。

   在文本編輯器中開啟[!DNL build-refimpl.xml]檔案並設定以下屬性值：

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 使用`all`屬性運行Ant構建指令碼，該屬性位於Ant構建指令碼所在的目錄中。

   ```
   ant -f build-refimpl.xml all
   ```

   Ant構建指令碼建立包含伺服器WAR檔案的[!DNL refimpl-build/wars]目錄。
