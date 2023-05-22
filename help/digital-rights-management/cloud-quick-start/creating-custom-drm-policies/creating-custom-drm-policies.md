---
title: 建立自定義DRM策略（可選）
description: 建立自定義DRM策略（可選）
copied-description: true
exl-id: a74f60b1-96a0-4fc4-bbf2-5db78f343562
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 建立自定義DRM策略（可選）{#create-custom-drm-policies-optional}

黃金時段雲DRM保護套件附帶了一些預配置的策略，可在打包期間使用。 如果需要其他策略配置，例如，特定的SWF允許清單權限，則包括的Mogine DRM策略管理器可用於生成自定義策略。

>[!NOTE]
>
>所有策略都必須使用ANONYMOUS身份驗證（不是用戶名密碼或自定義） — 無論是否使用自定義身份驗證/權利工作流。

策略管理器中包括 [!DNL flashaccesstools.properties] 配置檔案，已修改以僅公開Mogfire Cloud DRM服務支援的可配置策略選項。 設定黃金時段雲DRM服務不支援的策略選項將導致許可證獲取錯誤。 有關使用黃金時段DRM策略管理器的資訊，請參閱： [黃金時段DRM參考實現：策略管理器](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)。

要建立新策略，請更新 [!DNL flashaccesstools.properties] 檔案，然後使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 動態建立自定義身份驗證/權利的策略{#create-policies-dynamically-for-custom-auth-entitlement}

如果您正在使用Mogfise Cloud DRM自定義身份驗證/權利檔案，並且希望為每個許可請求動態建立新的DRM策略（而不是從預生成的池中提取策略），則Adobe建議您直接使用Migfise DRM Java SDK。 直接使用Java SDK比 [!DNL AdobePolicyManager.jar] 工具，它自動將策略檔案輸出到磁碟，導致磁碟I/O開銷。

可在 [!DNL /Primetime DRM PolicyManager/sampleCode/] 目錄，命名 [!DNL CreatePolicy.java] 和 [!DNL CreatePolicyWithOutputProtection.java]。 有關Java SDK的Javadoc和文檔，請訪問 [Adobe PrimetimeDRM SDK概述](../../../digital-rights-management/drm-sdk-overview/overview.md)

要生成和運行示例，請將.java檔案複製到……/libs/資料夾中並運行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
