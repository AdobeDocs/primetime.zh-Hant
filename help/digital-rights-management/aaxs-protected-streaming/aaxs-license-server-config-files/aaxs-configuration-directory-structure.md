---
description: 「保護串流Adobe Access Server」需要兩種組態檔：全域組態檔(flashaccess-global.xml)和每個租用戶的租用戶組態檔(flashaccess-tenant.xml)。
title: 配置目錄結構
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 許可證伺服器配置檔案和配置目錄結構{#configuration-directory-structure}

「Adobe Access Server保護串流」需要兩種組態檔：每個租用戶的全域設定檔(flashaccess-global.xml)和租用戶設定檔(flashaccess-tenant.xml)。

編輯配置檔案後，Adobe建議使用「受保護流」的Adobe Access Server提供的實用程式來驗證檔案格式正確。 如需詳細資訊，請參閱「[Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)」。

為避免在配置檔案中以明文形式提供密碼，必須加密全局配置檔案和租用戶配置檔案中指定的所有密碼。 有關加密密碼的詳細資訊，請參閱「[密碼刪除程式](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)」。

配置目錄具有以下結構：

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

