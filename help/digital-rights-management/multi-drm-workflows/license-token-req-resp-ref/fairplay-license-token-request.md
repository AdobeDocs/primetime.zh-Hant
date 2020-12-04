---
description: FairPlay授權Token介面提供製作和測試服務。
seo-description: FairPlay授權Token介面提供製作和測試服務。
seo-title: FairPlay授權Token要求／回應
title: FairPlay授權Token要求／回應
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---


# FairPlay授權Token請求與回應{#fairplay-license-token-request-response}

FairPlay授權Token介面提供製作和測試服務。 此要求會傳回可兌換為FairPlay授權的Token。

**方法：GET, POST** （含www-url編碼的內文，包含兩種方法的參數）

**URL:**

* **生產：** `https://fp-gen.{prod_domain}/hms/fp/token`

* **測試：** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **請求範例：**

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

* **範例回應：**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**請求查詢參數**

**表3:Token查詢參數**

| 查詢參數 | 說明 | 需要？ |
|--- |--- |--- |
| customerAuthenticator客戶驗證器作為查詢參數customerAuthenticator FairPlay | 這是您的客戶API金鑰，每個金鑰都適用於您的生產與測試環境。 您可在「ExpressPlay管理控制面板」標籤中找到這個選項。 | 是 |
| errorFormat | html或json。 如果html（預設值），回應的實體主體中會提供任何錯誤的HTML表示法。 如果指定json，則會傳回JSON格式的結構化回應。 如需詳細資訊，請參閱[JSON錯誤](https://www.expressplay.com/developer/restapi/#json-errors)。 回應的MIME類型為成功時的text/uri-list、HTML錯誤格式的text/html或JSON錯誤格式的application/json。 | 否 |

**表4:授權查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `generalFlags` | 代表許可證標誌的4位元組十六進位字串。 &#39;0000&#39;是唯一允許的值。 | 否 |
| `kek` | 密鑰加密密鑰(KEK)。 密鑰使用密鑰封裝算法（AES密鑰封裝，RFC3394）與KEK進行加密。 如果提供`kek`，則需要提供`kid`或`ek`參數之一，*但不同時提供*&#x200B;參數。 | 否 |
| `kid` | 內容加密密鑰或字串`'^somestring'`的16位元組十六進位字串表示。 字串後跟`'^'`的長度不能大於64個字元。 | 否 |
| `ek` | 加密內容密鑰的十六進位字串表示。 | 否 |
| `contentKey` | 內容加密密鑰的16位元組十六進位字串表示 | 是，除非提供`kek`和`ek`或`kid`。 |
| `iv` | 內容加密的16位元組十六進位字串表示法IV | 是 |
| `rentalDuration` | 租金的持續時間（以秒為單位）（預設值- 0） | 否 |
| `fpExtension` | 以逗號分隔字串包住`extensionType`和`extensionPayload`的簡短表格。 例如：[...] `&fpExtension=wudo,AAAAAA==&`[...] | 否，可以使用任何數字 |

**表5:Token限制查詢參數**

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
   <td> <span class="codeph"> expirationTime  </span> </td> 
   <td> 此代號的過期時間。 此值必須是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a>日期／時間格式中「Z」區域指示符（「祖魯時間」）的字串，或前面帶有「+」符號的整數。 RFC 3339日期／時間的示例為<span class="codeph"> 2006-04-14T12:01:10Z </span>。 <p>如果值是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a>日期／時間格式的字串，則它表示令牌的絕對到期日／時間。 如果值是前面有'+'符號的整數，則會將其解讀為從發行開始的相對秒數，表示代號有效。 </p> 例如，<span class="codeph"> +60 </span>指定一分鐘。 最大和預設（如果未指定）Token期限為30天。 </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表6:關聯查詢參數**

| **查詢參數** | **說明** | **需要？** |
|---|---|---|
| `cookie` | 長度高達32個字元的任意字串，載於Token中，並由Token兌換伺服器記錄。 這可用於將兌換伺服器上的日誌條目與服務提供商的伺服器上的日誌條目關聯起來。 | 否 |

**回應**

**表7:HTTP回應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體內文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 授權贏取URL + Token |
| `400 Bad Request` | 無效的標籤 | `text/html` 或  `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或  `application/json` | 錯誤說明 |
| `404 Not found` | 錯誤的URL | `text/html` 或  `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或  `application/json` | 錯誤說明 |

**表8:事件錯誤代碼**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>程式碼</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
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
   <td> 驗證Token無效：&lt;details&gt; <p>注意： 如果驗證器錯誤，或使用生產驗證器存取<span class="filepath"> *.test.expressplay.com </span>的測試API時，也會發生這種情況，反之亦然。 </p> <p importance="high">注意： 測試SDK和進階測試工具(ATT)僅適用於<span class="filepath"> *.test.expressplay.com </span>，而生產裝置必須使用<span class="filepath"> *.service.expressplay.com </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用預付碼不足 </td> 
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
   <td> 《失蹤小子》 </td> 
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
   <td> <span class="codeph"> 小 </span> 數字必須在^後長64個字元 </td> 
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
   <td> -6001 </td> 
   <td> 指定的<span class="codeph"> FPExtension </span>參數無效 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> 無效的FP Token類型 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 指定的<span class="codeph"> iv </span>參數無效 </td> 
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
   <td> 未授權FairPlay支援的服務 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租用期間無效 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay不支援裝置ID系結 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> 停用FairPlay選項 </td> 
  </tr> 
 </tbody> 
</table>