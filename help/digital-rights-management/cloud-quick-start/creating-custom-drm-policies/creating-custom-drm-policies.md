---
title: 建立自訂DRM政策（可選）
description: 建立自訂DRM政策（可選）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 建立自訂DRM政策（可選）{#create-custom-drm-policies-optional}

Primetime Cloud DRM Protection Kit隨附一些可在封裝期間使用的預先設定原則。 如果需要其他原則設定(例如特定的SWF允許清單許可權)，則可使用隨附的Primetime DRM Policy Manager來產生自訂原則。

>[!NOTE]
>
>所有原則都必須使用匿名驗證（不是使用者名稱密碼或自訂） — 無論是否使用自訂驗證/軟體權利檔案工作流程。

原則管理員隨附以下專案： [!DNL flashaccesstools.properties] 組態檔，已修改為僅公開Primetime雲端DRM服務支援的可設定原則選項。 設定Primetime Cloud DRM服務不支援的原則選項將會導致授權取得錯誤。 有關使用Primetime DRM Policy Manager的資訊，請參閱： [Primetime DRM參考實作：原則管理員](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

若要建立新原則，請更新 [!DNL flashaccesstools.properties] 檔案，然後使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 為自訂驗證/權益動態建立原則{#create-policies-dynamically-for-custom-auth-entitlement}

如果您使用Primetime Cloud DRM自訂驗證/權利，並且想要為每個授權請求動態建立新的DRM原則（而不是從預先產生的集區提取原則），Adobe建議您直接使用Primetime DRM Java SDK。 直接使用Java SDK比 [!DNL AdobePolicyManager.jar] 工具會自動將原則檔輸出至磁碟，造成磁碟I/O額外負荷。

使用Java SDK的範常式式碼可在以下網址找到： [!DNL /Primetime DRM PolicyManager/sampleCode/] 目錄，已命名 [!DNL CreatePolicy.java] 和 [!DNL CreatePolicyWithOutputProtection.java]. 如需Java SDK的Javadoc和檔案，請前往 [Adobe Primetime DRM SDK概覽](../../../digital-rights-management/drm-sdk-overview/overview.md)

若要建置並執行範例，請將.java檔案複製到……/libs/資料夾中並執行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
