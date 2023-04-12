---
title: 提供MVPD清單
description: 提供MVPD清單
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 提供MVPD清單 {#provide-mvpd-list}

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

傳回要求者已設定的MVPD清單。

| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Primetime驗證 | 1.申請人</br>    （路徑元件）</br>_2.  deviceType（已廢止）_ | GET | 包含MVPD清單的XML或JSON。 | 200 |

{style="table-layout:auto"}


| 輸入參數 | 說明 |
| --------------- | ------------------------------------------------------------- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| *deviceType* | 裝置類型。 |

{style="table-layout:auto"}

### 範例回應 {#sample-response}

與對/config servlet的現有MVPD XML響應相同

注意：所有設定為使用Platform SSO的MVPD，在其對應節點(JSON/XML)中都會有下列額外屬性：

* **enablePlatformServices（布林值）:** 此旗標可指出此MVPD是否透過Platform SSO整合
* **boardingStatus（字串）:** 此旗標可指出MVPD是否完全支援平台SSO（支援），或MVPD是否僅出現在平台選擇器(PICKER)中
* **displayInPlatformPicker（布林值）:** 此MVPD是否出現在平台選擇器中
* **platformMappingId(string):** 平台所知的此MVPD的標識符
* **requiredMetadataFields（字串陣列）:** 成功登入時預期可使用的使用者中繼資料欄位
