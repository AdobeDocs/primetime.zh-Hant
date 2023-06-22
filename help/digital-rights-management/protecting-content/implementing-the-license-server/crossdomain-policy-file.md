---
title: 跨網域DRM原則檔
description: 跨網域DRM原則檔
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 跨網域DRM原則檔 {#crossdomain-drm-policy-file}

如果授權伺服器託管在與視訊播放SWF不同的網域上，則為跨網域DRM原則檔( [!DNL crossdomain.xml])才能讓SWF向授權伺服器要求授權。 跨網域DRM原則檔案以XML檔案表示，可讓伺服器指出其資料和檔案可用於SWF從其他網域提供的檔案。 從授權伺服器的跨網域DRM原則檔中指定的網域提供的任何SWF檔，都允許從該授權伺服器存取資料或資產。

Adobe建議開發人員在部署跨網域原則檔案時，僅允許受信任的網域存取授權伺服器，並限制對Web伺服器上授權子目錄的存取，以遵循最佳實務。

如需有關跨領域DRM原則檔案的詳細資訊，請參閱下列位置：

* 網站控制（DRM原則檔）
* 跨網域DRM原則檔案規格： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

