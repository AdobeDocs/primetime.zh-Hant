---
description: FairPlay授權Token介面可提供生產和測試服務。
title: FairPlay授權權杖請求/回應
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# FairPlay授權Token要求與回應 {#fairplay-license-token-request-response}

FairPlay授權Token介面可提供生產和測試服務。 此請求傳回可兌換為FairPlay授權的代號。

**方法：GET，POST** （內含www-url編碼內文，其中包含這兩種方法的引數）

**URL：**

* **生產：** `https://fp-gen.{prod_domain}/hms/fp/token`

* **測試：** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **範例要求：**

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

**要求查詢引數**

**表3： Token查詢引數**

| 查詢引數 | 說明 | 必填？ |
|--- |--- |--- |
| customerAuthenticator作為查詢引數的客戶驗證器customerAuthenticator FairPlay | 這是您的客戶API金鑰，分別用於生產和測試環境。 您可以在ExpressPlay的「管理控制面板」標籤上找到此資訊。 | 是 |
| errororformat | html或json。 如果html （預設）會在回應的實體本文中提供任何錯誤的HTML表示。 若指定JSON，則會傳回JSON格式的結構化回應。 另請參閱 [JSON錯誤](https://www.expressplay.com/developer/restapi/#json-errors) 以取得詳細資訊。 回應的mime型別成功時為text/uri-list、HTML錯誤格式時為text/html，或JSON錯誤格式時為application/json。 | 否 |

**表4：授權查詢引數**

| **查詢引數** | **說明** | **必填？** |
|---|---|---|
| `generalFlags` | 代表授權旗標的4位元組十六進位字串。 &#39;0000&#39;是唯一允許的值。 | 否 |
| `kek` | 金鑰加密金鑰(KEK)。 金鑰是使用KEK使用金鑰包裝演演算法(AES Key Wrap，RFC3394)加密儲存的。 如果 `kek` 已提供， `kid` 或 `ek` 需要提供引數， *但不是兩者*. | 否 |
| `kid` | 內容加密金鑰或字串的16位元組十六進位字串表示法 `'^somestring'`. 字串的長度，後面接著 `'^'` 不可超過64個字元。 | 否 |
| `ek` | 已加密內容金鑰的十六進位字串表示法。 | 否 |
| `contentKey` | 內容加密金鑰的16位元組十六進位字串表示法 | 是，除非 `kek` 和 `ek` 或 `kid` 提供。 |
| `iv` | 內容加密IV的16位元組十六進位字串表示 | 是 |
| `rentalDuration` | 租用的期間（以秒為單位，預設為 — 0） | 否 |
| `fpExtension` | 簡短表單換行 `extensionType` 和 `extensionPayload`，以逗號分隔的字串。 例如： [...] `&fpExtension=wudo,AAAAAA==&`[...] | 否，可使用任何數字 |

**表5：權杖限制查詢引數**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查詢引數</b> </th> 
   <th class="entry"> <b>說明</b> </th> 
   <th class="entry"> <b>必填？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> 過期時間 </span> </td> 
   <td> 此Token的到期時間。 此值必須是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 'Z'區域指示符號中的日期/時間格式('Zulu time')，或開頭為'+'符號的整數。 RFC 3339日期/時間的範例為 <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>如果值是中的字串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 日期/時間格式，則代表權杖的絕對到期日期/時間。 如果值是前面有'+'符號的整數，則會從簽發將其解譯為權杖有效的相對秒數。 </p> 例如， <span class="codeph"> +60 </span> 指定一分鐘。 權杖存留期的上限和預設（如果未指定）為30天。 </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表6：相互關聯查詢引數**

| **查詢引數** | **說明** | **必填？** |
|---|---|---|
| `cookie` | 長度最多32個字元的任意字串，由權杖攜帶並由權杖兌換伺服器記錄。 這可用來將兌換伺服器的記錄專案與服務提供者伺服器的記錄專案相互關聯。 | 否 |

**回應**

**表7： HTTP回應**

| **HTTP狀態代碼** | **說明** | **Content-Type** | **實體本文包含** |
|---|---|---|---|
| `200 OK` | 沒有錯誤。 | `text/uri-list` | 授權贏取URL + Token |
| `400 Bad Request` | 無效的引數 | `text/html` 或 `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或 `application/json` | 錯誤說明 |
| `404 Not found` | URL錯誤 | `text/html` 或 `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤說明 |

**表8：事件錯誤代碼**

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
   <td> 驗證Token無效： &lt;details&gt; <p>注意：如果驗證器錯誤或在存取測試API時，可能會發生這種情況 <span class="filepath"> *.test.expressplay.com </span> 使用生產驗證器，反之亦然。 </p> <p importance="high">注意：測試SDK和進階測試工具(ATT)僅適用於 <span class="filepath"> *.test.expressplay.com </span>，但生產裝置必須使用 <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用的權杖不足 </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> 缺少許可權型別 </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> 無效的許可權型別 </td> 
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
   <td> 遺失的孩子 </td> 
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
   <td> <span class="codeph"> kid </span> ^後面必須為64個字元 </td> 
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
   <td> -6001 </td> 
   <td> 無效 <span class="codeph"> FPExtension </span> 指定的引數 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> 無效的FP Token型別 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 無效 <span class="codeph"> iv </span> 指定引數 </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> 無法產生FP的CKC </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的金鑰資料無效 </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> 服務未獲授權支援FairPlay </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租借期間無效 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay不支援裝置ID繫結 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> 已停用FairPlay選項 </td> 
  </tr> 
 </tbody> 
</table>
