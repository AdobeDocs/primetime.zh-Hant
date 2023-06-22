---
title: 授權伺服器屬性檔案
description: 授權伺服器屬性檔案
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 授權伺服器屬性檔案{#license-server-properties-file}

授權伺服器會參照在中設定的屬性。 [!DNL flashaccess-refimpl.properties] 檔案。 您可以直接參照該檔案，以取得有關特定值的詳細資訊，以及每個屬性的使用資訊。 完整功能範例提供於 [!DNL resources] 參考實作目錄( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`)。

**認證**  — 屬性檔案包含Adobe發給您的認證位置的設定。 您可以在下列位置指定這些認證： [!DNL .pfx] 使用密碼的檔案，或為HSM中儲存的認證提供別名與密碼。 您至少需要設定與傳輸認證和授權伺服器認證相關的屬性。 指定認證檔案相對於您在中指定的目錄的位置 `config.resourcesDirectory` 屬性。

**Flash媒體Rights Management伺服器** - `flashaccess-refimpl.properties` 檔案也包含數個與封裝內容相關的屬性。 這些屬性僅用於Flash媒體Rights Management伺服器1.x中繼資料轉換。 修改此屬性檔案中的值後，要使變更生效，請重新啟動許可證伺服器。
