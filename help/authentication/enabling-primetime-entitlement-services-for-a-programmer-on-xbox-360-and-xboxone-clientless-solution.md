---
title: 為Xbox 360和XboxOne無客戶端上的程式啟用Primetime權限服務
description: 為Xbox 360和XboxOne無客戶端上的程式啟用Primetime權限服務
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# 為Xbox 360和XboxOne無客戶端上的程式啟用Primetime權限服務 {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。




1. 程式設計師通過提供以下資訊建立Zendesk票證，以便為Primetime身份驗證無客戶端解決方案啟用Xbox 360/One:

   1. 平台：例如Xbox 360、Xbox One

   1. 請求者ID:例如netgeo、CNN等

1. Adobe將建立X509證書，並在其末端配置私鑰和密碼。

1. Adobe會在票證或透過電子郵件，將公開憑證（X509憑證）提供給程式師。

1. 程式設計人員隨後需要在GDNP門戶中安裝該公共證書，以便註冊到Microsoft的應用。

1. 程式設計師將分別從Microsoft Xbox Live服務中請求XboxOne或360的JWT(Java Web Token)或STS Token，該服務將使用步驟3中提供的X509公共證書進行加密。

1. 這些代號包含Xbox裝置的唯一deviceId。 使用&#39;x&#39;參數在授權標題中加入代號（JWT或STS），如下所示：

   1. 對於Xbox 360，在傳送至Primetime付費電視驗證之前，XSTS代號必須經過Base64編碼。
   1. 若為Xbox One,JWT已正確編碼，因此不應進行額外編碼。 

1. 來自Xbox裝置的所有API呼叫都應包含授權標題，且x參數中帶有上述代號。

 

>[!NOTE]
>
>Xbox尤其具有一些與數字簽名相關的獨特要求。 XSTS代號中包含XBox主控台的裝置ID。  對於Xbox 360，這是加密的SAML斷言；對於Xbox One，這是加密的JWT。 XBox主控台應用程式會傳送整個XSTS代號至Primetime付費電視驗證。 Primetime付費電視驗證會使用其公開金鑰解密Token、剖析Token，然後從中擷取deviceId。

>[!NOTE]
>
>由於XSTS代號的長度過長，XBox主控台有技術限制：它無法將代號以HTTPGET參數的形式傳送至Primetime付費電視驗證API。 為此，Primetime付費電視驗證可讓您在呼叫API時，將XSTS代號作為HTTP標題「授權」的一部分傳送。 XSTS代號必須使用來自Primetime付費電視驗證頒發給程式設計師的X.509憑證的公開金鑰進行加密。 Primetime付費電視驗證會儲存相關聯的私密金鑰，並使用該金鑰解密XSTS代號，並從中擷取deviceId。  


