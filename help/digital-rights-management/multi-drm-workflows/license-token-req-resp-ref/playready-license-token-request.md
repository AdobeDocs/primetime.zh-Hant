---
description: PlayReady授權Token介面提供生產和測試服務。
title: PlayReady授權權杖請求/回應
exl-id: 12f925f7-336b-42b2-95a9-e806801bab8c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# PlayReady授權權杖請求/回應 {#playready-license-token-request-response}

PlayReady授權Token介面提供生產和測試服務。

此HTTP要求傳回可兌換為PlayReady授權的Token。

**方法：GET、POST** （內含www-url編碼內文，其中包含這兩種方法的引數）

**URL：**

* **生產：** `https://pr-gen.{prod_domain}/hms/pr/token`

* **測試：** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **範例請求：**

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

## 要求查詢引數 {#section_26F8856641A64A46A3290DBE61ACFAD2}

**表9： Token查詢引數**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查詢引數</b> </th> 
   <th class="entry"><b>說明</b> </th> 
   <th class="entry"><b>必填？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticate</span> </td> 
   <td> <p>這是您的客戶API金鑰，生產環境和測試環境各一個。 您可以在ExpressPlay管理控制面板標籤上找到此專案。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td>兩者之一 <span class="codeph"> html</span> 或 <span class="codeph"> json</span>. 若 <span class="codeph"> html</span> （預設）在回應的圖元主體中提供任何錯誤的HTML表示。 <p>若 <span class="codeph"> json</span> 指定，則會傳回JSON格式的結構化回應。 另請參閱 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON錯誤</a> 以取得詳細資訊。 </p> <p>回應的mime型別是 <span class="codeph"> text/uri-list</span> 成功時， <span class="codeph"> text/html</span> HTML錯誤格式，或 <span class="codeph"> application/json</span> （JSON錯誤格式）。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表10：授權查詢引數**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查詢引數</b> </th> 
   <th class="entry"><b>說明</b> </th> 
   <th class="entry"><b>必填？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>代表授權旗標的4位元組十六進位字串。 永久授權必須設為'00000001'。 <p>注意：租用授權(<span class="codeph"> rightsType=租用</span>)必須為持續性。 </p> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 金鑰</span> </td> 
   <td> 金鑰加密金鑰(KEK)。 金鑰是使用KEK加密後使用金鑰包裝演演算法(AES Key Wrap，RFC3394)儲存的。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kid</span> </td> 
   <td>內容加密金鑰或字串的16位元組十六進位字串表示 <span class="codeph"> ^somestring'</span>. 字串後面接著'^'的長度不能超過64個字元。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> 加密內容金鑰的十六進位字串表示法。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> 內容加密金鑰的16位元組十六進位字串表示法 </td> 
   <td>是，除非 <span class="codeph"> 金鑰</span> 和 <span class="codeph"> ek</span> 或 <span class="codeph"> kid</span> 提供 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>指定許可權的種類。 必須是 <span class="codeph"> BuyTown</span> 或 <span class="codeph"> 租賃</span>. </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>租賃結束日期。 此值必須是'RFC 3339' _ 'Z'區域指示符（'Zulu時間'）格式的日期/時間格式，或是以'+'符號開頭的整數。 <p>如果值是 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> 日期/時間格式，則代表授權的絕對到期日/時間。 RFC 3339日期/時間的範例為2006-04-14T12:01:10Z。 </p> <p> 如果值是前面有'+'符號的整數，則會視為從核發權杖開始算起的相對秒數。 此時間之後無法播放內容。 只有在 <span class="codeph"> rightsType</span> 是 <span class="codeph"> 租賃</span>. </p> </td> 
   <td>是，當 <span class="codeph"> rightsType</span> 是 <span class="codeph"> 租賃</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>播放開始後可以播放內容的時間（以秒為單位）。 只有在 <span class="codeph"> rightsType</span> 為租用。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> 表示類比視訊輸出保護等級的整數值。 有效範圍為0到999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 表示壓縮數位音訊輸出保護等級的整數值。 有效範圍為0到999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> 表示壓縮數位視訊輸出保護等級的整數值。 有效範圍為0到999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> 表示未壓縮數位音訊輸出保護等級的整數值。 有效範圍為0到999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> 表示未壓縮數位視訊輸出保護等級的整數值。 有效範圍為0到999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>輸出不明時的必要行為。 允許的值： <span class="codeph"> 允許</span>， <span class="codeph"> 不允許</span> 或 <span class="codeph"> SDOnly</span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 4位元組的十六進位值，表示其他輸出控制選項的旗標 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>代表副檔名32位元識別碼的任意4字母單字。 每個字母的8位元ASCII代碼都是識別碼中對應的8位元組部分。 例如，識別碼值0x61626364 （十六進位）將會寫入'<span class="codeph"> abcd</span>'，因為'a'的ASCII程式碼為0x61等。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> 擴充功能的base64編碼字串。 </td> 
   <td>是，當 <span class="codeph"> extensionType</span> 已指定。 </td> 
  </tr> 
 </tbody> 
</table>

## 回應 {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**表11： HTTP回應**

| **HTTP狀態代碼** | **說明** | **Content-Type** | **實體內文包含** |
|---|---|---|---|
| `200 OK` | 沒有錯誤。 | `text/uri-list` | 授權贏取URL和權杖 |
| `400 Bad Request` | 無效的引數 | `text/html` 或 `application/json` | 錯誤說明 |
| `401 Unauthorized` | 驗證失敗 | `text/html` 或 `application/json` | 錯誤說明 |
| `404 Not found` | 錯誤的URL | `text/html` 或 `application/json` | 錯誤說明 |
| `50x Server Error` | 伺服器錯誤 | `text/html` 或 `application/json` | 錯誤說明 |

**表12：事件錯誤代碼**

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
   <td>驗證Token無效： &lt;details&gt; <p>注意：如果驗證器錯誤或使用生產驗證器在*.test.expressplay.com存取測試API時，可能會發生這種情況，反之亦然。 </p> <p importance="high">注意：測試SDK和進階測試工具(ATT)僅適用於 <span class="filepath"> *.test.expressplay.com</span>，但生產裝置必須使用 <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td> 無效的輸出控制，值超出指定範圍 </td> 
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
   <td> 擴充功能承載應為Base64編碼 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td><span class="codeph"> OutputControlFlag</span> 必須是4位元組的編碼 </td> 
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
   <td> -4018 </td> 
   <td>遺失 <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 無法從金鑰儲存服務取得內容金鑰 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> kid</span> 長度必須為32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> kid</span> ^後面必須為64個字元長 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>無效 <span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>加密無效 <span class="codeph"> 金鑰</span> 或金鑰 </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 無效的未知輸出型別錯誤 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 此服務的PlayReady選項已停用 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 無效的一般旗標 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 裝置ID長度必須是32個十六進位字元 </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> 無效的裝置識別碼 </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> 缺少OPL值 </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>只有一個 <span class="codeph"> 金鑰</span> 或 <span class="codeph"> contentKey</span> 可以指定 </td> 
  </tr> 
 </tbody> 
</table>
