---
title: Adobe Primetime驗證（選用）
description: Adobe Primetime驗證（選用）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Adobe Primetime驗證（選用） {#adobe-primetime-authentication-optional}

如果用於封裝內容的DRM原則是匿名原則，則會向所有授權請求頒發授權。 或者，Primetime Cloud DRM也支援透過Adobe Primetime驗證來驗證。 如果啟用此功能，除非使用者端裝置先取得Primetime驗證Token，並透過適當的使用者端API在本機設定它，否則不會核發授權( `setAuthenticationToken`)以設定自訂驗證Token。 如需將Primetime驗證整合至驗證工作流程的詳細資訊，請參閱： [Adobe Primetime驗證。](https://tve.helpdocsonline.com/home)

在取得授權期間，如果DRM政策指出需要Pri即時驗證，則授權伺服器會剖析並驗證Primetime驗證Short Media Token。 如果DRM政策指定 `ResourceID` 或 `RequestorID`，授權伺服器也會針對這些屬性驗證Token。 如果未設定，授權伺服器會在權杖驗證期間將屬性指定為「null」。 只有當權杖驗證成功時，才會核發授權；否則，使用者端將會傳送具有305子錯誤碼（使用者未授權）的3328 DRMErrorEvent。

Primetime驗證引數必須在用於封裝預定需要Primetime驗證的內容的原則中指定。

相關屬性包括：

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>在搭配使用Primetime驗證與(DRM)授權輪換功能時，請記住Primetime驗證短媒體權杖(SMT)的有效日期較短。 如果您的應用程式計畫使用授權輪換(例如，支援 *中斷* 使用案例)，應用程式必須瞭解這點，並更新其Primetime驗證Short Media Token，才能輪換其授權。
