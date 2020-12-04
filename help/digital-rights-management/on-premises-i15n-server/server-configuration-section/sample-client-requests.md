---
seo-title: 用戶端要求範例
title: 用戶端要求範例
uuid: 330d5e3c-1711-4375-bd11-e7702f0cde31
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# 客戶機請求示例{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具，收集用戶端要求範例的程式庫。 您應使用個人化傳輸憑證在個人化伺服器設定後，擷取用戶端要求。 然後，您可以將這些客戶機請求（通過&#x200B;*curl*&#x200B;或其他工具）發送到個性化伺服器的端點，以驗證伺服器是否正常啟動和運行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您也可能希望在任何伺服器組態變更或ECI / CRL更新後，再次傳送這些要求。

您還應該使用成功的個性化事務適當更新「個性化統計資訊」頁。
