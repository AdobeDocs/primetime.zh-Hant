---
title: 配置路徑和類路徑
description: 配置路徑和類路徑
copied-description: true
exl-id: e6e9f837-4e3d-43e1-971d-3fa0ccaeff39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 配置路徑和類路徑{#configure-the-path-and-classpath}

的 [!DNL flashaccess.war] 包含 [!DNL jsafeWithNative.jar]，即Crypto-J庫。 後者需要附加的本機庫來執行加密操作。

1. 添加本機 [!DNL jsafe] 庫。

   * **Linux / [!DNL libjsafe.so] -** 包含 [!DNL libjsafe.so] 必須位於路徑上（本機Crypto-J庫也可用於其他平台）。 例如，設定 [!DNL libjsafe.so] 上 `LD_LIBRARY_PATH`。

   * **Windows / [!DNL jsafe.dll] -** Windows上的對應對象 [!DNL libjsafe.so] 合適 [!DNL jsafe.dll]。
   這些庫在 [!DNL thirdparty] 庫資料夾。
1. 放上 [!DNL adobe-flashaccess-certs] 類路徑上的jar檔案。

       此JAR檔案未包含在WAR檔案中；必須將其顯式添加到類路徑中。
   
   * 開發伺服器 — 只應使用 [!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生產伺服器 — 只應使用 [!DNL adobe-flashaccess- certs.jar]

該分配包括 [!DNL shared] 包含jar檔案和預配置的資料夾 [!DNL AdobeInitial.properties] 的子菜單。 Adobe建議將這些項添加到 `common.loader` 通過 [!DNL catalina.properties] 的子菜單。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
