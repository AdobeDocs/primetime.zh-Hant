---
title: 避免在/authenticate請求中使用'&'reg_code
description: 避免在/authenticate請求中使用'&'reg_code
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 避免在/authenticate請求中使用&#39;&amp;&#39;reg_code {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>



## 問題

IE 9瀏覽器將「\®」解釋為特殊命令，並將其轉換為®。 

## 說明

若 `/authenticate` 請求的組成如下……

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...IE瀏覽器會如下加以解譯，並以此格式傳送至Adobe:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

請求者\_id會解譯為univision®\_code=EKAFMFI，因為沒有「&amp;」，且Adobe找不到 `regCode` 參數來將代號與關聯。  AuthN代號完全有可能不會建立，在此情況下 `/checkauthn` 呼叫將無法找到任何Token。



## 解決方案

下列其中一個選項應可解決此問題：

1. 避免使用 `&reg_code` 其他查詢字串參數之間的參數。  請改為將其移至請求URL中的第一個查詢字串參數，使請求URL如下所示：\
    

       &lt;fqdn>authenticate?reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   這樣， `&reg` 參數將不會被正確解釋。

1. 標準化 `&reg_code` 使用 `&amp;reg_code`.

1. 如果AuthN權杖建立失敗，Adobe會導入新功能，以回應驗證呼叫將錯誤碼傳回第2畫面。

