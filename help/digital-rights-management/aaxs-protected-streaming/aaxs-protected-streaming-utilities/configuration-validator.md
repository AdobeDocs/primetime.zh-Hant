---
title: 配置驗證程式
description: 配置驗證程式
copied-description: true
exl-id: 9b73e107-6ab7-4089-b415-0af8c9f86995
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 配置驗證程式 {#configuration-validator}

Adobe建議在對配置檔案進行任何更改之前，先運行配置驗證程式實用程式，然後啟動伺服器。 此實用程式可以在請求處理過程中導致故障之前，及早檢測大多數配置錯誤。

要運行驗證程式，請使用以下命令：

```
Validator.bat options  
```

或命令：

```
java -jar libs/flashaccess-validator.jar options 
```

對於每個許可證伺服器配置檔案，驗證程式可以執行基於檔案的驗證，這確保XML檔案格式良好並符合配置檔案模式。 要對全局配置檔案執行基於檔案的驗證，請運行以下命令：

```
Validator --file path/flashaccess-global.xml --global
```

要對租戶配置檔案執行基於檔案的驗證，請運行以下命令：

```
Validator --file path/flashaccess-tenant.xml --tenant
```

驗證程式還可以執行基於部署的驗證；除了檢查與架構的一致性外，此驗證級別還檢查指定的值是否有效（例如，它確保引用的檔案存在）。 基於部署的驗證可以在兩個級別執行：

* 租戶 — 驗證特定租戶的配置檔案和憑據。 要驗證&quot;tenant1&quot;的配置，請運行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 全局 — 驗證所有租戶的全局配置檔案和租戶驗證。 要執行基於全局部署的驗證，請運行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
