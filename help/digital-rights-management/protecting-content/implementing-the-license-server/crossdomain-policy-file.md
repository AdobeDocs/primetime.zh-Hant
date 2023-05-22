---
title: 跨域DRM策略檔案
description: 跨域DRM策略檔案
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# 跨域DRM策略檔案 {#crossdomain-drm-policy-file}

如果許可證伺服器托管在與視頻播放SWF不同的域上，則跨域DRM策略檔案( [!DNL crossdomain.xml])，以啟用SWF從許可證伺服器請求許可證。 跨域DRM策略檔案由XML檔案表示，該XML檔案使伺服器能夠指示其資料和文檔可用於SWF從其他域服務的檔案。 允許從許可證伺服器的跨域DRM策略檔案中指定的域提供的任何SWF檔案從該許可證伺服器訪問資料或資產。

Adobe建議開發人員在部署跨域策略檔案時遵循最佳做法，方法是僅允許受信任的域訪問許可證伺服器並限制對Web伺服器上許可證子目錄的訪問。

有關跨域DRM策略檔案的詳細資訊，請參閱以下位置：

* 網站控制項（DRM策略檔案）
* 跨域DRM策略檔案規範： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

