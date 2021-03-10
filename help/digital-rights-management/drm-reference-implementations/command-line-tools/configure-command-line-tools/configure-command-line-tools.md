---
title: 配置並運行命令行工具
description: 配置並運行命令行工具
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 配置並運行命令行工具{#configure-and-run-the-command-line-tools}

命令行工具具有相關屬性，您必須在[!DNL flashaccesstools.properties] *中設定值，然後才能運行工具。*&#x200B;有些命令列工具也可讓您從命令列指定屬性值。 您從命令行指定的值優先於從[!DNL flashaccesstools.properties]提供的值。

您必須修改[!DNL flashaccesstools.properties]下列各節中的設定，以啟用要使用的相應命令行工具：

* **Media Packager屬性** -(適用 [!DNL AdobePackager.jar])

* **策略更新清單管理器和撤銷清單管理器屬性** -(適 [!DNL AdobePolicyUpdateListManager.jar] 用於 [!DNL AdobeRevocationListManager.jar])

* **策略管理器屬性** -(適用於 [!DNL AdobePolicyManager.jar])

* **授權產生器屬性** -(適用 [!DNL AdobeLicenseGenerator.jar])