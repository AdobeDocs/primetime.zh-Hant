---
title: 使用機器識別碼
description: 使用機器識別碼
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 使用機器識別碼{#use-machine-identifiers}

所有Adobe Primetime DRM請求（支援FMRMS相容性的請求除外）都包含已在個人化期間核發給使用者端之機器權杖的相關資訊。 電腦Token包含電腦ID，這是已在個人化期間指派的識別碼。 您可以使用此識別碼來計算使用者已要求授權或加入網域的電腦數量。

您可以使用識別碼，如下所示：

* 此 `getUniqueId()` 方法會傳回在個人化期間指派給裝置的字串。 您可以將字串儲存在資料庫中並按識別碼搜尋。 但是，如果使用者重新格式化硬碟並再次個人化，此識別碼會變更。 在相同電腦上的不同瀏覽器中，此識別碼在Adobe AIR和AdobeFlash Player之間也有不同的值。
* 如果您想要更準確地計算電腦，可以使用 `getBytes()` 以儲存整個識別碼。 若要判斷電腦之前是否曾出現過，請取得使用者名稱的所有識別碼，並呼叫 `matches()` 以檢查是否有任何相符專案。 因為 `matches()` 方法必須用來比較下列專案傳回的值： `MachineId.getBytes`，此選項只有在要比較的值數目較少時（例如，與特定使用者相關聯的電腦）才切實可行。

