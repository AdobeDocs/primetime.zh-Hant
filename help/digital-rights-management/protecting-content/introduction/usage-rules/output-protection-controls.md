---
title: 輸出保護控制
description: 輸出保護控制
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# 輸出保護控制{#output-protection-controls}

輸出保護控制參數控制輸出到外部渲染設備是否受到保護。 您可以單獨指定模擬和數字輸出的限制。

控制輸出至外部轉換裝置的限制。 外部設備定義為未嵌入電腦中的任何視頻或音頻設備。 在輸出保護控制方案中，整合顯示器（如筆記型電腦）不被視為外部顯示器。

Over the air(OTA) connection types are all block sleck default by listed but can be allow deferenced. 支援的OTA連接包括：Miracast、AirPlay、DLNA和WIDI。

**基於解析度的輸出保護：（可從5.3版升級。） **這可根據內容的垂直像素計數提供輸出保護，以根據垂直像素計數指定各種保護要求。

可使用下列選項／強制級別：

| 選項 | 在模擬設備中支援 | 數位裝置支援 |
|---|---|---|
| **必要** — 模擬複製保護(ACP)或複製生成管理系統——必須啟用模擬(CGMS-A)輸出保護，以便向外部設備播放內容。Primetime DRM客戶端必須使用ACP或CGMS-A啟用輸出保護。在同時支援這兩種裝置上，Primetime DRM 3.0用戶端會嘗試同時啟用兩者。 但是，只有一個必須啟用才能播放內容。 | 是 | 是 |
| **需要ACP** — 需要ACP輸出保護。CGMS-A不允許播放。Primetime DRM 2.0用戶端不支援此選項。 如果設定，Primetime DRM 2.0用戶端的運作方式就像已指定「無播放」選項。 | 是 | - |
| **使用(如果可用** )— 嘗試啟用ACP和CGMS-A輸出保護（如果可用），如果不可用則允許播放。Primetime DRM 3.0客戶端嘗試啟用ACP和CGMS-A（如果可能）。 Primetime DRM 2.0客戶端僅嘗試啟用ACP或CGMS-A。例如，Primetime DRM客戶端嘗試啟用ACP或CGMS-A。如果嘗試成功，則無法啟用其他選項。 如果嘗試失敗，則會再次嘗試啟用另一個選項。 即使兩次嘗試都失敗，內容仍會播放。 | 是 | 是 |
| **使用ACP(如果可用** )— 嘗試啟用ACP輸出保護（如果可用），但如果不可用則允許播放。CGMS-A上不提供保護。Primetime DRM 2.0用戶端不支援此選項。 如果設定，Primetime DRM 2.0用戶端就會像已指定「無保護」選項一樣運作。 | 是 | - |
| **如果有，請使用CGMS-A **— 嘗試啟用CGMS-A輸出保護（如果可用），但如果不可用則允許播放。 ACP上不提供保護。 Primetime DRM 2.0用戶端不支援此選項。 如果設定，Primetime DRM 2.0用戶端就會像已指定「無保護」選項一樣運作。 | 是 | - |
| **沒有保護** — 模擬和數字輸出不啟用輸出保護。 | 是 | 是 |
| **無播放** — 不允許對外部設備播放模擬和數字輸出。 | 是 | 是 |

>[!NOTE]
>
>雖然這些規則在所有平台上都一致地執行，但您只能在Windows平台上安全地開啟輸出保護。 在其他平台（例如Macintosh和Linux）上，協力廠商應用程式沒有支援的作業系統功能。

範例使用案例：某些內容可能會強制執行輸出保護控制，因此內容分配器可以設定保護級別。 如果指定「必要」，並嘗試在Macintosh上播放，則用戶端不會在外部裝置上播放內容。 內容可在內部顯示器上播放。

如果指定「必要」並嘗試在Linux上播放，則用戶端不會在任何裝置上播放內容，因為它無法區分內部和外部裝置。

如果您指定「Use if available」（使用可用時），則會在可能的情況下開啟輸出保護。 例如，在支援認證輸出保護通訊協定(COPP)的Windows系統上，內容會隨輸出保護傳遞至外部顯示器。 此範例有時稱為&#x200B;*`selectable output control`*。
