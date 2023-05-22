---
description: FairPlay許可證令牌介面提供生產和test服務。
title: FairPlay許可證令牌請求/響應
exl-id: 7073a74b-d907-4d45-8550-4305655c33f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# FairPlay許可證令牌請求和響應 {#fairplay-license-token-request-response}

FairPlay許可證令牌介面提供生產和test服務。 此請求返回可兌換為FairPlay許可證的令牌。

**方法：GET,POST** （具有包含兩種方法參數的www-url編碼主體）

**URL:**

* **生產：** `https://fp-gen.{prod_domain}/hms/fp/token`

* **Test:** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **示例請求：**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **示例響應：**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**請求查詢參數**

**表3:令牌查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| customerAuthenticator客戶驗證器作為查詢參數customerAuthenticator公平播放 | 這是您的客戶API密鑰，每個密鑰用於您的生產和test環境。 您可以在「ExpressPlay管理儀表板」頁籤上找到此選項。 | 是 |
| 錯誤格式 | html或json。 如果html（預設），則在響應的實體主體中提供任何錯誤的HTML表示。 如果指定json，則返回JSON格式的結構化響應。 請參閱 [JSON錯誤](https://www.expressplay.com/developer/restapi/#json-errors) 的雙曲餘切值。 響應的mime類型為成功時的text/uri-list、HTML錯誤格式的text/html或JSON錯誤格式的application/json。 | 否 |

**表4:許可證查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `generalFlags` | 代表許可證標誌的4位元組十六進位字串。 「0000」是唯一允許的值。 | 否 |
| `kek` | 密鑰加密密鑰(KEK)。 密鑰使用密鑰包裝算法（AES密鑰包裝，RFC3394）使用KEK進行加密儲存。 如果 `kek` 是提供的，其中任一 `kid` 或 `ek` 需要提供參數， *但不同時*。 | 否 |
| `kid` | 內容加密密鑰或字串的16位元組十六進位字串表示 `'^somestring'`。 字串後跟的長度 `'^'` 不能超過64個字元。 | 否 |
| `ek` | 加密內容密鑰的十六進位字串表示形式。 | 否 |
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是的，除非 `kek` 和 `ek` 或 `kid` 中。 |
| `iv` | 內容加密IV的16位元組十六進位字串表示 | 是 |
| `rentalDuration` | 租用的持續時間（秒）（預設 — 0） | 否 |
| `fpExtension` | 短格式包裝 `extensionType` 和 `extensionPayload`，作為逗號分隔的字串。 例如： [...] `&fpExtension=wudo,AAAAAA==&`[...] | 否，可以使用任何數字 |

**表5:令牌限制查詢參數**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查詢參數</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
   <th class="entry"> <b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> 到期時間 </span> </td> 
   <td> 此令牌的過期時間。 此值必須是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 「Z」區域指示符（「祖魯時間」）中的日期/時間格式，或前面帶「+」符號的整數。 RFC 3339的一個示例是 <span class="codeph"> 2006-04-14T12:01:10Z </span>。 <p>如果值是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 日期/時間格式，則表示令牌的絕對到期日期/時間。 如果值是前面帶有「+」符號的整數，則從發佈開始，它被解釋為令牌有效的相對秒數。 </p> 比如說， <span class="codeph"> +60 </span> 指定一分鐘。 最大和預設（如果未指定）令牌生存期為30天。 </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表6:相關查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `cookie` | 長達32個字元的任意字串，在令牌中攜帶，並由令牌兌現伺服器記錄。 這可用於關聯兌現伺服器上的日誌條目和服務提供商伺服器上的日誌條目。 | 否 |

**響應**

**表7:HTTP響應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體正文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 許可證獲取URL +令牌 |
| `400 Bad Request` | 無效參數 | `text/html` 或 `application/json` | 錯誤描述 |
| `401 Unauthorized` | 身份驗證失敗 | `text/html` 或 `application/json` | 錯誤描述 |
| `404 Not found` | 錯誤URL | `text/html` 或 `application/json` | 錯誤描述 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤描述 |

**表8:事件錯誤代碼**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>代碼</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
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
   <td> 驗證令牌無效： &lt;details&gt; <p>注：如果驗證器錯誤或訪問testAPI時，可能會發生這種情況 <span class="filepath"> *.test.expressplay.com </span> 使用生產驗證器，反之亦然。 </p> <p importance="high">注：testSDK和高級Test工具(ATT)僅使用 <span class="filepath"> *.test.expressplay.com </span>，生產設備必須使用 <span class="filepath"> *.service.expressplay.com </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用令牌不足 </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> 缺少權限類型 </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> 權限類型無效 </td> 
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
   <td> 《失蹤的孩子》 </td> 
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
   <td> <span class="codeph"> 小孩 </span> ^後必須長64個字元 </td> 
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
   <td> -6001 </td> 
   <td> 無效 <span class="codeph"> FPExtension </span> 指定的參數 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> 無效的FP令牌類型 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 無效 <span class="codeph"> 四 </span> 指定的參數 </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> 無法為FP生成CKC </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密鑰資料無效 </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> 未授權為FairPlay支援的服務 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租期無效 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay不支援設備ID綁定 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> FairPlay選項已禁用 </td> 
  </tr> 
 </tbody> 
</table>
