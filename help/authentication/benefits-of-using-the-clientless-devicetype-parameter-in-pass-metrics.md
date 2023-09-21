---
title: 在Primetime驗證量度中使用無使用者端deviceType引數的好處
description: 在Primetime驗證量度中使用無使用者端deviceType引數的好處
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 在Primetime驗證量度中使用無使用者端deviceType引數的好處 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

</br>

## 內容

雖然是選用專案，但引數 `deviceType` 來自無使用者端API （如果存在）的API用於透過公開的Primetime驗證量度 [軟體權利檔案服務監視](/help/authentication/entitlement-service-monitoring-overview.md).

考量以下兩者之間的連線： `deviceType` 引數及其 **優點** 在Primetime驗證量度最初未說明時，此技術備註的範圍是新增有關它們的更多資訊。

## 說明

此 `deviceType` 自從第一個版本以來，無使用者端API中就存在引數，但是它對Primetime驗證量度的影響已新增到較新的版本中。



>[!IMPORTANT]
>
>若引數 `deviceType` 已正確設定，則有下列專案 **優點** 在軟體權利檔案服務監視中：它提供以下量度 [依裝置型別劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無使用者端時，因此可針對Roku、AppleTV、Xbox等執行不同型別的分析。


如需軟體權利檔案服務監控API的詳細資訊，請參閱 [向下鑽研樹狀結構、](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 這說明 [維度](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) （資源）可在ESM 2.0中使用。

>[!NOTE]
>
>此技術備忘稿的內容也已新增至 [無使用者端API](#clientless_device_type).




## 實施

為了充分受益於Primetime驗證量度，有2種型別 [無使用者端API](#web_srvs_summary) 目前正在使用且需要具備正確設定檔的 `deviceType` 設定：

1. API具有 `regcode` 作為必要引數，和將會使用 `deviceType` 建立時設定的引數 `regcode`，搭配下列API呼叫：
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. 具有下列專案的API： `deviceType` 作為選用引數：
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

我們建議使用 `deviceType` 引數，並為所有API傳遞正確的無使用者端裝置型別。
