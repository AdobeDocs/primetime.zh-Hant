---
title: 在「選擇」對話框中允許MVPD
description: 在「選擇」對話框中允許MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# 在「選擇」對話框中允許MVPD {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 問題 {#issue}

程式設計師可能想要在向最終用戶公開之前測試或檢查新MVPD整合的用戶體驗。

## 解決方案 {#solution}

在 `displayProviderDialog()` callback,Adobe Primetime驗證會傳回與所選程式設計人員（請求者ID）整合的所有MVPD。 但是程式設計師可以對返回的MVPD陣列應用一個過濾器，並只顯示這兩個清單中的那些。

## 範例 {#example}

本示例演示如何在MVPD選擇器對話框中僅顯示CableCompany_1和CableCompany_2，以及不顯示CableCompany_NewIntegration。

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