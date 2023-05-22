---
title: 使用Java API更新策略
description: 使用Java API更新策略
copied-description: true
exl-id: 1b03f033-0d29-46cc-ae14-d6fef96fe970
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 使用Java API更新策略 {#updating-a-policy-using-the-java-api}

要使用Java API更新策略，請執行以下步驟：

1. 設定開發環境並包括中提及的所有JAR檔案 [建立開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 你的項目。
1. 建立 `Policy` 從檔案或資料庫讀取策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 更新 `Policy` 對象，方法是設定其屬性，如名稱和使用規則。

   ```java
     // Change the policy name.  
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

1. 序列化已更新 `Policy` 對象並將其儲存在檔案或資料庫中。

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

有關此示例代碼的完整源，請參見 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 在「參考實現」命令行工具「示例」目錄中。
