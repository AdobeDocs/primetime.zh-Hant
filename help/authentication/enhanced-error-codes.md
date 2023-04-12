---
title: 增強的錯誤碼
description: 增強的錯誤碼
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# 增強的錯誤碼 {#enhanced-error-codes}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

本檔案說明API錯誤碼清單，以及傳回至應用程式的其他錯誤資訊。

要在程式設計師應用程式中使用增強錯誤代碼，需要向支援團隊提出請求，以便在配置更改後啟用它。

## 回應錯誤處理 {#response-error-handling}

在大多數情況下，Primetime驗證API會在回應內文中包含其他錯誤資訊，以便提供 **有意義的上下文** 說明發生某個錯誤的原因和/或自動修正問題的可能解決方案。  *不過，在某些涉及驗證或登出流程的特定情況下，Primetime驗證服務可能會傳回HTML回應或空白內文 — 請查看API檔案以取得詳細資訊。*

雖然某些類型的錯誤可以自動處理（例如在網路逾時時重試授權請求，或在其工作階段過期時要求使用者重新驗證），但其他類型可能需要變更設定或客戶服務團隊互動。 對於程式設計師來說，收集並提供此類情況下的完整錯誤資訊非常重要。

Primetime驗證API會傳回範圍400-500中的HTTP狀態代碼，以指出失敗或錯誤。 每個HTTP狀態代碼都有某些含意：

- 4xx錯誤碼表示錯誤是由用戶端產生，且用戶端需要執行額外工作來修正錯誤（例如在叫用受保護的API或提供任何必要參數前取得存取權杖）

- 5xx錯誤代碼表示錯誤是由伺服器產生，伺服器需要做其他工作才能修正。

其他錯誤資訊包含在回應內文的「錯誤」欄位中。 




| 名稱 | 類型 | 範例 | 說明 |
| --- | --- | --- | --- |
| **錯誤** | _物件_ | JSON <br>    {<br>        &quot;status&quot; :403,<br>        &quot;code&quot; :&quot;network_connection_failure&quot;,<br>        &quot;message&quot; :「無法聯繫您的電視提供商服務」，<br>        &quot;helpUrl&quot; :&quot;&quot;,<br>        &quot;trace&quot; :&quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; :&quot;retry&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | 嘗試完成請求時收集的集合或錯誤物件。 |

</br>

Adobe Primetime API可處理多個項目（預先授權API等），可能會使用項目層級錯誤資訊，指出處理特定項目是否失敗，以及處理其他項目是否成功。 在此情況下， ***&quot;error&quot;*** 物件位於項目層級，回應內文可能包含多個 ***&quot;errors&quot;*** 物件 — 請參閱API檔案。

</br>

| 有部分成功和項目層級錯誤的範例 |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; :&quot;TestStream1&quot;,<br>  &quot;authorized&quot; :true <br>}, </br>{ </br>  &quot;id&quot; :&quot;TestStream2&quot;, <br>   &quot;authorized&quot; :false, </br>   &quot;error&quot; :{ <br> </br>      &quot;status&quot; :403,<br>      &quot;code&quot; :&quot;network_connection_failure&quot;,<br>      &quot;message&quot; :「無法聯繫您的電視提供商服務」，<br>      「詳細資料」：&quot;&quot;,<br>      &quot;helpUrl&quot; :&quot;&quot;,<br>      &quot;trace&quot; :&quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; :&quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

每個錯誤物件都有下列參數：

| 名稱 | 類型 | 範例 | 受限 | 說明 |
|----|----|----|----|--------------|
| 狀態 | *整數* | 403 | ♦ | RFC 7231(https://tools.ietf.org/html/rfc7231#section-6)中記錄的回應HTTP狀態代碼 <br> - 400錯誤請求 <br> - 400錯誤請求 <br> - 400錯誤請求 <br> - 401未授權 <br>  — 禁止403 <br>  — 未找到404 <br> - 405不允許方法 <br> - 409衝突 <br> - 410已消失 <br> - 412先決條件失敗 <br> - 429請求太多 <br> - 500間隔伺服器錯誤 <br> - 503服務不可用 |
| 程式碼 | *字串* | network_connection_failure | ♦ | 標準Primetime驗證錯誤碼。 錯誤代碼的完整清單如下。 |
| 訊息 | *字串* | 無法聯繫您的電視提供商服務 |  | 可向最終用戶顯示的人類可讀消息。 |
| 詳細資訊 | *字串* | 您的訂閱套件不包含「即時」管道 |  | 在某些情況下，MVPD授權端點或程式設計師通過降級規則提供詳細消息。 <br> <br> 請注意，如果未從合作夥伴服務收到任何自訂訊息，則錯誤欄位中可能不會出現此欄位。 |
| helpUrl | *url* | &quot;&quot; |  | 此URL會連結至關於為何發生此錯誤的詳細資訊，以及可能的解決方案。 <br> <br>  URI表示絕對URL，不應從錯誤代碼推斷。 視錯誤內容而定，可提供不同的URL。 例如，相同的bad_request錯誤碼會為驗證和授權服務產生不同的URL。 |
| trace | *字串* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | 此回應的唯一識別碼，在聯絡支援人員以識別更複雜情境中的特定問題時，可使用此識別碼。 |
| 動作 | *字串* | 重試 | ♦ | *建議採取措施來糾正此情況：* </br><br> -none — 很遺憾，沒有預先定義的操作可修正此問題。 這可能表示公用API的呼叫不當 </br><br> — 配置 — 需要通過TVE儀表板或聯繫支援人員進行配置更改。 </br><br>-application-registration — 應用程式必須重新註冊。 </br><br>-authentication — 用戶必須進行身份驗證或重新驗證。 </br><br>-authorization — 用戶必須獲得特定資源的授權。 </br><br> — 退化 — 應採用某種形式的退化。 </br><br> — 重試 — 重試請求可能解決問題</br><br>-retry-after — 在指定的時間段後重試請求可能會解決問題。 |

</br>

**附註：**

- ***受限*** 欄 *指示各個欄位值是否表示有限集* (例如「」的現有HTTP狀態代碼&#x200B;*狀態*」欄位)。 將來對此規範的更新可能會將值添加到限制清單，但不會刪除或更改現有的值。 不受限制的欄位通常可以包含任何資料，但為確保合理大小可能存在限制。

- 每個Adobe回應都會包含「Adobe — 請求 — Id」，可在整個HTTP服務中識別用戶端請求。 「**trace**「欄位補充了這一點，它們應該一起報告。 

## HTTP狀態代碼和錯誤代碼 {#http-status-codes-and-error-codes}

各種錯誤碼及其相關的HTTP狀態碼之間的不一致是由於與舊sdk和應用程式(例如 *未知\_application* 產生400個錯誤請求，而 *未知\_software\_statement* 未經授權即可產生401)。 這些不一致的解決將在以後的迭代中定位。 
 
## 動作和錯誤碼 {#actions-and-error-codes}

對於大部分的錯誤代碼，多個動作可能適合作為解決現有問題的路徑，甚至可能需要多個動作才能自動修正它們。 我們選擇指出錯誤修正機率最高的。 此 **動作** 可分割為三個類別：

1. 嘗試修正請求上下文的內容（重試，重試後） 
1. 嘗試在應用程式中修復用戶上下文的應用程式（應用程式註冊、身份驗證、授權） 
1. 嘗試修復應用程式和身份提供程式之間整合上下文（配置、降級）的

對於第一個類別（重試後再重試），只要重試相同的請求就足以解決問題。 若是處理多個項目的API，應用程式應重複請求，並僅包含具有「重試」或「重試後」動作的項目。 對於「*重試後*&quot;操作， a &quot;<u>重試後</u>&quot;標題會指出應用程式在重複請求之前應等待多少秒。

對於第2和第3類別，實際操作實施與應用程式功能高度相關。 例如，「*降解*「可實作為「切換至15分鐘的臨時傳遞，以允許使用者播放內容」，或實作為「自動工具，以套用AUTHN-ALL或AUTHZ-ALL降級，以便與指定的MVPD整合」。 類似「*驗證*「動作可以觸發平板電腦上的被動驗證（後通道驗證），以及連線電視上的全第二螢幕驗證流程。 因此，我們選擇提供結構和所有參數的完整URL。 

## 錯誤代碼 {#error-codes}

以下錯誤表列出可能的錯誤代碼、相關消息和可能的操作。

| 動作 | 錯誤代碼 | HTTP狀態代碼 | 說明 |
|---|---|---|--------------|
| 配置 | *authorization_denied_by_mvpd* | 403 | 請求指定資源的授權時，MVPD已傳回「拒絕」決定。 |
|  | *authorization_denied_by_parental_controls* | 403 | MVPD已根據指定資源的父級控制設定傳回「拒絕」決定。 |
|  | *authorization_denied_by_programer* | 403 | 由程式設計師應用的降級規則會為當前用戶強制執行「拒絕」決策。 |
|  | *bad_request* | 400 | API要求無效或格式不正確。 檢閱API檔案，以判斷要求需求。 |
|  | *個性化服務_不可用* | 503 | 請求失敗，因為個性化服務不可用。 |
|  | *internal_error* | 500 | 由於內部伺服器錯誤，請求失敗。 |
|  | *invalid_client_time* | 400 | 客戶端電腦「日期/時間/時區」設定不正確。 這可能會導致驗證/授權錯誤。 |
|  | *invalid_custom_scheme* | 400 | 無法識別應用程式註冊中使用的指定自定義方案。 請檢查TVE儀表板配置，以了解正確的自定義配置值。 |
|  | *invalid_domain* | 400 | 請求者使用無效的網域。 特定請求者ID使用的所有網域都需加入白名單Adobe。 |
|  | *invalid_header* | 400 | 請求失敗，因為它包含無效的標題。 請參閱API檔案，判斷哪些標題對您的請求有效，以及其值是否有任何限制。 |
|  | *invalid_http_method* | 405 | 不支援與要求相關聯的HTTP方法。 請參閱API檔案，以判斷您請求的支援HTTP方法。 |
|  | *invalid_parameter_value* | 400 | 請求失敗，因為它包含無效的參數或參數值。 請參閱API檔案，判斷哪些參數對您的請求有效，以及其值是否有任何限制。 |
|  | *invalid_resource_value* | 400 | 請求失敗，因為使用的資源無效或格式錯誤。 檢閱API檔案，以判斷必須針對您的要求對複雜資源進行編碼的方式，以及其值和/或大小是否有任何限制。 |
|  | *invalid_registration_code | 404 | 指定的註冊代碼不再有效或已過期。 |
|  | *invalid_service_configuration* | 500 | 請求失敗，因為服務配置不正確。 |
|  | *missing_authentication_header* | 400 | 請求失敗，因為它未包含特定API所需的驗證標題。 |
|  | *missing_resource_mapping* | 400 | 指定的資源沒有相應的映射。 請聯絡支援以修正所需的對應。 |
|  | *preauthorization_denied_by_mvpd* | 403 | 請求指定資源的預授權時，MVPD已傳回「拒絕」決定。 |
|  | *preauthorization_denied_by_programer* | 403 | 由程式設計師應用的降級規則對當前用戶強制執行「拒絕」決策。 |
|  | *registration_code_service_uvalable* | 503 | 請求失敗，因為註冊代碼服務不可用。 |
|  | *service_unavailable | 503 | 由於身份驗證或授權服務不可用，請求失敗。 |
|  | *access_token_unavailable* | 400 | 檢索訪問令牌時出現意外錯誤，請求失敗。 請檢查TVE儀表板配置，了解可用的軟體語句和已註冊的自定義方案。 |
|  | *unsupported_client_version* | 400 | 此版本的Primetime驗證SDK太舊，不再支援。 請參閱API檔案，了解升級至最新版本所需的步驟。 |
|  | *network_required_ssl* | 403 | 目標合作夥伴服務有SSL連線問題。 請聯絡支援團隊。 |
|  | *too_many_resources* | 403 | 授權或預授權請求失敗，因為查詢了太多資源。 請聯絡支援團隊，以正確設定授權和預先授權限制。 |
|  | *unknown_programmer | 400 | 未識別程式設計師或服務提供商。 使用TVE儀表板註冊指定的程式設計師。 |
|  | *unknown_application* | 400 | 無法識別應用程式。 使用TVE儀表板註冊指定的應用程式。 |
|  | *unknown_integration* | 400 | 指定的程式設計師和身份提供者之間不存在整合。 使用TVE儀表板建立所需的整合。 |
|  | *unknown_software_statement* | 401 | 無法識別與存取權杖相關聯的軟體陳述式。 請與支援團隊聯繫，以澄清軟體聲明的狀態。 |
| 應用註冊 | *access_token_expired* | 401 | 存取權杖已過期。 應用程式應如API檔案所示，重新整理存取權杖。 |
|  | *invalid_access_token_signature* | 401 | 存取權杖簽章不再有效。 應用程式應如API檔案所示，重新整理存取權杖。 |
|  | *invalid_client_id* | 401 | 未識別關聯的客戶端標識符。 應用程式應依照API檔案中所述的應用程式註冊程式操作。 |
| 驗證 | *authentication_session_expired* | 410 | 當前身份驗證會話已過期。 使用者必須透過支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_missing* | 401 | 無法檢索與此請求關聯的驗證會話。 使用者必須透過支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_unvalided* | 401 | 身分提供者已使驗證工作階段失效。 使用者必須透過支援的MVPD重新驗證才能繼續。 |
|  | *authentication_session_issuer_mismatch | 400 | 授權請求失敗，因為授權流程的指示MVPD與發出驗證會話的MVPD不同。 使用者必須使用所需的MVPD重新驗證才能繼續。 |
|  | *authorization_denied_by_hba_policys* | 403 | MVPD已因基於家庭的驗證策略而返回「拒絕」決定。 當前驗證是使用基於家庭的驗證流(HBA)獲得的，但當請求指定資源的授權時，設備不再位於家中。 使用者必須透過支援的MVPD重新驗證才能繼續。 |
|  | *identity_not_recogned_by_mvpd* | 403 | 授權請求失敗，因為MVPD無法辨識使用者身分。 |
| 授權 | *authorization_expired* | 410 | 指定資源的先前授權已過期。 用戶必須獲得新授權才能繼續。 |
|  | *authorization_not_found* | 404 | 未找到指定資源的授權。 用戶必須獲得新授權才能繼續。 |
|  | *device_identifier_mismatch* | 403 | 指定的設備標識符與授權設備標識不匹配。 用戶必須獲得新授權才能繼續。 |
| 重試 | **network_connection_failure** | 403 | 與關聯的合作夥伴服務發生連接故障。 重試請求可能會解決問題。 |
|  | *network_connection_timeout* | 403 | 與關聯的合作夥伴服務存在連接超時。 重試請求可能會解決問題。 |
|  | *network_received_error* | 403 | 從關聯的合作夥伴服務檢索響應時出現讀取錯誤。 重試請求可能會解決問題。 |
|  | *maximum_execution_time_exceeded* | 403 | 請求未在允許的最大時間內完成。 重試請求可能會解決問題。 |
| 重試後 | *too_many_requests* | 429 | 在指定間隔內發送了太多請求。 應用程式可以在建議的時段後重試請求。 |
|  | *user_rate_limit_exceeded* | 429 | 特定用戶在指定時間間隔內發出了太多請求。 應用程式可以在建議的時段後重試請求。 |

