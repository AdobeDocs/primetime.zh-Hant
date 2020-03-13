---
seo-title: Adobe Primetime驗證（選用）
title: Adobe Primetime驗證（選用）
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime驗證（選用） {#adobe-primetime-authentication-optional}

如果用來封裝內容的DRM政策是匿名政策，則會向所有授權要求核發授權。 或者，Primetime Cloud DRM也支援透過Adobe Primetime驗證的驗證。 如果啟用此功能，除非用戶端裝置先取得Primetime驗證Token，並透過適當的用戶端API( `setAuthenticationToken`)在本機設定它以設定自訂驗證Token，否則將不會核發授權。 有關將Primetime驗證整合至驗證工作流程的詳細資訊，請參閱： [Adobe Primetime驗證。](https://tve.helpdocsonline.com/home)

在取得授權期間，如果DRM政策指出需要Primeme驗證，授權伺服器會剖析並驗證Primetime驗證Short Media Token。 如果DRM策略指定 `ResourceID` 或 `RequestorID`，則許可證伺服器還將根據這些屬性驗證令牌。 如果未設定，授權伺服器會在Token驗證期間將屬性指定為「null」。 只有當Token驗證成功時，才會核發授權；否則，客戶機將派送具有305個子錯誤代碼（用戶未授權）的3328 DRMErrorEvent。

Primetime驗證參數必須在用來封裝目的地需要Primetime驗證的內容的原則中指定。

相關物業包括：

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>當搭配(DRM)授權旋轉功能使用Primetime驗證時，請記住Primetime驗證簡短媒體代號(SMT)的有效日期較短。 如果您的應用程式打算使用授權輪替（例如，支援封鎖期使用案例），則應用程式必須知道此點，並在輪替授權前重新整理其Primetime驗證短媒體Token。 **