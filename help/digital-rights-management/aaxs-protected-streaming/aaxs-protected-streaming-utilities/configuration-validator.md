---
seo-title: 配置驗證器
title: 配置驗證器
uuid: 60ebd35c-290a-4f08-9bd0-178903857149
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# 配置驗證器{#configuration-validator}

Adobe建議在對配置檔案進行任何更改之前，先運行Configuration Validator實用程式，然後再啟動伺服器。 此公用程式可在請求處理期間，提早偵測大部分的設定錯誤，以免造成失敗。

要運行驗證器，請使用命令：

```
Validator.bat options  
```

或命令：

```
java -jar libs/flashaccess-validator.jar options 
```

對於每個許可證伺服器配置檔案，驗證器可以執行基於檔案的驗證，這可確保XML檔案格式正確，並符合配置檔案模式。 要對全局配置檔案執行基於檔案的驗證，請運行以下命令：

```
Validator --file path/flashaccess-global.xml --global
```

要對租用戶配置檔案執行基於檔案的驗證，請運行以下命令：

```
Validator --file path/flashaccess-tenant.xml --tenant
```

Validator還可以執行基於部署的驗證；除了檢查與架構的符合性外，此驗證級別還檢查指定的值是否有效（例如，它確保引用的檔案存在）。 可在兩個層級執行部署型驗證：

* 租用戶— 驗證特定租用戶的設定檔案和認證。 要驗證&quot;tenant1&quot;的配置，請運行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* 全球— 驗證所有租戶的全域設定檔案和租用戶驗證。 要執行基於部署的全局驗證，請運行以下命令：

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

