---
title: 使用者中繼資料
description: 使用者中繼資料
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# 使用者中繼資料 {#user-metadata}

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

擷取MVPD共用之已驗證使用者的中繼資料。

<div>


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者</br>2.  deviceId（必要）</br>3.  device_info/X-Device-Info（強制）</br>4.  deviceType</br>5。  deviceUser（已過時）</br>6.  appId（已過時） | GET | 包含使用者中繼資料或錯誤詳細資料（若失敗）的XML或JSON。 | 200 — 成功</br></br>404 — 未找到元資料</br></br>412 — 無效的AuthN代號（例如，過期的代號） |


| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br>請參閱 **傳遞裝置和連線資訊** <!--http://tve.helpdocsonline.com/passing-device-information-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) 使用無用戶端時，以便可以針對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [在傳遞量度中使用無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注意：** 此 `device_info` 會取代此參數。 </br> |
| _deviceUser_ | 裝置使用者識別碼。</br></br>**注意：**若使用， `deviceUser` 的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**注意：** `device_info` 會取代此參數。 若已使用， `appId` 的值應與 **建立註冊代碼** 請求。 |

>[!NOTE]
> 
>驗證流程完成後，應該可以使用用戶元資料資訊，但可以根據授權流程更新，具體取決於MVPD和元資料類型。

</br>

## 範例回應 {#sample-response}

成功呼叫後，伺服器會以XML（預設值）或JSON物件回應，其結構類似於下列所示的結構：

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
              },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
    }
```

物件的根節點會有三個節點：

* **更新**:指定代表上次更新中繼資料的UNIX時間戳記。 在驗證階段產生中繼資料時，伺服器最初會設定此屬性。 後續呼叫（更新中繼資料後）將產生遞增的時間戳記。

* **資料**:包含實際的中繼資料值。

* **加密**:列出加密屬性的陣列。 要解密特定元資料值，程式設計師必須對元資料執行Base64解碼，然後使用其自己的私鑰對生成的值應用RSA解密(Adobe使用程式設計師的公共證書對伺服器上的元資料進行加密)。

發生錯誤時，伺服器會傳回XML或JSON物件，用以指定詳細的錯誤訊息。

如需詳細資訊，請參閱 [使用者中繼資料](/help/authentication/user-metadata.md).

### [返回REST API參考](/help/authentication/rest-api-reference.md).
