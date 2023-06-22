---
title: 範例使用者端請求
description: 範例使用者端請求
copied-description: true
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 範例使用者端請求{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具收集範例使用者端請求的資料庫。 您應使用個人化傳輸認證，在設定個人化伺服器後擷取使用者端請求。 然後，您可以傳送這些使用者端請求(透過 *curl* 或其他工具)，驗證伺服器是否正常運作。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您也可以在伺服器設定變更或ECI / CRL更新後，再次傳送這些要求。

您也應使用成功的個人化交易適當地更新「個人化統計資料」頁面。
