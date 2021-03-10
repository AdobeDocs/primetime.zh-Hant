---
title: 廢止機器認證
description: 廢止機器認證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# 撤消電腦憑據{#revoking-machine-credentials}

Adobe會維護CRL，以廢止已知受到危害的機器憑證。 此CRL由SDK自動執行。 如果您不希望您的授權伺服器向其他電腦核發授權，您可以建立電腦撤銷清單並新增您要排除之電腦Token的發行者名稱和序號（使用`MachineToken.getMachineTokenId()`擷取電腦憑證的發行者名稱和序號）。

撤消電腦憑據涉及`RevocationListFactory`對象的使用。 若要建立撤銷清單、載入現有的撤銷清單，並檢查使用Java API是否已撤銷機器Token，請執行下列步驟：

1. 設定您的開發環境並包括[在項目中設定開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)中提及的所有JAR檔案。
1. 建立`ServerCredentialFactory`例項以載入簽署所需的憑證。 許可證伺服器憑證用於簽署撤銷清單。
1. 建立`RevocationListFactory`實例。
1. 使用`IssuerAndSerialNumber`物件指定要撤銷的機器Token發行者和序號。 所有Adobe存取請求都包含機器Token。
1. 使用您剛建立的`IssuerAndSerialNumber`物件建立`RevocationList`物件，並將它傳入`RevocationListFactory.addRevocationEntry()`以新增至撤銷清單。 呼叫`RevocationListFactory.generateRevocationList()`以產生新的撤銷清單。
1. 若要儲存撤銷清單，您可以呼叫`RevocationList.getBytes()`將其序列化。 要載入清單，請調用`RevocationListFactory.loadRevocationList()`並傳入序列化清單。
1. 請呼叫`RevocationList.verifySignature()`，確認簽名有效且清單已由正確的授權伺服器簽署。
1. 要檢查條目是否已撤銷，請將`IssuerAndSerialNumber`對象傳遞到`RevocationList.isRevoked()`。 撤銷清單也可傳入`HandlerConfiguration`，讓SDK對所有驗證和授權要求執行撤銷清單。

若要新增其他項目至現有的`RevocationList`，請載入現有的撤銷清單。 建立新的`RevocationListFactory`實例，並確保增加CRL編號。 呼叫`RevocationListFactioryEntries.addRevocationEntries`，將舊清單中的所有條目添加到新清單中。 呼叫`RevocationListFactory.addRevocationEntry`將任何新的撤銷項目新增至RevocationList。

如需示範如何建立撤銷清單、載入現有的撤銷清單以及檢查機器Token是否已被撤銷的范常式式碼，請參閱參考實作命令列工具「samples」目錄中的`com.adobe.flashaccess.samples.revocation.CreateRevocationList`。
