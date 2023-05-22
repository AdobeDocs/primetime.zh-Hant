---
title: 為Xbox 360和XboxOne無客戶端上的程式設計師啟用黃金時段權利服務
description: 為Xbox 360和XboxOne無客戶端上的程式設計師啟用黃金時段權利服務
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 為Xbox 360和XboxOne無客戶端上的程式設計師啟用黃金時段權利服務 {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。




1. 程式設計師通過提供以下資訊建立Zendesk票證，以啟用Xbox 360/One用於黃金時段驗證無客戶端解決方案：

   1. 平台：例如，Xbox 360、Xbox One

   1. 請求者ID:例如netgeo、CNN等。

1. Adobe將建立X509證書，並在其末尾配置私鑰和密碼。

1. Adobe將通過票證或電子郵件向程式設計師提供公共證書（X509證書）。

1. 然後程式設計師需要在GDNP門戶中為註冊到Microsoft的應用程式安裝該公共證書。

1. 然後程式設計師將分別從MicrosoftXbox Live服務請求XboxOne或360的JWT(Java Web Token)或STS Token，該服務將使用步驟3中提供的X509公共證書進行加密。

1. 這些令牌包含Xbox設備的唯一設備ID。 在「授權」標頭中使用「x」參數包括令牌（JWT或STS），如下所示：

   1. 對於Xbox 360,XSTS令牌必須在發送到黃金時段付費電視驗證之前進行Base64編碼。
   1. 對於Xbox One,JWT已正確編碼，因此不應發生額外編碼。 

1. 來自Xbox設備的所有API調用都應包含在x參數中具有上述令牌的授權標頭。

 

>[!NOTE]
>
>Xbox尤其具有一些與數字簽名相關的獨特要求。 XSTS令牌中包含XBox控制台的設備ID。  對於Xbox 360，這是加密的SAML斷言；對於Xbox One，這是加密的JWT。 XBox控制台應用將整個XSTS令牌發送到黃金時段付費電視驗證。 黃金時段付費電視驗證使用其公鑰解密令牌，解析令牌，並從其中提取設備ID。

>[!NOTE]
>
>由於XSTS令牌的長度較大，XBox控制台有一個技術限制：它不能將令牌作為HTTPGET參數發送到Mighipe付費電視驗證API。 為瞭解決這一問題，黃金時段付費電視驗證允許在調用API時將XSTS令牌作為HTTP頭「授權」的一部分發送。 XSTS令牌必須使用從Mogfire付費TV驗證中頒發給程式設計師的X.509證書中的公鑰進行加密。 黃金時段付費電視驗證儲存關聯的私鑰，並使用它解密XSTS令牌並從其中提取設備ID。
