---
title: 設定並執行命令列工具
description: 設定並執行命令列工具
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 設定並執行命令列工具 {#configure-and-run-the-command-line-tools}

命令列工具具有關聯的屬性，您必須針對這些屬性設定值 [!DNL flashaccesstools.properties] *早於* 您可以執行工具。 有些命令列工具也可讓您從命令列指定屬性值。 您從命令列指定的值優先於您從提供的值 [!DNL flashaccesstools.properties].

您必須修改以下區段中的設定： [!DNL flashaccesstools.properties] 啟用您打算使用的對應命令列工具：

* **媒體封裝程式屬性** - (適用於 [!DNL AdobePackager.jar])

* **原則更新清單管理員和撤銷清單管理員屬性** - (適用於 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **原則管理員屬性** - (適用於 [!DNL AdobePolicyManager.jar])

* **授權產生器屬性** - (適用於 [!DNL AdobeLicenseGenerator.jar])
