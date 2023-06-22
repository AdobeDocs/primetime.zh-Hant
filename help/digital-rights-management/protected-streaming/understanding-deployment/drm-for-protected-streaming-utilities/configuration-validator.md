---
description: Adobe建議您在組態檔中進行變更時，在啟動伺服器之前，先執行Configuration Validator公用程式。 此公用程式可及早偵測到大部分的設定錯誤，以免在要求處理期間導致失敗。
title: 設定驗證器
exl-id: 41d0a926-4e12-442c-886e-5f12cf10eed8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 設定驗證器{#configuration-validator}

Adobe建議您在組態檔中進行變更時，在啟動伺服器之前，先執行Configuration Validator公用程式。 此公用程式可及早偵測到大部分的設定錯誤，以免在要求處理期間導致失敗。

若要執行驗證器，請輸入：

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

對於每個許可證伺服器組態檔，「驗證器」都可以執行檔案型驗證，以確保XML檔案的格式正確，並且符合組態檔案架構。

若要對全域組態檔案執行檔案式驗證，請鍵入：

```
Validator --<file path>/flashaccess-global.xml --global
```

若要對租使用者設定檔案執行檔案式驗證，請輸入：

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

驗證器也可以執行部署型驗證。 除了檢查是否符合結構描述外，此層級的驗證也會驗證您指定的值是否有效。 例如，它可確保參考檔案存在。

部署型驗證可在下列層級執行：

* `Tenant`  — 驗證特定租使用者的設定檔和認證。 如果您想要驗證設定 `<tenant1>`，型別：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global`  — 驗證所有租使用者的全域設定檔和租使用者驗證。 如果要執行全域部署型驗證，請輸入：

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```
