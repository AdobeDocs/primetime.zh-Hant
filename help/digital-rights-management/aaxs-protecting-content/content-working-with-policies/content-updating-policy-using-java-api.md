---
seo-title: 使用Java API更新原則
title: 使用Java API更新原則
uuid: 23c50f05-799e-4f5a-869b-4b5e29a36ce1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Java API更新原則 {#updating-a-policy-using-the-java-api}

要使用Java API更新策略，請執行以下步驟：

1. 設定您的開發環境，並將「設定開發環境」中提 [及的所有JAR檔案包括在項目](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 中。
1. 建立實 `Policy` 例並從檔案或資料庫讀取策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通過設 `Policy` 置對象屬性（如其名稱和使用規則）來更新對象。

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

1. 序列化更新 `Policy` 的物件，並將它儲存在檔案或資料庫中。

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

有關此示例代碼的完整原始碼，請 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 參見Reference Implementation命令行工具&quot;samples&quot;目錄。
