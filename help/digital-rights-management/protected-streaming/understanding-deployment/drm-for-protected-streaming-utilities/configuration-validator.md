---
description: Adobe建議您在設定檔中進行變更時，在啟動伺服器之前，先執行Configuration Validator公用程式。 此公用程式可在請求處理期間，提早偵測大部分的設定錯誤，以免造成失敗。
seo-description: Adobe建議您在設定檔中進行變更時，在啟動伺服器之前，先執行Configuration Validator公用程式。 此公用程式可在請求處理期間，提早偵測大部分的設定錯誤，以免造成失敗。
seo-title: 配置驗證器
title: 配置驗證器
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置驗證器{#configuration-validator}

Adobe建議您在設定檔中進行變更時，在啟動伺服器之前，先執行Configuration Validator公用程式。 此公用程式可在請求處理期間，提早偵測大部分的設定錯誤，以免造成失敗。

要運行驗證器，請鍵入：

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

對於每個許可證伺服器配置檔案，驗證器可以執行基於檔案的驗證，這可確保XML檔案格式正確，並符合配置檔案模式。

要對全局配置檔案執行基於檔案的驗證，請鍵入：

```
Validator --<file path>/flashaccess-global.xml --global
```

要對租用戶配置檔案執行基於檔案的驗證，請鍵入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

Validator還可以執行基於部署的驗證。 除了檢查與方案的符合性外，此驗證級別還驗證您指定的值是否有效。 例如，它可確保引用的檔案存在。

可在下列層級執行部署型驗證：

* `Tenant` — 驗證特定租用戶的設定檔案和認證。 如果要驗證配置，請 `<tenant1>`鍵入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — 驗證所有租戶的全域設定檔案和租用戶驗證。 如果要執行基於全局部署的驗證，請鍵入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

