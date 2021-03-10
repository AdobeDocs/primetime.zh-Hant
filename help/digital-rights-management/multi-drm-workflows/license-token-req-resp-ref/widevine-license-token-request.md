---
description: Widevine授權Token介面提供生產與測試服務。
title: Widevine授權Token請求／回應
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---


# Widevine授權Token要求／回應{#widevine-license-token-request-response}

Widevine授權Token介面提供生產與測試服務。

此HTTP要求會傳回可兌換為Widevine授權的Token。

**方法：GET、POST** （含www-url編碼內文，其中包含兩種方法的參數）

**URL:**

* **生產：** `https://wv-gen.{prod_domain}/hms/wv/token`

* **測試：** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **請求範例：**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **範例回應：**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**表13:Token查詢參數**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查詢參數</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
   <th class="entry"> <b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator  </span> </td> 
   <td> <p>這是您的客戶API金鑰，每個金鑰都適用於您的生產與測試環境。 您可在「ExpressPlay管理控制面板」標籤中找到這個選項。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat  </span> </td> 
   <td> <span class="codeph"> html </span>或<span class="codeph"> json </span>。 <p>如果<span class="codeph"> html </span>（預設值），則回應的實體主體中會提供任何錯誤的HTML表示法。 如果指定<span class="codeph"> json </span>，則會傳回JSON格式的結構化回應。 如需詳細資訊，請參閱<a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤</a>。 </p> <p>回應的MIME類型為：成功時<span class="codeph"> text/uri-list </span>、<span class="codeph"> text/html </span>（<span class="codeph"> html </span>錯誤格式）或<span class="codeph"> application/json </span>（<span class="codeph"> </span>錯誤格式）。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表14:授權查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| `generalFlags` | 代表許可證標誌的4位元組十六進位字串。 &#39;0000&#39;是唯一允許的值 | 否 |
| `kek` | 密鑰加密密鑰(KEK)。 密鑰使用密鑰封裝算法（AES密鑰封裝，RFC3394）與KEK進行加密。 | 否 |
| `kid` | 內容加密密鑰或字串`^somestring'`的16位元組十六進位字串表示。 字串後跟`^`的長度不能大於64個字元。 請勾選下方的附註以取得範例。 | 是 |
| `ek` | 加密內容密鑰的十六進位字串表示。 | 否 |
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是，除非提供`kek`和`ek`或`kid` |
| `contentId` | 內容ID | 否 |
| `securityLevel` | 允許的值為1-5。 <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 是 |
| `hdcpOutputControl` | 允許的值為0、1、2。 <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 是 |
| `licenseDuration` * | 授權的持續時間（以秒為單位）。 如果未提供，則表示期間沒有限制。 請查看以下附註以取得詳細資訊。 | 否 |
| `wvExtension` | 以逗號分隔的字串包住extensionType和extensionPayload的簡短表單。 請參閱下方的格式。 範例：`…&wvExtension=wudo,AAAAAA==&…` | 否，可以使用任何數字 |

關於`licenseDuration`: <ol><li> 播放開始後，播放將停止`licenseDuration`秒。 </li><li> 若要允許在無限長時間內停止／繼續播放，請省略`licenseDuration`（預設為無限）。 否則，請指定使用者可享受串流的時間長度。 </li></ol>

**表15:Token限制查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| `expirationTime` | 此代號的過期時間。 此值必須是[RFC 3339](https://www.ietf.org/rfc/rfc3339.txt)日期／時間格式的字串(「Z」區域指示符（「祖魯時間」）)，或前面帶有+號的整數。 RFC 3339日期／時間的示例是2006-04-14T12:01:10Z。 <br> 如果該值是 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 日期／時間格式中的字串，則表示令牌的絕對到期日／時間。如果值是前面有+號的整數，則會將其解讀為從發行開始的相對秒數，表示代號有效。 例如，`+60`指定一分鐘。 <br> 最大和預設（如果未指定）Token期限為30天。 | 否 |

**表16:關聯查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `cookie` | 任意字串（長達32個字元）長期載入Token中，並由Token兌換伺服器記錄。 可用於將兌換伺服器上的日誌條目與服務提供商伺服器上的日誌條目關聯起來。 | 否 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**表17:HTTP回應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體內文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 授權贏取URL + Token |
| `400 Bad Request` | 無效的標籤 | `text/html` 或  `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或  `application/json` | 錯誤說明 |
| `404 Not found` | 錯誤的URL | `text/html` 或  `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或  `application/json` | 錯誤說明 |

**表18:事件錯誤代碼**

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
   <td> 無效的代號過期時間：&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 無效的IP位址 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 內容加密密鑰無效：&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 指定的輸出控制標誌無效：&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 必須提供驗證Token </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 驗證Token無效：&lt;details&gt; <p>注意： 如果驗證器錯誤，或使用生產驗證器存取*.test.expressplay.com的測試API時，會發生這種情況，反之亦然。 </p> <p importance="high">注意： 測試SDK和進階測試工具(ATT)僅適用於<span class="filepath"> *.test.expressplay.com </span>，而生產裝置必須使用<span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用預付碼不足 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 缺少租金期間結束時間 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 缺少租用播放時間 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 租用播放期間無效 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 內容加密金鑰必須有32位十六進位數字長 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理錯誤：&lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 服務帳戶已禁用 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> 無效的Cookie </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> 輸出控制無效，值超出指定範圍 </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> 未指定相應值 </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> 副檔名類型應為4個字元 </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 延伸裝載應使用Base64編碼 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag必 </span> 須編碼4個位元組 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 指定的錯誤格式無效：&lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> 無法驗證設備 </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> 無效的代號 </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> 缺少<span class="filepath">子項</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從密鑰儲存服務獲取內容密鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> 小 </span> 孩長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 小 </span> 孩在'^'後面必須有64個字元 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 無效的<span class="codeph">小子</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 無效的加密密鑰或<span class="codeph"> kek </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 一般標誌無效 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密鑰資料無效 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租用期間無效 </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Widevine不支援裝置ID系結 </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 缺少安全級別值 </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 安全級別值無效 </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> 缺少HDCP輸出控制值 </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> 指定的許可證持續時間無效 </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> 無法生成Widevine許可證 </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 指定的<span class="codeph"> WVExtension </span>參數無效 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Widevine選項已停用 </td> 
  </tr> 
 </tbody> 
</table>