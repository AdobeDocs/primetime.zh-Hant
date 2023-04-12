---
title: 防止MVPD出現在選取對話方塊中
description: 防止MVPD出現在選取對話方塊中
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 防止MVPD出現在選取對話方塊中

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 問題 {#issue-prevent-mvpd-sel-dialog}

您必須防止（「封鎖清單」）特定MVPD出現在MVPD選取器中。


## 解決方案 {#solution-prevent-mvpd-sel-dialog}

解決方案是在 `displayProviderDialog()` 的URL。

例如，如果希望CableCompany_1和CableCompany_2不顯示在MVPD選擇器內，您可以執行如下例所示的操作。

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