---
title: 使用Java API更新DRM策略
description: 使用Java API更新DRM策略
copied-description: true
exl-id: 00bb9b64-30f7-4900-b6bd-57604295b44d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 使用Java API更新DRM策略 {#updating-a-drm-policy-with-the-java-api}

要使用Java API更新DRM策略：

1. 設定開發環境並將項目中列出的所有JAR檔案包括在 [建立開發環境](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。
1. 建立DRM `Policy` 實例並從檔案或資料庫讀取DRM策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 更新DRM `Policy` 對象，方法是設定其屬性，如名稱和使用規則。

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

1. 序列化更新的DRM `Policy` 對象並將其儲存在檔案或資料庫中。

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

請參閱 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 在「參考實現」命令行工具中 [!DNL samples] 的子目錄。
