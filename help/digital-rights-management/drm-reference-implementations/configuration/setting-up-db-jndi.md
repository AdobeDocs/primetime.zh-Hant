---
title: 設定許可證伺服器資料庫
description: 設定許可證伺服器資料庫
copied-description: true
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 設定許可證伺服器資料庫{#set-up-the-license-server-database}

引用實施許可證伺服器需要資料庫來支援以下內容：

* 用戶驗證
* 使用模型演示業務規則
* 元資料轉換
* 域支援

匿名許可證獲取不要求資料庫正在運行。

>[!NOTE]
>
>此過程僅適用於MicrosoftWindows。 有關其他作業系統，請參閱作業系統文檔或MySQL文檔。

要運行許可證伺服器，需要安裝和配置MySQL:

1. 在DVD上，轉到 [!DNL Third Party\MySQL\Installer\5.1] 資料夾並啟動安裝程式。
1. 請參與MySQL安裝。
1. 選擇 **[!UICONTROL Configure MySQL Server Now]** 的子菜單。
1. 在第五個螢幕之前，使用預設設定或選擇特定的測試設定。
1. 在第五個螢幕上，選擇 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 並輸入允許的最大連接數。
1. 記下根密碼。
1. 要重新安裝MySQL，如果需要稍後啟動伺服器，請完成以下步驟：
   1. 刪除 *系統驅動器：* 的子菜單。

      此資料夾位於 [!DNL \Documents and Settings\All Users\Application Data\MySQL]。
   1. 刪除舊的MySQL安裝資料夾。

      比如說， *系統驅動器：*，位於 [!DNL \Program Files\MySQL\MySQL Server 5.1]。
1. 要安裝MySQL JDBC驅動程式5.1.7，請複製 [!DNL mysql-connector-java-5.1.7-bin.jar] 檔案 [!DNL Third Party\MySQL\Installer\5.1] 資料夾 [!DNL ...\Tomcat6.0\lib] 目錄。

   >[!NOTE]
   >
   >MySQL JDBC驅動程式5.1.7可與Tomcat 6.0配合使用。不再支援舊版本的Tomcat。
