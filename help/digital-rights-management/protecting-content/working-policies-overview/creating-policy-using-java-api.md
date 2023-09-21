---
title: 使用Java API建立DRM政策
description: 使用Java API建立DRM政策
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用Java API建立DRM政策 {#creating-a-drm-policy-with-the-java-api}

使用Java API建立DRM政策：

1. 設定您的開發環境，並將中列出的所有JAR檔案納入您的專案中 [設定您的開發環境。](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. 建立 `com.adobe.flashaccess.sdk.policy.Policy` 物件並指定其屬性，包括許可權、授權快取持續時間和DRM原則結束日期。

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
   
   policy.setName("DemoPolicy");  
   
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
   
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
   
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
   
   // Licenses can be stored on the client for 7 days after downloading  
   policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
   try {  
       // Content will expire December 31, 2010  
       SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
       policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
   } catch (ParseException e) {  
       // Invalid date specified in dateFormat.parse()  
       e.printStackTrace();  
   } 
   ```

1. 序列化DRM `Policy` 物件並將其儲存在檔案或資料庫中。

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
   
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   ```

另請參閱 [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] 在參照實作命令列工具中 [!DNL samples] 此範常式式碼的完整來源目錄。
