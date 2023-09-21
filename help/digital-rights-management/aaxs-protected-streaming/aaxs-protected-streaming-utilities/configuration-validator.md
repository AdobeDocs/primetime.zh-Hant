---
title: 設定驗證器
description: 設定驗證器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 設定驗證器 {#configuration-validator}

Adobe建議您在變更組態檔之前，先執行組態驗證器公用程式，再啟動伺服器。 此公用程式可及早偵測到大部分的組態錯誤，以免在要求處理期間導致失敗。

若要執行驗證器，請使用命令：

```
Validator.bat options  
```

或指令：

```
java -jar libs/flashaccess-validator.jar options 
```

對於每個許可證伺服器組態檔案，「驗證器」都可以執行檔案式驗證，以確保XML檔案的格式正確且符合組態檔案架構。 若要對全域組態檔案執行檔案式驗證，請執行以下命令：

```
Validator --file path/flashaccess-global.xml --global
```

若要對租使用者設定檔案執行檔案式驗證，請執行以下命令：

```
Validator --file path/flashaccess-tenant.xml --tenant
```

驗證器也可以執行以部署為基礎的驗證；除了檢查是否符合結構描述之外，此層級的驗證也會檢查指定的值是否有效（例如，它確保參考的檔案存在）。 部署型驗證可在兩個層級執行：

* 租使用者 — 驗證特定租使用者的組態檔與認證。 若要驗證「tenant1」的設定，請執行命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 全域 — 驗證所有租使用者的全域組態檔和租使用者驗證。 若要執行全域部署型驗證，請執行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
