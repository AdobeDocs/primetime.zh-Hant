---
title: 避免在/authenticate請求中使用'&'reg_code
description: 避免在/authenticate請求中使用'&'reg_code
exl-id: c0ecb6f9-2167-498c-8a2d-a692425b31c5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 避免在/authenticate請求中使用&#39;&amp;&#39;reg_code {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>



## 問題

IE 9瀏覽器將&#39;\®&#39;解譯為特殊命令，並將其轉換為®。 

## 說明

如果 `/authenticate` 請求的構成如下……

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...將由IE瀏覽器解譯，如下所示，並會以此格式傳送至Adobe：

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

請求者\_id將解譯為univision®\_code=EKAFMFI，因為沒有「&amp;」，而Adobe找不到 `regCode` 與權杖建立關聯的引數。  AuthN權杖有可能完全不會建立，在此情況下 `/checkauthn` 呼叫將找不到任何Token。



## 解決方案

下列其中一個選項應該可以解決此問題：

1. 避免使用 `&reg_code` 其他查詢字串引數之間的引數。  請改為將其移至請求URL中的第一個查詢字串引數，使請求URL如下所示：\
    

       &lt;fqdn>authenticate？reg_code =EKAFMFI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   如此一來， `&reg` 不會錯誤解譯引數。

1. 標準化 `&reg_code` 如使用 `&amp;reg_code`.

1. 如果AuthN權杖建立失敗，Adobe可能會引入新功能，將錯誤代碼傳回第2個畫面以回應驗證呼叫。
