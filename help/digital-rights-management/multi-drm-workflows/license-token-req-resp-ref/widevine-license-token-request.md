---
description: Widevine授權Token介面可提供生產和測試服務。
title: Widevine授權Token要求/回應
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# Widevine授權Token要求/回應 {#widevine-license-token-request-response}

Widevine授權Token介面可提供生產和測試服務。

此HTTP要求傳回可兌換為Widevine授權的Token。

**方法：GET，POST** （內含www-url編碼內文，其中包含這兩種方法的引數）

**URL：**

* **生產：** `https://wv-gen.{prod_domain}/hms/wv/token`

* **測試：** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **範例要求：**

  ```
  https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
  <ExpressPlay customer authenticator identifier>
  ```

* **範例回應：**

  ```
  https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
  ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**表13： Token查詢引數**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查詢引數</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
   <th class="entry"> <b>必填？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>這是您的客戶API金鑰，分別用於生產和測試環境。 您可以在ExpressPlay的「管理控制面板」標籤上找到此資訊。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errororformat </span> </td> 
   <td> 兩者之一 <span class="codeph"> html </span> 或 <span class="codeph"> json </span>. <p>如果 <span class="codeph"> html </span> （預設值）任何錯誤的HTML表示會顯示在回應的圖元主體中。 如果 <span class="codeph"> json </span> 指定時，會傳回JSON格式的結構化回應。 另請參閱 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤 </a> 以取得詳細資訊。 </p> <p>回應的mime型別是 <span class="codeph"> text/uri-list </span> 成功時， <span class="codeph"> text/html </span> 的 <span class="codeph"> html </span> 錯誤格式，或 <span class="codeph"> application/json </span> 的 <span class="codeph"> json </span> 錯誤格式。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表14：授權查詢引數**

| 查詢引數 | 說明 | 必填？ |
|--- |--- |--- |
| `generalFlags` | 代表授權旗標的4位元組十六進位字串。 &#39;0000&#39;是唯一允許的值 | 否 |
| `kek` | 金鑰加密金鑰(KEK)。 金鑰是使用KEK使用金鑰包裝演演算法(AES Key Wrap，RFC3394)加密儲存的。 | 否 |
| `kid` | 內容加密金鑰或字串的16位元組十六進位字串表示法 `^somestring'`. 字串的長度，後面接著 `^` 不可超過64個字元。 如需範例，請檢視下方的注意事項。 | 是 |
| `ek` | 已加密內容金鑰的十六進位字串表示法。 | 否 |
| `contentKey` | 內容加密金鑰的16位元組十六進位字串表示法 | 是，除非 `kek` 和 `ek` 或 `kid` 已提供 |
| `contentId` | 內容ID | 否 |
| `securityLevel` | 允許值為1-5。 <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 是 |
| `hdcpOutputControl` | 允許值為0、1、2。 <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 是 |
| `licenseDuration` * | 授權持續時間（秒數）。 若未提供，表示持續時間沒有限制。 如需詳細資訊，請檢視下方的注意事項。 | 否 |
| `wvExtension` | 包裝extensionType和extensionPayload的簡短表單，以逗號分隔字串。 請參閱下方的格式。 範例： `…&wvExtension=wudo,AAAAAA==&…` | 否，可使用任何數字 |

關於 `licenseDuration`： <ol><li> 播放將停止 `licenseDuration` 播放開始後的秒數。 </li><li> 若要允許播放停止/繼續無限制的時間，請省略 `licenseDuration` （預設為無限）。 否則，請指定終端使用者應該能夠享受串流的時間長度。 </li></ol>

**表15：權杖限制查詢引數**

| 查詢引數 | 說明 | 必填？ |
|--- |--- |--- |
| `expirationTime` | 此Token的到期時間。 此值必須是中的字串 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) &#39;Z&#39;區域指示器中的日期/時間格式(&#39;Zulu time&#39;)，或前面有+號的整數。 RFC 3339日期/時間的範例為2006-04-14T12:01:10Z。 <br> 如果值是中的字串 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 日期/時間格式，則代表權杖的絕對到期日期/時間。 如果值是前面有+號的整數，則會從簽發將其解譯為權杖有效的相對秒數。 例如， `+60` 指定一分鐘。 <br> 權杖存留期的上限和預設（如果未指定）為30天。 | 否 |

**表16：相互關聯查詢引數**

| **查詢引數** | **說明** | **必填？** |
|---|---|---|
| `cookie` | Token中最多可包含32個字元的任意字串，由Token贖回伺服器記錄。 可用來關聯兌換伺服器的記錄專案與服務提供者伺服器的記錄專案。 | 否 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**表17： HTTP回應**

| **HTTP狀態代碼** | **說明** | **Content-Type** | **實體本文包含** |
|---|---|---|---|
| `200 OK` | 沒有錯誤。 | `text/uri-list` | 授權贏取URL + Token |
| `400 Bad Request` | 無效的引數 | `text/html` 或 `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或 `application/json` | 錯誤說明 |
| `404 Not found` | URL錯誤 | `text/html` 或 `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤說明 |

**表18：事件錯誤代碼**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> 程式碼 </th> 
   <th class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 無效的權杖到期時間： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 無效的IP位址 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 無效的內容加密金鑰： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 指定的輸出控制旗標無效： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 必須提供驗證權杖 </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 驗證Token無效： &lt;details&gt; <p>注意：如果驗證器錯誤或使用生產驗證器在*.test.expressplay.com存取測試API時，可能會發生這種情況，反之亦然。 </p> <p importance="high">注意：測試SDK和進階測試工具(ATT)僅適用於 <span class="filepath"> *.test.expressplay.com </span>，但生產裝置必須使用 <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用的權杖不足 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 缺少租借期間結束時間 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 缺少租借播放期間 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 無效的租借播放期間 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 內容加密金鑰長度必須為32個十六進位數字 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理錯誤： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 服務帳戶已停用 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> 無效的Cookie </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> 無效的輸出控制項，值超出指定範圍 </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> 未指定對應的值 </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> 擴充功能型別應為4個字元 </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 擴充功能承載應採用Base64編碼 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag </span> 必須編碼4個位元組 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 指定的錯誤格式無效： &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> 無法驗證裝置 </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> 無效的權杖 </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> 遺失 <span class="filepath"> kid </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從金鑰儲存服務取得內容金鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> kid </span> 長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> kid </span> 「^」之後必須為64個字元 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 無效 <span class="codeph"> kid </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 無效的加密金鑰或 <span class="codeph"> 金鑰 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 無效的一般旗標 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的金鑰資料無效 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租借期間無效 </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Widevine不支援裝置ID繫結 </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 缺少安全性層級值 </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 無效的安全性層級值 </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> 遺失HDCP輸出控制值 </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> 指定的授權期間無效 </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> 無法產生Widevine授權 </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 無效 <span class="codeph"> WVExtension </span> 指定的引數 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Widevine選項已停用 </td> 
  </tr> 
 </tbody> 
</table>
