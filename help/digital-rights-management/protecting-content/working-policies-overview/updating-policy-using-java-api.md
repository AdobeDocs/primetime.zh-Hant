---
title: 使用Java API更新DRM策略
description: 使用Java API更新DRM策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 使用Java API {#updating-a-drm-policy-with-the-java-api}更新DRM策略

要使用Java API更新DRM策略：

1. 設定您的開發環境並將[設定開發環境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)中列出的所有JAR檔案都包括在項目中。
1. 建立DRM `Policy`實例並從檔案或資料庫讀取DRM策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通過設定DRM `Policy`對象的屬性（如其名稱和使用規則）來更新該對象。

   ```java
   // Change the DRM policy name.  
   policy.setName("UpdatedDemoPolicy");  
   
   // Add DRM module restrictions to the play right  
   for (Right r: policy.getRights()) {  
       if (r instanceof PlayRight) {  
           PlayRight pr = (PlayRight) r;  
           // Disallow Linux versions up to and including 1.9.  Allow  
           // all other OSes and Linux versions above 1.9  
           VersionInfo toExclude = new VersionInfo();  
           toExclude.setOS("Linux");  
           toExclude.setReleaseVersion("1.9");  
           Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
           exclusions.add(toExclude);  
           ModuleRequirements drmRestrictions = new ModuleRequirements();  
           drmRestrictions.setExcludedVersions(exclusions);  
           pr.setDRMModuleRequirements(drmRestrictions);  
           break;  
       }  
   }
   ```

1. 序列化更新的DRM `Policy`對象，並將其儲存在檔案或資料庫中。

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

有關此示例代碼的源資訊，請參閱參考實施命令行工具[!DNL samples]目錄中的`com.adobe.flashaccess.samples.policy.UpdatePolicy`。
