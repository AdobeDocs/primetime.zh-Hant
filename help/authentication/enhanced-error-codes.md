---
title: 增強型錯誤代碼
description: 增強型錯誤代碼
exl-id: 2b0a9095-206b-4dc7-ab9e-e34abf4d359c
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# 增強型錯誤代碼 {#enhanced-error-codes}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#overview}

本檔案說明API錯誤碼清單以及傳回給應用程式的其他錯誤資訊。

若要在程式設計人員應用程式中使用增強型錯誤代碼，需要向支援團隊提出請求，才能在設定變更時啟用它。

## 回應錯誤處理 {#response-error-handling}

在大多數情況下，Primetime驗證API會在回應內文中包含其他錯誤資訊，以便提供 **有意義的上下文** 發生特定錯誤的原因和/或自動修正問題的可能解決方案。  *但是，在涉及驗證或登出流程的特定情況下，Primetime驗證服務可能會傳回HTML回應或空白內文 — 請檢視API檔案以取得更多資訊。*

雖然某些型別的錯誤可以自動處理（例如，在網路逾時的情況下重試授權請求，或在其工作階段過期時要求使用者重新驗證），但其他型別可能需要設定變更或客戶服務團隊互動。 在這種情況下，程式設計師必須收集並提供完整的錯誤資訊。

Primetime驗證API會傳回400-500範圍內的HTTP狀態代碼，以指出失敗或錯誤。 每個HTTP狀態程式碼都有特定的含意：

- 4xx錯誤代碼表示錯誤是由使用者端產生的，使用者端需要執行額外的操作來修正錯誤（例如，在叫用受保護的API或提供任何必要的引數之前取得存取權杖）

- 5xx錯誤碼表示錯誤是由伺服器產生的，而且伺服器需要執行其他工作來修正錯誤。

其他錯誤資訊會包含在回應內文的「error」欄位中。 




| 名稱 | 型別 | 範例 | 說明 |
| --- | --- | --- | --- |
| **錯誤** | _物件_ | JSON <br>    {<br>        &quot;status&quot; ：403，<br>        &quot;code&quot; ： &quot;network_connection_failure&quot;，<br>        &quot;message&quot; ：&quot;Unable to contact your TV provider service&quot;，<br>        &quot;helpUrl&quot; ： &quot;&quot;，<br>        &quot;trace&quot; ： &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;，<br>        &quot;action&quot; ： &quot;retry&quot;<br>    }<br><br>----------------------------------------------------------------------------<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | 嘗試完成請求時收集的集合或錯誤物件。 |

</br>

處理多個專案的Adobe Primetime API （預先授權API等）可能會使用專案層級錯誤資訊，指出特定專案的處理失敗而其他專案處理成功。 在此案例中， ***&quot;error&quot;*** 物件位於專案層級，且回應內文可能包含多個 ***&quot;errors&quot;*** 物件 — 請參閱API檔案。

</br>

| 部分成功與料號層次錯誤的範例 |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; ： &quot;TestStream1&quot;，<br>  &quot;authorized&quot; ： true <br>}， </br>{ </br>  &quot;id&quot; ： &quot;TestStream2&quot;， <br>   &quot;authorized&quot; ： false， </br>   &quot;error&quot; ： { <br> </br>      &quot;status&quot; ：403，<br>      &quot;code&quot; ： &quot;network_connection_failure&quot;，<br>      &quot;message&quot; ：&quot;Unable to contact your TV provider service&quot;，<br>      &quot;details&quot; ： &quot;&quot;，<br>      &quot;helpUrl&quot; ： &quot;&quot;，<br>      &quot;trace&quot; ： &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;，<br>      &quot;action&quot; ： &quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

每個錯誤物件都有以下引數：

| 名稱 | 型別 | 範例 | 受限制 | 說明 |
|----|----|----|----|--------------|
| 狀態 | *整數* | 403 | ♦ | RFC 7231中記錄的回應HTTP狀態碼(https://tools.ietf.org/html/rfc7231#section-6) <br> - 400個錯誤請求 <br> - 400個錯誤請求 <br> - 400個錯誤請求 <br> - 401未獲授權 <br> - 403禁止 <br> - 404找不到 <br> - 405不允許方法 <br> - 409衝突 <br> - 410已過期 <br> - 412先決條件失敗 <br> - 429請求太多 <br> - 500間隔伺服器錯誤 <br> - 503服務無法使用 |
| 程式碼 | *字串* | network_connection_failure | ♦ | 標準Primetime驗證錯誤代碼。 完整的錯誤碼清單包含於下方。 |
| message | *字串* | 無法連絡您的電視提供者服務 |  | 可顯示給一般使用者的人類可讀訊息。 |
| 詳細資料 | *字串* | 您的訂閱套件不包含「即時」頻道 |  | 在某些情況下，MVPD授權端點或程式設計師透過降級規則提供詳細訊息。 <br> <br> 請注意，如果未從合作夥伴服務收到自訂訊息，則錯誤欄位中可能不存在此欄位。 |
| helpUrl | *url* | &quot;&quot; |  | 此URL會連結至有關此錯誤發生原因和可能解決方案的詳細資訊。 <br> <br>  URI代表絕對URL，不應從錯誤代碼推斷。 根據錯誤內容，可以提供不同的url。 例如，相同的bad_request錯誤碼將會為驗證和授權服務產生不同的url。 |
| trace | *字串* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | 此回應的唯一識別碼，可在聯絡支援人員以識別更複雜情境中的特定問題時使用。 |
| 動作 | *字串* | 重試 | ♦ | *補救此情況的建議動作：* </br><br> -none — 很抱歉，沒有預先定義的動作來修正此問題。 這可能表示對公用API的呼叫不正確 </br><br>-configuration — 需要透過TVE儀表板或連絡支援人員來變更設定。 </br><br>-application-registration — 應用程式必須重新註冊自己。 </br><br>-authentication — 使用者必須驗證或重新驗證。 </br><br>-authorization — 使用者必須取得特定資源的授權。 </br><br>-degradation — 應套用某種形式的降級。 </br><br>-retry — 重試請求可能解決此問題</br><br>-retry-after — 在指定的時段後重試請求可解決問題。 |

</br>

**附註：**

- ***受限制*** 欄 *指示個別欄位值是否代表有限集* (例如「」的現有HTTP狀態代碼&#x200B;*狀態*「 」欄位)。 此規格的未來更新可能會將值新增至限制清單，但不會移除或變更現有值。 不受限制的欄位通常可以包含任何資料，但為確保合理的大小，可能存在限制。

- 每個Adobe回應將包含「Adobe-Request-Id」，用於識別整個HTTP服務的使用者端要求。 「**trace**」欄位是對的補充，應該一起報告。 

## HTTP狀態代碼和錯誤代碼 {#http-status-codes-and-error-codes}

各種錯誤碼與其相關HTTP狀態碼之間的不一致是由於與舊版sdk和應用程式(例如 *未知\_application* 產生400個錯誤請求，但 *未知\_software\_statement* 產生401 （未獲授權）。 未來反複專案會鎖定解決這些不一致的地方。 
 
## 動作和錯誤代碼 {#actions-and-error-codes}

對於大多數的錯誤碼，多個動作可能符合資格作為修正手頭問題的路徑，甚至可能需要多個動作才能自動修正這些問題。 我們選擇指出修正錯誤的可能性最高的錯誤。 此 **動作** 可分割為三個類別：

1. 嘗試修正請求內容的請求（重試、之後重試） 
1. 嘗試修正應用程式內的使用者內容（應用程式註冊、驗證、授權）的使用者內容 
1. 嘗試修正應用程式和身分提供者之間的整合內容（設定、降級）的訪客

對於第一個類別（重試和之後重試），僅重試相同請求可能足以解決問題。 在API處理多個專案的情況下，應用程式應重複該請求，並僅包含具有「重試」或「之後重試」動作的專案。 針對&quot;*重試之後*「動作，a 」<u>重試晚於</u>「標頭」會指出應用程式在重複請求前應等待的秒數。

對於第2和第3類別，實際動作實作與應用程式功能有很大的關係。 例如，「*退化*「可實作為」切換至15分鐘暫時通路以允許使用者播放內容「或實作為」自動工具套用AUTHN-ALL或AUTHZ-ALL降級，以便與指定的MVPD整合」。 類似於&quot;*驗證*「動作可能會在平板電腦上觸發被動驗證（背景通道驗證），並在連線的電視上觸發完整的第二個畫面驗證流程。 這就是我們選擇提供完整包含結構描述和所有引數的URL的原因。 

## 錯誤代碼 {#error-codes}

下列錯誤表列出了可能的錯誤代碼、相關訊息和可能的動作。

| 動作 | 錯誤代碼 | HTTP狀態代碼 | 說明 |
|---|---|---|--------------|
| 設定 | *authorization_denied_by_mvpd* | 403 | 請求指定資源的授權時，MVPD傳回「拒絕」決定。 |
|  | *authorization_denied_by_parental_controls* | 403 | 由於指定資源的家長監護設定，MVPD已傳回「拒絕」決定。 |
|  | *authorization_denied_by_programmer* | 403 | 程式設計師套用的降級規則會強制目前使用者執行「拒絕」決定。 |
|  | *bad_request* | 400 | API請求無效或格式錯誤。 請檢閱API檔案，以判斷要求需求。 |
|  | *individualization_service_unavailable* | 503 | 由於無法使用個人化服務，請求失敗。 |
|  | *internal_error* | 500 | 由於內部伺服器錯誤，請求失敗。 |
|  | *invalid_client_time* | 400 | 使用者端電腦日期/時間/時區未正確設定。 這可能會導致驗證/授權錯誤。 |
|  | *invalid_custom_scheme* | 400 | 無法辨識應用程式註冊中使用的指定自訂配置。 請檢查TVE儀表板設定，以取得適當的自訂配置值。 |
|  | *invalid_domain* | 400 | 請求者使用無效的網域。 特定請求者ID使用的所有網域都必須依Adobe列入白名單。 |
|  | *invalid_header* | 400 | 請求失敗，因為它包含無效的標頭。 請檢閱API檔案，判斷哪些標頭對您的請求有效，以及其值是否有任何限制。 |
|  | *invalid_http_method* | 405 | 不支援與要求關聯的HTTP方法。 請檢閱API檔案，判斷您的請求支援的HTTP方法。 |
|  | *invalid_parameter_value* | 400 | 請求失敗，因為它包含無效的引數或引數值。 請檢閱API檔案，判斷哪些引數適用於您的請求，以及其值是否有任何限制。 |
|  | *無效的resource_value* | 400 | 請求失敗，因為使用了無效或格式錯誤的資源。 請檢閱API檔案，以決定複雜資源必須如何針對您的請求編碼，以及其值和/或大小是否有任何限制。 |
|  | *invalid_registration_code | 404 | 指定的註冊代碼不再有效或已過期。 |
|  | *invalid_service_configuration* | 500 | 由於不正確的服務設定，請求失敗。 |
|  | *missing_authentication_header* | 400 | 請求失敗，因為它不包含特定API所需的驗證標頭。 |
|  | *missing_resource_mapping* | 400 | 指定的資源沒有對應的對應。 請聯絡支援以修正所需的對應。 |
|  | *preauthorization_denied_by_mvpd* | 403 | 請求指定資源的預先授權時，MVPD傳回「拒絕」決定。 |
|  | *preauthorization_denied_by_programmer* | 403 | 程式設計師套用的降級規則會強制目前使用者執行「拒絕」決定。 |
|  | *registration_code_service_unavailable* | 503 | 要求失敗，因為註冊代碼服務無法使用。 |
|  | *service_unavailable | 503 | 由於無法使用驗證或授權服務，請求失敗。 |
|  | *access_token_unavailable* | 400 | 擷取存取Token時發生意外錯誤，導致要求失敗。 請檢查TVE儀表板設定，瞭解可用的軟體陳述式和註冊的自訂配置。 |
|  | *unsupported_client_version* | 400 | 此版本的Primetime Authentication SDK太舊，不再受支援。 請檢視API檔案，瞭解升級至最新版本所需的步驟。 |
|  | *network_required_ssl* | 403 | 目標合作夥伴服務發生SSL連線問題。 請聯絡支援團隊。 |
|  | *too_many_resources* | 403 | 授權或預先授權要求失敗，因為查詢的資源太多。 請聯絡支援團隊，以正確設定授權和預先授許可權制。 |
|  | *unknown_programmer | 400 | 無法辨識程式設計師或服務提供者。 使用TVE Dashboard註冊指定的程式設計師。 |
|  | *未知的應用程式* | 400 | 無法辨識應用程式。 使用TVE儀表板註冊指定的應用程式。 |
|  | *unknown_integration* | 400 | 指定的程式設計師和身分提供者之間的整合不存在。 使用TVE儀表板建立所需的整合。 |
|  | *unknown_software_statement* | 401 | 無法辨識與存取權杖相關聯的軟體陳述式。 請連絡支援團隊，以釐清軟體宣告的狀態。 |
| application-registration | *access_token_expired* | 401 | 存取權杖已過期。 應用程式應按照API檔案中的指示重新整理存取權杖。 |
|  | *invalid_access_token_signature* | 401 | 存取權杖簽章已無效。 應用程式應按照API檔案中的指示重新整理存取權杖。 |
|  | *invalid_client_id* | 401 | 無法辨識關聯的使用者端識別碼。 應用程式應遵循API檔案中指示的應用程式註冊程式。 |
| 驗證 | *authentication_session_expired* | 410 | 目前的驗證工作階段已過期。 使用者必須使用支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_missing* | 401 | 無法擷取與此要求相關聯的驗證工作階段。 使用者必須使用支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_invalid* | 401 | 身分提供者已使驗證工作階段失效。 使用者必須使用支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_issuer_mismatch | 400 | 授權要求失敗，因為授權流程的指定MVPD與發出驗證工作階段的MVPD不同。 使用者必須使用所需的MVPD重新驗證才能繼續。 |
|  | *authorization_denied_by_hba_policies* | 403 | MVPD因為家用驗證原則而傳回「拒絕」決定。 目前的驗證是使用家用驗證流程(HBA)取得的，但是當請求指定資源的授權時，裝置不再在家中。 使用者必須使用支援的MVPD重新驗證才能繼續。 |
|  | *identity_not_recovered_by_mvpd* | 403 | 由於MVPD無法辨識使用者身分，授權要求失敗。 |
| 授權 | *authorization_expired* | 410 | 指定資源的先前授權已過期。 使用者必須取得新授權才能繼續。 |
|  | *authorization_not_found* | 404 | 找不到指定資源的授權。 使用者必須取得新授權才能繼續。 |
|  | *device_identifier_mismatch* | 403 | 指定的裝置識別碼與授權裝置識別碼不相符。 使用者必須取得新授權才能繼續。 |
| 重試 | **network_connection_failure** | 403 | 與關聯的合作夥伴服務發生連線失敗。 重試請求或許可以解決此問題。 |
|  | *network_connection_timeout* | 403 | 與關聯的合作夥伴服務發生連線逾時。 重試請求或許可以解決此問題。 |
|  | *network_received_error* | 403 | 從關聯的合作夥伴服務擷取回應時發生讀取錯誤。 重試請求或許可以解決此問題。 |
|  | *已超出最大執行時間* | 403 | 請求未在允許的最長時間內完成。 重試請求或許可以解決此問題。 |
| 重試之後 | *too_many_requests* | 429 | 在指定間隔內已傳送過多請求。 應用程式可在建議的時間段後重試請求。 |
|  | *user_rate_limit_exceeded* | 429 | 特定使用者在指定間隔內發出的請求過多。 應用程式可在建議的時間段後重試請求。 |
