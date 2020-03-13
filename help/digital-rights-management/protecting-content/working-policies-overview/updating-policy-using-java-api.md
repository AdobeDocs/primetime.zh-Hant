---
seo-title: 使用Java API更新DRM策略
title: 使用Java API更新DRM策略
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Java API更新DRM策略 {#updating-a-drm-policy-with-the-java-api}

要使用Java API更新DRM策略：

1. 設定您的開發環境並將「設定開發環境」中列出的所有JAR文 [件都包括在項目中](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。
1. 建立DRM實 `Policy` 例並從檔案或資料庫讀取DRM策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通過設定DRM `Policy` 對象的屬性（如其名稱和使用規則）來更新DRM對象。

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

1. 序列化更新的DRM `Policy` 對象，並將其儲存在檔案或資料庫中。

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

有關 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 此示例代碼的原始碼，請 [!DNL samples] 參閱Reference Implementation命令行工具目錄。
