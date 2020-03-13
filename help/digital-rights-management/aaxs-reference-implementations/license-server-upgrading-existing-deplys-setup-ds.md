---
seo-title: 設定域伺服器
title: 設定域伺服器
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 設定域伺服器 {#set-up-a-domain-server}

要在現有許可證伺服器安裝上配置域伺服器，請執行以下任務：

1. 在下面 [!DNL flashaccess-refimpl.properties] 開啟檔案 [!DNL tomcat/lib]。

1. 在選項 `Domain CA certificate` 下，填寫域CA證書詳細資訊。 此憑證將用於接受網域Token。
1. 在選項 `Domain CA credential` 下，填入詳細 `Domain CA credential certificate (PFX)` 資訊。 此憑證將用於簽署網域憑證和Token。

1. 指定值 `DomainServerlURL`。 如果此值為NULL，則域驗證可能成功。 但是，在加入網域時，會發生連接網域錯誤。

