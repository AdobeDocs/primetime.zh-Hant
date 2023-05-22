---
title: 使用Java API建立DRM策略
description: 使用Java API建立DRM策略
copied-description: true
exl-id: fcae76c3-4e51-449d-b6d5-2138bf1c583e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 使用Java API建立DRM策略 {#creating-a-drm-policy-with-the-java-api}

要使用Java API建立DRM策略：

1. 設定開發環境並將項目中列出的所有JAR檔案包括在 [設定開發環境。](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)。
1. 建立 `com.adobe.flashaccess.sdk.policy.Policy` 對象並指定其屬性，包括權限、許可證快取持續時間和DRM策略結束日期。

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

1. 序列化DRM `Policy` 對象並將其儲存在檔案或資料庫中。

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

請參閱 [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] 在「參考實現」命令行工具中 [!DNL samples] 的子目錄。
