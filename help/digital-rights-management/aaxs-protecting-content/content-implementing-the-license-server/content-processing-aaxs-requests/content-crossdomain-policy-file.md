---
seo-title: 跨域策略檔案
title: 跨域策略檔案
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 跨域策略檔案{#crossdomain-policy-file}

如果授權伺服器是裝載在視訊播放SWF以外的網域上，則必須有跨網域原則檔案(crossdomain.xml)才能讓SWF向授權伺服器要求授權。 跨網域原則檔案是XML檔案，可讓伺服器指出其資料和檔案可供其他網域提供的SWF檔案使用。 任何從授權伺服器的跨網域原則檔案中指定的網域提供的SWF檔案，都可從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，只要允許受信任網域存取授權伺服器，並限制對Web伺服器上授權子目錄的存取，就應遵循最佳實務。

如需跨網域原則檔案的詳細資訊，請參閱下列位置：

* 網站控制項（原則檔案）
* 跨域策略檔案規範：[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

