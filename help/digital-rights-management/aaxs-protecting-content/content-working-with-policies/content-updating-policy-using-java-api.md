---
title: 使用Java API更新原則
description: 使用Java API更新原則
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 使用Java API更新原則 {#updating-a-policy-using-the-java-api}

若要使用Java API更新原則，請執行以下步驟：

1. 設定您的開發環境，並包含中提到的所有JAR檔案 [設定開發環境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的專案中。
1. 建立 `Policy` 執行個體並從檔案或資料庫讀取原則。

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. 更新 `Policy` 物件，方法是設定其屬性，例如其名稱和使用規則。

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

1. 序列化已更新的 `Policy` 物件並將其儲存在檔案或資料庫中。

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

如需此範常式式碼的完整原始碼，請參閱 `com.adobe.flashaccess.samples.policy.UpdatePolicy` 在「參考實作」命令列工具「範例」目錄中。
