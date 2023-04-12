---
title: 臨時通行證和促銷臨時通行證的免費預覽
description: 臨時通行證和促銷臨時通行證的免費預覽
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 臨時通行證和促銷臨時通行證的免費預覽 {#free-preview-for-temp-pass-and-promotional-temp-pass}

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

允許為Temp Pass和Promotion Temp Pass建立驗證令牌，而不需要第二個螢幕。


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.requestor_id（必填）</br>    </br>2.  deviceId（必要）</br>    </br>3.  mso_id（必填）</br>    </br>4.  domain_name（必填）</br>    </br>5.  device_info/X-Device-Info（強制）</br>6.  deviceType</br>    </br>7.  deviceUser（已過時）</br>    </br>8.  appId（已過時）</br>    </br>9.  generic_data（可選） | POST | 成功的回應將是「204無內容」，表示Token已成功建立，且已準備好用於驗證流程。 | 204 — 無內容   </br>400 — 錯誤請求 |

<div>


| 輸入參數 | 說明 |
| --- | --- |
| requestor_id | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| mso_id | 此操作對其有效的MVPD ID。 |
| domain_name | 將為其授予令牌的域名。 授權Token時，會與服務提供者的網域進行比較。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便可以針對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [使用無客戶端設備類型參數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。</br></br>**附註**：若已使用，deviceUser的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 若已使用， `appId` 的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| generic_data | 用於限制促銷臨時通行證的代號範圍。 |


### [返回REST API參考](/help/authentication/rest-api-reference.md)
