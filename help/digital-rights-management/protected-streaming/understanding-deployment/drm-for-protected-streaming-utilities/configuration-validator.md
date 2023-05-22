---
description: Adobe建議，如果在配置檔案中進行更改，則應在啟動伺服器之前運行配置驗證程式實用程式。 此實用程式可以在請求處理過程中導致故障之前，及早檢測大多數配置錯誤。
title: 配置驗證程式
exl-id: 41d0a926-4e12-442c-886e-5f12cf10eed8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 配置驗證程式{#configuration-validator}

Adobe建議，如果在配置檔案中進行更改，則應在啟動伺服器之前運行配置驗證程式實用程式。 此實用程式可以在請求處理過程中導致故障之前，及早檢測大多數配置錯誤。

要運行驗證程式，請鍵入：

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

或

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

對於每個許可證伺服器配置檔案，驗證程式可以執行基於檔案的驗證，這確保XML檔案格式良好並符合配置檔案模式。

要對全局配置檔案執行基於檔案的驗證，請鍵入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要對租戶配置檔案執行基於檔案的驗證，請鍵入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

驗證程式還可以執行基於部署的驗證。 除了檢查與架構的一致性外，此驗證級別還驗證您指定的值是否有效。 例如，它可確保引用的檔案存在。

可以在以下級別執行基於部署的驗證：

* `Tenant`  — 驗證特定租戶的配置檔案和憑據。 如果要驗證的配置 `<tenant1>`，類型：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global`  — 驗證所有租戶的全局配置檔案和租戶驗證。 如果要執行基於全局部署的驗證，請鍵入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```
