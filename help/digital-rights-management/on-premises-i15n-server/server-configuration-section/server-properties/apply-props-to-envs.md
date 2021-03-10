---
description: '您必須配置伺服器屬性以反映您的環境。 您可以使用下列任一項來執行此動作 '
title: 將屬性套用至伺服器環境
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 將屬性應用於伺服器環境{#apply-properties-to-server-environments}

您必須配置伺服器屬性以反映您的環境。 您可以使用下列任一項來執行此動作：

* [!DNL flashaccess-i15n.properties] -每個檔案包含的范 [!DNL .war] 例

* [!DNL AdobeInitial.properties] -位於DVD上 [!DNL /shared] 資料夾的示例

   可以使用此檔案覆蓋WAR檔案中設定的屬性，如下所示：

   1. 在[!DNL AdobeInitial.properties]中設定覆蓋屬性值
   1. 將[!DNL AdobeInitial.properties]放在類路徑上。

   >[!NOTE]
   >
   >Adobe建議您使用[!DNL AdobeInitial.properties]檔案，因為這可讓您更新應用程式WAR檔案，而不會遺失您在[!DNL flashaccess-i15n.properties]檔案中所做的任何先前屬性設定。

* Java System屬性機制。

您可以將個別屬性套用至這些特定伺服器環境：

* *開發*
* *測試*
* *製作*

使用此功能，您可以對所有伺服器環境使用相同的WAR檔案。 要將屬性應用於特定環境，請將兩個下划線字元(&#39; `__`&#39;)加上以下環境代碼之一附加到屬性&#x200B;*name*:

    * 「DEV」
    * 「STAGE」
    * 「PROD」

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，要將生產和測試伺服器的日誌級別設定為`INFO` ，將開發伺服器的日誌級別設定為`DEBUG`:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

伺服器使用以下屬性搜索順序：

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系統屬性中
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系統屬性中

>[!NOTE]
>
>啟動伺服器時，必須將伺服器的環境名稱指定為Java System屬性。 例如，在以[!DNL catalina.bat]啟動Tomcat時，請按如下方式設定`CATALINA_OPTS`環境變數：
>-DENVIRONMENT_NAME=[開發 | STAGE | PROD ]
