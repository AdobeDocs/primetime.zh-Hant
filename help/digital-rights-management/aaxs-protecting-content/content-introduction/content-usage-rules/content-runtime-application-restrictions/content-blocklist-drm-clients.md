---
seo-title: DRM客戶端阻止訪問受保護內容的塊清單
title: DRM客戶端阻止訪問受保護內容的塊清單
uuid: c05aa6f8-32d9-42aa-a9c5-0d0629d49778
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# DRM客戶端阻止訪問受保護內容的塊清單 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Access DRM模組版本限制存取受保護的內容。**

指定無法訪問內容的DRM客戶端。 由DRM客戶端版本和平台指定。

範例使用案例： 在發生安全違約時，可以指定較新版本的DRM客戶端作為獲取許可證和內容回放所需的最低版本。 授權伺服器會在核發授權之前，先檢查發出授權要求的DRM用戶端是否符合版本要求。 DRM客戶端在播放內容之前還檢查許可證中的DRM版本。 如果網域可將授權傳輸至另一部電腦，則需要進行此用戶端檢查。

DRM客戶端版本可由下表中指定的屬性標識：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 環境 | &quot;PC&quot;、&quot;PortingKit&quot; | 完全符合 | 識別客戶端是在案頭上還是任何其他設備上運行。 |
| 作業系統 | 「Win」、「Mac」、「Linux」、「Android」、「iOS」、「ChromeOS」 | 完全符合 | 平台 |
| 建築 | “32”, “64” | 完全符合 | 32位元或64位元 |
| 螢幕類型 | 「PC」、「行動」、「TV」 | 完全符合 |  |
| 執行時期版本 | 有效的版本號碼。 例如，「2.0.0」、「3.0」、「4.0」、「11.0」等。 | 如果用戶端版本小於或等於指定版本，則相符項目。 | 版本編號指定為數字和句號(&quot;。&quot;)的組合 任何長度。 |
| DRM庫版本 | 有效的版本號碼。 例如，&quot;2.0.0&quot;。 | 如果用戶端版本小於或等於指定版本，則相符項目。 | 版本編號指定為數字和句號(&quot;。&quot;)的組合 任何長度。 |
| OEM廠商 | OEM供應商字串 | 完全符合 | 使用移植套件之裝置的OEM廠商識別字串。 |
| 模型 | 模型字串。 例如，「iOS_Mobile」、「Android_Mobile」、「Chrome」、「ChromeOS_ARM」、「WindowsOnARM」、「AVE」 | 完全符合 | 使用移植套件之裝置的裝置型號識別字串。 |

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>在塊清單中指定條目時，可以為上表中提及的一個或多個屬性設定值。 未指定的任何屬性都視為萬用字元。 如果DRM客戶機與塊清單條目中指定的所有值匹配，則該客戶機不能訪問受保護的內容。

