---
title: 啟動註銷
description: 啟動註銷
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 啟動註銷 {#initiate-logout}

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

從儲存中移除AuthN和AuthZ代號。


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者</br>2.  deviceId（必要）</br>3.  device_info/X-Device-Info（強制）</br>4.  _deviceType_</br> 5。  _deviceUser_ （已過時）</br>6.  _appId_ （已過時） | DELETE | 無 | 204 |


| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便可以針對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [在傳遞量度中使用無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。</br></br>**附註**：若已使用，deviceUser的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 若已使用， `appId` 的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |

>[!IMPORTANT]
> 
>註銷呼叫當前具有以下限制：它會清除儲存中的AuthN和AuthZ代號（即在程式設計員/Primetime驗證端），但 **不** 呼叫MVPD登出端點。 


