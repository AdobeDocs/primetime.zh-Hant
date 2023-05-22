---
description: Widevine許可證令牌介面提供生產和test服務。
title: WideVine許可證令牌請求/響應
exl-id: f8d71f63-7783-44f9-8b1b-4b5646dca339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# WideVine許可證令牌請求/響應 {#widevine-license-token-request-response}

Widevine許可證令牌介面提供生產和test服務。

此HTTP請求返回可兌換為Widevine許可證的令牌。

**方法：GET,POST** （具有包含兩種方法參數的www-url編碼主體）

**URL:**

* **生產：** `https://wv-gen.{prod_domain}/hms/wv/token`

* **Test:** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **示例請求：**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **示例響應：**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**表13:令牌查詢參數**

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
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>這是您的客戶API密鑰，每個密鑰用於您的生產和test環境。 您可以在「ExpressPlay管理儀表板」頁籤上找到此選項。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> 錯誤格式 </span> </td> 
   <td> 要麼 <span class="codeph"> html </span> 或 <span class="codeph"> jon </span>。 <p>如果 <span class="codeph"> html </span> （預設）在響應的實體主體中提供任何錯誤的HTML表示。 如果 <span class="codeph"> jon </span> 指定後，將返回JSON格式的結構化響應。 請參閱 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤 </a> 的雙曲餘切值。 </p> <p>響應的MIME類型為 <span class="codeph"> 文本/URI清單 </span> 成功， <span class="codeph"> 文本/html </span> 為 <span class="codeph"> html </span> 錯誤格式，或 <span class="codeph"> 應用程式/json </span> 為 <span class="codeph"> jon </span> 錯誤格式。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表14:許可證查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| `generalFlags` | 代表許可證標誌的4位元組十六進位字串。 「0000」是唯一允許的值 | 否 |
| `kek` | 密鑰加密密鑰(KEK)。 密鑰使用密鑰包裝算法（AES密鑰包裝，RFC3394）使用KEK進行加密儲存。 | 否 |
| `kid` | 內容加密密鑰或字串的16位元組十六進位字串表示 `^somestring'`。 字串後跟的長度 `^` 不能超過64個字元。 有關示例，請查看下面的注釋。 | 是 |
| `ek` | 加密內容密鑰的十六進位字串表示形式。 | 否 |
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是，除非 `kek` 和 `ek` 或 `kid` 提供 |
| `contentId` | 內容ID | 否 |
| `securityLevel` | 允許的值為1-5。 <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 是 |
| `hdcpOutputControl` | 允許的值為0、1、2。 <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 是 |
| `licenseDuration` * | 許可證的持續時間（秒）。 如果未提供，則表示對持續時間沒有限制。 有關詳細資訊，請查看下面的說明。 | 否 |
| `wvExtension` | 用逗號分隔的字串形式包裝extensionType和extensionPayload的縮寫。 請參閱下面的格式。 示例： `…&wvExtension=wudo,AAAAAA==&…` | 否，可以使用任何數字 |

關於 `licenseDuration`: <ol><li> 播放將停止 `licenseDuration` 播放開始後幾秒鐘。 </li><li> 要允許在無限時間內停止/恢復播放，請忽略 `licenseDuration` （將預設為infinite）。 否則，請指定最終用戶應能享受流的時間。 </li></ol>

**表15:令牌限制查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| `expirationTime` | 此令牌的過期時間。 此值必須為 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 「Z」區域指示符（「祖魯時間」）中的日期/時間格式，或前面帶有+號的整數。 RFC 3339的一個示例是2006-04-14T12:01:10Z。 <br> 如果值是中的字串 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 日期/時間格式，則表示令牌的絕對到期日期/時間。 如果值是前面帶有+號的整數，則從發佈開始，它被解釋為令牌有效的相對秒數。 比如說， `+60` 指定一分鐘。 <br> 最大和預設（如果未指定）令牌生存期為30天。 | 否 |

**表16:相關查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `cookie` | 長達32個字元的任意字串，在令牌中攜帶，並由令牌兌現伺服器記錄。 可用於關聯兌現伺服器上的日誌條目和服務提供商伺服器上的日誌條目。 | 否 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**表17:HTTP響應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體正文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 許可證獲取URL +令牌 |
| `400 Bad Request` | 無效參數 | `text/html` 或 `application/json` | 錯誤描述 |
| `401 Unauthorized` | 身份驗證失敗 | `text/html` 或 `application/json` | 錯誤描述 |
| `404 Not found` | 錯誤URL | `text/html` 或 `application/json` | 錯誤描述 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤描述 |

**表18:事件錯誤代碼**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> 代碼 </th> 
   <th class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 無效的令牌過期時間： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 無效的IP地址 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 無效的內容加密密鑰： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 指定的輸出控制標誌無效： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 必須提供身份驗證令牌 </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 驗證令牌無效： &lt;details&gt; <p>注：如果驗證器錯誤或使用生產驗證器訪問*.test.expressplay.com上的testAPI時，可能會發生這種情況，反之亦然。 </p> <p importance="high">注：testSDK和高級Test工具(ATT)僅使用 <span class="filepath"> *.test.expressplay.com </span>，生產設備必須使用 <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用令牌不足 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 缺少租期結束時間 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 缺少租賃播放持續時間 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 租賃播放持續時間無效 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 內容加密密鑰必須為32個十六進位數字長 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理錯誤： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 已禁用服務帳戶 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie無效 </td> 
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
   <td> 擴展類型應為4個字元 </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 擴展負載應為Base64編碼 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> 輸出控制標誌 </span> 必須編碼4位元組 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 指定的錯誤格式無效： &lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> 無法驗證設備 </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> 無效的令牌 </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> 缺少 <span class="filepath"> 小孩 </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從密鑰儲存服務獲取內容密鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> 小孩 </span> 長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 小孩 </span> '^'後必須長64個字元 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 無效 <span class="codeph"> 小孩 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 無效的加密密鑰或 <span class="codeph"> 內科 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常規標誌無效 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密鑰資料無效 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租期無效 </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Widevine不支援設備ID綁定 </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 缺少安全級別值 </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 無效的安全級別值 </td> 
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
   <td> 未能生成Widevine許可證 </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 無效 <span class="codeph"> WVExtension </span> 指定的參數 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> 已禁用Widevine選項 </td> 
  </tr> 
 </tbody> 
</table>
