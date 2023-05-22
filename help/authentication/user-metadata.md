---
title: 用戶元資料
description: 用戶元資料
exl-id: 3d7b6429-972f-4ccb-80fd-a99870a02f65
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 用戶元資料 {#user-metadata}

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

檢索MVPD共用的關於已驗證用戶的元資料。

<div>


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求</br>2.  設備ID（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  設備類型</br>5.  deviceUser（不建議使用）</br>6。  appId（不建議使用） | GET | 包含用戶元資料或錯誤詳細資訊（如果失敗）的XML或JSON。 | 200 — 成功</br></br>404 — 未找到元資料</br></br>412 — 無效的AuthN令牌（例如，過期的令牌） |


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br>請參閱中的完整詳細資訊 **傳遞設備和連接資訊** <!--http://tve.helpdocsonline.com/passing-device-information-->。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [在Pass計量中使用無客戶端設備類型參數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注：** 的 `device_info` 替換此參數。 </br> |
| _設備用戶_ | 設備用戶標識符。</br></br>**注意：**如果使用， `deviceUser` 應具有與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注意：** `device_info` 替換此參數。 如果使用， `appId` 應具有與 **建立註冊代碼** 請求。 |

>[!NOTE]
> 
>驗證流完成後，用戶元資料資訊應該可用，但可以根據MVPD和元資料類型在授權流上更新。

</br>

## 示例響應 {#sample-response}

成功調用後，伺服器將使用XML（預設）或JSON對象進行響應，其結構與下面所示的類似：

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

在對象的根處將有三個節點：

* **更新**:指定表示上次更新元資料的時間的UNIX時間戳。 在驗證階段生成元資料時，伺服器將首先設定此屬性。 後續調用（更新元資料後）將產生遞增的時間戳。

* **資料**:包含實際元資料值。

* **加密**:列出加密屬性的陣列。 要解密特定元資料值，程式設計師必須對元資料執行Base64解碼，然後使用其自己的私鑰對結果值應用RSA解密(Adobe使用程式設計師的公共證書對伺服器上的元資料進行加密)。

如果出現錯誤，伺服器將返回指定詳細錯誤消息的XML或JSON對象。

有關詳細資訊，請參見 [用戶元資料](/help/authentication/user-metadata.md)。

### [返回REST API參考](/help/authentication/rest-api-reference.md)。
