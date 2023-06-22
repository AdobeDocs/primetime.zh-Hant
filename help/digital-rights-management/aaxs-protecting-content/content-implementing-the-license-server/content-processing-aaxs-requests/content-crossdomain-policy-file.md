---
title: 跨網域原則檔案
description: 跨網域原則檔案
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 跨網域原則檔案 {#crossdomain-policy-file}

如果授權伺服器託管在與視訊播放SWF不同的網域上，則需要跨網域原則檔案(crossdomain.xml)，以允許SWF從授權伺服器請求授權。 跨網域原則檔案是一種XML檔案，為伺服器提供一種方法，來指示其資料和檔案可用於SWF從其他網域提供的檔案。 從授權伺服器的跨網域原則檔中指定的網域提供的任何SWF檔，都可以從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，僅允許受信任的網域存取授權伺服器，並限制對Web伺服器上授權子目錄的存取，以遵循最佳實務。

如需跨網域原則檔案的詳細資訊，請參閱下列位置：

* 網站控制項（原則檔）
* 跨網域原則檔案規格： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
