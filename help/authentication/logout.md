---
title: 啟動註銷
description: 啟動註銷
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 啟動註銷 {#initiate-logout}

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

從儲存中刪除AuthN和AuthZ令牌。


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/logout | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求</br>2.  設備ID（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  _設備類型_</br> 5.  _設備用戶_ （不建議使用）</br>6。  _應用ID_ （不建議使用） | DELETE | 無 | 204 |


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br>請參閱中的完整詳細資訊 [傳遞設備和連接資訊](http://tve.helpdocsonline.com/passing-device-information)。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。</br></br>**注釋**：如果使用，則deviceUser的值應與 [建立註冊代碼](http://tve.helpdocsonline.com/registration-code-request) 請求。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 如果使用， `appId` 應具有與 [建立註冊代碼](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) 請求。 |

>[!IMPORTANT]
> 
>註銷呼叫當前具有以下限制：它會從儲存中清除AuthN和AuthZ令牌（即在程式設計師/黃金時段身份驗證端），但 **不** 調用MVPD註銷終結點。 

### [返回REST API參考](/help/authentication/rest-api-reference.md)
