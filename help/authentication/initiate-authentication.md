---
title: 啟動身份驗證
description: 啟動身份驗證
exl-id: 55dddd29-68d6-4aae-8744-307fea285e29
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 啟動身份驗證 {#initiate-authentication}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## REST API終結點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 說明 {#description}

通過通知MVPD選擇事件啟動驗證過程。 在黃金時段驗證資料庫上建立記錄，當從MVPD接收到成功響應時對其進行協調。 



| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | AuthN模組 | 1。requestor_id（必需）</br>2.  mso_id（必需）</br>3.  reg_code（必需）</br>4.  domain_name（必需）</br>5.  noflash=true  </br>    （必需，剩餘參數）</br>6。  no_iframe=true（強制，殘餘參數）</br>7。  額外參數（可選）</br>8.  redirect_url（必需） | GET | 「登錄Web應用」將重定向到MVPD登錄頁。 | 302用於完全重定向實施 |

{style="table-layout:auto"}


| 輸入參數 | 說明 |
| --- | --- |
| 請求者ID | 此操作有效的程式設計師請求者。 |
| mso_id | 此操作對其有效的MVPD ID。 |
| reg_code | 雷吉公司生成的註冊碼。 |
| 域名 | 原始域。 |
| 重定向/url | 驗證完成後登錄Webapp重定向url。 |

{style="table-layout:auto"}

</br>

>[!IMPORTANT]
> 
>**重要提示：必需參數 —** 無論客戶端實施如何，上述所有參數都是必需的。
>
>
>示例：    
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
>**重要提示：可選參數**
>
>該調用還可包含啟用其他功能的可選參數，如：
>
> * 一般\_data — 啟用 [促銷臨時傳遞](/help/authentication/promotional-temp-pass.md)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **注釋** {#notes}

* 的值 `domain_name` 必須將參數設定為通過Mogfire身份驗證註冊的域名之一。 有關詳細資訊，請參閱 [註冊和初始化](/help/authentication/programmer-overview.md)。

* [避免在/authenticate請求中使用&#39;&amp;&#39;reg\_code（技術說明）](/help/authentication/clientless-avoid-using-reg-code-in-authenticate-request.md)

* 的 `redirect_url` 參數必須是按順序排列的最後一個

* 的值 `redirect_url` 參數必須是URL編碼
