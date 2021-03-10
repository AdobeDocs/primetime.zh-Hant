---
title: 配置路徑和類路徑
description: 配置路徑和類路徑
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# 配置路徑和類路徑{#configure-the-path-and-classpath}

[!DNL flashaccess.war]包含[!DNL jsafeWithNative.jar]，該庫是Crypto-J庫。 後者需要額外的本機庫來執行加密操作。

1. 將原生[!DNL jsafe]程式庫新增至路徑。

   * **Linux /  [!DNL libjsafe.so] -** 包含的目 [!DNL libjsafe.so] 錄必須位於路徑上（本機Crypto-J庫也可用於其他平台）。例如，在`LD_LIBRARY_PATH`上設定[!DNL libjsafe.so]。

   * **Windows /  [!DNL jsafe.dll] -Windows** 上的對應項 [!DNL libjsafe.so] 是適當的 [!DNL jsafe.dll]。
   這些庫可用於[!DNL thirdparty]庫資料夾中。
1. 將[!DNL adobe-flashaccess-certs] jar檔案之一放在類路徑上。

       此JAR檔案不包含在WAR檔案中；必須將其顯式添加到類路徑中。
   
   * 開發伺服器——僅應使用[!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生產伺服器——僅應使用[!DNL adobe-flashaccess- certs.jar]

分發包括[!DNL shared]資料夾，其中包括jar檔案和預配置的[!DNL AdobeInitial.properties]檔案。 Adobe建議您通過[!DNL catalina.properties]檔案將這些項目添加到`common.loader`。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


