---
title: 在「選擇」對話框中允許MVPD
description: 在「選擇」對話框中允許MVPD
exl-id: 2c0e0f06-ddc6-4bea-90dc-d7ef8e78d27e
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 在「選擇」對話框中允許MVPD {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 問題 {#issue}

程式設計師可能希望在向最終用戶公開之前test或檢查新MVPD整合的用戶體驗。

## 解決方案 {#solution}

在 `displayProviderDialog()` 回調，Adobe Primetime驗證將返回與所選程式設計師（請求者ID）整合的所有MVPD。 但程式設計師可以對MVPD的返回陣列應用篩選器，並只顯示兩個清單中的篩選器。

## 示例 {#example}

此示例演示如何在MVPD選擇器對話框內僅顯示CableCompany_1和CableCompany_2，以及不顯示CableCompany_NewIntegration。

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}
```

<!--
**Related Information**
* [Prevent MVPDs from appearing in the Selection Dialog](/help/authentication/prevent-mvpd-selectn-dialog.md)
* **Code Samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->
