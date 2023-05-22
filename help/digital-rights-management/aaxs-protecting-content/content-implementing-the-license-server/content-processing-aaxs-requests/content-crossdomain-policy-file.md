---
title: 跨域策略檔案
description: 跨域策略檔案
copied-description: true
exl-id: dbe16692-cdf7-4a91-9303-8afc2d487112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 跨域策略檔案 {#crossdomain-policy-file}

如果許可證伺服器托管在與視頻播放SWF不同的域上，則需要跨域策略檔案(crossdomain.xml)以允許SWF從許可證伺服器請求許可證。 跨域策略檔案是XML檔案，它為伺服器提供了一種方法，以指示其資料和文檔可用於SWF從其他域提供的檔案。 允許從許可證伺服器的跨域策略檔案中指定的域提供的任何SWF檔案從該許可證伺服器訪問資料或資產。

Adobe建議開發人員在部署跨域策略檔案時遵循最佳做法，方法是僅允許受信任的域訪問許可證伺服器並限制對Web伺服器上許可證子目錄的訪問。

有關跨域策略檔案的詳細資訊，請參閱以下位置：

* 網站控制項（策略檔案）
* 跨域策略檔案規範： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
