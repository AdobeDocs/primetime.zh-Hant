---
title: 封鎖DRM使用者端清單，限制其存取受保護的內容
description: 封鎖DRM使用者端清單，限制其存取受保護的內容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 封鎖DRM使用者端清單，限制其存取受保護的內容 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

此封鎖清單指定無法存取受保護內容的Primetime DRM使用者端。 您會依使用者端版本和平台封鎖清單使用者端。

使用案例範例：在安全性違反的情況下，可將較新版本的Primetime DRM使用者端指定為授權取得和內容播放所需的最低版本。 許可證伺服器會先檢查發出許可證請求的Primetime DRM使用者端是否符合版本需求，然後再發行許可證。 Primetime DRM使用者端也會在播放內容之前檢查授權中的版本。 如果網域可能會將授權轉移到另一台電腦，則需要此使用者端檢查。

Primetime DRM使用者端版本可由下表中指定的屬性來識別：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 環境 | `“PC”, “PortingKit”` | 完全相符 | 識別使用者端是否正在桌上型電腦或任何其他裝置上執行。 |
| 作業系統 | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | 完全相符 | Platform |
| 架構 | `“32”, “64”` | 完全相符 | 32位元或64位元 |
| 熒幕型別 | `“PC”, “Mobile”, “TV”` | 完全相符 | |
| 執行階段版本 | 有效的版本號碼。 例如， `“2.0.0”, "3.0", "4.0", "11.0"`等 | 如果使用者端版本小於或等於指定的版本，則為相符。 | 版本編號是以數字和句點(「。」)的組合來指定 任何長度。 |
| Primetime DRM程式庫版本 | 有效的版本號碼。 例如， `“2.0.0”`. | 如果使用者端版本小於或等於指定的版本，則為相符。 | 版本編號是以數字和句點(「。」)的組合來指定 任何長度。 |
| OEM廠商 | OEM廠商字串；此字串可位於發行給將Primetime DRM移植到裝置的客戶的Runtime憑證中。 | 完全相符 | 使用移植套件之裝置的OEM廠商識別字串。 |
| 模型 | 可在發行給將Primetime DRM移植到裝置的客戶的執行階段憑證中找到的模型字串。 例如， `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | 完全相符 | 使用移植套件的裝置的裝置型號識別字串。 |

>[!NOTE]
>
>在區塊清單中指定專案時，您可以為上一個表格中提及的一或多個屬性設定值。 任何未指定的屬性都會視為萬用字元。 如果Primetime DRM使用者端符合封鎖清單專案中指定的所有值，則該使用者端可能無法存取受保護的內容。
