---
description: PlayReady授權Token介面提供生產與測試服務。
title: 播放就緒授權Token請求／回應
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---


# PlayReady授權Token要求／回應{#playready-license-token-request-response}

PlayReady授權Token介面提供生產與測試服務。

此HTTP要求會傳回可兌換為PlayReady授權的Token。

**方法：GET、POST** （含www-url編碼內文，其中包含兩種方法的參數）

**URL:**

* **生產：** `https://pr-gen.{prod_domain}/hms/pr/token`

* **測試：** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **請求範例：**

   ```
   <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
   https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
    <ExpressPlay customer authenticator identifier>
    &kid=<CEKSID>
    &contentKey=<CEK>
    &rightsType=BuyToOwn
    &analogVideoOPL=0
    &compressedDigitalAudioOPL=0
    &compressedDigitalVideoOPL=0
    &uncompressedDigitalAudioOPL=0
    &uncompressedDigitalVideoOPL=0
   </xref href="https:>
   ```

* **範例回應：**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## 請求查詢參數{#section_26F8856641A64A46A3290DBE61ACFAD2}

**表9:Token查詢參數**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查詢參數</b> </th> 
   <th class="entry"><b>說明</b> </th> 
   <th class="entry"><b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>這是您的客戶API金鑰，每個金鑰都適用於您的生產與測試環境。 您可在「ExpressPlay管理控制面板」標籤中找到這個選項。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td><span class="codeph"> html</span>或<span class="codeph"> json</span>。 如果<span class="codeph"> html</span>（預設值），則回應的實體主體中會提供任何錯誤的HTML表示法。 <p>如果指定<span class="codeph"> json</span>，則會傳回JSON格式的結構化回應。 如需詳細資訊，請參閱<a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤</a>。 </p> <p>回應的MIME類型為：成功時<span class="codeph"> text/uri-list</span>、HTML錯誤格式時的<span class="codeph"> text/html</span>或JSON錯誤格式時的<span class="codeph"> application/json</span>。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表10:授權查詢參數**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查詢參數</b> </th> 
   <th class="entry"><b>說明</b> </th> 
   <th class="entry"><b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>代表許可證標誌的4位元組十六進位字串。 對於永久許可證，必須將其設定為'0000001'。 <p>注意：租賃授權(<span class="codeph"> rightsType=Rental</span>)必須為永久性。 </p> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> key</span> </td> 
   <td> 密鑰加密密鑰(KEK)。 密鑰使用密鑰封裝算法（AES密鑰封裝，RFC3394）與KEK進行加密。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 小孩</span> </td> 
   <td>內容加密金鑰的16位元組十六進位字串表示法，或字串<span class="codeph"> ^somestring'</span>。 字串後跟'^'的長度不能大於64個字元。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> 加密內容密鑰的十六進位字串表示。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> 內容加密密鑰的16位元組十六進位字串表示 </td> 
   <td>是，除非提供<span class="codeph"> kek</span>和<span class="codeph"> ek</span>或<span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>指定權利的類別。 必須是<span class="codeph"> BuyToOwn</span>或<span class="codeph"> Rental</span>。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>租金結束日期。 此值必須採用「RFC 3339」_日期／時間格式，採用「Z」區域指示符（「祖魯時間」）格式，或前面帶有「+」符號的整數。 <p>如果值為<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a>日期／時間格式，則表示許可證的絕對到期日／時間。 RFC 3339日期／時間的示例是2006-04-14T12:01:10Z。 </p> <p> 如果值是前面有'+'符號的整數，則會以代號發出後的相對秒數表示。 此時後無法播放內容。 僅當<span class="codeph"> rightsType</span>是<span class="codeph"> Rental</span>時有效。 </p> </td> 
   <td>是，當<span class="codeph"> rightsType</span>為<span class="codeph"> Rental</span>時。 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>開始播放後，內容可播放的時間（以秒為單位）。 僅當<span class="codeph"> rightsType</span>為Rental時有效。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> 整數值，表示模擬視頻的「輸出保護級別」。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 整數值，表示壓縮數位音訊的輸出保護等級。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> 整數值，用以指示壓縮數位視訊的輸出保護等級。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompresstedDigitalAudioOPL</span> </td> 
   <td> 整數值，表示未壓縮數位音訊的輸出保護等級。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressentDigitalVideoOPL</span> </td> 
   <td> 整數值，表示未壓縮數位視訊的輸出保護等級。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>輸出未知時的必要行為。 允許的值：<span class="codeph">允許</span>、<span class="codeph">禁止</span>或<span class="codeph"> SDOnly</span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 4位元組的十六進位值，用以指出其他輸出控制選項的旗標 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>一個任意的4字母單詞，表示副檔名的32位標識符。 每個字母的8位ASCII碼是標識符的相應8位位元組部分。 例如，標識符值0x61626364（十六進位）將寫為「<span class="codeph"> chuang</span>」，因為「a」的ASCII代碼是0x61等。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> 擴充功能的base64編碼字串。 </td> 
   <td>是，當指定<span class="codeph"> extensionType</span>時。 </td> 
  </tr> 
 </tbody> 
</table>

## 響應{#section_0079C31B4AF14DBBB6277CF251FB90E3}

**表11:HTTP回應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體內文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 授權取得URL和Token |
| `400 Bad Request` | 無效的標籤 | `text/html` 或  `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或  `application/json` | 錯誤說明 |
| `404 Not found` | 錯誤的URL | `text/html` 或  `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或  `application/json` | 錯誤說明 |

**表12:事件錯誤代碼**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>程式碼</b> </th> 
   <th class="entry"><b>說明</b> </th> 
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
   <td>驗證Token無效：&lt;details&gt; <p>注意： 如果驗證器錯誤，或使用生產驗證器存取*.test.expressplay.com的測試API時，會發生這種情況，反之亦然。 </p> <p importance="high">注意：測試SDK和進階測試工具(ATT)僅適用於<span class="filepath"> *.test.expressplay.com</span>，而生產裝置必須使用<span class="filepath"> *.service.expressplay.com</span>。 </p> </td> 
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
   <td><span class="codeph"> </span> OutputControlFlags必須編碼4個位元組 </td> 
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
   <td> -4018 </td> 
   <td>缺少<span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從密鑰儲存服務獲取內容密鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> 孩</span> 子長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 在</span> ^後必須有64個字元 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>無效的<span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>無效的加密<span class="codeph">密鑰</span>或kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 無效的未知輸出類型錯誤 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 此服務的PlayReady選項已停用 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 一般標誌無效 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 設備ID必須有32個十六進位字元長 </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> 設備ID無效 </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> 缺少OPL值 </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>只能指定<span class="codeph"> kek</span>或<span class="codeph"> contentKey</span>中的一個 </td> 
  </tr> 
 </tbody> 
</table>
