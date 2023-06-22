---
description: 您必須設定伺服器屬性來反映您的環境。 您可以使用下列任何一項來執行此操作
title: 將屬性套用至伺服器環境
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 將屬性套用至伺服器環境{#apply-properties-to-server-environments}

您必須設定伺服器屬性來反映您的環境。 您可以使用下列任一項來達成此目的：

* [!DNL flashaccess-i15n.properties]  — 包含於各個 [!DNL .war] 檔案

* [!DNL AdobeInitial.properties]  — 位於中的範例 [!DNL /shared] DVD資料夾

   您可以使用此檔案來覆寫WAR檔案中設定的屬性，如下所示：

   1. 設定覆寫屬性值 [!DNL AdobeInitial.properties]
   1. 地標 [!DNL AdobeInitial.properties] 在類別路徑上。

   >[!NOTE]
   >
   >Adobe建議您使用 [!DNL AdobeInitial.properties] 檔案中，因為這樣可讓您更新應用程式WAR檔案，而不會失去先前在 [!DNL flashaccess-i15n.properties] 檔案。

* Java系統屬性機制。

您可以將個別屬性套用至這些特定的伺服器環境：

* *開發*
* *分段*
* *生產*

透過此功能，您可以針對所有伺服器環境使用相同的WAR檔案。 若要將屬性套用至特定環境，請附加兩個底線字元(&#39; `__`&#39;)加上下列其中一個環境程式碼到屬性 *名稱*：

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，若要將記錄層級設定為 `INFO` 用於您的生產和中繼伺服器，以及 `DEBUG` 對於您的開發伺服器：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

伺服器會採用下列搜尋順序來搜尋屬性：

1. `propertyname_environment` 在 [!DNL AdobeInitial.properties]

1. `propertyname_environment` 在 [!DNL flashaccess-15n.properties]

1. `propertyname_environment` Java系統屬性中的
1. `propertyname` 在 [!DNL AdobeInitial.properties]

1. `propertyname` 在 [!DNL flashaccess-15n.properties]

1. `propertyname` Java系統屬性中的

>[!NOTE]
>
>啟動伺服器時，必須將伺服器的環境名稱指定為Java System屬性。 例如，啟動Tomcat時 [!DNL catalina.bat]，設定 `CATALINA_OPTS` 環境變數，如下所示：
>-DENVIRONMENT_NAME=[ 開發 |階段 | PROD ]
