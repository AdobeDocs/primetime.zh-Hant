---
seo-title: 自訂驗證／權益概觀（選用）
title: 自訂驗證／權益概觀（選用）
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# 自訂驗證／權益概觀（選用）{#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM可設定為可觸及您自己的後端驗證／權益服務，以判斷：

* 此使用者是否可取得授權？
* 授權應包含哪些權利／限制？

Primetime Cloud DRM包含後端驗證／權益服務的參考實作。 為了進行演示，此伺服器正在對BEES請求發出「允許」響應。 請參閱[!DNL BEESServlet.java]以修改伺服器行為。

>[!NOTE]
>
>以前，這是個別產品，稱為&#x200B;*Back End Entitlement Server*(BEES)，因此在本檔案和來源檔案中都引用了BEES。

