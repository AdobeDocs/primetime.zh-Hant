---
title: 在黃金時段驗證度量中使用無客戶端設備類型參數的好處
description: 在黃金時段驗證度量中使用無客戶端設備類型參數的好處
exl-id: a5004887-d5fa-468e-971b-10806519175b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 在黃金時段驗證度量中使用無客戶端設備類型參數的好處 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 上下文

儘管是可選的，但參數 `deviceType` 無客戶端API（如果存在）用於通過以下方式公開的黃金時段驗證度量 [權利服務監視](/help/authentication/entitlement-service-monitoring-overview.md)。

考慮到 `deviceType` 參數及其 **利益** 在黃金時段驗證指標最初未說明時，本技術說明的範圍是添加有關這些指標的更多資訊。

## 解釋

的 `deviceType` 參數自第一個版本起就存在於Clientless API中，但其對Mighine身份驗證度量的影響在最近的版本中添加。



>[!IMPORTANT]
>
>如果參數 `deviceType` 設定正確，則它具有以下 **利益** 在權利服務監視中：它提供了 [按設備類型分解](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。


有關權利服務監視API的詳細資訊，請參閱 [深入樹，](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 這說明 [尺寸](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) （資源）。

>[!NOTE]
>
>此技術說明的內容也添加到 [無客戶端API](#clientless_device_type)。




## 實施

要充分受益於黃金時段驗證指標，有2種類型 [無客戶端API](#web_srvs_summary) 當前正在使用的，並且需要 `deviceType` 設定：

1. 具有 `regcode` 作為必需參數，並將 `deviceType` 建立時設定的參數 `regcode`，使用以下API調用：
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. 具有 `deviceType` 作為可選參數：
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediaken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

我們的建議是 `deviceType` 為所有API傳遞正確的無客戶端設備類型。
