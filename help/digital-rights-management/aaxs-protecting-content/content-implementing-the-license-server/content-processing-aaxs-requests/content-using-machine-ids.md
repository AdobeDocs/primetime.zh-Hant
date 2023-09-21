---
title: 使用電腦識別碼
description: 使用電腦識別碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 使用電腦識別碼{#using-machine-identifiers}

所有Adobe存取要求（支援FMRMS相容性的要求除外）都包含在個人化期間核發給使用者端之電腦權杖的相關資訊。 電腦Token包含電腦ID，這是個人化期間指派的識別碼。 使用此識別碼可計算使用者要求授權或加入網域的電腦數量。

識別碼的使用方式有兩種。 此 `getUniqueId()` 方法會傳回在個人化期間指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼搜尋。 但是，如果使用者重新格式化硬碟並再次個人化，此識別碼將會變更。 此識別碼在相同電腦上不同瀏覽器中的Adobe® AIR®與Adobe® Flash®播放器之間也具有不同的值。

若要更準確地計算電腦，您可以使用 `getBytes()` 以儲存整個識別碼。 若要判斷電腦之前是否曾出現過，請取得使用者名稱的所有識別碼，並呼叫 `matches()` 以檢查是否有任何相符專案。 因為 `matches()` 方法必須用來比較下列專案傳回的值： `MachineId.getBytes`，此選項只有在要比較的值數目較少時（例如，與特定使用者相關聯的電腦）才切實可行。
