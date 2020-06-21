---
seo-title: 建立自訂DRM原則（選用）
title: 建立自訂DRM原則（選用）
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 建立自訂DRM原則（選用）{#create-custom-drm-policies-optional}

Primetime Cloud DRM Protection Kit隨附一些預先設定的原則，可在封裝期間使用。 如果需要其他策略配置，例如特定的SWF-Allowsliting權限，則可使用隨附的Primetime DRM策略管理器生成自定義策略。

>[!NOTE]
>
>所有原則都必須使用ANONYMOUS驗證（非「使用者名稱密碼」或「自訂」）-不論是否使用「自訂驗證／權益」工作流程。

策略管理器隨附的配置文 [!DNL flashaccesstools.properties] 件已修改，僅顯示Primetime Cloud DRM服務支援的可配置策略選項。 設定Primetime Cloud DRM服務不支援的原則選項，將會導致授權取得錯誤。 有關使用Primetime DRM策略管理器的資訊，請參閱： [Primetime DRM參考實作： 策略管理器](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)。

若要建立新原則，請視需要 [!DNL flashaccesstools.properties] 更新檔案，然後使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 動態建立自訂驗證／權益的原則{#create-policies-dynamically-for-custom-auth-entitlement}

如果您使用Primetime Cloud DRM自訂驗證／權益，並想要針對每個授權要求動態建立新的DRM原則（而非從預先產生的存放區提取原則）,Adobe建議您直接使用Primetime DRM Java SDK。 直接使用Java SDK的速度比自動將原則檔 [!DNL AdobePolicyManager.jar] 案輸出至磁碟的工具快，造成磁碟I/O負荷。

使用Java SDK的范常式式碼可在名為和 [!DNL /Primetime DRM PolicyManager/sampleCode/] 的目錄中找 [!DNL CreatePolicy.java] 到 [!DNL CreatePolicyWithOutputProtection.java]。 如需Java SDK的Javadoc和檔案，請參閱Adobe Primetime DRM SDK [總覽(An Overview of Adobe Primetime DRM SDK)](../../../digital-rights-management/drm-sdk-overview/overview.md)

若要建立並執行範例，請將。java檔案複製至。./libs/檔案夾並執行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
