---
description: 您必須設定伺服器屬性以反映您的環境。 您可使用下列任一項來達成此目的
title: 套用屬性至伺服器環境
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 套用屬性至伺服器環境{#apply-properties-to-server-environments}

您必須設定伺服器屬性以反映您的環境。 您可使用下列任一項來達成此目的：

* [!DNL flashaccess-i15n.properties]  — 包含在各個 [!DNL .war] 檔案

* [!DNL AdobeInitial.properties]  — 位於 [!DNL /shared] DVD資料夾

  您可以使用此檔案來覆寫WAR檔案中設定的屬性，如下所示：

   1. 設定覆寫屬性值 [!DNL AdobeInitial.properties]
   1. 地標 [!DNL AdobeInitial.properties] 在類別路徑上。

  >[!NOTE]
  >
  >Adobe建議您使用 [!DNL AdobeInitial.properties] 檔案，因為這樣可讓您更新應用程式WAR檔案，而不會遺失之前您可能在 [!DNL flashaccess-i15n.properties] 檔案。

* Java系統屬性機制。

您可以將個別屬性套用至這些特定的伺服器環境：

* *開發*
* *分段*
* *生產*

有了這項功能，您可以針對所有伺服器環境使用相同的WAR檔案。 若要將屬性套用至特定環境，請附加兩個底線字元(&#39; `__`&#39;)加上下列其中一個環境程式碼至屬性 *名稱*：

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，若要將記錄層級設為 `INFO` 用於您的生產及中繼伺服器，以及 `DEBUG` 針對您的開發伺服器：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

伺服器會採用下列搜尋順序來搜尋屬性：

1. `propertyname_environment` 在 [!DNL AdobeInitial.properties]

1. `propertyname_environment` 在 [!DNL flashaccess-15n.properties]

1. `propertyname_environment` Java系統屬性中
1. `propertyname` 在 [!DNL AdobeInitial.properties]

1. `propertyname` 在 [!DNL flashaccess-15n.properties]

1. `propertyname` Java系統屬性中

>[!NOTE]
>
>啟動伺服器時，必須將伺服器的環境名稱指定為Java System屬性。 例如，以啟動Tomcat時 [!DNL catalina.bat]，設定 `CATALINA_OPTS` 環境變數，如下所示：
>-DENVIRONMENT_NAME=[開發 |階段 |生產]
