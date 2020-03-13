---
seo-title: 配置檔案屬性
title: 配置檔案屬性
uuid: f0d36240-e5fa-4bf9-9a82-7e963d03cdd0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置檔案屬性 {#configuration-file-properties}

在執行Media Packager之前，請指定Media Packager屬性的值。 配置檔案指定以下屬性。 對於包含* n*的屬性名稱， *n* 表示從1開始的整數，並且會為屬性的每個實例增加。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">屬性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> 指出是否加密視訊內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密音頻。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">指出是否加密FLV中的指令碼資料。 <i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> 指令碼資料標籤不會加密，即使啟用此選項亦然。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示視頻加密級別。 高值用於加密所有視頻內容，而中值和低值用於加密包含H.264內容的F4V檔案的視頻內容部分。 </p> <p class="- topic/p ">值=高 <span class="codeph"> |中級|低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，則不會加密檔案開頭處指定的內容秒數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.ansymmet.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於加密密鑰的許可證伺服器證書檔案。 encrypt.keys. <span class="codeph"> ansymetric.certfile</span> 屬性指定僅包含證書的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性會重複用來建立要套用至內容的原則清單。 <span class="codeph"> n</span> 是值為1或更大的整數。 根據預設，用戶端會使用第一個例項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器的傳輸證書。 此屬性指定僅包 <span class="filepath"> 含證書的。cer</span> 檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含用於簽署內容的封裝憑證的PKCS12檔案。 encrypt. <span class="codeph"> sign.certfile</span> 應該引用包含證書和私鑰 <span class="filepath"> 的。pfx</span> 檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於保護由 <span class="codeph"> encrypt.sign.certfile指定檔案的口令</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為要封裝的內容發行授權所需的最低伺服器版本。 指定x(Adobe Access x.0)，其中x =主要版本號碼。 Adobe Access 3.0之前的伺服器不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果策略 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 需要向使用不同於 <span class="+ topic/ph pr-d/codeph codeph"></span>encrypt.license.servercert中指定的傳輸證書的伺服器註冊域，則需要提供域傳輸證書。 </p> <p class="- topic/p ">此屬性指定僅包含證書的檔案（PEM或DER格式是可接受的）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定授權金鑰。 如果未指定密鑰，則會隨機生成密鑰。 當未啟用密鑰旋轉時，此為用於加密內容的密鑰。 </p> <p class="- topic/p ">啟用密鑰旋轉時，此密鑰用於保護旋轉密鑰。 索引鍵長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用密鑰旋轉。 如果設定為false（預設值），則禁用密鑰旋轉，並且主CEK將用於加密內容中的所有樣本。 </p> <p class="- topic/p ">如果設為true，則會啟用金鑰旋轉，並使用不同的金鑰來加密內容的部分。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">啟用密鑰旋轉時用來加密內容的旋轉密鑰序列。 如果未指定任何金鑰，則會隨機產生金鑰。 密鑰長度必須為16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空格是可選的。 <i class="+ topic/ph hi-d/i ">n必</i> 須單調增加，從1開始。 指定多個鍵時，按指示順序循環使用鍵。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用旋轉密鑰加密內容樣本的間隔（以秒為單位）。 </p> <p class="- topic/p ">在內容中的這段時間經過加密後，將會使用下一個旋轉金鑰。 如果啟用密鑰輪替且未指定間隔，則每15分鐘輪替一次密鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果為true，則沒有可從中取得授權的授權伺服器。 授權必須內嵌或取得帶外授權。 如果未指定，則預設為false。 僅支援Adobe Access Professional。 </p> </td> 
  </tr> 
 </tbody> 
</table>

