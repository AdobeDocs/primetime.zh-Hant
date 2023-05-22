---
title: 客戶端請求示例
description: 客戶端請求示例
copied-description: true
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 客戶端請求示例{#sample-client-requests}

您可以使用Charles Proxy或Wireshark等工具收集示例客戶端請求庫。 應使用個性化傳輸憑據在個性化伺服器設定後捕獲客戶端請求。 然後，您可以發送這些客戶端請求(通過 *捲曲* 或其他工具)到個性化伺服器的端點，以驗證伺服器是否正常運行。 例如：

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

您可能還希望在任何伺服器配置更改或ECI / CRL更新後再次發送這些請求。

您還應使用成功的個性化事務處理相應地更新「個性化統計資訊」頁。
