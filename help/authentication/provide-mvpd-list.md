---
title: 提供MVPD清單
description: 提供MVPD清單
exl-id: db2d8f19-d0b9-4195-bf0b-f9de0d96062b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 提供MVPD清單 {#provide-mvpd-list}

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

返回請求方的已配置MVPD清單。

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestorId}</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | 黃金時段驗證 | 1。請求者</br>    （路徑元件）</br>_2.  deviceType（不建議使用）_ | GET | 包含MVPD清單的XML或JSON。 | 200 |

{style="table-layout:auto"}


| 輸入參數 | 說明 |
| --------------- | ------------------------------------------------------------- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| *設備類型* | 設備類型。 |

{style="table-layout:auto"}

### 示例響應 {#sample-response}

與現有MVPD XML對/config servlet的響應相同

注：配置為使用平台SSO的所有MVPD在其相應節點(JSON/XML)中將具有以下額外屬性：

* **enablePlatformServices（布爾型）:** 指示是否通過平台SSO整合此MVPD的標誌
* **boardingStatus（字串）:** 指示MVPD是否完全支援平台SSO(SUPPORTED)或MVPD是否僅出現在平台選取器(PICKER)中的標誌
* **displayInPlatformPicker（布爾型）:** 此MVPD是否出現在平台選取器中
* **platformMappingId（字串）:** 平台所知的此MVPD的標識符
* **requiredMetadataFields（字串陣列）:** 成功登錄時，用戶元資料欄位預期可用
