---
title: 啟動登出
description: 啟動登出
exl-id: 9625b5a2-31d9-4e20-8703-4a9e4eeb1618
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 啟動登出 {#initiate-logout}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## REST API端點 {#clientless-endpoints}

&lt;reggie_fqdn>：

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 分段 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>：

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 分段 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 說明 {#description}

從儲存空間中移除AuthN和AuthZ權杖。


| 端點 | 已呼叫  </br>作者： | 輸入   </br>引數 | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | 串流應用程式</br></br>或</br></br>程式設計師服務 | 1.請求者</br>2.  deviceId （必要）</br>3.  device_info/X-Device-Info （必要）</br>4.  _deviceType_</br> 5.  _deviceuser_ （已棄用）</br>6.  _appId_ （已棄用） | DELETE | 無 | 204 |


| 輸入引數 | 說明 |
| --- | --- |
| 請求者 | 此作業有效的程式設計員requestorId。 |
| deviceId | 裝置ID位元組。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**注意**：此引數可以作為URL引數傳遞，但由於此引數潛在的大小以及GETURL的長度限制，它應該在http標頭中作為X-Device-Info傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置型別（例如Roku、PC）。</br></br>如果此引數設定正確，ESM會提供 [依裝置型別劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clienless時，因此可針對Roku、AppleTV、Xbox等執行不同型別的分析。</br></br>另請參閱 [在通過的量度中使用無使用者端裝置型別引數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**：device_info會取代此引數。 |
| _deviceuser_ | 裝置使用者識別碼。</br></br>**注意**：若使用，deviceUser的值應與中的相同 [建立註冊代碼](/help/authentication/registration-code-request.md) 要求。 |
| _appId_ | 應用程式id/名稱。 </br></br>**注意**：device_info會取代此引數。 若已使用， `appId` 應具有與中的相同的值 [建立註冊代碼](/help/authentication/registration-code-request.md) 要求。 |

>[!IMPORTANT]
> 
>登出呼叫目前具有下列限制：它會從儲存空間中清除AuthN和AuthZ權杖（例如在程式設計師/Primetime驗證端），但 **不會** 呼叫MVPD登出端點。
