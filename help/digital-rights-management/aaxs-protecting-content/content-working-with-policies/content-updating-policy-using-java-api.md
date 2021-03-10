---
title: 使用Java API更新原則
description: 使用Java API更新原則
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 使用Java API {#updating-a-policy-using-the-java-api}更新策略

要使用Java API更新策略，請執行以下步驟：

1. 設定您的開發環境並包括[在項目中設定開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)中提及的所有JAR檔案。
1. 建立`Policy`實例並從檔案或資料庫讀取策略。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 通過設定`Policy`對象的屬性（如其名稱和使用規則）來更新對象。

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

1. 序列化更新的`Policy`物件，並將它儲存在檔案或資料庫中。

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

有關此示例代碼的完整原始碼，請參見Reference Implementation Command Line Tools &quot;samples&quot;目錄中的`com.adobe.flashaccess.samples.policy.UpdatePolicy`。
