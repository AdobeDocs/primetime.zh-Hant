---
title: 跨域DRM策略檔案
description: 跨域DRM策略檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 跨域DRM策略檔案{#crossdomain-drm-policy-file}

如果授權伺服器是裝載在視訊播放SWF以外的網域上，則需要跨網域DRM原則檔案([!DNL crossdomain.xml])，才能讓SWF向授權伺服器要求授權。 跨網域DRM原則檔案由XML檔案表示，讓伺服器指出其資料和檔案可供其他網域提供的SWF檔案使用。 任何從授權伺服器的跨網域DRM原則檔案中指定之網域提供的SWF檔案，都可從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，只要允許受信任網域存取授權伺服器，並限制存取Web伺服器上的授權子目錄，就應遵循最佳實務。

如需跨網域DRM原則檔案的詳細資訊，請參閱下列位置：

* 網站控制項（DRM原則檔案）
* 跨域DRM策略檔案規範：[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

