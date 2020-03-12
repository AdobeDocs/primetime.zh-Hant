---
seo-title: 防火牆規則
title: 防火牆規則
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 防火牆規則{#firewall-rules}

為確保對個人化伺服器的訪問安全，只需公開某些應用程式路徑。 個人化伺服器必須接受客戶端到以下路徑的請求：

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

服務路徑(如 [!DNL /flashaccess/admin/*] 狀態和管理頁)只能從防火牆內訪問。 不應從防火牆外部訪問密鑰生成伺服器的任何部分。
