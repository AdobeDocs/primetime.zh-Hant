---
seo-title: 伺服器屬性參考
title: 伺服器屬性參考
uuid: 24a187fe-9b7d-411f-a358-d10c70a5dd0e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 伺服器屬性參考{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## 個人化伺服器

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> 配置 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 範例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 傳輸憑證 </td> 
   <td>傳輸憑證用於解密從客戶端接收的請求並簽署返回的響應。 請務必使用傳輸憑證 <span class="filepath"></span> 檔的路徑以及加密的PKCS12密碼，正確設定AdobeInitial.properties檔案。 </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [包含個性化傳輸證書和密鑰的PKCS12檔案] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個人化CA憑證 </td> 
   <td>個性化伺服器使用個性化CA憑證來簽署其頒發的電腦證書。 請務必使用I15N CA憑證檔案的路徑以及加密的PKCS12密碼，正確設定 <span class="filepath"></span> AdobeInitial.properties檔案。 </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [包含個性化CA憑證和金鑰的PKCS12檔案] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個人化加密憑證 </td> 
   <td> 個人化伺服器使用加密憑證來加密需要傳送至個人化伺服器的敏感檔案。 例如，此證書支援許可證遷移，並用於加密個人化伺服器的DRM私鑰。 </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 內容快取 </td> 
   <td>這些設定可控制個人化伺服器下載內容的位置，以及快取內容至磁碟的位置。 個性化伺服器將在啟動時檢查內容伺服器是否有新內容一次，然後按這些屬性指定的頻率／時間檢查。 <p>對於內部個人化伺服器，我們包括了一組初始內容快取資料。 請務必將快取資 <i>料夾</i> （而非快取資料夾本身）的 <span class="filepath"> CONTENTS</span> 複製到已設定的 <span class="codeph"> AdobeInitial.properties</span> contentServer.localDirectory位置。 </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [要儲存本地內容的目錄（通常為tomcat/temp）] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Web server to contact for ECI info(本版<i>本不支援</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [連線逾時，以秒為單位] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [輪詢伺服器的頻率，以天為單位（最小值為1天）] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [輪詢伺服器的時間，自午夜以來的分鐘數] </li> 
    </ul> <p>請務必閱讀 <i>CRL和ECI Files</i> （有關保持快取最新的資訊）一節。 </p> </td> 
  </tr> 
  <tr> 
   <td> 個人化CA CRL </td> 
   <td> <p>此證書撤銷清單(CRL)分發點包含在個性化伺服器頒發的每台電腦證書中。 在授權伺服器上的機器憑證驗證期間，CRL將從憑證中所列的散布點下載(或從快取中讀取（如果已下載），並檢查以確保憑證未被撤銷。 建議在完成建立和部署個性化CA CRL的過程後執行此伺服器配置更改。 在任何配置更改後重新啟動個性化伺服器。 </p> <p>若要設定CRL散發點的URL，您必須設定 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> 欄位。 </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL分發點] </li> 
    </ul> <p>例如： </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>在處理授權要求後，授權伺服器應自動下載此CRL。 </p> <p importance="high">注意：Primetime DRM不會檢 <i>查此</i> 散布點是否有效。 您必須確認此URL有效。 除非從授權伺服器出現驗證錯誤，否則無效URL所產生的錯誤將不會出現。 </p> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td>視需要 <span class="filepath"> 設定AdobeInitial.properties</span> ，以進行記錄。 </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [將建立記錄檔的目錄] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [日誌中可能出現的最低級別的日誌消 <span class="codeph"> 息[DEBUG]| INFO]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [記錄檔的首碼。 日期／時間和副檔名"。log"將新增至檔案名稱] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [指定記錄的頻率。] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [記錄檔達到此大小時滾動(到達 <span class="codeph"> RollInterval或</span><span class="codeph"></span> RollSize時，記錄檔將滾動，以先到者為準)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true]| false ]指定是否應產生包含Adobe用來產生個人化報表之資料的個別檔案。] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [報表記錄檔的首碼。 日期／時間 <span class="filepath"> 和。log</span> 副檔名將會新增至檔案名稱。 l<span class="codeph"> og.Level</span> 屬性不適用於此日誌檔案，但 <span class="codeph"> log.RollInterval</span> 和 <span class="codeph"> log.RollSize</span> 。] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 其他 </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [加密的Base64編碼金鑰，用於HMAC裝置資訊，然後再將它加入機器Token中。 對於開發／測試／生產環境，密鑰可以不同，但對於特定環境中的所有伺服器，密鑰必須相同。] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [密鑰生成伺服器的位置（單個主機／埠，表示密鑰伺服器的池）] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [當隊列中還有這麼多鍵時，從KGS中擷取另一批鍵] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [Status頁將ping KGS以確定它是否可以到達伺服器。 如果未在指定的時間內收到回覆，則逾時。] </li> 
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
   <th class="entry"> 範例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 關鍵產生 </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.threads =</span> [用於生成密鑰的線程數（應等於電腦上可用的處理器數）] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [每批生成的鍵數] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [儲存關鍵批次檔案的目錄] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [要產生的關鍵批次檔案數上限] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [將建立記錄檔的目錄] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [記錄檔的首碼。 日期／時間 <span class="filepath"> 和。log</span> extension將新增至檔案名稱] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [日誌中可能出現的最低級別的日誌消息] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [指定記錄的頻率。] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [記錄檔達到此大小時滾動(到達 <span class="codeph"> RollInterval或</span><span class="codeph"></span> RollSize時，記錄檔將滾動，以先到者為準)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
