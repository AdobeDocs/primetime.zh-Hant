---
title: Adobe Primetime身份驗證（可選）
description: Adobe Primetime身份驗證（可選）
copied-description: true
exl-id: 59fbbefa-0c84-474a-ace9-141b50ad5f5f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Adobe Primetime身份驗證（可選） {#adobe-primetime-authentication-optional}

如果用於封裝內容的DRM策略是匿名策略，則將向所有許可證請求頒發許可證。 可選地，Mighide Cloud DRM還支援通過Adobe Primetime驗證進行驗證。 如果啟用此功能，則除非客戶端設備先獲得黃金時段驗證令牌並通過相應客戶端API將其本地設定( `setAuthenticationToken`)，用於設定自定義身份驗證令牌。 有關將黃金時段身份驗證整合到您的身份驗證工作流中的詳細資訊，請參閱： [Adobe Primetime驗證。](https://tve.helpdocsonline.com/home)

在獲取許可證期間，如果DRM策略聲明需要Primetime驗證，則許可證伺服器將分析並驗證Mighine驗證短媒體令牌。 如果DRM策略指定 `ResourceID` 或 `RequestorID`，許可證伺服器還將根據這些屬性驗證令牌。 如果未設定這些屬性，則許可證伺服器將在令牌驗證期間將屬性指定為「null」。 僅當令牌驗證成功時，才會頒發許可證；否則，客戶端將派送具有305個子錯誤代碼（用戶未授權）的3328 DRMErrorEvent。

必須在用於打包注定需要黃金時段身份驗證的內容的策略中指定黃金時段身份驗證參數。

相關物業包括：

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>當將黃金時間驗證與(DRM)許可證輪換功能結合使用時，請記住黃金時間驗證短媒體令牌(SMT)具有短的有效日期。 如果您的應用程式計畫使用許可證輪換(例如， *封鎖* 使用案例)，應用程式必須瞭解這一點並在轉換許可證之前刷新其Mighaine身份驗證短媒體令牌。
