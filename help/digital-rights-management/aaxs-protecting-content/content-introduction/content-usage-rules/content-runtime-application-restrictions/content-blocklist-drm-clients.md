---
title: 阻止限制訪問受保護內容的DRM客戶端清單
description: 阻止限制訪問受保護內容的DRM客戶端清單
copied-description: true
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 阻止限制訪問受保護內容的DRM客戶端清單 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe訪問限制訪問受保護內容的DRM模組版本。**

指定無法訪問內容的DRM客戶端。 由DRM客戶端版本和平台指定。

示例用例：在發生安全違規時，可以將DRM客戶端的較新版本指定為許可證獲取和內容回放所需的最低版本。 許可伺服器在發出許可之前檢查發出許可請求的DRM客戶端是否滿足版本要求。 DRM客戶端還在播放內容之前檢查許可證中的DRM版本。 在許可證可以轉移到其他電腦的域中，需要進行此客戶端檢查。

DRM客戶端版本可由下表中指定的屬性標識：

| **屬性** | **支援的值** | **匹配條件** | **說明** |
|---|---|---|---|
| 環境 | &quot;PC&quot;、&quot;PortingKit&quot; | 完全匹配 | 標識客戶端是否在案頭或任何其他設備上運行。 |
| 作業系統 | &quot;Win&quot;、&quot;Mac&quot;、&quot;Linux&quot;、&quot;Android&quot;、&quot;iOS&quot;、&quot;ChromeOS&quot; | 完全匹配 | 平台 |
| 建築 | “32”, “64” | 完全匹配 | 32位或64位 |
| 螢幕類型 | &quot;PC&quot;、&quot;移動&quot;、&quot;電視&quot; | 完全匹配 |  |
| 運行時版本 | 有效的版本號。 例如，&quot;2.0.0&quot;、&quot;3.0&quot;、&quot;4.0&quot;、&quot;11.0&quot;等。 | 如果客戶端版本小於或等於指定版本，則匹配。 | 版本號被指定為數字和期間(&quot;。&quot;)的組合 任何長度。 |
| DRM庫版本 | 有效的版本號。 例如，&quot;2.0.0&quot;。 | 如果客戶端版本小於或等於指定版本，則匹配。 | 版本號被指定為數字和期間(&quot;。&quot;)的組合 任何長度。 |
| OEM供應商 | OEM供應商字串 | 完全匹配 | 使用移植套件的設備的OEM供應商標識字串。 |
| 模型 | 模型字串。 例如，&quot;iOS移動&quot;、&quot;Android移動&quot;、&quot;Chrome&quot;、&quot;ChromeOS_ARM&quot;、&quot;WindowsOnARM&quot;、&quot;AVE&quot; | 完全匹配 | 使用移植套件的設備的設備型號標識字串。 |

>[!NOTE]
>
>當在塊清單中指定條目時，可以為上表中提到的一個或多個屬性設定值。 未指定的任何屬性都被視為通配符。 如果DRM客戶端與塊清單條目中指定的所有值匹配，則受保護的內容可能不被該客戶端訪問。
