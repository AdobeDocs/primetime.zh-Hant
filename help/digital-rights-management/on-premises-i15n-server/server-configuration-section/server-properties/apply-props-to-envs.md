---
description: 必須配置伺服器屬性以反映您的環境。 可以使用下列任一項執行此操作
title: 將屬性應用於伺服器環境
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 將屬性應用於伺服器環境{#apply-properties-to-server-environments}

必須配置伺服器屬性以反映您的環境。 可以使用下列任一方法執行此操作：

* [!DNL flashaccess-i15n.properties]  — 包括於各 [!DNL .war] 檔案

* [!DNL AdobeInitial.properties]  — 位於 [!DNL /shared] 資料夾

   可以使用此檔案覆蓋WAR檔案中設定的屬性，如下所示：

   1. 在中設定覆蓋屬性值 [!DNL AdobeInitial.properties]
   1. 位置 [!DNL AdobeInitial.properties] 類路徑中。

   >[!NOTE]
   >
   >Adobe建議您使用 [!DNL AdobeInitial.properties] 檔案，因為這樣，您就可以更新應用程式WAR檔案，而不會丟失您以前在中可能完成的任何屬性配置設定 [!DNL flashaccess-i15n.properties] 的子菜單。

* Java系統屬性機制。

您可以將各個屬性應用到以下特定伺服器環境：

* *開發*
* *暫存*
* *生產*

使用此功能，您可以對所有伺服器環境使用相同的WAR檔案。 要將屬性應用於特定環境，請追加兩個下划線字元(&#39; `__`&#39;)加上屬性的以下環境代碼之一 *名稱*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，將日誌級別設定為 `INFO` 用於生產和暫存伺服器， `DEBUG` 用於開發伺服器：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

伺服器對以下屬性使用此搜索順序：

1. `propertyname_environment` 在 [!DNL AdobeInitial.properties]

1. `propertyname_environment` 在 [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系統屬性中
1. `propertyname` 在 [!DNL AdobeInitial.properties]

1. `propertyname` 在 [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系統屬性中

>[!NOTE]
>
>啟動伺服器時，必須將伺服器的環境名稱指定為Java System屬性。 例如，在啟動Tomcat時 [!DNL catalina.bat]的子菜單。 `CATALINA_OPTS` 環境變數如下：
> — 環境名稱=[ 開發 |舞台 |PROD ]
