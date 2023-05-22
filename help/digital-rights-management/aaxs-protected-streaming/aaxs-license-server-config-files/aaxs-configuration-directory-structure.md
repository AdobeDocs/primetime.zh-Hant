---
description: 「受保護流」的Adobe Access Server需要兩種類型的配置檔案：全局配置檔案(flashaccess-global.xml)和每個租戶的租戶配置檔案(flashaccess-tenant.xml)。
title: 配置目錄結構
exl-id: 6561c001-798c-4503-8afb-93580d957372
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 許可證伺服器配置檔案和配置目錄結構 {#configuration-directory-structure}

「受保護流式處理的Adobe Access Server」需要兩種類型的配置檔案：全局配置檔案(flashaccess-global.xml)和每個租戶的租戶配置檔案(flashaccess-tenant.xml)。

編輯配置檔案後，Adobe建議使用Adobe Access Server提供的用於受保護流的實用程式來驗證檔案的格式是否正確。 有關詳細資訊，請參閱「」[配置驗證程式](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)。

為避免在配置檔案中以明文方式提供密碼，必須對全局配置檔案和租戶配置檔案中指定的所有密碼進行加密。 有關加密密碼的詳細資訊，請參閱「」[密碼加擾器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)。

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
