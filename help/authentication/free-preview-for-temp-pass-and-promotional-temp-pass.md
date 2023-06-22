---
title: 臨時通行證和促銷臨時通行證的免費預覽
description: 臨時通行證和促銷臨時通行證的免費預覽
exl-id: c584bf0c-15c4-4a4d-b6a2-8d15ee786fe3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# 臨時通行證和促銷臨時通行證的免費預覽 {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

允許為Temp Pass和Promotional Temp Pass建立驗證Token，而不需要第二個畫面。


| 端點 | 已呼叫  </br>作者： | 輸入   </br>引數 | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | 串流應用程式</br></br>或</br></br>程式設計師服務 | 1. requestor_id （必要）</br>    </br>2.  deviceId （必要）</br>    </br>3.  mso_id （必要）</br>    </br>4.  domain_name （必要）</br>    </br>5.  device_info/X-Device-Info （必要）</br>6.  deviceType</br>    </br>7.  deviceUser （已棄用）</br>    </br>8.  appId （已棄用）</br>    </br>9.  generic_data （選用） | POST | 成功的回應將是「204無內容」，這表示已成功建立權杖，且已準備好用於授權流程。 | 204 — 無內容   </br>400 — 錯誤請求 |

<div>


| 輸入引數 | 說明 |
| --- | --- |
| requestor_id | 此作業有效的程式設計員requestorId。 |
| deviceId | 裝置ID位元組。 |
| mso_id | 此作業適用的MVPD ID。 |
| domain_name | 將授與權杖的網域名稱。 在授予授權權杖時，會與服務提供者的網域進行比較。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**注意**：此引數可以作為URL引數傳遞，但由於此引數潛在的大小以及GETURL的長度限制，它應該在http標頭中作為X-Device-Info傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置型別（例如Roku、PC）。</br></br>如果此引數設定正確，ESM會提供 [依裝置型別劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clienless時，因此可針對Roku、AppleTV、Xbox等執行不同型別的分析。</br></br>另請參閱 [使用無使用者端裝置型別引數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意**：device_info會取代此引數。 |
| _deviceuser_ | 裝置使用者識別碼。</br></br>**注意**：若使用，deviceUser的值應與中的相同 [建立註冊代碼](/help/authentication/registration-code-request.md) 要求。 |
| _appId_ | 應用程式id/名稱。 </br></br>**注意**：device_info會取代此引數。 若已使用， `appId` 應具有與中的相同的值 [建立註冊代碼](/help/authentication/registration-code-request.md) 要求。 |
| generic_data | 用於限制促銷臨時傳遞的權杖範圍。 |


### [返回REST API參考](/help/authentication/rest-api-reference.md)
