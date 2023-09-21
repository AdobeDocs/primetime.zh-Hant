---
title: 伺服器屬性參考
description: 伺服器屬性參考
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# 伺服器屬性參考{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## 個人化伺服器

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> 設定 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 範例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 傳輸認證 </td> 
   <td>傳輸認證可用來解密從使用者端收到的要求，並簽署傳回的回應。 請務必設定 <span class="filepath"> AdobeInitial.properties</span> 以傳輸認證檔案的路徑以及加密的PKCS12密碼適當設定檔案。 </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [包含個人化傳輸憑證和金鑰的PKCS12檔案] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個人化CA認證 </td> 
   <td>Individualization伺服器會使用Individualization CA憑證來簽署它發行的電腦憑證。 請務必設定 <span class="filepath"> AdobeInitial.properties</span> 與I15N CA認證檔案的路徑以及加密的PKCS12密碼適當地搭配檔案。 </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [包含個人化CA憑證和金鑰的PKCS12檔案] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [PKCS12檔案的加密密碼] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 個人化加密認證 </td> 
   <td> Individualization伺服器會使用「加密」認證來加密需要傳送至Individualization伺服器的機密檔案。 例如，此憑證支援授權移轉，也用於加密「個人化」伺服器的DRM私密金鑰。 </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 內容快取 </td> 
   <td>這些設定可控制個人化伺服器下載內容的來源位置，以及內容在磁碟上的快取位置。 「個人化」伺服器會在啟動時，依這些屬性指定的頻率/時間，檢查內容伺服器是否有新內容。 <p>對於On Premises Individualization Server，我們包含一組初始的內容快取資料。 請務必複製 <i>內容</i> 快取資料夾（而非快取資料夾本身）的設定檔 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> 位置。 </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [儲存本機內容的目錄（通常是tomcat/temp）] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [要連絡以取得ECI資訊的網頁伺服器(<i>此版本不支援</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [連線逾時，以秒為單位] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [輪詢伺服器的頻率，以天為單位（最少1天）] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [每日輪詢伺服器的時間，以分鐘為單位，從午夜開始] </li> 
    </ul> <p>請務必閱讀本節 <i>CRL和ECI檔案</i> 讓快取保持最新狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td> 個人化CA CRL </td> 
   <td> <p>此憑證撤銷清單(CRL)散發點包含在個人化伺服器所發行的每個電腦憑證中。 在授權伺服器上進行電腦憑證驗證期間，將會從憑證中列出的散發點下載CRL （或從快取中讀取，如果已下載），並檢查以確定憑證尚未被撤銷。 建議您先完成建立和部署個人化CA CRL的程式，然後再執行此伺服器組態變更。 進行任何組態變更後，重新啟動Individualization伺服器。 </p> <p>若要設定CRL發佈點的URL，您必須設定 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> 欄位。 </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL發佈點] </li> 
    </ul> <p>例如： </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>授權伺服器應該在處理授權請求後自動下載此CRL。 </p> <p importance="high">注意：此發佈點為 <i>非</i> 已由Primetime DRM檢查有效性。 您必須確認此URL有效。 除非授權伺服器出現驗證錯誤，否則不會顯示無效URL所產生的錯誤。 </p> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td>設定 <span class="filepath"> AdobeInitial.properties</span> 進行必要的記錄。 </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [將建立記錄檔的目錄] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [日誌中可能顯示的最低層級日誌訊息 <span class="codeph"> [偵錯 |資訊]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [記錄檔的前置詞。 日期/時間和「.log」副檔名將新增至檔案名稱] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [指定記錄滾動的頻率。] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [當記錄達到此大小時捲動記錄(當 <span class="codeph"> 滾動間隔</span> 或 <span class="codeph"> RollSize</span> 已到達（以先達到者為準）] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ]指定是否應產生個別檔案，其中包含Adobe用來產生個人化報表的資料。] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [報告記錄檔的前置詞。 日期/時間和 <span class="filepath"> .log</span> 副檔名將新增至檔案名稱。 l<span class="codeph"> og.Level</span> 屬性不適用於此記錄檔，但 <span class="codeph"> log.RollInterval</span> 和 <span class="codeph"> log.RollSize</span> 可以。] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 其他 </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [加密的Base64編碼金鑰，用於在將裝置資訊加入電腦權杖之前對其進行HMAC處理。 開發/測試/生產環境的索引鍵可能不同，但特定環境中的所有伺服器索引鍵都必須相同。] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Key Gen Server的位置（單一主機/連線埠，代表主要伺服器集區） ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [當佇列中剩餘這麼多金鑰時，從KGS擷取另一批金鑰] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [狀態頁面會偵測KGS以判斷它是否可以連線到伺服器。 如果未在指定的時間內收到回應，則會逾時。] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 金鑰產生伺服器 {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> 設定 </th> 
   <th class="entry"> 說明 </th> 
   <th class="entry"> 範例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 金鑰產生 </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [用來產生金鑰的系線數目（應該等於機器上可用的處理器數目）] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [每批次要產生的索引鍵數目] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [儲存關鍵批次檔案的目錄] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [要產生的關鍵批次檔案的最大數量] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 記錄 </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [將建立記錄檔的目錄] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [記錄檔的前置詞。 日期/時間和 <span class="filepath"> .log</span> 副檔名將新增至檔案名稱] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [可能出現在記錄中的記錄訊息的最低層級] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [指定記錄滾動的頻率。] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [當記錄達到此大小時捲動記錄(當 <span class="codeph"> 滾動間隔</span> 或 <span class="codeph"> RollSize</span> 已到達（以先達到者為準）] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
