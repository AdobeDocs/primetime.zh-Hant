---
title: 建立自訂DRM原則（選用）
description: 建立自訂DRM原則（選用）
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 建立自訂DRM原則（可選）{#create-custom-drm-policies-optional}

Primetime Cloud DRM Protection Kit隨附一些預先設定的原則，可在封裝期間使用。 如果需要其他原則設定，例如特定的SWF允許清單權限，則可使用隨附的Primetime DRM原則管理員來產生自訂原則。

>[!NOTE]
>
>所有原則都必須使用ANONYMOUS驗證（非「使用者名稱密碼」或「自訂」）-不論是否使用「自訂驗證／權益」工作流程。

策略管理器中包含[!DNL flashaccesstools.properties]配置檔案，該配置檔案已修改，僅顯示Primetime Cloud DRM服務支援的可配置策略選項。 設定Primetime Cloud DRM服務不支援的原則選項，將會導致授權取得錯誤。 有關使用Primetime DRM策略管理器的資訊，請參閱：[Primetime DRM參考實施：策略管理器](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)。

若要建立新原則，請視需要更新[!DNL flashaccesstools.properties]檔案，然後使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 動態建立自訂驗證／權益的原則{#create-policies-dynamically-for-custom-auth-entitlement}

如果您使用Primetime Cloud DRM自訂驗證／權益，並想要針對每個授權要求動態建立新的DRM原則（而非從預先產生的存放區提取原則）,Adobe建議您直接使用Primetime DRM Java SDK。 直接使用Java SDK比[!DNL AdobePolicyManager.jar]工具更快，該工具會自動將原則檔案輸出至磁碟，從而產生磁碟I/O開銷。

使用Java SDK的范常式式碼可在[!DNL /Primetime DRM PolicyManager/sampleCode/]目錄中找到，名為[!DNL CreatePolicy.java]和[!DNL CreatePolicyWithOutputProtection.java]。 有關Java SDK的Javadoc和文檔，請參閱[Adobe PrimetimeDRM SDK](../../../digital-rights-management/drm-sdk-overview/overview.md)概觀

若要建立並執行範例，請將。java檔案複製至。./libs/檔案夾並執行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
