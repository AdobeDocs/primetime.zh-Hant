---
title: 封鎖無法存取受保護內容的DRM使用者端清單
description: 封鎖無法存取受保護內容的DRM使用者端清單
copied-description: true
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 封鎖無法存取受保護內容的DRM使用者端清單 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe存取DRM模組版本限制存取受保護的內容。**

指定無法存取內容的DRM使用者端。 由DRM使用者端版本和平台指定。

使用案例範例：在安全性違反的情況下，可將較新版本的DRM使用者端指定為授權取得和內容播放所需的最低版本。 許可證伺服器會先檢查發出許可證請求的DRM使用者端是否符合版本要求，然後再發出許可證。 在播放內容之前，DRM使用者端也會檢查許可證中的DRM版本。 如果網域中的授權可能傳輸到其他電腦，則需要此使用者端檢查。

DRM使用者端版本可由下表中指定的屬性來識別：

| **屬性** | **支援的值** | **符合條件** | **說明** |
|---|---|---|---|
| 環境 | &quot;PC&quot;、&quot;PortingKit&quot; | 完全相符 | 識別使用者端是否正在桌上型電腦或任何其他裝置上執行。 |
| 作業系統 | &quot;Win&quot;、&quot;Mac&quot;、&quot;Linux&quot;、&quot;Android&quot;、&quot;iOS&quot;、&quot;ChromeOS&quot; | 完全相符 | Platform |
| 架構 | “32”, “64” | 完全相符 | 32位元或64位元 |
| 熒幕型別 | &quot;PC&quot;、&quot;Mobile&quot;、&quot;TV&quot; | 完全相符 |  |
| 執行階段版本 | 有效的版本號碼。 例如，「2.0.0」、「3.0」、「4.0」、「11.0」等。 | 如果使用者端版本小於或等於指定的版本，則相符。 | 版本編號是以數字和句點(「。」)的組合來指定 任何長度。 |
| DRM程式庫版本 | 有效的版本號碼。 例如，「2.0.0」。 | 如果使用者端版本小於或等於指定的版本，則相符。 | 版本編號是以數字和句點(「。」)的組合來指定 任何長度。 |
| OEM廠商 | OEM廠商字串 | 完全相符 | 使用移植套件之裝置的OEM廠商識別字串。 |
| 模型 | 模型字串。 例如，「iOS_Mobile」、「Android_Mobile」、「Chrome」、「ChromeOS_ARM」、「WindowsOnARM」、「AVE」 | 完全相符 | 使用移植套件的裝置的裝置型號識別字串。 |

>[!NOTE]
>
>在區塊清單中指定專案時，可設定上一個表格中所提及之一或多個屬性的值。 任何未指定的屬性都會視為萬用字元。 如果DRM使用者端符合封鎖清單專案中指定的所有值，則該使用者端可能無法存取受保護的內容。
