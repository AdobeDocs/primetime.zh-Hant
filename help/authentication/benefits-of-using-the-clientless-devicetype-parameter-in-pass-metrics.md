---
title: 在Primetime驗證量度中使用無用戶端deviceType參數的優點
description: 在Primetime驗證量度中使用無用戶端deviceType參數的優點
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# 在Primetime驗證量度中使用無用戶端deviceType參數的優點 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 內容

雖然為選用，但參數 `deviceType` 來自無用戶端API（若存在），則用於透過公開的Primetime驗證量度 [權利服務監視](/help/authentication/entitlement-service-monitoring-overview.md).

考慮到 `deviceType` 參數及其 **福利** 在Primetime驗證量度最初未說明時，此技術說明的範圍是新增關於這些量度的詳細資訊。

## 說明

此 `deviceType` 參數自第一個版本起就存在於無用戶端API中，但在較新的版本中已新增其對Primetime驗證量度的影響。



>[!IMPORTANT]
>
>如果參數 `deviceType` 已正確設定，則會有下列項目 **效益** 在「權利服務監視」中：它提供量度 [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便可以針對Roku、AppleTV、Xbox等執行不同類型的分析。


如需權益服務監控API的詳細資訊，請參閱 [向下鑽取樹，](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 這說明 [維度](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) （資源）。

>[!NOTE]
>
>此技術說明的內容也新增至 [無用戶端API](#clientless_device_type).




## 實作

為了充分受益於Primetime驗證量度，有2種類型 [無用戶端API](#web_srvs_summary) 正在使用且需要有正確的 `deviceType` 設定：

1. 具有 `regcode` 作為必要參數，並將使用 `deviceType` 建立時設定的參數 `regcode`，搭配下列API呼叫：
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggei/v1/{requestorId}/regcode](#reg_serv)

1. 具有 `deviceType` 作為選用參數：
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

我們的建議是使用 `deviceType` 參數，並為所有API傳遞正確的無用戶端裝置類型。


