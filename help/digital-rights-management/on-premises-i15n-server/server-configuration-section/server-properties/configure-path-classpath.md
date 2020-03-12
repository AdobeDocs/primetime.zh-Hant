---
seo-title: 配置路徑和類路徑
title: 配置路徑和類路徑
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 配置路徑和類路徑{#configure-the-path-and-classpath}

包 [!DNL flashaccess.war] 含 [!DNL jsafeWithNative.jar]Crypto-J庫。 後者需要額外的本機庫來執行加密操作。

1. 將原生程 [!DNL jsafe] 式庫新增至路徑。

   * **Linux /[!DNL libjsafe.so]-** —— 包含的目 [!DNL libjsafe.so] 錄必須位於路徑上（本地Crypto-J庫也可用於其他平台）。 例如，設 [!DNL libjsafe.so] 置 `LD_LIBRARY_PATH`。

   * **Windows /[!DNL jsafe.dll]-** Windows上的對應項 [!DNL libjsafe.so] 是適當的 [!DNL jsafe.dll]。
   這些程式庫可供您在程式庫資料 [!DNL thirdparty] 夾中使用。
1. 將其中一個 [!DNL adobe-flashaccess-certs] jar檔案放在類路徑上。

       此JAR檔案不包含在WAR檔案中；必須將其顯式添加到類路徑中。
   
   * 開發伺服器——僅應使用 [!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生產伺服器——僅應使用 [!DNL adobe-flashaccess- certs.jar]

分發包括包 [!DNL shared] 括jar檔案和預配置檔案的檔案 [!DNL AdobeInitial.properties] 夾。 Adobe建議您透過檔案將這些項目 `common.loader` 新增至 [!DNL catalina.properties] 中。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


