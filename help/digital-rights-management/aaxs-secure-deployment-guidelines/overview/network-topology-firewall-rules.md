---
seo-title: 防火牆規則
title: 防火牆規則
uuid: a5667030-c4d0-42e3-b56e-20a12c903954
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 防火牆規則 {#firewall-rules}

## 傳入的URL {#section-F111526A9DB844CBBF21A3CAE5F50880}

配置外部防火牆，使其僅公開您要提供給最終用戶的應用程式功能的URL。 僅允許外部用戶通過外部防火牆訪問下表所列的URL:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-bqs-whz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">根URL </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">目的 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/getServerVersion/v3</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於確定伺服器版本的URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-xr4-hdn-44"> 
     <li id="li-05925A4DE4114F7786FF93A66AB8A117"><span class="filepath"> /flashaccess/authn/v1/*</span> </li> 
     <li id="li-E76E9BA0160F4E7F9EBB64428C2D9F31"><span class="filepath"> /flashaccess/authn/v3/*</span> </li> 
     <li id="li-ED3C15EB4D194FFE99954BDB7D5C1E41"><span class="filepath"> /flashaccess/authn/v4/*</span> </li> 
     <li id="li-4DD6CBBE939F4E6EABA474E3DCCBD893"><span class="filepath"> /flashaccess/authn/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用者驗證的URL。 只有當您使用Adobe Access Client API執行使用者驗證時，才能存取此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-yxs-rdn-44"> 
     <li id="li-49B9987ED6E14FADA66727448F923F84"><span class="filepath"> /flashaccess/license/v1/*</span> </li> 
     <li id="li-BF4A415E573C4C728E24D548F53D923C"><span class="filepath"> /flashaccess/license/v3/*</span> </li> 
     <li id="li-E6C551DDA030429B9D0073D2685B778A"><span class="filepath"> /flashaccess/license/v4/*</span> </li> 
     <li id="li-57811F4CD7304DBDAFADD65244AED0D9"><span class="filepath"> /flashaccess/license/v5/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">向使用者發行授權的URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-ibl-5dn-44"> 
     <li id="li-189BE370CD5044F988A42335C3BFE420"><span class="filepath"> /flashaccess/sync/v3</span> </li> 
     <li id="li-B333B85FFE8A46DD884595B0A620B4EE"><span class="filepath"> /flashaccess/sync/v4</span> </li> 
     <li id="li-E4771D3C5AA5454CA1EDCFAA3E027CC1"><span class="filepath"> /flashaccess/sync/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">同步請求的URL。 只有當您在授權中指定同步需求時，才能存取此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-plq-ydn-44"> 
     <li id="li-81C96F93BA904C8C95B907F1A77E6494"><span class="filepath"> /flashaccess/domain/v3</span> </li> 
     <li id="li-40F0952F09674CA3B9AAFB5A62F9D02E"><span class="filepath"> /flashaccess/domain/v4</span> </li> 
     <li id="li-3ADE44B959B548F8A31A6FF08537AF46"><span class="filepath"> /flashaccess/domain/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">網域註冊的URL。 只有在您實作網域支援時，才能存取此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul-btm-c2n-44"> 
     <li id="li-3535EDF7C644406FAC471D4234C4AF98"><span class="filepath"> /flashaccess/dereg/v3</span> </li> 
     <li id="li-AB33657BC7E140E695767710DF7AEC72"><span class="filepath"> /flashaccess/dereg/v4</span> </li> 
     <li id="li-D15B32BCD4674269A3A2644DD5204707"><span class="filepath"> /flashaccess/dereg/v5</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">取消註冊網域的URL。 只有在您實作網域支援時，才能存取此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/headerconversion/v1/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用戶端用來將FMRMS 1.x DRM中繼資料轉換為Adobe Access DRM中繼資料的URL。 </p> <p class="- topic/p ">注意：此 <i class="+ topic/ph hi-d/i ">URL必須使用SSL(HTTPS)</i>。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /edcws/services/urn:EDCLicenseService/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">LiveCycle Rights Management ES web service URL。 如果內容是使用舊版FMRMS發佈，此URL可讓舊版用戶端連線至伺服器，並提示您升級至Adobe Access。 </p> <p class="- topic/p ">注意：此 <i class="+ topic/ph hi-d/i ">URL必須使用SSL(HTTPS)</i>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/lreturn/v5</span> </td> 
   <td colname="2" class="- topic/entry "> <p>傳回授權的URL。 只有在您實作授權退貨支援時，才能存取URL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>內部防火牆只能允許透過反向代理與Adobe Access授權伺服器進行連線，且只能與上述URL連線。 為改善可擴充性，反向proxy和Adobe Access之間的連線將會透過HTTP進行。

## 傳出URL {#section-FFF9F7BB353149F4A27F8788E9934A48}

授權伺服器需要透過防火牆存取，才能從Adobe下載下列CRL:

* <span></span>https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl
* <span></span>https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl
* <span></span>https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl
* <span></span>https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl