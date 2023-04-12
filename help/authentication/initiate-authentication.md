---
title: 啟動驗證
description: 啟動驗證
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# 啟動驗證 {#initiate-authentication}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 重設API端點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 說明 {#description}

通知MVPD選擇事件，以啟動驗證過程。 在Primetime驗證資料庫上建立記錄，當從MVPD收到成功回應時調解。 



| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | AuthN模組 | 1.requestor_id（必填）</br>2.  mso_id（必填）</br>3.  reg_code（必要）</br>4.  domain_name（必填）</br>5。  noflash=true -  </br>    （強制，殘餘參數）</br>6.  no_iframe=true（必要，殘餘參數）</br>7.  額外參數（可選）</br>8.  redirect_url（必要） | GET | 登入Web應用程式會重新導向至MVPD登入頁面。 | 302，用於完整重新導向實作 |

{style="table-layout:auto"}


| 輸入參數 | 說明 |
| --- | --- |
| requestor_id | 此操作對其有效的程式設計師請求者。 |
| mso_id | 此操作對其有效的MVPD ID。 |
| reg_code | Reggie服務生成的註冊碼。 |
| domain_name | 原始網域。 |
| redirect_url | 驗證完成後的登入網頁應用程式重新導向url。 |

{style="table-layout:auto"}

</br>

>[!IMPORTANT]
> 
>**重要：強制參數 —** 無論是否實作用戶端，上述所有參數都為必要項目。
>
>
>範例：    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**重要：選用參數**
>
>呼叫也可包含可啟用其他功能的選用參數，例如：
>
> * generic\_data — 啟用 [促銷TempPass](/help/authentication/promotional-temp-pass.md)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **附註** {#notes}

* 的值 `domain_name` 參數必須設為透過Primetime驗證註冊的網域名稱之一。 如需詳細資訊，請參閱 [註冊和初始化](/help/authentication/programmer-overview.md).

* [避免在/authenticate請求中使用&#39;&amp;&#39;reg\_code（技術說明）](/help/authentication/clientless-avoid-using-reg-code-in-authenticate-request.md)

* 此 `redirect_url` 參數必須是順序中的最後一個

* 的值 `redirect_url` 參數必須是URL編碼


