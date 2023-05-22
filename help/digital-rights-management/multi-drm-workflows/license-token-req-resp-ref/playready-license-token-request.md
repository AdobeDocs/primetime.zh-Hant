---
description: PlayReady許可證令牌介面提供生產和test服務。
title: PlayReady許可證令牌請求/響應
exl-id: 12f925f7-336b-42b2-95a9-e806801bab8c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# PlayReady許可證令牌請求/響應 {#playready-license-token-request-response}

PlayReady許可證令牌介面提供生產和test服務。

此HTTP請求返回可兌換為PlayReady許可證的令牌。

**方法：GET,POST** （具有包含兩種方法參數的www-url編碼主體）

**URL:**

* **生產：** `https://pr-gen.{prod_domain}/hms/pr/token`

* **Test:** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **示例請求：**

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

* **示例響應：**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## 請求查詢參數 {#section_26F8856641A64A46A3290DBE61ACFAD2}

**表9:令牌查詢參數**

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
   <td> <p>這是您的客戶API密鑰，每個密鑰用於您的生產和test環境。 您可以在「ExpressPlay管理儀表板」頁籤上找到此選項。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 錯誤格式</span> </td> 
   <td>要麼 <span class="codeph"> html</span> 或 <span class="codeph"> jon</span>。 如果 <span class="codeph"> html</span> （預設）在響應的實體主體中提供任何錯誤的HTML表示。 <p>如果 <span class="codeph"> jon</span> 指定後，將返回JSON格式的結構化響應。 請參閱 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤</a> 的雙曲餘切值。 </p> <p>響應的MIME類型為 <span class="codeph"> 文本/URI清單</span> 成功， <span class="codeph"> 文本/html</span> HTML錯誤格式，或 <span class="codeph"> 應用程式/json</span> JSON錯誤格式。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表10:許可證查詢參數**

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
   <td><span class="codeph"> 常規標誌</span> </td> 
   <td>代表許可證標誌的4位元組十六進位字串。 對於永久許可證，必須將其設定為'0000001'。 <p>注：租賃許可證(<span class="codeph"> rightsType=Rental</span>)必須持久。 </p> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 內科</span> </td> 
   <td> 密鑰加密密鑰(KEK)。 密鑰使用密鑰包裝算法（AES密鑰包裝，RFC3394）使用KEK進行加密儲存。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 小孩</span> </td> 
   <td>內容加密密鑰或字串的16位元組十六進位字串表示 <span class="codeph"> ^somstring</span>。 字串後跟「^」的長度不能大於64個字元。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 臭</span> </td> 
   <td> 加密內容密鑰的十六進位字串表示形式。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 內容密鑰</span> </td> 
   <td> 內容加密密鑰的16位元組十六進位字串表示 </td> 
   <td>是，除非 <span class="codeph"> 內科</span> 和 <span class="codeph"> 臭</span> 或 <span class="codeph"> 小孩</span> 提供 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 權限類型</span> </td> 
   <td>指定權限的類型。 必須 <span class="codeph"> 購買至擁有</span> 或 <span class="codeph"> 租金</span>。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>租賃結束日期。 此值必須採用「RFC 3339」_日期/時間格式，採用「Z」區域指示符（「祖魯時間」）格式，或前面帶「+」符號的整數。 <p>如果值為 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> 日期/時間格式，則表示許可證的絕對到期日/時間。 RFC 3339的一個示例是2006-04-14T12:01:10Z。 </p> <p> 如果值是前面帶有「+」符號的整數，則該值被視為自發出令牌時起的相對秒數。 此時後無法播放內容。 僅在 <span class="codeph"> 權限類型</span> 是 <span class="codeph"> 租金</span>。 </p> </td> 
   <td>是，當 <span class="codeph"> 權限類型</span> 是 <span class="codeph"> 租金</span>。 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>開始播放後可以播放內容的時間（秒）。 僅在 <span class="codeph"> 權限類型</span> 就是租。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 模擬視頻OPL</span> </td> 
   <td> 用於指示模擬視頻的輸出保護級別的整數值。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 壓縮DigitalAudioOPL</span> </td> 
   <td> 用於指示壓縮數字音頻的輸出保護級別的整數值。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 壓縮DigitalVideoOPL</span> </td> 
   <td> 用於指示壓縮數字視頻的輸出保護級別的整數值。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 未壓縮的DigitalAudioOPL</span> </td> 
   <td> 用於指示未壓縮數字音頻的輸出保護級別的整數值。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 未壓縮的DigitalVideoOPL</span> </td> 
   <td> 用於指示未壓縮數字視頻的輸出保護級別的整數值。 有效範圍0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 未知輸出行為</span> </td> 
   <td>輸出未知時所需的行為。 允許的值： <span class="codeph"> 允許</span>。 <span class="codeph"> 不允許</span> 或 <span class="codeph"> 僅</span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 一個4位元組的十六進位值，用於指示其他輸出控制選項的標誌 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 擴展類型</span> </td> 
   <td>表示擴展的32位標識符的任意4字母字。 每個字母的8位ASCII代碼是標識符的相應8位位元組部分。 例如，標識符值0x61626364（十六進位）將寫入「<span class="codeph"> xan</span>「 」，因為「 a」的ASCII代碼是0x61等。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 擴展負載</span> </td> 
   <td> 擴展的base64編碼字串。 </td> 
   <td>是，當 <span class="codeph"> 擴展類型</span> 。 </td> 
  </tr> 
 </tbody> 
</table>

## 響應 {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**表11:HTTP響應**

| **HTTP狀態代碼** | **說明** | **內容類型** | **實體正文包含** |
|---|---|---|---|
| `200 OK` | 無錯誤。 | `text/uri-list` | 許可證獲取URL和令牌 |
| `400 Bad Request` | 無效參數 | `text/html` 或 `application/json` | 錯誤描述 |
| `401 Unauthorized` | 身份驗證失敗 | `text/html` 或 `application/json` | 錯誤描述 |
| `404 Not found` | 錯誤URL | `text/html` 或 `application/json` | 錯誤描述 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤描述 |

**表12:事件錯誤代碼**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>代碼</b> </th> 
   <th class="entry"><b>說明</b> </th> 
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
   <td>驗證令牌無效： &lt;details&gt; <p>注：如果驗證器錯誤或使用生產驗證器訪問*.test.expressplay.com上的testAPI時，可能會發生這種情況，反之亦然。 </p> <p importance="high">注：testSDK和高級Test工具(ATT)僅使用 <span class="filepath"> *.test.expressplay.com</span>，生產設備必須使用 <span class="filepath"> *.service.expressplay.com</span>。 </p> </td> 
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
   <td><span class="codeph"> 輸出控制標誌</span> 必須編碼4位元組 </td> 
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
   <td> -4018 </td> 
   <td>缺少 <span class="codeph"> 小孩</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從密鑰儲存服務獲取內容密鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> 小孩</span> 長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 小孩</span> ^後必須長64個字元 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>無效 <span class="codeph"> 小孩</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>無效加密 <span class="codeph"> 鍵</span> 或 </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 未知輸出類型錯誤無效 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 此服務已禁用PlayReady選項 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常規標誌無效 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 設備ID必須長32個十六進位字元 </td> 
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
   <td>只有一個 <span class="codeph"> 內科</span> 或 <span class="codeph"> 內容密鑰</span> 可以指定 </td> 
  </tr> 
 </tbody> 
</table>
