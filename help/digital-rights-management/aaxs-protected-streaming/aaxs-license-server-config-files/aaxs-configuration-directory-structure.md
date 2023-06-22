---
description: 適用於受保護串流的Adobe Access Server需要兩種型別的設定檔：全域設定檔(flashaccess-global.xml)和每個租使用者的租使用者設定檔(flashaccess-tenant.xml)。
title: 組態目錄結構
exl-id: 6561c001-798c-4503-8afb-93580d957372
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 授權伺服器組態檔與組態目錄結構 {#configuration-directory-structure}

適用於受保護串流的Adobe Access Server需要兩種型別的設定檔：全域設定檔(flashaccess-global.xml)和每個租使用者的租使用者設定檔(flashaccess-tenant.xml)。

編輯設定檔案後，Adobe建議使用Adobe Access Server for Protected Streaming隨附的公用程式，驗證檔案格式正確。 如需詳細資訊，請參閱「[設定驗證器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)「。

為了避免在設定檔案中以純文字提供密碼，全域和租使用者設定檔案中指定的所有密碼都必須加密。 如需加密密碼的詳細資訊，請參閱「[密碼加擾器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)「。

組態目錄具有下列結構：

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
