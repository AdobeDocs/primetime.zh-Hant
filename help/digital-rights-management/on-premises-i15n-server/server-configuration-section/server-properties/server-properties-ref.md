---
title: 伺服器屬性引用
description: 伺服器屬性引用
copied-description: true
exl-id: 8724d097-7cba-4ca9-b597-df56f80b2e9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# 伺服器屬性引用{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## 個性化伺服器

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> 配置 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 示例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 傳輸憑據 </td> 
   <td>傳輸憑據用於解密從客戶端接收的請求並對發送回的響應進行簽名。 確保配置 <span class="filepath"> AdobeInitial.properties</span> 檔案，同時包含傳輸憑據檔案的路徑以及加密的PKCS12密碼。 </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [包含個性化傳輸證書和密鑰的PKCS12檔案] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個性化CA憑據 </td> 
   <td>個性化伺服器使用個性化CA憑據來簽名其頒發的電腦證書。 確保配置 <span class="filepath"> AdobeInitial.properties</span> 檔案，同時包含I15N CA憑據檔案的路徑以及加密的PKCS12密碼。 </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [包含個性化CA證書和密鑰的PKCS12檔案] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個性化加密憑據 </td> 
   <td> 個性化伺服器使用加密憑據對需要傳輸到個性化伺服器的敏感檔案進行加密。 例如，此證書支援許可證遷移，還用於加密個性化伺服器的DRM私鑰。 </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 內容快取 </td> 
   <td>這些設定控制個性化伺服器從中下載內容的位置以及內容快取到磁碟上的位置。 個性化伺服器將在啟動時檢查內容伺服器是否有新內容，然後按這些屬性指定的頻率/時間檢查。 <p>對於本地個性化伺服器，我們包含了一組初始內容快取資料。 確保複製 <i>內容</i> 將快取資料夾（而不是快取資料夾本身） <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> 位置。 </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [儲存本地內容的目錄（通常為tomcat/temp）] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [要聯繫的Web伺服器獲取ECI資訊(<i>此版本不支援</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [連接超時，秒] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [輪詢伺服器的頻率（以天為單位）（最少為1天）] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [輪詢伺服器的時間，自午夜以來的分鐘數] </li> 
    </ul> <p>請務必閱讀該部分 <i>CRL和ECI檔案</i> 讓快取保持最新。 </p> </td> 
  </tr> 
  <tr> 
   <td> 個性化CA CRL </td> 
   <td> <p>此證書吊銷清單(CRL)分發點包含在個性化伺服器頒發的每個電腦證書中。 在許可證伺服器上的電腦證書驗證期間，將從證書中列出的分發點下載CRL（如果已下載，則從快取中讀取），並檢查以確保證書未被吊銷。 建議在完成建立和部署個性化CA CRL的過程後執行此伺服器配置更改。 在任何配置更改後重新啟動個性化伺服器。 </p> <p>要設定CRL分發點的URL，需要設定 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> 的子菜單。 </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL分發點] </li> 
    </ul> <p>例如： </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>一旦處理了許可證請求，許可證伺服器應自動下載此CRL。 </p> <p importance="high">注：此分發點 <i>不</i> 已由黃金時段DRM檢查有效性。 必須驗證此URL是否有效。 在許可證伺服器中出現驗證錯誤之前，將不會顯示無效URL導致的錯誤。 </p> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td>配置 <span class="filepath"> AdobeInitial.properties</span> 記錄。 </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [將建立日誌檔案的目錄] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [日誌中可能顯示的最低級別日誌消息 <span class="codeph"> [調試] |資訊]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [日誌檔案的前置詞。 日期/時間和"。log"副檔名將添加到檔案名] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [指定日誌滾動的頻率。] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [當日誌達到此大小時滾動(日誌將在 <span class="codeph"> 滾動間隔</span> 或 <span class="codeph"> 卷大小</span> 已到達（以先到者為準）] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[true] |false ]指定是否應生成包含Adobe用於生成個性化報告的資料的單獨檔案。] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [報告日誌檔案的前置詞。 日期/時間和 <span class="filepath"> .日誌</span> 副檔名將添加到檔案名。 L<span class="codeph"> 日誌級別</span> 屬性不適用於此日誌檔案，但 <span class="codeph"> log.RollInterval</span> 和 <span class="codeph"> log.RollSize</span> 。] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 其他 </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [將加密的Base64編碼密鑰用於HMAC設備資訊，然後將其包含在電腦令牌中。 對於開發/暫存/生產環境，密鑰可以不同，但對於特定環境中的所有伺服器，密鑰必須相同。] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [密鑰代伺服器的位置（單個主機/埠，表示密鑰伺服器池）] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [當隊列中剩餘的鍵數如此多時，從KGS中提取另一批鍵] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.timeout =</span> [狀態頁將ping KGS以確定它是否可以訪問伺服器。 如果在指定的時間內未收到回復，則將超時。] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 密鑰生成伺服器 {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> 配置 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 示例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 密鑰生成 </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.threads =</span> [用於生成密鑰的線程數（應等於電腦上可用的處理器數）] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [每批生成的密鑰數] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [儲存密鑰批處理檔案的目錄] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [要生成的密鑰批處理檔案的最大數量] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [將建立日誌檔案的目錄] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [日誌檔案的前置詞。 日期/時間和 <span class="filepath"> .日誌</span> 副檔名將添加到檔案名] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [日誌中可能顯示的最低級別日誌消息] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [指定日誌滾動的頻率。] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [當日誌達到此大小時滾動(日誌將在 <span class="codeph"> 滾動間隔</span> 或 <span class="codeph"> 卷大小</span> 已到達（以先到者為準）] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
