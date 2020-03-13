---
seo-title: 用戶端要求範例
title: 用戶端要求範例
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 用戶端要求範例{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具，收集用戶端要求範例的程式庫。 您應使用個人化傳輸憑證在個人化伺服器設定後，擷取用戶端要求。 然後，您可以(透過 *curl* 或其他工具)將這些用戶端要求傳送至個人化伺服器的端點，以確認伺服器已正常啟動並執行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您也可能希望在任何伺服器組態變更或ECI / CRL更新後，再次傳送這些要求。

您還應該使用成功的個性化事務適當更新「個性化統計資訊」頁。
