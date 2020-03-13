---
seo-title: 配置並運行命令行工具
title: 配置並運行命令行工具
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 配置並運行命令行工具 {#configure-and-run-the-command-line-tools}

命令行工具具有相關屬性，您必須在其中設定值， [!DNL flashaccesstools.properties] 才 *能運* 行工具。 有些命令列工具也可讓您從命令列指定屬性值。 您從命令行指定的值優先於您從中提供的值 [!DNL flashaccesstools.properties]。

您必須修改下列章節中的設 [!DNL flashaccesstools.properties] 定，才能啟用您要使用的對應命令列工具：

* **Media Packager屬性** -(適用 [!DNL AdobePackager.jar])

* **策略更新清單管理器和撤銷清單管理器屬性** -(用於 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器屬性** -(適用於 [!DNL AdobePolicyManager.jar])

* **授權產生器屬性** -(適用 [!DNL AdobeLicenseGenerator.jar])