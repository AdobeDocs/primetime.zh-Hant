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

允許為臨時通過和促銷臨時通過建立身份驗證令牌，而不需要第二個螢幕。


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。requestor_id（必需）</br>    </br>2.  設備ID（必需）</br>    </br>3.  mso_id（必需）</br>    </br>4.  domain_name（必需）</br>    </br>5.  device_info/X-Device-Info（必需）</br>6。  設備類型</br>    </br>7.  deviceUser（不建議使用）</br>    </br>8.  appId（不建議使用）</br>    </br>9.  generic_data（可選） | POST | 成功的響應將是204無內容，表示令牌已成功建立並準備用於驗證流。 | 204 — 無內容   </br>400 — 錯誤請求 |

<div>


| 輸入參數 | 說明 |
| --- | --- |
| 請求者ID | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| mso_id | 此操作對其有效的MVPD ID。 |
| 域名 | 將為其授予令牌的域名。 當授予授權令牌時，將與服務提供商的域進行比較。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [使用無客戶端設備類型參數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。</br></br>**注釋**：如果使用，則deviceUser的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 如果使用， `appId` 應具有與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| 泛型資料 | 用於限制促銷臨時傳遞的令牌的範圍。 |


### [返回REST API參考](/help/authentication/rest-api-reference.md)
