---
description: '您必須配置伺服器屬性以反映您的環境。 您可以使用下列任一項來執行此動作 '
seo-description: '您必須配置伺服器屬性以反映您的環境。 您可以使用下列任一項來執行此動作 '
seo-title: 將屬性套用至伺服器環境
title: 將屬性套用至伺服器環境
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 將屬性套用至伺服器環境{#apply-properties-to-server-environments}

您必須配置伺服器屬性以反映您的環境。 您可以使用下列任一項來執行此動作：

* [!DNL flashaccess-i15n.properties] -每個檔案包含的范 [!DNL .war] 例

* [!DNL AdobeInitial.properties] -位於DVD上 [!DNL /shared] 資料夾的示例

   可以使用此檔案覆蓋WAR檔案中設定的屬性，如下所示：

   1. 在 [!DNL AdobeInitial.properties]
   1. 放 [!DNL AdobeInitial.properties] 在類路徑上。
   >[!NOTE]
   >
   >Adobe建議您使用檔案，因為這可讓您更新應用程式 [!DNL AdobeInitial.properties] WAR檔案，而不會遺失檔案中先前可能進行的任何屬性設定設 [!DNL flashaccess-i15n.properties] 定。

* Java System屬性機制。

您可以將個別屬性套用至這些特定伺服器環境：

* *開發*
* *測試*
* *製作*

使用此功能，您可以對所有伺服器環境使用相同的WAR檔案。 若要將屬性套用至特定環境，請在屬性名稱中附加兩個底線字元(&#39; `__`&#39;)加上下列其中一個環境代 *碼*:

    * 「DEV」
    * 「STAGE」
    * 「PROD」

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，要將生產和測試伺服器的 `INFO` 日誌級別設定為，以及將開發服 `DEBUG` 務器的日誌級別設定為：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

伺服器使用以下屬性搜索順序：

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系統屬性中
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系統屬性中

>[!NOTE]
>
>啟動伺服器時，必須將伺服器的環境名稱指定為Java System屬性。 例如，在啟動Tomcat時 [!DNL catalina.bat]，請按如 `CATALINA_OPTS` 下方式設定環境變數：
>-DENVIRONMENT_NAME=[ DEV| STAGE| PROD ]
