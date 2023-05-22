---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 55b18fee-b7d8-4a5a-91a7-a08cd23e7866
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

使用介質打包器之前，請確保滿足「要求」中列出的要求，並且配置檔案包含所需資訊(請參閱 *使用Adobe訪問參考實現*。

介質打包器位於 [!DNL \Reference Implementation\Command Line tools] 的下界。 要加密單個檔案，請使用以下語法：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` 是要加密的檔案。
* `dest` 指定加密內容的寫入位置。 如果指定了目錄，則加密檔案將使用與源檔案相同的檔案名保存到此資料夾中，但該目錄不能是包含源檔案的目錄。

要使用相同的密鑰加密多個檔案（用於多比特率支援），請使用以下語法：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` 是一系列以空格分隔的源條目，代表要加密的檔案。
* `dest-directory` 指定加密內容的寫入位置。 加密的檔案將使用與源檔案相同的檔案名保存到此資料夾中，但目錄不得是包含源檔案的目錄。

要查看有關加密檔案的資訊，請使用以下語法：

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` 是加密檔案。

要查看有關元資料檔案的資訊，請使用以下語法：

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM元資料的檔案。

>[!NOTE]
>
>在打包期間，預設情況下，介質打包器將不再生成.header檔案。 要生成此檔案，請使用 `-h` 選項。

下表包含上述語法中所示的命令行選項的說明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行選項 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置檔案的位置。 如果未使用此選項，介質打包器將查找 <span class="filepath"> flashaccessols.properties </span> 的子菜單。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> 加密檔案 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關已打包的檔案的資訊。 源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 元資料 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">顯示有關現有元資料的資訊。 源檔案和目標檔案不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與 <span class="codeph"> -d </span> 從打包的檔案中提取策略。 將使用檔案名和策略標識符在加密檔案的同一目錄中建立檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">與 <span class="codeph"> -d </span> 從封裝檔案中提取DRM頭。 使用檔案名和副檔名在與加密檔案相同的目錄中建立檔案 <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> 內容ID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此內容的唯一標識符。 如果未指定標識符，則將使用目標檔案名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 鍵 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到內容元資料的自定義鍵/值。 多重 <span class="codeph"> -k </span> 可以指定選項。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">將此選項與 <span class="codeph"> -d </span> 從打包的檔案中提取元資料。 將使用檔案名和副檔名在與加密檔案相同的目錄中建立檔案 <span class="codeph"> .元資料 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要詢問是否應覆蓋目標檔案。 如果目標檔案已存在，並且 <span class="codeph"> -o </span> 未設定，將返回錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目標檔案已存在，則覆蓋該檔案而不出現提示。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 檔案名[域 — 傳輸 — 證書] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含策略的檔案的名稱。 如果策略要求向使用與屬性檔案中指定的傳輸證書不同的傳輸證書的伺服器註冊域，則還需要提供域傳輸證書。 </p> <p class="- topic/p ">多重 <span class="codeph"> -p </span> 可以指定選項，預設情況下，客戶端將使用第一個選項。 命令行上指定的值優先於配置檔案中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>
