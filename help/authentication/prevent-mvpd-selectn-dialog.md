---
title: 防止MVPD出現在「選擇」對話框中
description: 防止MVPD出現在「選擇」對話框中
exl-id: 20faf501-c006-45e2-a725-fb1273ecaffe
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 防止MVPD出現在「選擇」對話框中

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 問題 {#issue-prevent-mvpd-sel-dialog}

您需要防止(&quot;block-list&quot;)特定的MVPD出現在MVPD選擇器中。


## 解決方案 {#solution-prevent-mvpd-sel-dialog}

解決方案是在 `displayProviderDialog()` 。

例如，如果希望CableCompany_1和CableCompany_2不顯示在MVPD選擇器內，則應執行如下例所示的操作。

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->
