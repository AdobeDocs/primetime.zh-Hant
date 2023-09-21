---
title: 設定路徑和類別路徑
description: 設定路徑和類別路徑
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 設定路徑和類別路徑{#configure-the-path-and-classpath}

此 [!DNL flashaccess.war] 包含 [!DNL jsafeWithNative.jar]，亦即Crypto-J資料庫。 後者需要額外的原生程式庫來執行加密作業。

1. 新增原生 [!DNL jsafe] 資料庫至您的路徑。

   * **Linux / [!DNL libjsafe.so] -** 包含的目錄 [!DNL libjsafe.so] 必須位於路徑上（原生Crypto-J程式庫也可用於其他平台）。 例如，設定 [!DNL libjsafe.so] 於 `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** Windows上的對應專案 [!DNL libjsafe.so] 是否適當 [!DNL jsafe.dll].

   您可在以下位置使用這些程式庫： [!DNL thirdparty] 資料庫資料夾。
1. 放一個 [!DNL adobe-flashaccess-certs] 類別路徑上的jar檔案。

       這個JAR檔案不包括在WAR檔案中；您必須將它明確加入類別路徑。
   
   * 開發伺服器 — 應該僅使用 [!DNL adobe-flashaccess-certs-prerelease.jar].
   * 生產伺服器 — 應該僅使用 [!DNL adobe-flashaccess- certs.jar]

此分佈包含 [!DNL shared] 同時包含jar檔案和預先設定的資料夾 [!DNL AdobeInitial.properties] 檔案。 Adobe建議您將這些專案新增至 `common.loader` 透過 [!DNL catalina.properties] 檔案。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
