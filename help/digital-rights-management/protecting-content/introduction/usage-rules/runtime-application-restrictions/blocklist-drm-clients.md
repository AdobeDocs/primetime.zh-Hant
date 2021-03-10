---
title: DRM客戶端阻止訪問受保護內容的塊清單
description: DRM客戶端阻止訪問受保護內容的塊清單
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# DRM客戶端的塊清單，限制訪問受保護的內容{#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

此區塊清單會指定無法存取受保護內容的Primetime DRM用戶端。 您可以按客戶端版本和平台阻止清單客戶端。

範例使用案例：在發生安全性違約時，Primetime DRM用戶端的較新版本可指定為取得授權和內容播放所需的最低版本。 授權伺服器會在核發授權之前，先檢查發出授權要求的Primetime DRM用戶端是否符合版本需求。 Primetime DRM用戶端也會在播放內容之前先檢查授權中的版本。 如果網域可將授權傳輸至另一部電腦，則需要進行此用戶端檢查。

Primetime DRM客戶端版本可由下表中指定的屬性標識：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 環境 | `“PC”, “PortingKit”` | 完全符合 | 識別客戶端是在案頭上還是任何其他設備上運行。 |
| 作業系統 | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | 完全符合 | 平台 |
| 建築 | `“32”, “64”` | 完全符合 | 32位元或64位元 |
| 螢幕類型 | `“PC”, “Mobile”, “TV”` | 完全符合 |  |
| 執行時期版本 | 有效的版本號碼。 例如，`“2.0.0”, "3.0", "4.0", "11.0"`等。 | 如果用戶端版本小於或等於指定版本，則相符項目。 | 版本編號指定為數字和句點(&quot;。&quot;)的組合 任何長度。 |
| Primetime DRM庫版本 | 有效的版本號碼。 例如，`“2.0.0”`。 | 如果用戶端版本小於或等於指定版本，則相符項目。 | 版本編號指定為數字和句點(&quot;。&quot;)的組合 任何長度。 |
| OEM廠商 | OEM廠商字串，可位於發佈給將Primetime DRM發佈至裝置之客戶的執行時期憑證中。 | 完全符合 | 使用移植套件之裝置的OEM廠商識別字串。 |
| 模型 | 可在發佈給將Primetime DRM發佈至裝置之客戶的「執行階段憑證」中找到的模型字串。 例如， `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | 完全符合 | 使用移植套件之裝置的裝置型號識別字串。 |

>[!NOTE]
>
>在塊清單中指定條目時，可以為上表中提及的一個或多個屬性設定值。 未指定的任何屬性都視為萬用字元。 如果Primetime DRM客戶端與塊清單條目中指定的所有值匹配，則該客戶端可能無法訪問受保護的內容。

