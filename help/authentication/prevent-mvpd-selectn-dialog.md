---
title: 防止MVPD出現在「選取」對話方塊中
description: 防止MVPD出現在「選取」對話方塊中
exl-id: 20faf501-c006-45e2-a725-fb1273ecaffe
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 防止MVPD出現在「選取」對話方塊中

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 問題 {#issue-prevent-mvpd-sel-dialog}

您需要防止(「block-list」)特定的MVPD出現在MVPD選擇器中。


## 解決方案 {#solution-prevent-mvpd-sel-dialog}

解決方案是在下列情況下執行區塊清單 `displayProviderDialog()` 稱為。

例如，如果您希望CableCompany_1和CableCompany_2不要顯示在MVPD選取器中，您可以執行類似以下範例中顯示的操作。

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
